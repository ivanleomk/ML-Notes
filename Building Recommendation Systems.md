
## Introduction

There are three core components of recommendation systems: The collector, ranker and server

- Collector: Know what is in the collection of things to be recommended
- Ranker : Re-order the collection provided
- Server: Take the ordered subset and ensure that the necessary data schema is satisfied and return the requested number of recommendations. 


| Method                  | Collector                                   | Ranker             | Server                                                                                           |
| ----------------------- | ------------------------------------------- | ------------------ | ------------------------------------------------------------------------------------------------ |
| Random Choice           | A random id is generated                    | This is a no-op    | We then return a chosen item or none                                                             |
| Most Popular Item       | Get the popularity for each individual item | Rank by popularity | Return either a list of items or non                                                             |
| MPI with k Armed Bandit | Get individual item popularities            | Rank by popularity | Set a threshold and sample to see if we exceed threshold. If we do, return a randomly chosen arm |

## Collaborative Filtering

### Overview

The essence of collaborative filtering is that those with similar tastes help others to know what they like. Typically we have a matrix where we have two axes - users and items.

The key thing to consider here is whether we prioritise user or item similarity.

- Item Similarity : We find an item that a user liked and try to find similar items
- User Similarity : We find another user that is similar to our our user and try to find similar users

### Ratings

What sort of data should we be collecting? There are a few different types of data that we can collect. Ultimately rich and verbose logging is one of the most important ways to improve a recommendation system.

There are two kinds of user ratings - soft and hard. Soft ratings are implicit feedback on an item while Hard ratings are an explicit form of feedback (Eg. a rating score)

Examples of soft ratings include

- Page Loads : If a user has seen an option, then they have the opportunity to click it. We need to account for the entire population of choices that the user was exposed to
- Page Views : If a user mouses over a specific section to try and discover more information about an item OR identify more items that are similar to it, this is a signal that we should definitely discover/log.
- Clicks : Clicks are an explicit expression of interest and are often times included in the KPI of the recommendation team itself. Modern systems have included the ordering of these clicks into the systems as [[Sequential Recomendations]]
- Add to Bag : This is an **extremely strong indicator of interest** and is often correlated with purchasing. 

Ideally we want to use a mix of these two ratings because they each give different forms of signals. These soft ratings are collected by logging events and then sending it to a consumer to be stored elsewhere for analysis. We can even connect an event stream to a sequence of transformations to process the data for downstream learning tasks

Often times, we collect this data to identify if our funnel is working as intended. A funnel in this case is simply a collection of steps that a user must take to get from one state to another. This helps us to understand how good our recommendation system is performing at each individual portion.

### Dataset Considerations

There are a few important things to consider when looking at user ranking data

1. Sparsity : The least popular items are starved for data and recommendations. The matrix becomes more sparse over time. This means that certain items/users will tend to dominate the recommendations.
 
2. Popularity : The most popular items attract the most attention and widen the gap with other items significantly. 

Therefore, it's necessary to factor in specific implementations so that we can serve up good recommendations

### Multi armed Bandits

The basis strategy for an explore-exploit scheme is to take not only the outcome-maximising recommendation but also a collection of alternative variants and randomly determine which to use as a response.

In short, the agent has a prior assumption about what is the greatest expected reward but explores other alternatives with some frequency so that its prior is constantly being updated.

# Content-Based Filtering

We can instead utilise vector representations of indiv