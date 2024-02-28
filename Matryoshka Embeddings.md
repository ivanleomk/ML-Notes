
Questions
? : What's the rationale behind the renormalization that we need to do with OpenAI Embeddings ( https://ujjwalm29.medium.com/matryoshka-representation-learning-a-guide-to-faster-semantic-search-1c9025543530 ) when it should be able to seamlessly interpolate

> We forgot to account for an important vector operation that OpenAI applies to all of their embeddings: normalization. Embeddings are normalized in order to make them compatible with similarity functions like dot product. A normalized vector means that its length (magnitude) is 1 - also referred to as a unit vector.
> 
> It's important to remember that as soon as we truncate a unit vector, that new vector is no longer normalized. If we expect to see the same output as OpenAI, we need to renormalize it:
