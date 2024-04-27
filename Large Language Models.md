
# Introduction

LLMs are a new form of language models which have a tremendous ability to understand, generate and interpret human language. They are incredibly useful because they are able to perform many tasks without having handcrafted rules or specialised datasets.

Fundamentally, these are models that are trained to understand, generate and respond to human-like text. They are considered large because their parameters tend to scale up to the hundreds of billions. They are trained in a self-supervised manner by being made to predict the next token.

They utilise a [[Transformer Architecture]] which allows them to pay selective attention to different parts of the input when making predictions. Typically training for these models happens in 2 stages

1. Pre-training : This is when the model is trained on a large corpus of text data and is made to predict the next token. This creates what is known as a **base model** 
2. Finetuning : Once the model knows how to complete sentences, we then perform either [[Instruction Finetuning]] or [[Classification Finetuning]] on this base model. 

This process varies from model to model. Some popular algorithms are 

1. [RLHF](/RLHF.md)

# Text Processing for LLMs

Large Language Models cannot understand text. Therefore, for large models like ChatGPT, any text that they work with is always going to be tokenised using a known tokenisation scheme.

Common examples are [Byte Pair Encoding](Byte%20Pair%20Encoding.md) and [[Sentence Piece]]. It's important here to note that the language model never sees the text, it only sees the token Ids.![image | 400](assets/Screenshot%202024-04-26%20at%201.58.51%20PM.png)

# Attention

Translation is difficult because the sentence cannot be translated word by word. As a result, for each chunk of words/portion of the sentence, there's a need to be able to refer to the entire context of the sentence.

![](assets/Screenshot%202024-04-26%20at%202.02.54%20PM.png)
This was originally done in an encoder-decoder architecture setup where we had a RNN encode information iteratively with each token into its hidden state before it passed this hidden state into a decoder.

However, this made it difficult for the RNN to selectively gate information when it found the need to refer to prior state. Therefore this resulted in the introduction of [[Bahdanau Attention]] which gave a RNN decoder network access to the encoder state for each token. It would then combine these hidden states into a single representation.

This mechanism was subsequently adopted in the transformer architecture that allows us to selectively weight token representations according to their relevance to a specific token. [[Attention Is All You Need]] introduced the concept of [[Scaled Dot Attention Product]] which scales the qk matrix by the root of the embedding dimensionality in order to avoid small gradients.