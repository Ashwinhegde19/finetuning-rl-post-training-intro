# Data for Fine-Tuning and Grading for RL

## Core principle
Fine-tuning works because of good data.
Reinforcement learning works because of good grading.

## Fine-tuning data
- Format: input → target output
- Model imitates the target output pattern
- Data quality controls behavior
- The model only learns behavior that exists in the data

## Conversation history must be included
- One-turn QA is not enough for chat behavior
- Include full conversation context in training examples

## Prompt/tag structure matters
- Include role tags for clarity
- Example: `<user>`, `<assistant>`
- Tags define who speaks and what to generate

## Reasoning structure
- Can teach step-by-step reasoning with tags
- Example: `<think>...</think>`, `<answer>...</answer>`
- Useful for training and evaluation even if not exposed in production

## Failure handling training
- Teach model to handle bad RAG results
- Teach model to handle incorrect retrieved documents
- Useful for production reliability

## Guardrails
- Safety guardrails: refuse harmful requests
- Product boundaries: refuse out-of-scope requests
- Both can be taught via fine-tuning examples

## RL grading
- Format: input → model output → reward score
- Grading controls learned behavior
- Deterministic graders: regex, exact match, JSON schema, unit tests
- LLM-as-judge graders: for subjective or complex tasks

## Reward hacking
- Model can find shortcuts to maximize reward without solving task
- Bad grader leads to bad behavior
- Biggest RL failure mode

## RL environment requirements
- Needs realistic training environment
- May include tools: calculator, search API, files, codebase
- Can become expensive if tools are called excessively
- Must mirror real-world use case

## Practical guidance
- Start with SFT when output format is clearly structured
- Use RL only after strong graders and evaluation exist
- For your AI Liability Risk Classifier, start with SFT dataset
- Later, build graders for category, severity, reason, and safe action quality

## Remember
Fine-tuning quality comes from data quality.
Reinforcement learning quality comes from grader quality.
