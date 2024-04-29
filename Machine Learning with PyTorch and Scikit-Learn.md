
Pytorch relies on building out a computation graph to derive relationships betwen tensors from the input all the way to the output. It's useful for helping us to work with multiple devices easily and compute the gradients of the loss with respect to the NN weights.

## Modules

In cases where we want to define a new layer that isn't supported by PyTorch, we can define a new class with the `nn.Module` class. This helps us to potentially implement/work with layers that are customized to our needs.
## DataLoaders

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
### Transformations

Transformations help us to transform our input data into a form that works well with our model. In order to use Transformations, we can either code up our own or use inbuilt ones provided by Pytorch

```python
class ToTensor:
    def __call__(self,sample):
        inputs, targets = sample
        return torch.from_numpy(inputs), torch.from_numpy(targets)

class MulTransform:
    def __init__(self,factor):
        self.factor = factor
    
    def __call__(self,sample):
        inputs,target = sample
        inputs *= self.factor
        return inputs,target

composed = torchvision.transforms.Compose([
    ToTensor(),
    MulTransform(2)
])
```

We can see here how easily it is for us to scale up our transforms so that they are applied to inputs. We can then in turn use them in a `Dataset` object by doing

```python
class WineDataset(Dataset):

    def __init__(self, transform=None):
        xy = np.loadtxt('./data/wine/wine.csv', delimiter=',', dtype=np.float32, skiprows=1)
        self.n_samples = xy.shape[0]

        # note that we do not convert to tensor here
        self.x_data = xy[:, 1:]
        self.y_data = xy[:, [0]]

        self.transform = transform

    def __getitem__(self, index):
        sample = self.x_data[index], self.y_data[index]

        if self.transform:
            sample = self.transform(sample)

        return sample

    def __len__(self):
        return self.n_samples
```

## Activation Functions

We typically use an activation function after each layer so that our network can approximate more complex tasks.

- ReLU is a popular choice to be used in-between different layers
- If you're noticing the gradients vanishing, then work towards using a leaky ReLU

# Pytorch Lightning

Pytorch Lightning is an extension built on top of Pytorch that allows us to be able to train models at a distributed scale. It provides more methods such as 

- `training_step` : It defines a single forward pass during training which is executed to process each individual batch
- `validation_step`: This is executed on a single batch of data during the validation step
- `test_step`: This is executed on a single batch of data during the test stage

It also provides easy utilities such as `torchmetrics` which allows us to compute metrics such as Accuracy, Recall, Precision etc.
