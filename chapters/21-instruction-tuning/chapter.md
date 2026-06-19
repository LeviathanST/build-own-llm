# Instruction Tuning

**Build Your Own LLM Workshop — Chapter 21 of 23**

| | |
|---|---|
| **Duration** | 40m 26s |
| **Video** | https://www.youtube.com/watch?v=8iwxM6XRpVQ |

---

## The Problem: Autocomplete ≠ Chatbot

A pre-trained model is a **fancy autocomplete**. It speaks English, but it doesn't follow instructions. [0:29]

Example: asking "Explain what a neural network is in simple terms" → the pre-trained model responds "What is the difference between a neural network and a neural network?" and keeps repeating itself. [0:57]

Example: "What is the capital of France?" → responds "The capital of France is France" — even though it knows the answer is Paris. [1:26]

**Pre-trained models don't understand the concept of answering a question.** They predict the next token — period. [1:38]

### After Instruction Tuning

- "Explain what a neural network" → gives a coherent explanation (sounds like a high schooler wrote a Wikipedia answer — which is fine)
- "Capital of France?" → "Paris"

Instruction tuning converts an autocomplete engine into something resembling an AI chatbot. [2:14]

---

## How It Works

Pre-training: ~10 billion tokens of internet text. [2:44]

Instruction tuning: **a few thousand examples** — tiny by comparison.

We show the model examples of desired behavior:

```
### Instruction:
What is 2 + 2?

### Response:
4
```

The model learns to generalize from these examples. It goes from "generate whatever token comes next statistically" to "respond to the user's request." [3:17]

**It's style over substance.** Instruction tuning doesn't teach the model new facts. It teaches it *how to respond*. The model already knows the capital of France from pre-training — instruction tuning teaches it to *answer the question* instead of autocompleting. [9:42]

---

## Pre-Training vs Mid-Training vs Instruction Tuning

| Phase | Data Size | Goal | Loss Function |
|-------|-----------|------|---------------|
| **Pre-training** | Trillions of tokens | Learn language (grammar, facts, reasoning) | Cross-entropy on next-token prediction |
| **Mid-training** | ~100K examples | Improve style, reasoning, long context, tool use | Cross-entropy on formatted prompts |
| **Instruction tuning** | ~100K examples | Create AI assistant persona — follow instructions | Cross-entropy on instruction/response pairs |

**Mid-training** (emerged in 2025): teaches the model *how* to reason (step-by-step chains), handle long contexts, use tools. Not mandatory if you don't need those capabilities. [4:48]

---

## Instruction Format: Alpaca Style

The most common format for instruction tuning: [12:39]

```
### Instruction:
{user's request}

### Response:
{desired response}
```

Other formats exist (ChatML, Gemini, LLaMA 3, Zephyr, Mistral) — they're all cosmetically different but functionally identical. We use Alpaca because it's simple and well-accepted. [13:51]

### Teaching Capabilities via Format [14:04]

**System prompts:**

```
### System:
You are a helpful AI assistant. You are thoughtful and harmless.

### Instruction:
Tell me about...

### Response:
...
```

**Reasoning traces:**

```
### Instruction:
How many prime numbers are between 50 and 70?

### Response:
Let me think step by step:
50 → no (even)
51 → no (3×17)
52 → no (even)
53 → yes
...
Therefore, there are 4 prime numbers.
```

**Tool use:** Define function signatures in the format, show examples of the model calling them.

---

## Data Sources for Instruction Tuning

### 1. NLP Benchmarks (Pre-2019) [15:45]

Existing NLP datasets can be converted to instruction format. Example: **Balanced COPA** (commonsense reasoning):

> Premise: "The garden looked well groomed."
> Alternative 1: "The grass was cut."
> Alternative 2: "The sun was rising."
>
> Correct answer: "The grass was cut."

Converted to Alpaca format:

```
### Instruction:
Given the premise, which alternative is more likely?

### Response:
Choice 1: The grass was cut.
```

### 2. Human-Written Prompts [17:07]

OpenAssistant (2023): paid workers wrote prompts and responses. Problem: workers in different countries used regional dialects — models learned Nigerian English ("delve") instead of standard instruction following. [17:28]

### 3. LLM-Generated [17:56]

The dominant source today: frontier LLMs generate instruction-following examples, which smaller models learn from. No humans needed.

---

## Fine-Tuning (Not Full Training) [18:56]

Fine-tuning a pre-trained model is different from training from scratch:

- We **don't** update all parameters
- We use techniques like **LoRA** (Low-Rank Adaptation) — train small adapter matrices instead of the full model
- This is a full day workshop in itself, but the key insight: [19:23]

```python
# LoRA: train only low-rank adapters
from peft import LoraConfig, get_peft_model

lora_config = LoraConfig(
    r=16,          # rank
    lora_alpha=32,  # scaling factor
    target_modules=["q_proj", "v_proj"],  # which layers to adapt
)

model = get_peft_model(base_model, lora_config)
# Only ~0.1-1% of parameters are trainable
```

### Fine-Tuning Approaches [22:06]

| Approach | Trainable Params | When to Use |
|----------|-----------------|-------------|
| Full fine-tune | 100% | Maximum quality, high compute |
| LoRA | ~0.1-1% | Good quality, very efficient |
| QLoRA | ~0.1-1% | LoRA + quantization, runs on consumer GPUs |

---

## Cool vs Cold Tokens [25:37]

During instruction tuning, we don't want the model to learn that the **instruction** is something to predict — only the **response** matters.

- **Cold tokens:** The instruction and prompt — mask these in the loss function
- **Cool tokens:** The response — compute loss only on these

```python
labels = input_ids.clone()
labels[instruction_mask] = -100  # Ignored in cross-entropy
loss = F.cross_entropy(logits.view(-1, vocab_size), labels.view(-1))
```

---

## Exercise

Run the instruction tuning notebook:
1. Load your pre-trained model
2. Format the Balanced COPA dataset into Alpaca style
3. Fine-tune with LoRA
4. Test: ask the model a commonsense question

---

## Recommended Reading [39:45]

- **Alpaca paper (2023)** — the original instruction tuning approach
- **SmolLM2 paper** — excellent instruction tuning section on capabilities
- **Zephyr, Trinity** papers — modern instruction tuning methods

---

## Next Up: Reinforcement Learning [40:04]

Even after instruction tuning, models don't always get things right. RL adds both positive and negative signals — rewarding good behavior and penalizing bad — to further align the model with what we actually want.
