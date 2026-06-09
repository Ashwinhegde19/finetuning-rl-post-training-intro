# Deep Learning Notes

## Focus Areas
- Post-training for LLMs
- Fine-tuning, LoRA, QLoRA
- Reward modeling, RLHF, GRPO
- Evaluation for LLMs
- Project: AI Risk Evaluation Workbench / AI Liability Risk Classifier

## Key Principle
- Fine-tuning is NOT for changing knowledge — that's RAG's job.
- Fine-tuning is for changing behavior, format, style, classification, and task-specific patterns.

## Best Project Fit
- Given an AI output or agent action → classify liability risk, explain risk, assign severity, suggest safer behavior.

---

# Training Stages Overview

## LLM training has 3 main stages
```text
Pre-training → Mid-training → Post-training
```

1. **Pre-training**
   - First major stage
   - Task: predict next token
   - Model learns: language, grammar, facts, reasoning, word relationships
   - Output: base model (raw capability, not yet assistant-ready)

2. **Mid-training**
   - Continued pre-training on curated data
   - Improves: languages, domain knowledge, modalities, context length
   - Still uses next-token prediction

3. **Post-training**
   - Makes model useful and controllable
   - Methods: SFT and Reinforcement Learning
   - Teaches: behavior, format, helpfulness, preference alignment

## Model Comparison
| Model Type | Stage | Strength | Weakness |
|---|---|---|---|
| Base | Pre-training | Raw knowledge | Not reliably instruction-following |
| Fine-tuned | SFT | Follows desired input-output | Limited preference optimization |
| RL-trained | Reinforcement Learning | Optimized for preferred responses | Requires reward signal |

---

# SFT (Supervised Fine-Tuning)

## How it works
- Teach model with input → target output examples
- Also called: instruction tuning

## Use cases
- Response format
- Instruction following
- Domain-specific behavior
- Task patterns
- Classification style
- Assistant-like responses

## Key concept: NOT for adding NEW knowledge
Use RAG for knowledge retrieval.
Use SFT for behavior reformatting and repeatable patterns.

---

# LoRA / Adapters

## Why use LoRA
- Full fine-tuning of large models is very expensive
- LoRA trains only small additional weights called "adapters"

## Mental model
```text
Base model = mostly frozen
LoRA adapter = small trainable layer
```

Result: fine-tuning is cheaper and needs fewer GPUs.

---

# Reinforcement Learning Basics

## Core idea
Instead of always providing exact target output, score model responses:
- Good response → high reward
- Bad response → low reward
Model learns to maximize reward.

## RLHF
- Reinforcement Learning from Human Feedback
- Humans compare responses and indicate which is better
- Reward model learns preferences and scores future outputs
- Then the LLM is optimized against that reward model

## Learning priority
- Learn SFT and LoRA first
- Understand evaluations deeply
- RLHF conceptually next
- GRPO/PPO/advanced RL later

---

# Fine-tuning vs Reinforcement Learning

## Core difference
```text
Fine-tuning:    Input → Target output
Reinforcement:  Input → Model output → Reward score
```

- Fine-tuning imitates good examples.
- RL optimizes for reward.

## Fine-tuning strengths
- Works when you know the desired output
- Best for: response format, classification, structured outputs, domain behavior
- More stable
- Usually cheaper
- Easier to debug

## RL strengths
- Works when many answers are acceptable
- Best for: reasoning, preference alignment, helpfulness/safety optimization
- Can discover better-than-human strategies
- Usually expensive and less stable

## Risks
- Fine-tuning copies dataset errors
- RL can reward-hack if the grader is weak

## Frontier lab workflow
```text
Base model → SFT → Reinforcement Learning → Improved model
```

## Key takeaway
```text
Fine-tuning asset = high-quality data
RL asset = high-quality grading
```

## Practical project guidance
- Start with SFT for your AI Liability Risk Classifier
- Reason: your output format is clearly structured
- Later, add RL with a strong grader if needed

## What to remember
```text
Fine-tuning is imitation.
Reinforcement learning is optimization.
```

## Developer analogy
- Fine-tuning resembles unit-test snapshots/expected outputs.
- RL resembles scoring an implementation with a broader test suite and quality metrics.
