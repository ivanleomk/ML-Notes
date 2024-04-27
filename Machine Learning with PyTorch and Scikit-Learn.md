- There are three types of machine learning algorithms
	- Supervised Learning : Labels + Data => Goal is to learn a mapping between data and the actual target labels. Examples of tasks that require supervised learning are classification and regression
	- Unsupervised Learning : No Labels + Data => 
	- Reinforcement Learning : Reward System + Environment => Goal is to learn a policy
- Important terminology
	- Training Example: This is a single row in a table representing the dataset 
	- Training: Fitting a model's parameters given a desired objective
	- Feature: A column in a data table/matrix
	- Target: A desired outcome that we want
	- Loss Function: This is a measurement that computes how well our model is performing 
	
![|400](assets/Screenshot%202024-04-27%20at%209.15.45%20PM.png)
When we work with raw data, typically we need to extract meaningful features. A feature in this case is just a measurement that is useful to our final prediction.

## Training Classification Algorithms

The simplest example is simply 

$$
W = \begin{bmatrix}  
w_1\\  
w_2 \\
w_3 \\
\dots \\
w_n
\end{bmatrix} \space X = \begin{bmatrix}  
x_1\\  
x_2 \\
x_3 \\
\dots \\
x_n
\end{bmatrix}
$$
We can then take 

$$
\sigma(WX^T) = \begin{cases} 1 &\text{if  $WX^T \geq \theta$} \\0 & \text{otherwise} \end{cases}
$$
We can alternatively utilise a simple bias term so that this instead becomes

$$
\sigma(WX^T + \theta) = \begin{cases} 1 &\text{if  $WX^T \geq 0$} \\0 & \text{otherwise} \end{cases}
$$
