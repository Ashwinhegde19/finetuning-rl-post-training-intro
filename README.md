# Fine-tuning & RL for LLMs: Intro to Post-training

Study notes for LLM post-training, fine-tuning, reinforcement learning, evaluation, and the AI Liability Risk Classifier project direction.

## Structure

```text
log/       daily learning log
topics/    consolidated revision notes by concept
```

## Topics

1. `topics/00-training-stages.md` — pre-training, mid-training, post-training
2. `topics/01-fine-tuning-vs-rl.md` — fine-tuning vs reinforcement learning
3. `topics/02-data-and-grading.md` — SFT data and RL graders
4. `topics/03-constitutional-ai.md` — constitutional AI, RLAIF, safety alignment

## Project focus

AI Liability Risk Classifier:
```text
Input: AI output or agent action
Output: risk category, severity, reason, safe action
```

## Study order

1. Training stages
2. Fine-tuning / SFT
3. LoRA / QLoRA
4. Evaluation
5. RLHF / RLAIF
6. GRPO / advanced RL

## Core principle

Fine-tuning shapes behavior using examples.
RL shapes behavior using rewards.
Evaluation tells whether either method actually improved the model.
