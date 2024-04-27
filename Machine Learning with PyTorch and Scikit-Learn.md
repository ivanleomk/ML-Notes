## Pytorch

### Dataloaders

We can use Data Loaders in order to easily access and batch data. There are two ways to do this

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

The beauty of using the DataLoader and Dataset classes is that we have a tremendous amount of functionality implemented for us out of the box.