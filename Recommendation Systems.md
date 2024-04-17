# Introduction

Recommendation systems are important in many production systems. While most commonly used in e-commerce or video applications, they're present in a variety of other cases.

Some examples include Netflix and Amazon, which use Carousel based recommendation systems and Linkedin that uses your network to make content recommendations to you.

## Types

There are 3 broad categories of personalised Recommendation Systems

1. Collaborative Filtering : Where we use a matrix of rankings to determine a vector of User and Item factors. This subsequently helps us to be able to calculate the probability of a successful recommendation
2. Content-Based Filtering: Where we use embeddings to learn the semantic meaning of the items and the users. These are learned embeddings and are derived from a separate process as compared to collaborative filtering.
3. Hybrid Models: These combine the two of them

We want to use Collaborative filtering systems when we have a good amount of data because they are cheap and fast to train. We want to use content-based filtering when we have no user data and are starting from zero. Ideally, we combine both to get information from user signals and content signals.

## Architecture

Often times we'll see what's known as a two-tower architecture

In this architecture, we learn a separate encoding for the item and another for the user. This is then projected into the same latent space and we can calculate a similarity score based off this.

![[Pasted image 20240417224503.png | 400]]
This might be used as the final step as a way to filter out irrelevant items. 

## Metrics

When looking at recommendation systems, we want to look at different metrics. Two useful metrics are precision and recall. Often times, we might take a `metric@k` which means that we perform the calculation on a slice of `k` items from the predictions.

Say for instance we had 5 known relevant items and fetched 10 predictions, 2 of which were relevant. This would mean that our precision would be $\frac{2}{10}$ while our recall would be $\frac{2}{5}=0.4$

![|400](https://i.stack.imgur.com/W8rc6.png)


