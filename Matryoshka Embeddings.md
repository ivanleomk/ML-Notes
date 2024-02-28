# Problem Statement

Most models operate on a fixed dimensionality that is determined during training. This makes it difficult for optimisations to happen.

Matryoshka Embeddings provide a way for us to use models that have learnt embeddings that can encode information at different granularities, thus allowing us to now perform new optimisations that trade off accuracy for cost savings in memory/compute time.

Since the model learns coarse-to-fine representation vectors, intuitively it learns to share more semantic information across various dimensions.

## Use Cases

**Information Retrieval** - Shortlist retrieval candidates using the first few dimensions and then successively use more dimensions to re-rank the retrieved set.

**Efficient Classification** : Using a lower dimensionality where the model is able to determine/make the same prediction as per the full dimensionality

> Matryoshka Embeddings are as accurate as independently trained counterparts without the multiple expensive forward passes

## Intuition

Matryoshka embeddings aggregate losses after scaling with their relative important.

![[CleanShot 2024-02-29 at 03.52.19.png]]

In the example above, we utilise a simple linear classifier which allows us to use a multi-class softmax cross-entropy loss function. The model is then trained using sub-gradient descent methods.

Note that for ablations, we utilise $c_m$ as 1 for all dimensions.

# Ablations

## Representation Learning

![[CleanShot 2024-02-29 at 03.56.16.png]]
## Classification

Matryoshka Representations are up to 2% more accurate than their fixed-feature counterparts for the lower-dimensions while being as accurate elsewhere

![[CleanShot 2024-02-29 at 03.56.43.png]]

We can see that the MRL model outperforms the other classification models, especially at lower dimensionalities. 

MRL models are capable of performing accurate retrieval at various granularities without the additional expense of multiple model forward passes for the web-scale databases. FF models also generate independent databases which become prohibitively expense to store and switch in between.


## Adaptive Retrieval

![[CleanShot 2024-02-29 at 03.57.16.png]]

Even with adaptive retrieval, it is hard to determine the choice of Ds & Dr . In order to alleviate this issue to an extent, we propose Funnel Retrieval, a consistent cascade for adaptive retrieval. Funnel thins out the initial shortlist by a repeated re-ranking and shortlisting with a series of increasing capacity representations.

