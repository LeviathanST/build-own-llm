# Pre-training

**Build Your Own LLM Workshop — Chapter 19 of 23**

| | |
|---|---|
| **Duration** | 1h 12m 50s |
| **Video** | https://www.youtube.com/watch?v=nN335-483Pg |

---

## What's Missing? Data

We have the full transformer architecture. We know how to do backpropagation. The missing piece: **what data do we train on?** [0:18]

By the end of this section, we'll have a working pre-training script and all our data ready to go. [0:24]

There's no Excel worksheet for this section — there's nothing new conceptually. Just assembling everything we've learned into a working training pipeline. [0:43]

---

## How LLMs Learn English

The solution: train on **word distributions from a massive corpus**. [1:20]

Combine:
- A massive amount of human-written text
- The transformer architecture
- Backpropagation with cross-entropy loss

The model learns English — not through rules or grammar, but through exposure to the statistical patterns of language. It learns previous words, knowledge, sentence structure — all from predicting the next token. [1:26]

**Pre-training loss:** cross-entropy on next-token prediction. Same loss function we covered in Section 7. [1:56]

### How Pre-training Works [2:22]

Pre-training teaches basic language skill — English (or whatever language) from a massive dataset. We compress language patterns into the model weights, then use those weights to generate text.

The training setup: [3:03]

```
Input tokens:  [START] [the] [capital] [of] [Texas] [is]
Target tokens: [the] [capital] [of] [Texas] [is] [Austin]
```

Shifted by one position. The model learns to predict each token given the preceding ones.

---

## The Dataset: FineWeb-Edu [4:25]

The dataset we use is **FineWeb-Edu**, an education-focused subset of the web.

Why FineWeb-Edu?
- High quality — filtered for educational content
- Large scale — billions of tokens
- Publicly available on Hugging Face

### Dataset Statistics

| Property | Value |
|----------|-------|
| Total tokens | ~10 billion |
| Quality filter | Education score |
| Format | Pre-tokenized |

---

## Data Processing Pipeline

### Loading [14:09]

```python
from datasets import load_dataset

dataset = load_dataset("HuggingFaceFW/fineweb-edu", split="train")
```

### Tokenization

The raw text needs to be tokenized using our GPT-2 tokenizer:

```python
def tokenize_function(examples):
    return tokenizer(examples["text"], truncation=True, max_length=1024)
```

### Binning [14:42]

Binning groups sequences by length for efficient batching:

| Bin | Sequence Length | Purpose |
|-----|----------------|---------|
| Short | 128–256 | Early training |
| Medium | 256–512 | Intermediate |
| Long | 512–1024 | Full context |

This prevents wasting compute on padding short sequences alongside long ones.

### DataLoader Setup

```python
train_loader = DataLoader(
    dataset,
    batch_size=16,
    shuffle=True,
    collate_fn=collate_fn
)
```

---

## The Pre-training Script [16:08]

The full script brings together everything from the workshop:

### Model Initialization

```python
config = GPT2Config(
    vocab_size=50257,
    hidden_size=768,
    num_layers=12,
    num_heads=12,
    dropout_rate=0.1,
    max_position=1024,
)
model = GPT2Model(config)
```

### Weight Initialization (He init, Section 10)

```python
def init_weights(module):
    if isinstance(module, nn.Linear):
        nn.init.kaiming_normal_(module.weight, mode='fan_in', nonlinearity='relu')
```

### Training Configuration

| Hyperparameter | Value | Reference |
|---------------|-------|-----------|
| Optimizer | AdamW | Section 8 |
| Learning rate | 3e-4 (warmup → cosine decay) | Section 8 |
| Weight decay | 0.1 | Section 13 |
| Batch size | 16 | Section 8 |
| Gradient accumulation | 4 steps | Section 8 |
| Gradient clipping | 1.0 | Section 13 |
| Total steps | ~19,000 (for 10B tokens) | |

### Training Loop

```python
optimizer = torch.optim.AdamW(model.parameters(), lr=3e-4, weight_decay=0.1)
scheduler = torch.optim.lr_scheduler.CosineAnnealingLR(optimizer, T_max=19000)

for step, batch in enumerate(train_loader):
    # Forward pass
    logits = model(batch.input_ids)
    loss = F.cross_entropy(logits.view(-1, logits.size(-1)), batch.labels.view(-1))
    
    # Backward pass
    loss.backward()
    
    # Gradient clipping
    torch.nn.utils.clip_grad_norm_(model.parameters(), 1.0)
    
    # Optimizer step
    if (step + 1) % 4 == 0:  # Gradient accumulation
        optimizer.step()
        scheduler.step()
        optimizer.zero_grad()
    
    # Logging
    if step % 1000 == 0:
        print(f"Step {step}: loss {loss.item():.4f}")
        evaluate(model, val_loader)  # Section 20
        save_checkpoint(model, optimizer, step)
```

---

## Running the Training [19:18]

The training script was designed to run on **Google Colab Pro Plus** (A100 GPU).

### Cost Breakdown

| Resource | Cost |
|----------|------|
| Colab Pro Plus A100 | ~$50/month (background execution needed) |
| Modal A100 | ~$82 for 8-hour run (faster GPU) |
| Total training time | ~20 hours on A100 |
| Total steps | ~19,000 (10B tokens) |

### Monitoring Progress

The script logs:
- **Training loss** over time — should steadily decrease [1:10:48]
- **Perplexity** — evaluating how surprised the model is by each token
- **Learning rate** — warmup then cosine decay
- **Checkpoints** — every 100 steps, saved as `.pth` files

---

## The Result

After 20 hours of training: [1:11:08]

> **Prompt:** "Once upon a time in a small village,"
> **Output:** "an ancient man and woman lived there."

The model speaks English. It learned:
- Word order and grammar
- Subject-verb agreement
- Basic world knowledge
- Coherent sentence structure

### Upload to Hugging Face [1:11:14]

```python
model.push_to_hub("your-username/workshop-v1-pretraining")
tokenizer.push_to_hub("your-username/workshop-v1-pretraining")
```

The model is automatically uploaded when training completes.

---

## Using the Lego Builder [23:00]

The Lego Builder at `go.justinangel.ai/lego` generates the pre-training script for you:

1. Enter hyperparameters
2. Click generate
3. Get a complete Colab notebook

You can also use `go.justinangel.ai/go` to generate a prompt for your AI coding assistant.

**The important thing:** you can now read and understand every single line of the generated script. There are no secrets from you. [1:12:18]

---

## Next Up: Evaluation, Instruction Tuning, and RL

With a pre-trained model, we need to:
1. **Evaluate** — is it any good? (Section 20)
2. **Instruction tune** — teach it to follow instructions (Section 21)
3. **Reinforcement learning** — align it with human preferences (Section 22)
4. **What we didn't cover** — the stuff that's beyond this workshop (Section 23)
