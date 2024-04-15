RLHF is the process of taking a pre-trained model and aligning it to a specific human preference. In this process, we perform the following steps

1. **Supervised fine-tuning (SFT)**: Typical fine-tuning performed on prompts (e.g., questions) paired with expected outputs (e.g., answers)
    
2. **Reward model training (RM)**: A model trained to compute a scalar reward given a prompt paired with a ranking of outputs. Typically, the datasets for this task are limited to prompts paired with a correct output and an incorrect output.

3. **Reinforcement learning (RL)**: Given a prompt, the model trained at step 1 generates an output that is scored by the reward model trained at step 2. RL is optimised given the reward to improve the generation.

![[Pasted image 20240415202001.png]]

## Supervised Fine Tuning (SFT)
