> https://arxiv.org/abs/2405.09673

?: Full Fine-Tuning barely changes the spectrum of the base model's weight matrices, and yet the difference between the two is high rank?

?: For CPT, we manipulate the number of unique tokens (0.25, 0.5, 1, 2, 4, 8, 16, 20 billion), using individual learning rate cooldown schedules
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

## 