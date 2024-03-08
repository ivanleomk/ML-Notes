> Language models can perform down-stream tasks in a zero-shot setting ( without using any examples ) that does not require any parameter or architecture modification yet achieve state of the art performance in different tasks
## Background

It is difficult for specialised systems to generalise to slight changes in the data distribution. The traditional approach was to collect a dataset of training examples demonstrating correct behaviour for a desired task, train a system to imitate these behaviours and then test its performance on independent and identically distributed held-out examples.

These datasets need to include hundreds to thousands of examples to induce functions which generalise well. Therefore it is difficult to scale the creation of said datasets with current techniques. 

Models learn to estimate a conditional distribution of $p(output|input)$ from the training dataset which in turn allows them to perform tasks in a zero-shot setting. For instance, a translation training example can be written as

```
translate_to_french, english_text, french_text
```

This can in turn be easily modified to a test example by removing the `french_text` to achieve the following.
```
translate_to_french, english_text,
```

## Model

### Datasets

They used a new curated dataset called `WebText` which contains a text subset of 45 million reddit links that each received at least 3 karma points. They then did some de-duplication and heuristic based cleaning before removing all wikipedia documents to prevent any data contamination.

Prior models had used Common Crawl which is a free/open-source scrapped version of the internet. However, a major criticism of Common Crawl is that a large amount of documents are mostly unintelligible. 

### Tokeniser

The model uses a BPE encoder to encode text input to be processed.

### Architecture

They use a vanilla transformer architecture with the following modifications

- Layer Normalisation moved to the input of each sub-block
- Additional Layer Normalisation added to the final self-attention block at the end
- Vocabulary expanded to 50,257 tokens
- Context size increased from 512 to 1024 and a larger batchsize used

| Parameters | Layers | Embedding Dimensionality |
| ---------- | ------ | ------------------------ |
| 117 M      | 12     | 768                      |
| 345M       | 24     | 1024                     |
| 762M       | 25     | 1280                     |
| 1542M      | 48     | 1600                     |
This is also a decoder-only model which was popularised in the paper [Generating Wikipedia By Summarising Long Sequences](https://arxiv.org/pdf/1801.10198.pdf)

![[CleanShot 2024-03-08 at 08.59.59.png]]
This comes from the OpenAI Official [GPT-2 implementation](https://github.com/openai/gpt-2/blob/master/src/model.py)

```python
def block(x, scope, *, past, hparams):
    with tf.variable_scope(scope):
        nx = x.shape[-1].value
        a, present = attn(norm(x, 'ln_1'), 'attn', nx, past=past, hparams=hparams)
        x = x + a
        m = mlp(norm(x, 'ln_2'), 'mlp', nx*4, hparams=hparams)
        x = x + m
        return x, present
```

## Results

GPT-2 improved the state of the art scores on 7 out of 8 datasets in a zero-shot setting. 

### Children Books

The Children's Book Test has two portions - one to examine the performance on named entities and another on common nouns. Models are made to predict which of 10 possible choices for an omitted word is correct.

GPT-2 scored ~ 83-89% when SOTA was ~82% at the time for named entities and ~87-93% when SOTA was ~85.7 at the time

### LAMBADA

LAMBADA aims to get a model to predict the final word of a sentence given a prior context.

```
Context: They tuned, discussed for a moment, then struck up a lively jig. Everyone joined in, turning the courtyard into an even more chaotic scene, people now dancing in circles, swinging and spinning in circles, everyone making up their own dance steps. I felt my feet tapping, my body wanting to move. 
Target sentence: Aside from writing, I ’ve always loved . 
Target word: dancing
```

There were two main metrics measured here

- Perplexity : Is the model confident about its predictions?
- Accuracy : Does it get the word correct?

> Perplexity is defined as the exponentiated average negative log-likelihood of a sequence. Remember that for 
![[CleanShot 2024-03-08 at 01.11.09.png]]

GPT-2 improves state of the art predictions

- Perplexity from 99.8 to 8.63
- Accuracy from 59.23 to 63.24

### CoQA ( Conversation Question and Answer)

The Conversation Question Answering dataset (CoQA) Reddy et al. (2018) consists of documents from 7 different domains paired with natural language dialogues between a question asker and a question answerer about the document. 

GPT-2 was conditioned on a document with greedy-decoding being used with the final token (A,B,C or D ) being used to determine the answer

> Greedy decoding from GPT-2 when conditioned on a doc- ument, the history of the associated conversation, and a final token A:

```
Passage: Once upon a time, in a barn near a farm house, there lived a little white kitten named Cotton. Cotton lived high up in a nice warm place above the barn where all of the farmer's horses slept. But Cotton wasn't alone in her little home above the barn, oh no. She shared her hay bed with her mommy and 5 other sisters. All of her sisters were cute and fluffy, like Cotton. But she was the only white one in the bunch. The rest of her sisters were all orange with beautiful white tiger stripes like Cotton's mommy. Being different made Cotton quite sad. She often wished she looked like the rest of her family. So one day, when Cotton found a can of the old farmer's orange paint, she used it to paint herself like them. When her mommy and sisters found her they started laughing. 

"What are you doing, Cotton?!" 

"I only wanted to be more like you". 

Cotton's mommy rubbed her face on Cotton's and said "Oh Cotton, but your fur is so pretty and special, like you. We would never want you to be any other way". And with that, Cotton's mommy picked her up and dropped her into a big bucket of water. When Cotton came out she was herself again. Her sisters licked her face until Cotton's fur was all all dry. 

"Don't ever do that again, Cotton!" they all cried. "Next time you might mess up that pretty white fur of yours and we wouldn't want that!" 

Then Cotton thought, "I change my mind. I like being special".

Question
Q		Where did she live?
A		in a barn || in a barn near a farm house, there lived a little white kitten
A		in a barn ||  in a barn near a farm house, there lived a little white kitten named Cotton
A		in a barn || in a barn
A		in a barn near ||  in a barn near a farm house, there lived a little white kitten named Cotton.
```

### Summarisation 

The CNN and Daily Mail dataset was used to test the ability of GPT-2 to perform summarisation. This was done by adding the text `TL;DR:` after the text and 100 tokens with top-k random sampling done thereafter.

> GPT-2’s performance drops by 6.4 points on the aggregate metric when the task hint is removed which demonstrates the ability to invoke task specific behavior in a language model with natural language.


They measured summaries using ROUGE

ROUGE-1 measures the overlap of individual words (unigrams) between the generated and reference texts .
ROUGE-2 assesses the overlap of two consecutive words (bigrams) .
ROUGE-L evaluates the longest common subsequence (LCS) of words, which does not require the words to be in the same order