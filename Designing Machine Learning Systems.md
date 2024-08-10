# Introduction

Machine Learning Systems are useful in the following situations

1. **Capacity To Learn** : There has to be input and output pairs that are provided to the model so that it learns how to approximate some form of relationship between the two
2. **Patterns Exist** : There's no point getting a model to learn how to predict the next set of lottery numbers. This is because this is completely up to chance.
3. **Data is Available** : Data is necessary to train these models, and so we need to make sure that we have a method to collect this data. There's also the option for models that have been pre-trained but ultimately you'll need to ensure that there's enough data captured in production for the model to perform well in production.
4. **Predictive Patterns** : Machine Learning is incredibly appealing when we're able to benefit from a large quantity of cheap but approximate predictions
5. **Training and Production data are similar** : Our model can only predict things that it has seen so it's important to make sure our training data is reflective of what the model will see in production.
6. **The Task is Repetitive** : ML Algorithms learn better the more data they see, so when we provide more data, we're able to allow our model ot perform well
7. **Wrong Predictions Are Cheap** : ML models will not always be right so it's important that we find use cases where the cost of a wrong prediction is not that big. We can compare say a recommendation system vs a cancer detection algorithm - the stakes are very different.
8. **It's at Scale**: Since ML Systems require non-trivial investments in technology, talent and resources, it's important to make sure we are dealing with a problem that can benefit from scale

It's important to note too that when building Machine Learning systems, we'll be working with many different stakeholders. These stakeholders are each having their own set of requirements that might be in conflict with each other.

For instance, for a food delivery service that recommends restaurants, we might have

- Engineers might want to optimise for performance
- Sales teams might want to optimise for commissions
- Product Manager teams might want to optimise for latency because each ms results in x% drop in revenue

It's difficult to balance all these requirements at the same time.

