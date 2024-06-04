
Ranking documents/chunks in response to a query that we have is fundamentally different from regression and classification

- We're not just doing a classification of whether a chunk is relevant or not, we need an ordering
- We can't just output a single scalar score because each chunk is going to be compared to one another - therefore we need to consider not only the relevance to the query but how one is better than the other

Therefore a common way to encode the training data is a pairwise comparison

```
f(Query, (chunk_1,chunk_2)) -> 0
f(Query, (chunk_2,chunk_1)) -> 1 
```

Note here that `f(query,chunks)` outputs a classification of whether we should rank the first element in the pair ahead of the second.

# Classification

### Accuracy, Precision and Recall

When we look at Classification Metrics - we can look at Accuracy, Precision and Recall. 

Precision - % of correctly labelled positive instances out of all positive labelled instances
Recall - % of correctly labelled positive instances out of all positive instances

In short we can think of Precision vs Recall as two different questions

1. How many retrieved items are relevant?
2. How many relevant items were retrieved?

## NDCG




