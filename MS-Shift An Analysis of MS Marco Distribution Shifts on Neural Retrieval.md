> Arxiv : https://arxiv.org/abs/2205.02870

Pre Trained Language Models are able to extract a significant amount of contextual information. We can encode this information by using encoder-heavy models such as BERT which can not only extract semantic information but also encode the context in which the words are used in.

# Approach

They create three different clusters

1. Semantic Clustering - use K Means to generate 5 clusters
2. WH-Words Queries - Split the train and test set by manually building clusters based on queries related to definitions, instructions and the more general questions 
3. Short and Long Queries - Split the train set into groups of short and long queries with `6` being the cut off

## Semantic Clustering

Semantic clustering was done as follows

1. K-Means on `[CLS]` representation of the MS Marco queries to build 100 initial clusters
2. Selecting the five clusters that maximize the sum of pairwise l2 distances
3. Expand the five native clusters until they have no overlap

## WH-Words

Thy investigate query styles and goals through question words. This results in 3 manual clusters being built

1. Definition Queries : What, definition
2. Instruction Queries : How
3. Persons, locations and context ( Who, When, Where, Which )

This then creates three train-test sets which are 10M and 3500 elements large each