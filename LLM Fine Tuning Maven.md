
# Introduction

Fine-tuning should be considered as a last solution. Often times, it's useful as a way to deal with problems whereby we are working with a lot of complex logic or if-then rules which the model might not be able to follow.

Additionally, if you have custom data, fine-tuning a model might be a way for you to in-house specific capabilities to approach the capabilities of a larger model. 

In general

- Work hard to scope the requirements for a use-case (Eg. Instead of a general purpose chat bot work to develop software with smaller scope )

## Dataset

When working with a dataset, you need to define a good standard for the data that you choose to train your model on. It's useful to work on generating preferred and rejected responses (Eg. We want to train a model to output emails, therefore we get two agents to write emails and use that to train a model using DPO)

We can then evaluate it using a blinded test