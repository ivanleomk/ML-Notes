## Numpy

`numpy` adds in a missing array data type to python so that we can perform calculations quickly and efficiently. That's why it requires the use of a data type because it helps numpy perform its optimisations more effectively.
### Efficient Indexing

We can index into `numpy` arrays by using a slice notation

```python
>>> import numpy as np
>>> b = np.zeros((3,4),dtype='uint8')
>>> b
array([[0, 0, 0, 0],
       [0, 0, 0, 0],
       [0, 0, 0, 0]], dtype=uint8)
>>> b[0,1]=2
>>> b[0,3]=4
>>> b
array([[0, 2, 0, 4],
       [0, 0, 0, 0],
       [0, 0, 0, 0]], dtype=uint8)
```

We can also select entire rows by using ranges

```
>>> a
array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> a[1:10:2]
array([1, 3, 5, 7, 9])
>>> a[0:10:2]
array([0, 2, 4, 6, 8])
>>> 
```

The same goes for multidimensional numpy arrays

```
>>> b = np.arange(27).reshape((3,3,3))
>>> b
array([[[ 0,  1,  2],
        [ 3,  4,  5],
        [ 6,  7,  8]],

       [[ 9, 10, 11],
        [12, 13, 14],
        [15, 16, 17]],

       [[18, 19, 20],
        [21, 22, 23],
        [24, 25, 26]]])
>>> b[1,:,:]
array([[ 9, 10, 11],
       [12, 13, 14],
       [15, 16, 17]])
```

### Save to Disk

Numpy also allows us to save files to disc by using a `.npy` extension

```
>>> a = np.arange(27).reshape((3,9))
>>> np.save("a.npy",a)
>>> b = np.load("a.npy")
>>> b == a
array([[ True,  True,  True,  True,  True,  True,  True,  True,  True],
       [ True,  True,  True,  True,  True,  True,  True,  True,  True],
       [ True,  True,  True,  True,  True,  True,  True,  True,  True]])
```

We can also save a collection of arrays to a single `.npz` file for convinience

```
>>> a
array([[ 0,  1,  2,  3,  4,  5,  6,  7,  8],
       [ 9, 10, 11, 12, 13, 14, 15, 16, 17],
       [18, 19, 20, 21, 22, 23, 24, 25, 26]])
>>> c
array([[ 5,  6,  7,  8,  9],
       [10, 11, 12, 13, 14],
       [15, 16, 17, 18, 19],
       [20, 21, 22, 23, 24],
       [25, 26, 27, 28, 29]])
>>> np.savez("combi.npz",a=a,c=c)
>>> np.load("combi.npz")
NpzFile 'combi.npz' with keys: a, c
>>> np.load("combi.npz")["a"]
array([[ 0,  1,  2,  3,  4,  5,  6,  7,  8],
       [ 9, 10, 11, 12, 13, 14, 15, 16, 17],
       [18, 19, 20, 21, 22, 23, 24, 25, 26]])
```

## Datasets

When [[Working with Datasets]], we need to thoroughly investigate our dataset to make sure there's nothing funny going on with it.

# Classical machine Learning

We can still apply older machine learning methods to help us deal with cases where we have a small amount of data points and a newer model might be overkill. Here are some useful traditional approaches that were used pre deep learning.
## K-Nearest Centroids

The algorithm works by randomly placing 'K' centroids in the data space and assigning each data point to the nearest centroid. The centroids are then updated to be the mean of all points assigned to them. This process is repeated until the centroids no longer move significantly or a certain number of iterations have been reached

However, since we're using a single point, key problems are that 

- We're might have overlapping centroids, as a result this makes it difficult to efficiently predict clusters sometimes
- As the number of centroids increases, this makes it difficult to work with

## K - Nearest Neighbours

The K-NN algorithm works by considering the 'K' closest neighbours to a new data point in the training dataset and assigns the new data point to the category that has the maximum number of neighbours. For instance, if 'K' is set to 5, the algorithm will look at the five nearest neighbours to the new data point. If three of these neighbours belong to category A and two belong to category B, the new data point will be assigned to category A, as it has the majority of neighbours.

## Naive-Bayes

Naive Bayes is a simple probabilistic classifier based on applying Bayes' theorem with strong (naive) independence assumptions between the features. It's called "naive" because it assumes that the features of a data point are independent of each other, which is often not the case in reality.

Also, if a categorical variable has a category in the test data set that wasn't included in the training data set, then the model will assign it a 0 probability and will be unable to make a prediction. This is known as the Zero Frequency problem

## Decision Trees

Decision Trees are used to classify items. Each node defines a set of conditions and based on the result of the evaluation, the sample is then further processed in the decision tree.

When building a decision tree, we brute force across all of the different values until we find a good split between all of the samples within our dataset. The goal of the decision tree here is to maximise the Gini index within the samples at that node recursively.

It terminates once we've subdivided all the nodes and have the min number of nodes defined inside a sample. 

It's worthwhile here to note that decision trees tend to work well with categorical and discrete data. They also tend to grow very large and overfit on the training dataset unless we manage it well with depth parameters.
## Random Forest

A way to get around the dimensionality issue with a decision tree is to use a random forest. In this case, we utilise a collection of multiple decision trees, each one trained with a random subset of the training dataset which is sampled with replacement from the original dataset.

This breaks the correlation between the trees and increases the robustness of the classifier. In practice, each tree will randomly select $\sqrt{n}$ features assuming you have $n$ features in your dataset.

## Support Vector Machines

This aims to learn a hyperplane to separate groups of data points. It was popular for some time due to the fact that it's computationally efficient and has good performance. It's fallen behind to some degree nowadays.




