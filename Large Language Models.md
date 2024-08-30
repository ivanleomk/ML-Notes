# Introduction 

Large Language Models are unique in that they can respond to a user's query in a natural manner. This enables more natural forms of conversation and makes them invaluable for any task that requires parsing and generating text.

## Attention

LLMs are powerful because of the self-attention mechanism that they've learnt how to apply. There are two forms of self-attention that are widely used.

1. **Self-Attention** : This is when a model is able to weight the importance of every previous token w.r.t itself. It cannot see tokens that are after it.
2. **Bidirectional Self-Attention**: This is when a model is trained to utilise the full context of the tokens. it can see every single token in the context window.

GPT mainly uses Self-Attention while something like BERT uses Bidirectional Self-Attention. This is because GPT is a decoder based model while BERT is a encoder based model.

## Training 

LLMs are trained in a few stages. These can be described as 

1. **Base Foundation Model training** : We train the large language model on a large corpus of unlabelled text. It's sole job is to complete the text chunk and predict the next token
2. **Fine-Tuning** : Once we've obtained a fine-tuned LLM, we can then fine-tune it to learn how to follow instructions or for classification tasks. 

### Next Token Prediction

When training LLMs, we are able to utilise [[Self Supervised Learning]] because our models are trained to predict the next token. This means that we have natural labels generated from the data 

Interestingly, this creates the concept of [[Emergent Behaviours]] which are capabilities that the model wasn't trained for. This is because of the diverse context of the information that the model is exposed to. 

# Training Datasets

When working with multi-modal data, we need to convert the data into a vector representation. This is done through an [[encoder]] which helps us to convert the data into a representation that our LLM can work with.

An early example of an encoder that worked was [[Word2Vec]] that trained neural network architectures to generate embeddings by predicting a completion for a word given a set of target words. When we are training our LLMs, they learn to generate these representations during their training.

This makes it more efficient to utilise a LLM's own native embeddings if possible because they are task-specific as compared to a more general implementation like [Word2Vec](Word2Vec). 

## Tokenization