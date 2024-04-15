> Original Source: https://kaitchup.substack.com/p/a-guide-on-hyperparameters-and-training

#thedailykaitchup #finetuning #hyperparameters

There are a few important hyper-parameters that we need to configure when working with large language models.

1. Batch Size
2. Sequence Length
3. Epochs and Steps

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

