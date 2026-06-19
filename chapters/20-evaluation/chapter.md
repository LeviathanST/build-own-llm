# Evaluation

**Build Your Own LLM Workshop — Chapter 20 of 23**

| | |
|---|---|
| **Duration** | 34m 56s |
| **Video** | https://www.youtube.com/watch?v=S6uLzsqOOUc |

---

## The Problem: Is Our Model Any Good?

We've pre-trained a model. But how do we know if it's actually good? [0:23]

Three naive approaches, all flawed:

### 1. Leaderboards (OpenRouter) [0:37]

The most-used models on OpenRouter: DeepSeek V4 Flash, Tencent Hunyuan 3, Claude Opus. But usage is driven by cost as much as quality — Hunyuan 3 is free, which explains its popularity. [1:01]

**Problem:** Popularity ≠ quality. Cost distorts the signal. You'd need `capabilities / price` to normalize. [1:40]

### 2. Model Cards [4:25]

Every model release comes with benchmarks showing it "wins in everything." The metrics the model doesn't win on get conveniently dropped from the card. [5:20]

**Problem:** Saturation — most benchmarks hover at 80–90%, making tiny differences look like big gaps. The leaderboard might show 20 spots difference for 1.5% performance difference. [5:36]

### 3. Formal Benchmarks (LM Arena, MMLU) [2:52]

LM Arena shows Opus 4.6 at #1 across most categories. But "hard prompts" feels subjective.

**Problem:** Benchmarks are gameable. Models know when they're being evaluated (the format is distinctive). Most benchmarks use short interactions — not how people actually use LLMs. [11:32]

---

## Why Evaluation Is Hard

### Problem 1–2: Model Card Bias [5:38]

If you're writing a model card, you probably cherry-pick the benchmarks you win on. And most benchmarks are **saturated** — all models score 90%+, making differences meaningless.

### Problem 3: Wrong Answer Keys [9:48]

Multiple-choice benchmarks sometimes have wrong answer keys. Do models need to learn to ignore wrong keys — even though those keys are in the training data (the internet)?

### Problem 4: Format Sensitivity [10:11]

"The sky is blue." → the model could answer "3" (3rd option), "blue", or "the third one" — all correct, but only one format matches the benchmark's parser.

### Problem 5: Verifiable vs. Free-Text [10:27]

- **Code and math** are easy to evaluate — verifiable results (does it compile? is the answer right?)
- **Creative writing, summarization** — you need an LLM-as-judge, which has its own errors

**LLM-as-judge problems:** Models from the same family tend to rate each other higher (Claude rates Claude higher). Judges are inconsistent. [11:04]

### Problem 6: Unnatural Interactions [11:32]

Most benchmarks use single multiple-choice questions. Nobody uses LLMs that way — real use involves multi-turn conversations, system prompts, tool use.

---

## The Benchmark Landscape

A 2025 survey of 243 benchmarks categorizes them: [14:15]

### Linguistic (NLP-era) [14:37]
- Language understanding, common sense reasoning, text generation, dialogue, multilingual
- Example: **LAMBADA** — predict the last word of a long passage. This is the benchmark we'll use. [15:12]

### Knowledge & Expertise
- General knowledge (MMLU), exams, language-based expertise

### Reasoning
- Logic, common sense, mathematics

### Domain-Specific
- STEM: math, physics, chemistry, biology
- Humanities: law, IP, education, psychology
- Engineering & technology

### Safety & Reliability [15:58]
- AI safety benchmarks, red-teaming evaluations

---

## MMLU: The Classic [16:22]

Massive Multitask Language Understanding — high school to expert level general knowledge.

Example question: *"Which of the following statements could be best described as a liberal perspective on future energy security?"* [16:38]

Subjects include anatomy, astronomy, biology, computer science. I can maybe score 50% on this. The model needs genuine knowledge. [17:06]

**Problem for us:** Our model is 124M parameters. MMLU capabilities only **emerge** at larger scales (Wei et al., 2022 demonstrated minimum scale requirements for broad knowledge). [19:17]

---

## LAMBADA: Our Benchmark

LAMBADA evaluates **next-token prediction on long passages**:

- Given a long context, can the model correctly predict the final word?
- Tests both language understanding and long-range dependencies
- Appropriate for our 124M parameter model

### Implementation

```python
def evaluate_lambada(model, tokenizer, dataset):
    total = 0
    correct = 0
    for example in dataset:
        input_ids = tokenizer.encode(example["text"])
        context = input_ids[:-1]  # All tokens except last
        target = input_ids[-1]     # Last token to predict
        
        with torch.no_grad():
            logits = model(torch.tensor([context]))
            prediction = logits[0, -1].argmax()
        
        if prediction == target:
            correct += 1
        total += 1
    
    accuracy = correct / total
    return accuracy
```

### Smoke Test Prompts

After pre-training, we test with simple completions:

- "Once upon a time in a small village, ___" → should produce coherent text
- "The capital of France is ___" → Paris
- "The theory of relativity states that ___" → physics-related continuation

---

## Emerging Capabilities [19:07]

Wei et al. (2022) showed that certain capabilities only emerge at scale:

| Capability | Minimum Scale |
|-----------|---------------|
| Broad knowledge (MMLU) | ~1B+ parameters |
| Multi-step math | ~100B+ parameters |
| Complex translation | ~10B+ parameters |
| Advanced linguistic patterns | Varies |

Our 124M model won't ace MMLU. It's too small. But it **will** learn English grammar, basic facts, and coherent sentence structure. That's the win.

---

## Key Takeaways

| What | Takeaway |
|------|----------|
| **Evaluation is unsolved** | More exciting than pre-training as a research area |
| **Benchmarks are gameable** | Always read model cards critically |
| **MMLU is saturated** | Small differences, large rankings |
| **Our benchmark** | LAMBADA for next-token accuracy |
| **Scale matters** | 124M won't do MMLU — that's expected |

---

## Next Up: Instruction Tuning [34:30]

Pre-training builds a fancy autocomplete. Instruction tuning turns it into an AI chatbot that follows instructions. We've built the engine — now we teach it manners.
