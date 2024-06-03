
Ranking documents/chunks in response to a query that we have is fundamentally different from regression and classification

- We're not just doing a classification of whether a chunk is relevant or not, we need an ordering
- We can't just output a single scalar score because each chunk is going to be related to one another - therefore we need to consider not only the relevance to the query but how one is better than the other

# Classification

### Accuracy, Precision and Recall

When we look at Classification Metrics - we can look at Accuracy, Precision and Recall. 

Precision - % of correctly labelled positive instances out of all positive labelled instances
Recall - % of correctly labelled positive instances out of all positive instances

In short we can think of Precision vs Recall as two different questions

1. How many retrieved items are relevant?
2. How many relevant items were retrieved?

## NDCG




