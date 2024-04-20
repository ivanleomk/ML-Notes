> Link: https://www.youtube.com/watch?v=VMj-3S1tku0


- We can calculate the derivative of a function with respect to its inputs by solving for a specific function analytically (Eg. $y=3x+2$ implies that if we want $\frac{dy}{dx}$ then we can just take $3$ )
	- however for larger scale machine learning networks, it's impossible to solve for an entire network's analytical solutions given that there are billions of parameters to optimise for.
	- As a result, what we go for is the numerical approximation, where we calculate the local derivative of a specific operation and then use the chain rule to derive the derivative of the gradient with respect to that input
	  
- In most cases, what this is implemented with is by using a computational graph which stores the relationship between different operations. We then propagate updates throughout this graph when we want to find the gradients of each individual input 
	- Important note here is that the loss itself has a gradient of 1 since $\frac{dL}{dL}$ is going to be equal to 1. Intuitively, if we increase the loss by $h$, it will increase linearly by $h$ too. 
	- Micro grad is an implementation of a computational graph which allows us to do this easily for scalar values ( at most vectors )
	  
- When we perform back propagation, we want to adjust our weights slightly based on their contribution to the final loss function. The idea here is that if we move in the direction opposite of our gradients, we can move towards a global minimum for the final function. 
	- This is why at each step, we're essentially going to be updating our weights by their gradients multiplied by a certain constant (This is known as the learning rate)
	- This update of the weights by the gradients multiplied by a constant term is known as stochastic gradient descent. Depending on the implementation, sometimes we might either use a constant learning rate or a scheduler
	  
- Optimizers affect the weight update portion and not the calculation of gradients. Things like Adam do slight optimisations so that when we have a gradient we can apply it more intelligently to the weights to be updated.