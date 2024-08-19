Routing is necessary because we're making a bet that a local decision model will outperform a global decision model (Eg. Google Maps will be much better at helping you determine what's the nearest bakery to you than google search )

We can improve the quality of our retrievals by doing two things

- Just use a re-ranker
- Develop our own re-ranker

How can we improve candidate selection. There are two main ways

1. We can expose existing structured data as additional filtering criteria (Eg. including calendar months, generating automatic categories )
2. We can generate synthetic data and text chunks to our original text chunks (Eg. we can extract specific information about the chunk or image that we're looking at )

But fundamentally, we're just generating more indexes and pointers that act as augmented materialised views.

> Routing is just a classification task

Visual Language Models are trained on captioning data therefore it's difficult to extract an answer from a model sometimes. Multimodal embeddings might make cost sense but it's not always that the embedding will match 