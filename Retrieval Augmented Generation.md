RAG is the art of stitching together Retrieval and Generation to ground the latter. The retrieval comes from [[Information Retrieval]] while the LLM handles the generation.

A typical method is called a [[Bi-Encoder]] approach which combines the use of a single embedding model to embed documents and queries. Cosine similarity is then used to determine the relevance a specific document with respect to the query

![](assets/CleanShot%202024-06-13%20at%2020.13.56.png)

This is a good approach because it is computationally efficient. In order to run inference, all we need is to encode a single query instead of re-encoding all of the documents. However, this comes along with retrieval performance tradeoffs.

A more accurate but computationally expensive way is to use a [[Cross Encoder]] which computes a query-aware document representation. A Cross Encoder is fundamentally a binary classifier which outputs a probability of the document being relevant to the query.

Another method is called a [[Reranker]] which uses a simple idea - leveraging a powerful but computationally expensive model to score only a subset of your documents, previously retrieved by a more efficient model. 

However, semantic search via embeddings will result in information loss. A few reasons are
- Embeddings learn to represent information that is useful to their training queries. This will never be fully representative of your query or dataset
- Compressing information from hundreds of tokens to a single vector is bound to lose information
- Humans love to use keywords such as certain acronyms, domain-specific words etc

We can utilise [[BM25]] which is a variant of the [[TF-IDF]] representation. It is specifically strong because it deals well with domain-specific jargon. 

![](assets/CleanShot%202024-06-13%20at%2020.27.01.png)

## Fine Tuning

If we're fine-tuning our [Bi-Encoder](Bi-Encoder) and Cross Encoder, ideally we'd like our [Bi-Encoder](Bi-Encoder)
 to be more coarse grained and our [Cross Encoder](Cross%20Encoder) to be more specific
## Metadata Search

Documents do not exist in a vacuum. There's a lot of metadata around them, some of which can be very informative. (Eg. A query for a specific document for a time period Q4)

The model needs to represent all of the main request. If we provide it a lot of irrelevant financial reports to your LLM, it might not work great.

Therefore we just need an entity detection model such as [[GliNER]] which can do zero-shot entity detection. 

![](assets/CleanShot%202024-06-13%20at%2020.29.37.png)

## Other Improvements

## Query Expansion
We can also utilise query/document sparse expansion such as [[SPLADE]].


### Multi-Vector Representations

We can also usemulti-vector representations such as [[ColBERT]] in order to improve the efficiency of individual retrieval pipelines. 

### Clustering/Topic Modelling

We can use [[Topic Modelling]] as a way to identify clusters in our user queries that we can then process idependently.

This will involve

1. Selecting a subset of queries
2. Using [[t-SNE]] to understand how the data distribution looks like
3. Using a [[Gensim]] [[Coherence Model]] to determine the best number of topics and clusters
4. Then using [[LDA]] to cluster topics. Ideally we can start with a higher value of `k` and then work towards finding better representations
