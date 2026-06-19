# Using Large Language Models

**Build Your Own LLM Workshop — Chapter 1 of 23**

| | |
|---|---|
| **Duration** | 50m 37s |
| **Video** | https://www.youtube.com/watch?v=vXiB0UdDhk8 |

---

## Workshop Welcome

Welcome to Build Your Own Large Language Model. This workshop is about developing **intuition** — understanding how AI and ML models are built, their limitations, and that there's no magic behind any of it. Just math and backpropagation. [0:07]

You can get the deck at [go.justinangel.ai/deck](https://go.justinangel.ai/deck).

---

## Why Build an LLM?

Three reasons to spend many hours on this: [0:38]

**1. Taste and intuition.** Understanding how models are built gives you a sense for their limitations, which is critical if you're building applications or agents on top of them. [0:39]

**2. Technical skill.** By the end, you'll be able to write all the code for a small LLM — architecture, pre-training, and post-training. You'll be able to read any open-source LLM code (nanoGPT, etc.) and understand it. [1:18]

**3. Model literacy.** When DeepSeek releases a model and crashes the stock market, you'll understand what "sparse attention vs dense attention" actually means. You'll be able to read model cards and technical reports. [2:20]

### Hireability Reality Check

This workshop alone won't get you hired at a frontier lab. But **everything in here is base knowledge** you'll need for those positions. If you want to work at a frontier lab, you'll also need deep GPU programming skills and AI safety expertise. [2:51]

---

## Prerequisites

This workshop is for **software engineers** — people comfortable with code who can spend a day learning new concepts. [3:58]

**Not required:**
- Math (linear algebra, calculus, statistics) — we'll teach it
- Python — we keep it simple and cross-lingual
- Machine learning background — we start from scratch

**We live in 2026.** Feel free to use AI to help read and write code. [5:12]

---

## Meet Justin Angel

I've been a software engineer for 23 years — Meta (IC8/Director), Uber, Amazon, Apple, Microsoft. I'm not a machine learning engineer with 20 years of experience; this has been a recent conversion over the last 6–12 months. [5:48]

> **"Any software engineer that doesn't intrinsically understand AI will soon be unemployable."** — Justin Angel (2024)

All of my code in 2023 and 2024 was written by AI. It became clear that understanding the models powering these tools is the future. I went and got an AI/ML masters, writing my thesis on LLM psychotherapy. [6:36]

---

## Teaching Methodology

Every section has three parts: [8:11]

1. **Slides** — I explain the problem, the technology, and how it fits into the bigger picture
2. **AI by hand** — we work through the math in Google Sheets/Excel, building intuition visually
3. **Code** — we review Python + PyTorch notebooks that implement what we learned

Your job: fill in the exercise sheets, run the notebooks, tinker, and do the exercises (~15 minutes each). [9:53]

---

## Workshop Roadmap

The day is divided into four modules: [11:13]

1. **Intro to LLMs** — run GPT-2, learn autoregressive loops, build the roadmap
2. **ML Fundamentals** — single neuron → loss functions → backpropagation
3. **Transformer Architecture** — tokenizers → embeddings → attention → full transformer
4. **LLM Training** — pre-training → instruction tuning → RL

We'll cover 23 sections, each building on the last.

---

## Kick Off Training Now

Before we learn anything, we need to start the 20-hour training run. [15:18]

We connect to an A100 GPU on Google Colab Pro Plus (~$50/month for background execution) and run the pre-training script. At the start, the model outputs **nonsense**: [16:30]

> **Prompt:** "In a galaxy far, far away"
> **Output:** "outdoor corn today Denver preview examples push half emoji bracket unrelated natural drowning military malice milk"

After 20 hours of training:

> **Prompt:** "Once upon a time in a small village"
> **Output:** "an ancient man and woman lived there"

The model learned English. While that runs, we'll learn *how*. [17:29]

### Training Options

| Option | Cost | Time |
|--------|------|------|
| Colab Pro Plus A100 | ~$50/mo | ~20 hours |
| Modal (faster GPU) | ~$82 | ~8 hours |
| Use pre-trained weights | Free | Instant (download from Hugging Face) |

---

## Intro to LLMs

### Next-Word Prediction

LLMs generate text **autoregressively** — one token at a time. [21:10]

Given "Justin and I as software engineers worked for", GPT-2 outputs probabilities:
- Meta: 53%
- Microsoft: 23%
- Uber: 11%
- Amazon: 8%
- Apple: 3%

It has a probabilistic model of the world based on everything it's read.

LLMs are:
- **Machine learning models** — trained on data, evaluated on unseen data
- **Deep neural networks** — fixed architecture with learnable parameters (covered in the second half of the day)

### The Sampling Problem [23:03]

We could just pick the highest probability token every time (greedy decoding). But that leads to repetitive, boring text.

Ideally, we'd use **beam search** — explore all possible future token combinations to find the most probable sentence. Problem: for 100 tokens with just 2 options each, we'd need 2¹⁰⁰ checks — more compute than all of humanity has ever produced. [23:46]

We need **heuristic sampling strategies**.

---

## Temperature

Temperature controls the "creativity" of the output by reshaping the probability distribution: [25:51]

```
softmax(logits / temperature)
```

- **Lower temperature (< 1):** extenuates differences — the highest probability token becomes even more likely (more deterministic)
- **Higher temperature (> 1):** flattens the distribution — all tokens become more equally likely (more "creative")

---

## Top-K and Top-P

**Top-K:** Limit sampling to the K most likely tokens. Set all others to zero probability, renormalize. [28:01]

**Top-P (nucleus sampling):** Choose the smallest set of tokens whose cumulative probability exceeds P. [28:14]

Example: if top tokens have probabilities [40%, 20%, 15%, 10%, 5%, 5%, 3%, 2%] and P=0.85:
- Select [40% + 20% + 15% + 10% = 85%] → keep those 4 tokens, drop the rest

---

## Excel Sampling Demo [29:46]

The Excel sheet demonstrates:
- Temperature: reduce → sharpens distribution, increase → flattens
- Top-K: limit to N options, renormalize
- Top-P: cumulative probability threshold
- How each strategy affects the generated text

---

## Colab Setup and GPUs [35:45]

```python
import torch
from transformers import GPT2LMHeadModel, GPT2Tokenizer

model = GPT2LMHeadModel.from_pretrained('gpt2')
tokenizer = GPT2Tokenizer.from_pretrained('gpt2')

# Use GPU
device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
model = model.to(device)
```

---

## Generating Tokens with GPT-2 [37:03]

```python
input_text = "The meaning of life is"
input_ids = tokenizer.encode(input_text, return_tensors='pt').to(device)

# Simple generation
output = model.generate(
    input_ids,
    max_length=50,
    temperature=0.8,
    top_k=50,
    do_sample=True
)

print(tokenizer.decode(output[0]))
```

### Autoregressive Loop (from Scratch) [39:29]

```python
def generate(model, tokenizer, prompt, max_length=50, temperature=1.0):
    input_ids = tokenizer.encode(prompt, return_tensors='pt').to(device)
    
    for _ in range(max_length):
        with torch.no_grad():
            logits = model(input_ids).logits[:, -1, :]
        
        # Apply temperature
        logits = logits / temperature
        
        # Sample from distribution
        probs = torch.softmax(logits, dim=-1)
        next_token = torch.multinomial(probs, num_samples=1)
        
        input_ids = torch.cat([input_ids, next_token], dim=-1)
        
        if next_token.item() == tokenizer.eos_token_id:
            break
    
    return tokenizer.decode(input_ids[0])
```

### Stop Token

The EOS (End of Sequence) token signals when to stop generating. Without it, the model would generate forever. The loop checks `if next_token == eos_token_id` and breaks.

---

## Exercise [47:06]

Complete the sentence: "The meaning of life is ___"

Build your own autoregressive loop to:
1. Set up the prompt
2. Generate one token at a time
3. Apply temperature, top-K, or top-P
4. Stop at the EOS token

Expected output (from GPT-2): "The meaning of life is to be happy. To be happy is to be free."

> **Tip:** Every exercise has an answer in the notebook under "Show Code." Try it yourself first, but don't get stuck — the goal is learning, not suffering.

---

## Key Takeaways

| Concept | What We Learned |
|---------|-----------------|
| **LLMs** | Generate text autoregressively, one token at a time |
| **Temperature** | Controls sharpness of probability distribution |
| **Top-K** | Limits tokens to top K choices |
| **Top-P** | Limits tokens to top cumulative probability P |
| **model.generate()** | Easy mode — built-in Hugging Face function |
| **Autoregressive loop** | Full control — implement from scratch |
| **GPUs** | Required for practical training and inference |

---

## Next Up: Reverse Engineering LLMs

We just used GPT-2. Now we'll take it apart — calling `print(model)` and `summary()` to discover all the components that make up a transformer. That gives us our workshop roadmap for the rest of the day.
