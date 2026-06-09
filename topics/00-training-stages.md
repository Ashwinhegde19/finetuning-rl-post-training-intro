# Training Stages

## Big picture
Pre-training → Mid-training → Post-training

## Pre-training
- First major stage
- Task: next-token prediction
- Learns: language, facts, reasoning, context
- Output: base model
- Strength: raw capability
- Weakness: not reliably instruction-following

## Mid-training
- Continued pre-training on curated data
- Still next-token prediction
- Improves: languages, domain knowledge, modalities, context length

## Post-training
- Makes model useful and controllable
- Methods: SFT and reinforcement learning
- Teaches: behavior, format, helpfulness, preference alignment

## Model comparison
| Model | Stage | Strength | Weakness |
|---|---|---|---|
| Base | Pre-training | Raw knowledge | Not reliable assistant |
| Fine-tuned | SFT | Follows desired behavior | Limited preference optimization |
| RL-trained | RL | Optimized preferred responses | Needs reward signal |

## Core takeaway
```text
Pre-training = raw intelligence
Mid-training   = specialization
Post-training  = behavior shaping
```
