
General principles
- Fine-Tuning is a last resort
- Choose an appropriate model
- Do start with a prompted model and see how far you can get - the important thing here is to figure out how feasible the task is
- Generally you want to fine-tune based on the bad examples too so that the model learns a good decision boundary
- Run Fast Evals - LLM as a judge is a useful way to quickly compare and generate some ground truth comparison about the quality of your generations
- Slow Evaluations - These are important to invest in (Eg. What percentage of customer upvoted this! ) because often times deploying a model in production ( if we quantise the model ) might result in different behaviour and we want to catch that
- Always be measuring the evals - this helps catch data drift and issues that we might not expect

