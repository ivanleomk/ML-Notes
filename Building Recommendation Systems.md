
## Introduction

There are three core components of recommendation systems: The collector, ranker and server

- Collector: Know what is in the collection of things to be recommended
- Ranker : Re-order the collection provided
- Server: Take the ordered subset and ensure that the necessary data schema is satisfied and return the requested number of recommendations. 


| Method            | Collector                                   | Ranker                    | Server                               |
| ----------------- | ------------------------------------------- | ------------------------- | ------------------------------------ |
| Random Choice     | A random id is generated                    | This is a no-op           | We then return a chosen item or none |
| Most Popular Item | Get the popularity for each individual item | Rank by sorting on values | Return either a list of items or non | 

## Collaborative Filtering

The essence of collaborative filtering is that those with similar tastes help others to know what they like. Typically we have a matrix where we have two axes - users and items.

The key thing to consider here is whether we prioritise user or item similarity.

- Item Similarity : We find an item that a user liked and try to find similar items
- User Similarity : We find another user that is similar to our our user and try to find similar users

We need to often consider user ratings. These are critical for training effective