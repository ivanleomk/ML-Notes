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

We can also perform [[Weight Pruning]] on the model itself to reduce the model size. These have unstructured and structured methods. The former considers individual weights while those that work primarily on networks structure are said to be structured in nature.

[[Knowledge Distillation]] remains a popular approach where we have the knowledge of a large model or an ensemble of models being used to teach a student model to reproduce teacher's outputs or its internal behaviour. We then utilise the student at inference time and discard the larger teacher model thereafter. 

![](assets/CleanShot%202024-06-13%20at%2018.01.19.png)

[[Mixed Precision]] is a useful method to reduce the precision that we store the weights in so that we can utilise less space to store these weights. This however will result in the lower performance of the model.

We can also use [[Micro Batches]] which are useful in helping to split the mini-batch into. By using micro batches, we immediately start computing the result of the gradients to obtain the gradients. 

Another possible approach is to use a [[Mixture Of Experts]] approach where we train multiple sub-networks within our model itself. This keeps the computational cost constant since the model always selects the same number of experts for each input regardless of the number of experts. These networks typically reach the same quality threshold faster when compared to dense networks with the same number of parameters.

## Transformer Approaches

Initial approaches focused heavily on modifying the attention mechanism. We can see this from the [[Sparse Transformer]] which reduced the complexity to $O(n \sqrt{n})$ using two different sparse attention patterns.
![](assets/CleanShot%202024-06-13%20at%2018.13.09.png)

We can see how strided attention allows for a local approach to dealing with token attention while fixed attention introduces global tokens at every $s$ steps. They generally are implemented by limiting the number of tokens that a single token can attend to or introduce global token.

We can also use [[Low Rank Factorisation]] to that approximates the attention with a low rank factorisation before performing the dot product. 

![](assets/CleanShot%202024-06-13%20at%2018.17.47.png)

We also had some architectural changes which proposed the use of segment based recurrence between windows. This however, results in the transformer model not being able to capture dependencies outside the FIFO memory range.
