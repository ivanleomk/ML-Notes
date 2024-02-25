## Datasets

### Features

Machine Learning projects live and die by the quality of their datasets. These datasets will have what are known as features, which are numbers representing a specific measurement. A feature vector is a set of these numbers used as a single input to the model.

Typically we can have a variety of different types of values for our features
- **Continuous**: These are floating point values that are continuous
- **Interval Values**: These are single integers which are discrete 
- **Ordinal Values**: These are encoded values which represent a specific ordering of values. However the differences between these values are not necessarily the same
- **Categorical**: These would be considered one-hot encoded values. In order to use one-hot encoded values, we need to make sure that the categories we're working with are mutually exclusive

Typically as the number of features that our model considers grows, the number of values contained within our set of possible values grows exponentially. This causes the **curse of dimensionality** which refers to the challenge of analysing and organising data in high-dimensional spaces.

### What makes a good dataset?

Typically when we want to look at a dataset, there are a few things we should consider

1. **Parent Distribution**: Does it accurately consider the different classes that exist within the real unknown distribution. Ultimately the dataset should cover the variation within the classes that the model will see when predicting labels for unknown inputs
2. **Confusers**: Our dataset needs to include a lot of examples that show the fine-grained differences between the different classes/labels we'd like our model to learn. These are particularly important
3. **Size**: The model typically improves in performance with a larger dataset but that comes at the cost of a more expensive training job or cost to acquire the data. Additionally, models tend to have a capacity - which is the complexity that they can support relative to the amount of training data available. 
### Dataset Preparation

When working with a dataset, it's important to work on cleaning our data itself. There are three things that we care about here 

1. The features
2. Data contamination
3. Dataset Size

#### Features

There are a few common things that we need to watch out for when working with a dataset

1. **Uneven Features**: We want to make sure that features lie within the same range. This is because if models are too large, then some features might dominate others and reduce the performance of our model. There are a few common tricks that we can use to do so including normalising our data by reducing the mean to 0 and the standard to 1
   
2. **Missing Features**: When we work with larger datasets, often times we'll have missing features within our dataset. In these cases, we need to fill in the missing values inside our rows. A good way to do so is to simply replace these values with the mean value of features over the dataset. Real data is always going to be better but the mean is the simplest substitution
   
3. **Mislabelled Data**: Often times you want to make sure that your data is as clean as it possibly can. This will involve manually looking through the data points to see if there are any potential problems with the dataset.
   
4. **Outlier Data** : When looking at data points, you'll want to make sure that you don't have any data points which are going to become a hindrance to the model. This is because any outliers will affect standardization significantly
#### Data Contamination

When working with data, we ideally want to separate our data into a Train, Test and Validation split. This helps us to see how our model performs on data that is out of distribution and ensure that it hasn't performed well due to overfitting on the dataset.

The breakdown of each split is seen below

- **Train**: This is the subset of data used to train our model. It's important here to select feature vectors that well represent the parent distribution of the data
- **Test**: We use this to test our model's performance and experiment with different hyper-parameters.
- **Validation**: We never train the model on this and we only use this sparingly. It's important here to do so because then we can accurately assess our model's performance.

Some common ways of generating the split are to 

- **Partition by Class**: When we do so, we ensure that the proportion of different classes are accurately represented as best as we can. This is important especially when working with datasets that have rare classes appearing.
- **Random Sampling**: Most of the time, if we have a large amount of data points, random sampling will allow us to have a split that is representative of the original dataset. 

Sometimes when we have insufficient data to work with a large split, we can instead work with k-folds validation. This means that we train `k` models with `1/k` of the data back for validation use at each step. We can then average out the metrics to get an idea of how a model trained on the whole dataset might behave.

### Dataset Size

Sometimes, we might not have enough data within our dataset. In such cases, we should consider using data augmentation in order to increase the number of samples our model can learn from. This can be done in a few ways

1. **Vision Datasets**: We can perform simple transformations such as cropping the image, changing the colour of the image to create new training dataset pairs. This ensures that our model is more robust to different changes and variations

It's important that any augmentations to a original training dataset example stay within the same split. This is very important to make sure of.