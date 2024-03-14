Large Language Models have emerged as cutting edge systems that can process and generate text with coherent communication. They are also able to selectively process specific bits of information in their input, allowing them to be prompted using custom instructions and prompts.

Many of these models appear to have emergent abilities that are a function of their scale and pre-training process.

## What is a LLM

There are a few key components to understand about LLMs

1. **Tokenisation** : How text content is parsed into small units called tokens. This is done by using a common algorithm such as [wordpiece](Wordpiece), [BPE](Byte Pair Encoding) or unigramLM. 
2. **Positional Encodings**: Attention is a positional invariant operation but we want to capture positional information of tokens. Therefore we compute a transformation on each token. We can use algorithms such as [[RoPE]] and [[Alibi]] in order to extend the context of a model beyond that of what was seen during training. 
3. **Attention** : This is a mathematical operation that assigns weights to input tokens based on relevance. There are a few different kinds of attention that we work with - self-attention, cross-attention and flash attention.
4. **Activation Functions** : These are non-linear functions which helps introduce non-linearity to our model. This in turn helps us to model more complex relations
5. **Layer Normalisation** : This is used to ensure that the input in a single example has a mean of 0 and a variance of 1. We typically use this in order to prevent potentially exploding gradients. Layer normalisation has been shown to provide training stability in LLMs with better results observed from performing the layer norm before the attention calculation rather than afterwards.
6. **Data Pre-processing**: Training data is extremely important when considering the final result of training a LLM. Often times, we'll use a few methods such as quality filtering, data deduplication and privacy reduction to ensure we have unique chunks and no sensitive data within the training data.

### Attention

There are three main types to know

1. **Self-Attention**: We calculate attention using queries, keys and values from the same block.
2. **Cross Attention** : This is used in encoder-decoder architectures where encoder outputs are the queries and key-value pairs come from the decoder
3. **Sparse Attention**: This is used to iteratively calculate the attention in sliding windows for speed gains
4. **Flash Attention**: Better attention algorithm to optimise the memory reads and writes

### Training LLMs

There are a few different training approaches to working with large LLMs

- [[Tensor Parallelism]] : We shard a tensor computation across devices
- [[Data Parallelism]]: We replicate the model on multiple devices where data gets divided across devices. We then synchronise the weights across all devices.
- [[Pipeline Parallelism]] : We have model layers sharded across different devices
- [[Model Parallelism]] : We shard tensor computations and batch processing across multiple devices
- [[Optimiser Parallelism]]: We shard calculation of optimiser optimisation across multiple devices

## 