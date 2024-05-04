JAX is a functional programming language that is a competitor to [Pytorch](Pytorch.md). Often times, we'll find that Jax has a different way of operating as compared to Pytorch due to its functional nature.

## Generating Random Seeds

```python
import jax.random as random
key = random.PRNGKey(0)
x = random.uniform(key,shape=[3,3])
print(x)

key,subkey = random.split(key)
x = random.uniform(key,shape=[3,3])
x

y = random.uniform(subkey,shape=[3,3])
y
```

