> Original Source: https://kaitchup.substack.com/p/a-guide-on-hyperparameters-and-training

#thedailykaitchup #finetuning #hyperparameters

There are a few important hyper-parameters that we need to configure when working with large language models.

1. Batch Size
2. Sequence Length
3. Epochs and Steps
4. Learning Rate
5. Schedulers
6. Regularisation and Optimisers
7. Float16 vs bFloat16

## Batch Size

Larger batch sizes yield better models and accelerate training. This is because our model overfits less to a specific example and sees a more representative sample of the true population with a larger batch.

Ideally we want to increase batch size until the model goes out of memory. GPU s are optimised for specific batch sizes. Therefore, we should avoid odd numbers and instead set a batch size to 9 or 13.

## Sequence Length

When working with larger batches, we need to pad our examples so that they're all of the same size. This allows our model to efficiently process these inputs.

```
tokenizer.padding_side = "left"
tokenizer.pad_token = tokenizer.unk_token
input = tokenizer(prompts, padding='max_length', max_length=20, return_tensors="pt");
```

We can achieve this using the `trl` library which allows us to pad our token inputs

## Epochs and steps

> Sometimes if we're using a target batch size which is larger than the device's capacity, we'll end up accumulating the gradients over several steps. Once we've accumulated all of the gradients, then we'll update the weights
> 
> Additionally, if memory is a big constraint, we might use gradient checkpointing, which involves recomputing intermediate states instead of keeping it in memory. This reduces memory consumption by ~40% in some cases, especially as batch sizes increase.

A training step occurs when the model's weights are updated - this happens per batch since we back propagate the loss from the batch to the weights. An epoch occurs when every example in the training dataset has been presented to the model exactly once. 

By training for more epochs, we can expose the model to the same data multiple times, with the hopes of it learning more each time. This corresponds to the `num_train_epochs` or `max_steps` in the `transformers` trainer arguments. If epochs are set, then the `max_steps` will be ignored.

## Learning Rate

The learning rate controls the speed at which the model updates its weights during training. It controls the size of the steps that the model takes. If the learning rate is too high, then our model might not converge to an optimal solution. On the contrary, if the learning rate is too low, this might result in very slow convergence.

## Schedulers

When working with models, we might want to vary the learning rate at different stages of the training process. This can be done using a learning rate scheduler. Typically, we have a few different options to choose from - linear, cosine and constant schedulers. 

The linear scheduler is a good choice in a majority of situations. Typically we would combine this linear scheduler with warmup steps so that our learning rate is incrementally increased from a lower initial value to the desired value. Warmup Ratio of 10% would mean that out of 10,000 steps, we would use 1,000 of them to build up to the learning rate we want. We can alternatively specify a fixed number of warmup steps.


## Regularisation

We can encourage our model to have smaller weights by adding a term to the loss function that includes the sum of squares of the weights. This gently pushes the weights towards zero.

A stronger value of regularisation imposes a stronger penalty on large weights and aims to discourage the model from relying too heavily on any individual input feature. This is normally set to `0` in hugging face

### Optimiser

Typically we'd use something like AdamW to be able to optimise our model's parameters. AdamW is the most commonly used algorithm and decouples the update from the weight decay term. This helps to increase the regularisation and prevent it from getting mixed up with gradient updates


## BFloat16 vs Float16

The key difference between the two lies in how they allocate bits to the exponent and fraction, with bfloat16's design allowing for broader range handling without significantly affecting computational accuracy, thus optimizing it for high-speed and memory-efficient deep learning operations.

bfloat16 is better but is only supported by GPUs from the Ampere generation or more recent. If your GPU is compatible, use bfloat16. If not, use float16, but if you have some overflow issues (e.g., the loss falls to 0.0 or NaN), you might have to use float32.

