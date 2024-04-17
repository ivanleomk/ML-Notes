# Introduction

Recommendation systems are important in many production systems. While most commonly used in e-commerce or video applications, they're present in a variety of other cases.

Some examples include Netflix and Amazon, which use Carousel based recommendation systems and Linkedin that uses your network to make content recommendations to you.

## Types

There are 3 broad categories of personalised Recommendation Systems

1. Collaborative Filtering : Where we use a matrix of rankings to determine a vector of User and Item factors. This subsequently helps us to be able to calculate the probability of a successful recommendation
2. Content-Based Filtering: Where we use embeddings to learn the semantic meaning of the items and the users. These are learned embeddings and are derived from a separate process as compared to collaborative filtering.
3. Hybrid Models: These combine the two of them

## Architecture

Often times we'll see what's known as a two-tower architecture


In this architecture, we learn a separate encoding for the item and another for the user. This is then combined with other bits of information to generate a 
