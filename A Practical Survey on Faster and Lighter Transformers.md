>  Sequences are a natural way to model long range dependencies and problems. In this paper, we investigate how the transformer helps solve several of issues that RNNs were not able to and how we can build faster and lighter transformer models using some optimisation methods

## Background

RNNs align the input and output sequences, allowing for a one-to-one mapping between the two sequences. However, due to the iterative generation/update of the context vector, it was often difficult to train these models on longer sequences.

They also struggled to perform well on long range dependencies because of the fixed-size nature of the hidden representation. Attention was first introduced by Bahdanau et Al which chose to compute a different representation of the input for each output step.

This eventually became the cornerstone of the [Transformer Architecture](Transformer%20Architecture) which relies on the attention mechanism to achieve a significant performance boost over that of the RNN models.

## Transformers

Transformers are useful because of their attention mechanism. Fundamentally the biggest challenge here is that the attention mechanism scales quadratically.

![](assets/CleanShot%202024-06-13%20at%2017.54.12.png)

This $QK^T$ multiplication requires $n^2$ computations and memory. Such attention is said to be full since any output position is able to attend to any input position. Quadratic complexity prevents researchers and practitioners from applying Transformers on long sequences.

## General Approaches

During training we can do some [[Gradient Checkpointing]] so that we only store the activations for a subset of the layers. This results in the gradients being recomputed for some of the layers, allowing for memory savings in return for increased computational cost.

Another possible approach is that of [[Parameter Sharing]] where we reduce the number of trainable parameters. This in turn means that we re-use different parameters for different layers so the number of back propagations we need to compute are significantly reduced.

We can also perform [[Weight Pruning]] on the model itself to reduce the model size. These have unstructured and structured methods. The former considers individual weights while