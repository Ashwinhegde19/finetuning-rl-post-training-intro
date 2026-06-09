# Fine-tuning vs Reinforcement Learning

## Core difference
```text
Fine-tuning   Input → Target output
Reinforcement Input → Output → Reward
```

## Fine-tuning
- Learns by imitation
- Best when desired output is clear
- Best for: format, classification, structured output, behavior
- Usually more stable
- Usually cheaper
- Risk: copies bad dataset patterns

## Reinforcement learning
- Learns by optimization
- Best when many answers are acceptable
- Best for: reasoning, preferences, helpfulness, safety
- Can discover strong strategies
- Usually expensive and less stable
- Risk: reward hacking

## When frontier labs use both
```text
Base → SFT → RL → Improved model
```

## Key takeaway
```text
Fine-tuning asset = data
Reinforcement asset = grading
```

## Practical guidance
- Start with SFT for your AI Liability Risk Classifier
- Output pattern is clearly structured
- Add RL later with a strong grader if needed

## Remember
```text
Fine-tuning = imitation
RL          = optimization
```

## Developer analogy
- Fine-tuning resembles snapshot tests
- RL resembles scoring code by test suite and quality metrics
