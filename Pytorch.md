> Pytorch is an easy library that helps us to easily work with neural networks. It's main use-case is for easy optimisation of large computational graphs

Pytorch operates at the level of a tensor - this is what enables efficient and fast computation of gradients. We can perform a single optimisation step for a neural network as seen below.

```python
import torch.optim as optim

# create your optimizer
optimizer = optim.SGD(net.parameters(), lr=0.01)
criterion = nn.MSELoss()

# in your training loop:
optimizer.zero_grad()   # zero the gradient buffers
output = net(input)
loss = criterion(output, target)
loss.backward()
optimizer.step()    # Does the update
```

