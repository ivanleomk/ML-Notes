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

- Perplexity from 99.8