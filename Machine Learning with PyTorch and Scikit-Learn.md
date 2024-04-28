## Pytorch

Pytorch relies on building out a computation graph to derive relationships betwen tensors from the input all the way to the output. It's useful for helping us to work with multiple devices easily and compute the gradients of the loss with respect to the NN weights.

### Modules

In cases where we want to define a new layer that isn't supported by PyTorch, we can define a new class with the `nn.Module` class. This helps us to potentially implement/work with layers that are customized to our needs.
### DataLoaders

We can use DataLoaders in order to easily access and batch data. There are two ways to do this

1. Pass a generator over to Pytorch's `Dataloader`
2. Define a custom `Dataset` object and then pass it over to a `DataLoader`

```python
import torch
from torch.utils.data import Dataset
from torch.utils.data import DataLoader

class JointDataset(Dataset):
    def __init__(self,x,y):
        self.x = x
        self.y = y
    
    def __len__(self):
        return len(self.x)

data_loader = DataLoader(dataset=joint_dataset,batch_size=2,shuffle=True)
```

The beauty of using the DataLoader and Dataset classes is that we have a tremendous amount of functionality implemented for us out of the box. We can also implement more complex functionality.

```python
class ImageDataset(Dataset):
    def __init__(self, file_list, labels, transform=None):
        self.file_list = file_list
        self.labels = labels
        self.transform = transform
    def __getitem__(self, index):
        img = Image.open(self.file_list[index])        
        if self.transform is not None:
            img = self.transform(img)
        label = self.labels[index]
        return img, label
    def __len__(self):
        return len(self.labels)
```

In this example above, we're doing transformations on an image given a file path and then returning the transformed image and the label for each item.

When choosing our loss function we need to make sure we get the right tool for the job. Some things to consider are that
- Logistic Functions go from 0 -> 1 and try to identify a threshold for a binary classification job
- Softmax allows us to convert a real number valued vector to a set of probabilities ( by normalising every value so that it essentially sums to 1. )
- When choosing between a logistic function and a tanh, tanh might be a better choice by virtue of it's larger range. This means that it has a larger space for values to flow.

![|300](assets/Screenshot%202024-04-28%20at%2012.43.51%20AM.png)

# Pytorch Lightning

Pytorch Lightning is an extension built on top of Pytorch that allows us to be able to train models at a distributed scale. It provides more methods such as 

- `training_step` : It defines a single forward pass during training which is executed to process each individual batch
- `validation_step`: This is executed on a single batch of data during the validation step
- `test_step`: This is executed on a single batch of data during the test stage

It also provides easy utilities such as `torchmetrics` which allows us to compute metrics such as Accuracy, Recall, Precision etc.
