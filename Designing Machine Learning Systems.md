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

It's difficult to balance all these requirements at the same time but it's important to build with these in mind.

# Designing Machine Learning Systems

Machine Learning Systems need to be designed with business objectives in mind. Without tying a machine learning project to a clear business metric it's difficult to ensure the long term sustainability of the project.

This return of investment needs to be tied closely to the maturity stage of adoption - the longer a company has invested in its Machine Learning projects, the more it can do.

There are a few big requirements for Machine Learning Systems

1. **Reliability** : The system should continue to be reliable in the face of unexpected challenges.
2. **Scalability** : We need to find ways to allow for our models to be served on an efficient basis. Typically, as models grow in complexity or the number of models increase, we need to automate more of the pipeline and ensure we're saving/keeping all of the artefacts generated during training
3. **Maintainability** : We need to structure our workloads and set up infrastructure so that different contributors can work nicely with one another. 
4. **Adaptability** : The system should be able to adapt to changing customer inputs 

A machine learning is always in the process of being worked on. It's an iterative process to improve it. This can be summarised in the following steps

1. Project Scoping : Figure out stakeholders and allocate budget
2. Data Engineering : How do we handle the data processing and pipelines that we need so that our models work
3. ML Model Development : Extract Features and develop initial models leveraging these features
4. Deployment : Figure out how to deploy the model
5. Monitoring and Continual Learning : Monitor the model for performance decays and drops

## Types of ML Problems

A Machine Learning problem is characterised by inputs, outputs and having a clear objective function that guides the learning process. There are a few key types of machine learning problems

1. Regression : Let's predict a real number value
2. Classification
	1. Binary Classification : We have two classes - let's try to classify into one of them
	2. Multi Class Classification : We have a single input, we have a few probable classes it could belong to, let's try to classify into one of them
	3. Multi Label Classification : We have a single input, we have a few different classes, our input can belong to one or more of them

When we've got a classification class with a large number of classes, this becomes an issue of high cardinality. 
If your model needs on average 100 examples to be able to accurately classify a class, then this means that you need `100n` examples to accurately train a model for `n` total classes.

## Framing a problem

Typically, we want to have our systems setup in such a way that we're able to easily adapt it for future usage without retraining a model from scratch

Take the following example where we use a set of input features and an app's input features to determine the likelihood of a user liking it.
![](assets/CleanShot%202024-08-11%20at%2008.26.17@2x.png)

Compare this instead if we had framed it as a multi-class classification problem.
![](assets/CleanShot%202024-08-11%20at%2008.27.12@2x.png)

We can adapt this to a case whereby we might have multiple learning objectives - eg. to increase engagement and reduce the instance of engagement-baiting posts on user feeds. We can represent this as 

$$
pred = \alpha (\text{Engagement}) + \beta(\text{Engagement Baiting})
$$
There are two real ways to do this

1. Train a single model using a loss function that combines the two
2. Train two separate models and tune the values of $\alpha$ and $\beta$ in production depending on how it's received

# Data Engineering

Three key things to consider

- How is my data stored?
- How does my data flow into my system?
- How is my data processed?

## Storing 

There are two main distinctions here between the different types of data - structured and unstructured. The main difference here is who takes the responsibility for ensuring some form of structure.

Unstructured data is normally stored in a [[Datalake]] in raw format where there isn't any assumed sch
