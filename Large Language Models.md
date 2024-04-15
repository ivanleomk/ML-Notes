Instruct language models have dominated the public space. There are a good amount of models which mimic the style of ChatGPT. This is done through the following proccess.

![[Pasted image 20240415202001.png]]
1. **Supervised fine-tuning (SFT)**: Typical fine-tuning performed on prompts (e.g., questions) paired with expected outputs (e.g., answers)
    
2. **Reward model training (RM)**: A model trained to compute a scalar reward given a prompt paired with a ranking of outputs. Typically, the datasets for this task are limited to prompts paired with a correct output and an incorrect output.

3. **Reinforcement learning (RL)**: Given a prompt, the model trained at step 1 generates an output that is scored by the reward model trained at step 2. RL is optimised given the reward to improve the generation.

This was subsequently modified down the line as the optimisation algorithms changed significantly.