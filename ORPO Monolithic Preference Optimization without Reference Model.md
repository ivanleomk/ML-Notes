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
![|400](assets/CleanShot%202024-05-16%20at%2001.13.23@2x.png)
This can be done by computing the odds of the chosen and rejected responses and then optimising our loss based off that. Ideally we want the odds of the winning response to be better than that of the losing response. 

Odds are computed using the formula below
![|300](assets/CleanShot%202024-05-16%20at%2001.14.29@2x.png)
Where $P_\theta(y|x)$ can be computed using the average log prob of each token in the desired response.
![|400](assets/CleanShot%202024-05-16%20at%2001.14.48@2x.png)
Intuitively, as odds of winning response > odds of losing response, then our log ( odds_winning / odds_losing ) becomes more positive

![|400](assets/CleanShot%202024-05-16%20at%2001.16.10.png)

This in turn causes the value of the sigmoid to increase and approach 1. Therefore as our odds increases, our loss approaches 0 ( When the sigmoid of the value is equal to 1).

## Performance

We can see that ORPO tuned base models consistently outperform models that are of the same size and in some cases show significant improvements ( see phi-2 )
![](assets/CleanShot%202024-05-16%20at%2001.17.21@2x.png)

The authors also explore two main metrics - Per Input Diversity (PID) and Across Input Diversity (AID)

- PID measures the cosine similarity of the generated outputs for the same prompt. The higher the cosine similarity, the closer the generated outputs are and hence, the more consistent the model's responses
- AID measures the cosine similarity of generated outputs for different prompts. The lower the cosine similarity, the more diverse the responses. Authors hypothesise that with a larger AID, the model is more tuned to the specific prompt instead of a rough general distribution.

Notably, they choose to maximise the odds since maximising the probabilities results in overly suppressing the logits for the tokens. Therefore, the odds ratio is a better choice when the preference alignment is done with SFT due to the mild discrimination of disfavoured responses and the prioritising of the favoured responses to be generated.
![](assets/CleanShot%202024-05-16%20at%2001.20.37@2x.png)
