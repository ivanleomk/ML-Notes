> https://arxiv.org/abs/2405.09673

?: Inst

?: Full Fine-Tuning barely changes the spectrum of the base model's weight matrices, and yet the difference between the two is high rank?

?: For CPT, we manipulate the number of unique tokens (0.25, 0.5, 1, 2, 4, 8, 16, 20 billion), using individual learning rate cooldown schedules

?: It seems a bit weird that we would evaluate a coding/math model on common sense reasoning datasets. I wonder if we could instead finetune a coding.math model using a full-fine tune then see how its performance drops when we do LoRA vs fine tune on an unrelated dataset (Eg. FineWeb)
# Abstract

LoRA is a method used to fine tune large language models by training an adaptor that approximates the original weights of the matrix. By using LoRA, we're able to significantly reduce the memory footprint of the fine tune job.

This paper studies the extent that LoRA is able to match up to a full fine tune for continued pre-training and instruction fine-tuning.

- Continued Pre-Training: Text given is unlabelled, model just performs next token predictions
- Instruction Tuning : Text given is domain specific and contains a specific way of responding to user requests

Notably, they find that LoRA requires more epochs to achieve the same performance as a full fine tune but is able to retain more of its original performance on a source dataset.

## Datasets Used

- Coding CPT -  Starcoder Python - This consists of permissively licensed repositories from Github in 80+ Programming Languages. 
- Math CPT - OpenWebMath : This dataset includes mathematical web pages from Common Crawl
- Coding IFT - Magicoder-Evol-Instruct-110K : This contains 72.97 tokens of programming questions and answers with the LLM being iteratively prompted to increase the difficulty of a set of question-answer pairs
- Math IFT - MetaMathQA : This contains roughly 103M tokens and uses the training sets of GSM8K and MATH to generate additional synthetic examples using GPT3.5

## Measurement

**Improvement in Target Domain** -> HumanEval and GSM8K for seeing how the model has performed
**Original Source Metric** -> HellaSwag, WinoGrande and ARC-Challenge to test model's reasoning ability

# Results

## Lora underperforms a full fine tune

We can see that for the same number of tokens, LoRa achieves a significantly lower performance in both it's HumanEval and GSM8K score. 

Interestingly on Math, LoRa first outperforms GSM8K before being beat around 0.27 billion tokens? 

![](assets/CleanShot%202024-05-23%20at%2020.49.44.png)
When comparing LoRA vs a full fine-tune, it seems like LoRA is able to retain more of it's general reasoning ability ( given its better performance in the chosen datasets )
![](assets/CleanShot%202024-05-23%20at%2020.51.11.png)