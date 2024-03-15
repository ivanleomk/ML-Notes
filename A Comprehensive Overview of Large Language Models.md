Large Language Models have emerged as cutting edge systems that can process and generate text with coherent communication. They are also able to selectively process specific bits of information in their input, allowing them to be prompted using custom instructions and prompts.

Many of these models appear to have emergent abilities that are a function of their scale and pre-training process.

There are a few key components to understand about LLMs

1. **Tokenisation** : How text content is parsed into small units called tokens. This is done by using a common algorithm such as [wordpiece](Wordpiece), [[Byte Pair Encoding]] or unigramLM. 
2. **Positional Encodings**: Attention is a positional invariant operation but we want to capture positional information of tokens. Therefore we compute a transformation on each token. We can use algorithms such as [[RoPE]] and [[Alibi]] in order to extend the context of a model beyond that of what was seen during training. 
3. **Attention** : This is a mathematical operation that assigns weights to input tokens based on relevance. There are a few different kinds of attention that we work with - self-attention, cross-attention and flash attention.
4. **Activation Functions** : These are non-linear functions which helps introduce non-linearity to our model. This in turn helps us to model more complex relations
5. **Layer Normalisation** : This is used to ensure that the input in a single example has a mean of 0 and a variance of 1. We typically use this in order to prevent potentially exploding gradients. Layer normalisation has been shown to provide training stability in LLMs with better results observed from performing the layer norm before the attention calculation rather than afterwards.
6. **Data Pre-processing**: Training data is extremely important when considering the final result of training a LLM. Often times, we'll use a few methods such as quality filtering, data deduplication and privacy reduction to ensure we have unique chunks and no sensitive data within the training data.

## Attention

There are three main types to know

1. **Self-Attention**: We calculate attention using queries, keys and values from the same block.
2. **Cross Attention** : This is used in encoder-decoder architectures where encoder outputs are the queries and key-value pairs come from the decoder
3. **Sparse Attention**: This is used to iteratively calculate the attention in sliding windows for speed gains
4. **Flash Attention**: Better attention algorithm to optimise the memory reads and writes


### Architectures

Typically when we look at LLMs, we have three different configurations

1. **Encoder-Decoder**: This processes inputs through the encoder and passes the intermediate representations through the decoder to generate output. 
2. **Causal Decoder**: This doesn't have an encoder and generates output using the decoder only
3. **Prefix Decoder**: The prefix decoder modifies the masking mechanism of causal decoders to allow bidirectional attention on prefix tokens and unidirectional attention on generated tokens.

## Training LLMs

There are a few different training approaches to working with large LLMs

- [[Tensor Parallelism]] : We shard a tensor computation across devices
- [[Data Parallelism]]: We replicate the model on multiple devices where data gets divided across devices. We then synchronise the weights across all devices.
- [[Pipeline Parallelism]] : We have model layers sharded across different devices
- [[Model Parallelism]] : We shard tensor computations and batch processing across multiple devices
- [[Optimiser Parallelism]]: We shard calculation of optimiser optimisation across multiple devices

## Tasks

We can then use these architectures to train our models to perform specific tasks. These tend to be the rough buckets

1. **Full Language Modelling** : A model is asked to predict future tokens given previous tokens.
2. **Prefix Language Modelling**: Prefix is chosen randomly and the remaining targets are used to calculate loss
3. **Masked Language Modelling**: One or more contiguous tokens are masked in the input and the model is asked to predict masked tokens given the past and future content

### Training Stages

This is normally done in a few stages 
1. **Pre-Training**: The model is trained in a self-supervised manner on a large corpus to predict the next tokens given the input.
2. **Fine-Tuning**: There are a few different means of fine-tuning
	1. **Instruction-Tuning** : To enable a model to respond to use queries effectively using instruction and input/output pairs
	2. **Transfer Learning**: We fine-tune a model with task-specific data (Eg. BERT for sentiment analysis )
	3. **Alignment Tuning**: The goal is to get a model to be helpful, harmless and honest. This is normally done through a reinforcement learning pipeline like RLHF or using DPO/PPO/KTO

## Working with LLMs

Some general useful methods when working with LLMs is to utilise a few prompting techniques such as 

- [[Chain Of Thought]]: Get the LLM to generate some reasoning before it's response
- [[Self-Consistency]]: Get the LLM to generate multiple responses and see what is the most common one
- [[Tree Of Thought]]: Explore multiple reasoning paths with possibilities to look ahead and backtrack for problem solving

## Notable LLMs

- [[Exploring the Limits Of Transfer Learning with a Unified Text To Text Transformer]] : This introduced the T5 model as the C4 dataset. It uses masked language modelling as a pre-training objective where spans (consecutive tokens) are replaced with a single mask instead of separate masks for each token. Notably, they do a variety of ablations in order to find the optimal hyper-parameters.
  
- [[Language Models are Unsupervised Multitask Learners]]: This introduced the GPT-2 model which was able to perform similar to SOTA models just with simple prompts. 
  
- [[Language Models are Few-Shot Learners]]: This introduced the GPT-3 model that had a significantly larger parameter count of 175B parameters and showed that we could increase performance by scaling up parameters. Notably it showed that language models could train on larger batch sizes with a lower learning rate to boost performance.
  
- [[mT5: A massively multilingual pre-trained text-to-text transformer]]: This introduced the mT5 paper which indicated that we need a large number of parameters for good multi-lingual models to perform equivalent to single language models
  
- [[Scaling Language Models: Methods, Analysis & Insights from Training Gopher]]: Deepmind trains a new model called Gopher and scales parameter count up to 300B. They demonstrate that relative encodings allow models for longer sequences that those on which it was trained.
  
- [[Training Compute-Optimal Large Language Model]]: In this paper, researchers try to find the optimal allocation of fixed compute resources to tokens to model parameters. They find that we should instead double the number of training tokens for every doubling of tokens