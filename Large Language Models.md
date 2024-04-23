
# Introduction

LLMs are a new form of language models which have a tremendous ability to understand, generate and interpret human language. They are incredibly useful because they are able to perform many tasks without having handcrafted rules or specialised datasets.

Fundamentally, these are models that are trained to understand, generate and respond to human-like text. They are considered large because their parameters tend to scale up to the hundreds of billions. They are trained in a self-supervised manner by being made to predict the next token.

They utilise a [[Transformer Architecture]] which allows them to pay selective attention to different parts of the input when making predictions. Typically training for these models happens in 2 stages

1. Pre-training : This is when the model is trained on a large corpus of text data and is made to predict the next token. This creates what is known as a **base model** 
2. Finetuning : Once the model knows how to complete sentences, we then perform either [[Instruction Finetuning]] or [[Classification Finetuning]] on this base model. 

This process varies from model to model. Some popular algorithms are 

1. [[RLHF]]

# Text Processing for LLMs

