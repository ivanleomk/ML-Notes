# Introduction 

Large Language Models are unique in that they can respond to a user's query in a natural manner. This enables more natural forms of conversation and makes them invaluable for any task that requires parsing and generating text.

## Attention

LLMs are powerful because of the self-attention mechanism that they've learnt how to apply. There are two forms of self-attention that are widely used.

1. **Self-Attention** : This is when a model is able to weight the importance of every previous token w.r.t itself. It cannot see tokens that are after it.
2. **Bidirectional Self-Attention**: This is when a model is trained to utilise the full context of the tokens. it can see every single token in the context window.

GPT mainly uses Self-Attention while something like BERT uses Bidirectional Self-Attention. This is because GPT is a decoder based model while BERT is a encoder based model.

## Training 

![](assets/CleanShot%202024-08-31%20at%2009.52.33@2x.png)

LLMs are trained in a few stages. These can be described as 

1. **Base Foundation Model training** : We train the large language model on a large corpus of unlabelled text. It's sole job is to complete the text chunk and predict the next token
2. **Fine-Tuning** : Once we've obtained a fine-tuned LLM, we can then fine-tune it to learn how to follow instructions or for classification tasks. 

### Next Token Prediction

When training LLMs, we are able to utilise [[Self Supervised Learning]] because our models are trained to predict the next token. This means that we have natural labels generated from the data 

Interestingly, this creates the concept of [[Emergent Behaviours]] which are capabilities that the model wasn't trained for. This is because of the diverse context of the information that the model is exposed to. 

# Training Datasets

When working with multi-modal data, we need to convert the data into a vector representation. This is done through an [[encoder]] which helps us to convert the data into a representation that our LLM can work with.

![](assets/CleanShot%202024-08-31%20at%2009.52.07@2x.png)

An early example of an encoder that worked was [[Word2Vec]] that trained neural network architectures to generate embeddings by predicting a completion for a word given a set of target words. When we are training our LLMs, they learn to generate these representations during their training.

This makes it more efficient to utilise a LLM's own native embeddings if possible because they are task-specific as compared to a more general implementation like [Word2Vec](Word2Vec). 

## Tokenisation

When dealing with text, we need to tokenise it into known character ngrams that the model learns about during the training stage. This means that our model learns a mapping of `token->embedding` in it's initial embedding layer which helps it to make good predictions.

![](assets/CleanShot%202024-08-31%20at%2017.03.45.png)

It's important here to emphasise that our model **never sees raw text**. It just sees the token-id or the raw embeddings that the encoder produces. Therefore, it's important to have a large and diverse training set so that our model has a large vocabulary to work with so that our model is able to learn a useful representation.

There are two ways that we've tried to deal with this problem of unknown tokens
1. We can have a `[UNK]` token which is used to represent unknown tokens
2. We can use an algorithm like `BPE` that recursively breaks down tokens into subwords and single characters, this means that for relative rare words or non-english characters, we might end up using a lot of tokens

### Special Tokens

In general, there are a set of special tokens that we can use to indicate to our model to treat it differently.

1. `[BOS]` : This marks the start of a text chunk and signifies to the LLM where a piece of content begins.
2. `[EOS]` : This token in positioned at the end of a text, and is especially useful when concatenating multiple unrelated texts.
3. `[PAD]` : This token is useful when we're training LLMs with batch sizes larger than one

Some other models might even include special tokens to be able to implement special cases like Function Calling. 

### Byte Pair Encoding

Popular LLMs like GPT-2, GPT-3 were trained using an algorithm called [Byte Pair Encoding](Byte%20Pair%20Encoding.md). This is implemented most popularly in a library called `tiktoken`.

![](assets/CleanShot%202024-08-31%20at%2017.17.38.png)

On a high level, BPE works by building a vocabulary through iteratively merging frequent characters into subwords and frequent subwords into words. This helps it to build a rich vocabulary that preserves the token space and for common words or subwords to be represented more efficiently.


## Data Sampling

Since we are doing next token prediction, our data gives us labels. But since our models need to operate on a fixed number of tokens, how can we construct the training dataset?

![](assets/CleanShot%202024-08-31%20at%2017.29.57.png)

### Embeddings

There are two forms of embeddings that we'd like our model to learn

1. Absolute Embeddings : These are the embeddings for specific tokens that we care about
2. Positional Embeddings : These are the embeddings that represent the information for a specific position. While these can be learnt or calculated in advance, ultimately, it's just used to help the model understand the concept of position.

These size of these embeddings are going to depend on the specific model that we're looking at.
![](assets/CleanShot%202024-08-31%20at%2017.48.10.png)

# Attention

Attention is an architectural choice. It was first implemented in [RNN](RNN.md) but ultimately found its biggest use in the [Transformer Architecture](Transformer%20Architecture) where it was used in an encoder-decoder framework.

![](assets/CleanShot%202024-08-31%20at%2017.51.02.png)

There are three main variants that we see in popular usage

1. **Self-Attention**
2. **Causal Attention**
3. **Multi-Head Attention**

Attention in transformers was created to solve the complexity of machine translation tasks. 

This created the first few [[Encoder Decoder]] models which would first encode a source sentence into a vector representation of hidden states before passing it to a decoder which would then generate a predicted translation.
![](assets/CleanShot%202024-09-01%20at%2010.12.46@2x.png)
## Self Attention

With Self Attention, each position in the input sequence attends to all positions in the same sequence. This allows it to weight the importance of information for each individual position w.r.t itself.

![ | 250](assets/CleanShot%202024-09-01%20at%2010.20.19@2x.png)

This is done by 

1. First we compute a hidden state for each individual token
2. Then we take the dot product between each hidden state to calculate the dot product. This means that we perform `O(n^2)` operations
3. Lastly, for each row, we normalise it using a softmax operation so that the dot products sum to 1
4. We then create a new weighted sum based off the weightage of individual dot product values

### Self Attention in the Transformer

In the transformer, they introduce the concept of `key`, `query` and `value` matrices that we multiply our hidden states by. These are useful in helping to cast our original hidden states into a better representation that we can fine-tune during training.

Once our model has computed the new matrices `Q,K,V` we can then take `Q@K` to get a `nxn` matrix which we then scale using $\sqrt{d_k}$ before applying a softmax. This is known as [[Scaled Dot Attention Product]] which was first introduced in the original transformer paper.

Once we've gotten the normalised attention weights that sum to 1, we can then compute a new representation for each token by summing up the respective representations of the `V` matrix that it corresponds to.

## Multi-Head Attention

By having multiple heads working in parallel, we can train our model to have different heads that learn different aspects of the data. This enables it to attend to information from different representation subspaces at different positions.

## Causal Attention

Causal Attention is a specialised form of attention that only allows the model to only consider previous and current inputs. 

![](assets/CleanShot%202024-09-01%20at%2011.02.05@2x.png)

This means that we mask out the attention weights above the diagonal before computing the softmax. This prevents the model from looking ahead and cheating. This can be done with a simple tril mask

```python
context_length = attn_scores.shape[0]
mask_simple = torch.tril(torch.ones(context_length, context_length))
print(mask_simple)
```

This creates a mask as seen below.

```bash
tensor([[1., 0., 0., 0., 0., 0.],
        [1., 1., 0., 0., 0., 0.],
        [1., 1., 1., 0., 0., 0.],
        [1., 1., 1., 1., 0., 0.],
        [1., 1., 1., 1., 1., 0.],
        [1., 1., 1., 1., 1., 1.]])
```

We can then apply a simple element wise multiplication so that we only preserve the attention scores from the positions that have a `1`.

## Dropout in Attention

Sometimes, we might also implement dropout in the attention calculation by randomly masking out specific attention scores before we compute the softmax.

![](assets/CleanShot%202024-09-01%20at%2022.47.56@2x.png)
This helps our model to not be dependent on a specific set of hidden layer units. This helps our model to generalise better to its training dataset.

