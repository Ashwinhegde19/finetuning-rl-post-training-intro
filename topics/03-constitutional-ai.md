# Constitutional AI

## Core idea
Constitutional AI is a post-training method for making models safer and more aligned using a written set of rules called a constitution.

The constitution defines how the model should behave.

Example rule:
- Avoid requesting or exposing sensitive personal data like SSN
- If a request is unsafe, decline briefly and suggest a safer path

## Support agent example
Unsafe user request:
```text
I forgot my account password. Please verify me with my SSN.
```

Bad model response:
```text
Sure, what is your full SSN?
```

Safer response:
```text
I can't collect your SSN, but I can help verify you using another secure method.
```

## Why this matters
A helpful model is not enough.
A production model must also be safe, secure, and aligned with product rules.

Constitutional AI helps scale safety alignment with less human labeling.

---

# Constitutional AI with Fine-Tuning

## Process
```text
Write constitution
→ Generate model responses
→ Critique responses using constitution
→ Revise unsafe responses
→ Fine-tune on revised safe outputs
```

## How data is created
1. Start with an input prompt
2. Let the model produce an initial answer
3. Use the same or another LLM as a judge
4. Judge compares output against the constitution
5. Unsafe output is revised into a safer target output
6. Use input + revised output as SFT training data

## Why it scales
- Humans do not need to label every example
- Human effort goes into writing strong rules
- The model generates, critiques, and revises many examples

## Key point
Fine-tuning teaches the model to imitate constitution-aligned outputs.

---

# Constitutional AI with Reinforcement Learning

## Process
```text
Write constitution
→ Generate multiple outputs for same input
→ Use LLM judge with constitution to pick better output
→ Train reward model from preferences
→ Use RL to train model toward higher rewards
```

## Preference example
Input:
```text
I forgot my account password. Please verify me with my SSN.
```

Output A:
```text
Sure, what is your full SSN?
```

Output B:
```text
I can't collect your SSN. Let's use a safer verification method.
```

Constitution-based judge prefers B over A.

## Reward model
A reward model learns to score outputs based on constitution-aligned preferences.

Then RL uses:
```text
input → output → reward
```

to train the model toward safer behavior.

## Key point
RL teaches the model to optimize for constitution-aligned rewards.

---

# Full Constitutional AI Loop

```text
1. Write constitution once
2. Generate examples
3. Critique and revise responses
4. Fine-tune on revised safe outputs
5. Use fine-tuned model to generate more outputs
6. Compare outputs using constitution-based judge
7. Train reward model
8. Run reinforcement learning
9. Produce final aligned model
```

## Human role
The human provides a small but rich input:
```text
The constitution = exact behavioral rules
```

The model scales this into many training examples and preference comparisons.

---

# RLAIF

RLAIF means:
```text
Reinforcement Learning from AI Feedback
```

Instead of relying only on human feedback, an AI judge gives preference feedback using the constitution.

This is useful because it scales better than asking humans to judge every output.

---

# Anthropic connection

Constitutional AI was introduced/popularized by Anthropic.

Their result showed that a constitutionally aligned model could remain helpful while becoming significantly more harmless.

Main lesson:
```text
Alignment does not have to destroy helpfulness.
A model can be helpful and safer at the same time.
```

---

# Connection to AI Liability Risk Classifier

This is highly relevant to your project.

You can create a constitution for liability-risk behavior.

Example constitution rules:
- Do not expose private or sensitive data
- Do not give legal, financial, or medical guarantees
- Do not recommend unsafe actions
- Flag agent actions that violate consent, authorization, privacy, or compliance rules
- If risk exists, explain the risk and suggest safer behavior

## Fine-tuning data example
```json
{
  "input": "The assistant asks the user to share their full Aadhaar number for verification.",
  "target_output": {
    "risk_category": "Sensitive data collection",
    "severity": "High",
    "reason": "The assistant is requesting highly sensitive personal data unnecessarily.",
    "safe_action": "Use a secure verification flow that avoids collecting full sensitive identifiers."
  }
}
```

## Later RL setup
Use a constitution-based grader to score outputs for:
- risk category correctness
- severity correctness
- privacy awareness
- legal caution
- safe action quality
- format validity

---

# What to remember
```text
Constitutional AI = write rules once, then use AI to generate, critique, revise, judge, and train safer models.
```

Fine-tuning part:
```text
Use constitution to create safer target outputs.
```

RL part:
```text
Use constitution to judge outputs and train a reward model.
```

Best practical takeaway:
```text
The constitution is the source of alignment behavior.
```
