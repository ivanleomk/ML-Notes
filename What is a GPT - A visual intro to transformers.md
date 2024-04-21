# Introduction

A Generative Pre-trained Transformer is a GPT model which is able to produce text. It takes in a series of tokens as input and outputs a probability distribution over it's known vocabulary.

There are a few important portions to understand

1. **Embeddings** : 
2. **Multi-Layer Perceptrons**
3. **Attention Blocks**

Typically it would look like 

```
System Prompt: <Prompt>

User: <Prompt>

Assistant: <Response>
```

Under the hood, all the computation is done using real-numbers so that we are able to use back-propagation to tune the weights.  We turn our words into numbers using tokenisations, where we map subwords within our words into known tokens.

## Embeddings

We have two kinds of embeddings - positional and token embeddings. 

### Token Embeddings

Once we've broken our prompt into subwords using the GPT's predefined vocabulary, we transform it into an embedding vector using an embedding matrix. 

Embeddings are a large list of `n` numbers that represent the semantic meaning of a phrase. GPT had 12,288 dimension embeddings.

The similarity of embeddings is typically computed using a cosine similarity calculation. This returns 1 when all their components are in the same direction, 0 when they're perpendicular and -1 when they are in the opposite direction from one another.

### Positional Embeddings

Embeddings don't have any information about the position that a word has w.r.t it's other components. Therefore, we have positional embeddings that help provide this information through either a learned or fixed transformation that is unique to each individual position.

## Softmax

A softmax function takes in a real number vector and from there, it normalises all the values in the vector so that they all add up to 1. This helps us treat the entire vector as a single probability distribution. 

We do so by applying the formula to each value in the vector with $n$ values at the $i$-th position.

$$
\frac{e^{x_i}}{\sum_{j=0}^n{e^{x_j}}}
$$
Typically we might have a temperature component which can be added in to help bias / increase the probabilities of the smaller values in the softmax.

$$
\frac{e^{\frac{x_i}{T}}}{\sum_{j=0}^n{e^{\frac{x_j}{T}}}}
$$

## Attention

### Basic Idea

> Source : https://www.youtube.com/watch?v=eMlx5fFNoYc&t=1s

We start by associating each token with a high dimensional vector which encodes it's semantic meaning. Attention aims to solve the problem of embeddings lacking context of their surrounding words/phrases.

Eg. Tower vs Eiffel Tower vs Miniature Eiffel Tower

Typically in a transformer we'd have what's known as [[Multi Headed Attention]] which processes chunks of the input in parallel. Attention relies on a few different matrices

1. Query : A questions
2. Key : Answering the queries
3. Value: A transformation of the embedding matrix 

These are learnt from the data itself and help map our big embedding vector for each token into a smaller embedding space. We then take the dot product between the query and key to see how similar they are, the more similar these are, the more we say they **attend to** each other.

We end up normalising the input relative to each other in order to get a weighted distribution of each token importance w.r.t each individual token. This helps each token weight the representation of other tokens against itself. Because we need to do this pairwise comparison, the attention computation scales quadratically.

Since we have both a weightage of each individual token w.r.t each token for each row and a new rescaled semantic vector for each token, we can then compute a new representation for each token by computing a weighted sum of the rescaled semantic vectors for every other token before it.

### Multi Headed Attention

Multi Headed Attention involves breaking up the original embedding vector into multiple separate chunks. 