![](assets/CleanShot%202024-05-16%20at%2001.05.18@2x.png)
Traditional LLMs are trained using a complex three step process

1. First we train a base model during a pre-training process over a large text corpus
2. Next, we use SFT to get the model to learn a specific format of response ( using say <|assistant|> tags or what not)
3. Then, we use RLHF/DPO to be able to train our model to output specific distributions of responses

The intuition is that by using RLHF/DPO, we train our model to output a specific chosen response over a rejected response. This is done using a reward model or by directly modelling the log probs of the two models itself.
![|400](assets/CleanShot%202024-05-16%20at%2001.07.06@2x.png)
However, indirectly, this doesn't help our model learn to prefer the chosen response over the rejected response. We can see above that the log probabilities of the chosen response and the reject response increase linearly despite only the chosen responses being used for fine-tuning.

## ORPO

ORPO ( Odds Ratio Preference Optimisation ) is a new method to train models which we can entirely forego the SFT + DPO/RLHF dynamic
![|400](assets/CleanShot%202024-05-16%20at%2001.09.13@2x.png)
The intuition for ORPO is that we can simultaneously train our model to learn an instruction format and to learn the preference for a chosen response over a rejected response. 

This can be done by computing the odds of the 