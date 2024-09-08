
# Introduction

Many Software Engineers are building evaluations based off vibe-checks. These are just random stabs in the dark that don't have a quantifiable way of determining improvements/regressions in our systems.

By setting up a consistent and repeatable way of judging LLM Outputs over time, it pays dividends for us.

In short

- Product Managers can correlate the eval metrics with specific business KPIs
- Engineers can make informed decisions on whether or not to fine-tune or to use a vector database

## System Evals

System Evals are a way of creating a systematic process for capturing the intuition for qualitative metrics and using it to judge subsequent LLM outputs. 

The goal is to have a corpus of example query/output judgement triplets as a golden dataset.

![](assets/CleanShot%202024-09-08%20at%2016.13.36@2x.png)

These judgement triplets could look like

```
query,output,judgement
What is the Capital of Japan, Tokyo is a ... , 3
```

System evaluations are distinct from the model evals. Model evals could be something like the GSM8k dataset where different models are tested on the same standardised set of questions.

System Evaluations on the other hand are meant for specific task completion measurements. Often times, we'll also want to have the evaluation metric measure something qualitative like Relevance and Toxicity. This might involve the use of [[LLM as a Judge]].

This also includes testing the performance of specific LLM-driven components such as routers and synthetic data generation.

## Starting with Evals

The process looks something like this

1. Log as many intermediate results as you can
2. Create a example dataset by sampling a diverse set of inputs from user feedback, bug reports and real user sessions.
3. Look at the easiest changes to make - ideally these are high impact low hanging fruits to solve.

Starting with a vibes based check is important because it helps us to get a sense of what the outputs from our system. This is a golden amount of data that we have on hand. 

There are a few kinds of tests we can write to create system evals

1. **Property-Based tests** : These are assertions about specific properties


### Property Based Tests

A simple way we can implement this in Pydantic would be

```python
from pydantic import BaseModel

class User(BaseModel):
    name: str
    age: int

	@field_validator("name")
	@classmethod
	def validate_name(cls,v:str)->str:
		if not v.isupper():
			raise ValueError("Name should be uppercased!")
		
		return v
```

This can be done using a simple unit testing framework that will include the inputs to reproduce the test. The goal here is to have **simple, reliable heuristics** to check if an output satisfies each property.

If we're using something like [LLM as a Judge](LLM%20as%20a%20Judge) then we need to consider more abstract conditions

1. **Grounding** : How faithful is the answer to the source documents?
2. **Relevance** : How relevant is the answer to the user's question
3. **Recall** : How many relevant context documents did the system retrieve?
4. **Extraction Accuracy** : How accurately does the system identify and extract the target information?

# Writing Evaluations

Often times, when working to implement evaluations, you'll find that there might be a conflict between the different metrics that you're caring about. 

A classic example is that of Harmfulness and Helpfulness. A model can be violate harmfulness in its attempt to be helpful if you ask it for advice to perform tasks such as making a bomb.

It's important here to start working on decomposing the high-level quality dimensions into questions that are specific, actionable and simple. This allows you to pinpoint exactly where the system excels or falls short.

We have the following four types of evaluations

1. **Binary** : Yes or No questions
2. **Comparison** : Comparing two different inputs side by side to help identify incremental improvements
3. **Categorical** : Categorise the actual input into a set number of possible categories (Eg. Relevant, Irrelevant, Highly Relevant )
4. **Numerical** : Grade this from a 1 - 5 scale

We can also use Reference Based questions

