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