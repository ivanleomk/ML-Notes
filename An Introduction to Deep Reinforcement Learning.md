> Link: https://thomassimonini.medium.com/an-introduction-to-deep-reinforcement-learning-17a565999c0c

The big idea behind Reinforcement Learning is that an agent will learn from the environment by interacting with it and receiving rewards. Without any supervision the agent learns to get better and better at playing the game.

![](assets/Screenshot%202024-04-20%20at%2010.21.39%20PM.png)
The goal of the agent is to maximise it's cumulative reward by taking actions that lead to positive outcomes it wants. Ultimately, this means that we can either choose to have a policy based approach or a value based approach.

A policy based approach means that our agent  learns a policy which maps a world state into a suggested action ( **deterministic** ) or a set of probability distributions over actions ( **stochastic** ). This policy is commonly referred to as $\pi$.

A value based approach means that we map a specific state to the expected value of being at that state (Eg. in a maze, specific positions are more valuable because we know they lead to the exit)

The agent has access to state - which is the complete description of the world. However, sometimes this is merely an observation - or in other words, a partial description of the state.

## Useful Definitions

- State : A complete description of the world
- Observation: A partial description ( Not the complete world state - Eg. being only being able to see 8 squares around the user )
- Action Space: The set of all possible actions in an environment. This can be a continuous or discrete space.
- Tasks : Tasks can either be episodic or continuous. An episodic task has a starting and an ending point whereas a continuous task continues forever, 

## Implementing RL

### Gamma

We can calculate the cumulative expected reward for $k$ steps from time $t$ as 

$$
R(\tau) = r_{t+1} + r_{t+2} + \dots + r_{t+k}
$$
However, this in turn results in higher weightage being given for subsequent reward steps that are closer to the goal. We can influence this using a discount rate that we call gamma.

$$
R(\tau) = r_{t+1} + \gamma r_{t+2} + \gamma^2 r_{t+3} + \dots + \gamma^{k-1} r_{t+k}
$$
Intuitively, the larger we make gamma, the less we care about long term rewards. This is because smaller values of gamma discount the final reward value significantly more as compared to the initial values.

### Exploration/Exploitation Tradeoff

Note that when it comes to this tradeoff
- Exploration is exploring the environment by trying random actions in order to **find more information about the environment.**
- Exploitation is **exploiting known information to maximise the reward.**



