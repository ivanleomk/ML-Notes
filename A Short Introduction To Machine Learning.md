> https://www.alignmentforum.org/posts/qE73pqxAZmeACsAdF/a-short-introduction-to-machine-learning
> 
> #machinelearning #summary #elicitml


- Early wave of AI was symbolic AI which wanted to represent problems using statements in formal languages and fixed rules. 
	- Real life is a bit too complicated to be easily described using formal languages. As a result, we moved on to using machine learning
- Idea is that instead of manually hard-coding all of the details ourselves, we specify models with free parameters that are learned from the data they're given.
	- Eventually moved on to deep learning which involved training networks with many layers using optimisation techniques like gradient descent and back propagation.
- Neural Networks are inspired by the brain. Each artificial neuron receives signals from neurons in the previous layer, combines them together into a single value (known as its _activation_), and then passes that value on to neurons in the next layer.
	- These weights are not manually specified, but instead they are learned via a process of **optimisation**, which finds weights that make the network score highly on whatever metric we’re using.
	- initially sets weights to arbitrary values, and then at each step changes them so that the network does slightly better on its objective function
- Categories
	- Supervised Learning : Use a dataset where each datapoint has a corresponding label. The goal is for the model to predict the labels which correspond to each data point
	- Unsupervised Learning : When we want a model to learn from an unlabelled dataset. The goal is to find automatic ways to convert an unlabelled dataset into a labeled dataset
	- Reinforcement Learning: We provide an environment for the agent to take actions and receive rewards. We then assign rewards for successful actions being taken.
- Challenges
	- It is often difficult to get our model to generalise incredibly well to examples which are outside of what it has seen. This is still poorly understood
	- It is also difficult to put together a training setup which is a incomplete or biased representation of the real-world tasks that you care about. This might not always map over 1-1
