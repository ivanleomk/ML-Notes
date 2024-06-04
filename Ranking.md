# Problem Setup

Ranking documents/chunks in response to a query that we have is fundamentally different from regression and classification

- We're not just doing a classification of whether a chunk is relevant or not, we need an ordering
- We're not just predicting a number here because we need to also consider the generated value with regard to the other row items

Therefore a common way to encode the training data is a pairwise comparison

```
f(Query, (chunk_1,chunk_2)) -> 0
f(Query, (chunk_2,chunk_1)) -> 1 
```

Note here that `f(query,chunks)` outputs a classification of whether we should rank the first element in the pair ahead of the second.

## Generating Dataset

We have two main ways of generating a labelled dataset to train a ranking model

1. Using a Corpus centric approach
2. Closed Loop

## Corpus Centric

We generate some queries from the dataset / sample from an active production system in order to benchmark the results of our query itself. We can then get actual human labellers to go and score the relevance/quality of the retrieved items relative to one another.

This can be combined with [[Active Learning]] where we continuously train our model over time with actual production data.

## Closed Loop

We record the interactions between the user and the application itself. We're tracking metrics such as Click Through Rate and other outcomes.

When we have these set-ups, we want to incorporate some degree of exploitation and exploration.
- We want to explore new potential items that we don't have with a probability of $\epsilon$ 
- We exploit otherwise the known value

This allows us to see how the users respond to new choices that weren't in the original dataset.

# Metrics

## Accuracy, Precision and Recall

When we look at Classification Metrics - we can look at Accuracy, Precision and Recall. 

Precision - % of correctly labelled positive instances out of all positive labelled instances
Recall - % of correctly labelled positive instances out of all positive instances

In short we can think of Precision vs Recall as two different questions

1. How many retrieved items are relevant?
2. How many relevant items were retrieved?

## NDCG

This is used when we have relevance metrics for each of the retrieved items. Typically we might use a score from 0 -> 3 where a higher score indicates a more relevant item.



# Key Considerations

When looking at ranking models, a key reason why we want to have these metrics is because we need to balance latency and cost of our system.

Often times, with a more complex system we can get a better result. But we also need to weight the cost of implementation and the extra latency with an actual quantifiable/comparable metric that we can use as an evaluator between these different implementations

Additionally it gives us much more flexibility in terms of choosing what to cache/work with. With hard metrics, we can also start to more accurately segregate and segment the different questions that our model struggles with.

This helps us deliver a better service if we can give users a disclaimer that certain features are just not supported.
