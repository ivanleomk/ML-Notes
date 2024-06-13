RAG is the art of stitching together Retrieval and Generation to ground the latter. The retrieval comes from [[Information Retrieval]] while the LLM handles the generation.

## Similarity Search

A typical method is called a Bi Encoder approach which combines the use of a single embedding model to embed documents and queries. Cosine similarity is then used to determine the relevance a specific document with respect to the query

![](assets/CleanShot%202024-06-13%20at%2020.13.56.png)

This is a good approach because it is computationally efficient. In order to run inference, all we need is to encode a single query instead of re-encoding all of the documents. However, this comes along with retrieval performance tradeoffs.

A more accurate but computationally expensive way is to use a [[Cross Encoder]] which computes a query-aware document representation. A Cross Encoder is fundamentally a binary classifier which outputs a probability of the document being relevant to the query.

Another method is called a [[Reranker]] which uses a simple idea - leveraging a powerful but computationally expensive model to score only a subset of your documents, previously retrieved by a more efficient model.

