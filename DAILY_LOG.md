# Daily Learning Log

## Format
Each entry: date, topic, key points, revision notes.

## Entries

### 2026-06-09 — Training Stages and Post-Training Overview
- Topics: pre-training, mid-training, post-training, SFT, LoRA, RLHF basics
- Summary:
  - LLM training happens in three stages: pre-training, mid-training, post-training
  - Pre-training: next-token prediction on huge text corpus → base model
  - Mid-training: curated continued pre-training for domains/languages/modalities
  - Post-training: SFT and RL to make the model useful, controllable, and product-ready
  - SFT teaches behavior from input-output examples
  - LoRA reduces cost by training small adapters instead of full model
  - RL teaches the model via reward signals instead of exact targets
  - RLHF learns preferences from human feedback
- Revision bullets:
  - Pre-training = raw intelligence
  - Mid-training = specialization
  - Post-training = behavior shaping
  - Fine-tuning for behavior; RAG for new knowledge
  - SFT → LoRA → Eval → RLHF should be the study order

### 2026-06-09 — Fine-tuning vs Reinforcement Learning
- Topics: post-training methods comparison, SFT vs RL, reward hacking, grading quality
- Summary:
  - Fine-tuning teaches by showing correct target output
  - RL teaches by scoring model output
  - Fine-tuning is stable and cheaper; higher risk if data quality is poor
  - RL can optimize for reward but is less stable and more compute-heavy
  - Good graders are the main asset for RL
  - Good labeled data is the main asset for fine-tuning
  - Reward hacking is a key risk in RL
- Revision bullets:
  - Fine-tuning = imitation
  - RL = optimization
  - Data quality drives SFT; grader quality drives RL
  - Start with SFT; RL later with strong evaluation
