# Frontier Model Post-Training Pipelines

## Core idea
Frontier labs do not usually train a model with only one simple step of fine-tuning and one simple step of RL.

They often use an iterative pipeline:
```text
Base model
→ SFT
→ RL
→ generate better data
→ SFT again
→ RL again
→ select best checkpoint
→ continue improving
```

Post-training is a loop, not just a one-time step.

---

# How frontier labs combine SFT and RL

## Why use both?
Fine-tuning and reinforcement learning solve different parts of the problem.

SFT helps the model learn:
- what good answers look like
- response structure
- reasoning format
- instruction-following behavior

RL helps the model improve:
- reasoning quality
- preference alignment
- safety
- helpfulness
- scoring against reward models or graders

Simple mental model:
```text
SFT gives the model the pattern.
RL improves the quality of the pattern.
```

---

# DeepSeek R1 example

DeepSeek R1 used multiple post-training stages.

Simplified flow:
```text
Pre-trained base model
→ SFT on long chain-of-thought reasoning data
→ RL for reasoning
→ use that model to create more reasoning data
→ combine reasoning + non-reasoning data
→ SFT again
→ RL again
→ final DeepSeek R1 model
```

## Important lesson
A model checkpoint can be used to create training data for the next checkpoint.

This means post-training can be self-improving when combined with filtering, grading, and careful evaluation.

---

# Qwen example

Qwen-style post-training also uses multiple stages.

Simplified flow:
```text
Base model
→ chain-of-thought SFT
→ reasoning RL
→ another SFT stage
→ general RL
→ final model
```

## Important lesson
Different stages can target different capabilities:
- reasoning
- general helpfulness
- instruction following
- safety
- domain behavior

---

# Llama-style iterative post-training

Llama pipelines also use repeated SFT and RL stages.

One important idea mentioned is rejection sampling.

## Rejection sampling
Rejection sampling means:
```text
Generate many possible outputs
→ score/filter them
→ reject weak samples
→ keep only high-quality samples
→ use those as better training data
```

A reward model can help choose the best outputs.

This improves SFT data quality.

## DPO
DPO stands for Direct Preference Optimization.

It is an RL-style preference optimization method that can train a model from preference data.

For now, remember only the high-level idea:
```text
DPO helps train models to prefer better outputs over worse outputs.
```

---

# Post-training after deployment/open-source release

Post-training is not only something frontier labs do before release.

After a model is released, other people can continue post-training it.

Examples:
- code generation variants
- long-context variants
- medical text processing variants
- domain-specific assistants
- safer instruction-following models

This is why open-source models like Llama, Qwen, and DeepSeek have many community variants.

---

# Where post-training fits in the full ecosystem

Full model/product path:
```text
Pre-training
→ Mid-training
→ Post-training
→ Hosted model API or open-source model
→ Agents / RAG / SaaS applications
→ Optional further post-training
```

Examples:
- Hosted API: ChatGPT, Claude
- Open-source model: DeepSeek R1, Qwen, Llama
- Application layer: agents, RAG apps, SaaS products

---

# Your own post-training

You can also do post-training on open-source models.

The scale can vary:
- light local fine-tuning using LoRA/QLoRA
- heavier training with stronger GPUs
- domain-specific variants
- product-specific behavior tuning

For your project, you are not building a frontier base model.
You are taking an existing model and adapting its behavior.

---

# Connection to AI Liability Risk Classifier

Your project can follow a smaller version of the frontier-lab loop.

Practical pipeline:
```text
Open-source instruct/base model
→ Create SFT dataset for liability risk classification
→ Fine-tune with LoRA/QLoRA
→ Evaluate on held-out examples
→ Generate more examples with the model
→ Filter/reject weak examples
→ Add better examples to dataset
→ Fine-tune again
→ Later: add preference data or grader-based optimization
```

## Example iterative improvement
1. Create initial examples manually
2. Fine-tune model to output:
   - risk category
   - severity
   - reason
   - safe action
3. Test model on new failure cases
4. Identify weak areas
5. Add better examples for those failures
6. Re-train or continue fine-tuning

---

# Developer analogy

Think of frontier post-training like CI/CD for model behavior.

Software version:
```text
write code → run tests → fix bugs → add tests → release → monitor → improve
```

Model version:
```text
train model → evaluate → find failures → create better data → train again → evaluate again
```

Rejection sampling is like accepting only high-quality generated test cases or PRs and rejecting weak ones.

---

# What to remember
```text
Frontier model post-training is iterative.
SFT and RL are reused multiple times.
Models can help generate better data for later training stages.
```

Most important takeaway:
```text
Post-training is not one step. It is a pipeline of data generation, filtering, SFT, RL, evaluation, and repetition.
```
