# Regularization

**Build Your Own LLM Workshop — Chapter 13 of 23**

| | |
|---|---|
| **Duration** | 40m 27s |
| **Video** | https://www.youtube.com/watch?v=2O8v8BX1LgM |

---

## Overfitting: The Core Problem

Our A×B mod C dataset had deterministic answers — no room for overfitting. But language is **nondeterministic**: [0:48]

> "The capital of France is ___"
> → Paris ✓
> → full of cheese ✓
> → having a metro strike ✓

All equally valid. Language has inherent noise. [1:03]

To simulate this, we add **10% noise** to our training data — 10% of labels get randomly shifted. [1:23]

---

## Chinchilla's Irreducible Loss [1:48]

The 2022 Chinchilla paper calculated the **irreducible error** of LLMs: **1.69 loss**. [1:51]

No matter how much compute, parameters, or data they added, they couldn't push training loss below 1.69. Poetically: **the entropy of language is 1.69.** [2:05]

This is the floor — the inherent unpredictability of language that no amount of scaling can eliminate.

---

## Spotting Overfitting [2:58]

Running our normalized model on the 10%-noise dataset:

| Metric | Value | Expected |
|--------|-------|----------|
| Test accuracy | **80%** | 90% (naively) |

We lost 10% more accuracy than the noise accounts for. That's overfitting. [3:28]

**The telltale sign:** a gap between training accuracy and test accuracy. If the model performs better on data it's seen vs. data it hasn't, it's memorizing the noise. [3:45]

---

## Solution 1: Dropout

Randomly turn off a percentage of neurons during training: [4:48]

```
input → [neuron₁, neuron₂, neuron₃, neuron₄]
         ↓ 50% dropout
       → [neuron₁,    0   ,    0   , neuron₄]
```

**Why it works:** The network can't rely on any single neuron being present. Every neuron has to learn independently useful features. If one weight is too important, the network learns to compensate with others. [18:00]

### Dropout in Practice

GPT-2 (2019) used **10% dropout**. [5:48] But **modern LLMs don't use dropout at all.** [5:58]

Why? The kind of overfitting dropout prevents comes from seeing the same data multiple times (epochs). LLMs have so much data that they rarely see any example twice. The overfitting dynamics are different. [6:11]

For our GPT-2 style model, we use 10% dropout as a learning exercise. [6:38]

### Dropout in Excel [13:21]

A dropout mask:

```excel
=IF(RAND() > dropout_rate, 1, 0)   # 1 = keep, 0 = drop
```

Apply the mask:

```excel
=weight * dropout_mask             # Zeroes out dropped weights
```

With 10% dropout, about 10% of weights get zeroed each training step. The mask changes each step — different weights get dropped each time.

**Scaling up:** Since we dropped 10% of the signal, we multiply remaining weights by **1.11** (1 / 0.9) to preserve overall magnitude. [16:00]

At inference time, dropout is **disabled** — all neurons are active. If we scaled up during training, no inference adjustment is needed. [17:00]

---

## Solution 2: Gradient Clipping

Gradient clipping prevents individual gradients from getting too large and destabilizing training.

### Value Clipping (Bad) [7:01]

```
clipped_grad = max(min(grad, max_val), min_val)
```

If gradients are [15.1, 5.3, 1.2] and we clip to [-1, 1]:
- 15.1 → 1 (lost 14 points)
- 5.3 → 1 (lost 4 points)
- 1.2 → 1 (lost 0.2 points)

**Problem:** The *direction* of the gradient is destroyed. The ratio between values is lost. In high-dimensional spaces, direction matters as much as magnitude. [8:15]

### Norm Clipping (Good) [8:48]

Instead of clipping each value independently, clip the **norm** (magnitude) of the entire gradient vector:

```
grad_norm = √(Σ gradᵢ²)
scale = min(1, max_norm / grad_norm)
clipped_grads = [g * scale for g in grads]
```

Every gradient is scaled by the same factor — **direction is preserved**. [10:03]

### Backprop Setup in Excel [19:19]

Using our existing feedforward network (from Section 8):
- 2 inputs, 1 neuron
- Current output: 3.1, expected: 4.0
- Residual: -0.9

Backpropagation computes gradient values, then clipping scales them down by the norm factor.

### Value Clip vs Norm Clip [21:14]

| Method | Direction Preserved? | Used In Practice? |
|--------|---------------------|-------------------|
| Value clipping | ❌ | Rarely |
| Norm clipping | ✅ | AdamW, most optimizers |

---

## Solution 3: Weight Decay

The model can overfit by using super large weights when smaller values would work. [10:18]

**Weight decay** penalizes large weights by subtracting a small percentage at every update: [11:10]

```python
new_weight = old_weight - lr * gradient - weight_decay * old_weight
```

Think of it like building a sandcastle at the beach. The ocean (weight decay) takes a little bit each time. If the sandcastle isn't important, it'll wash away. [11:33]

### Weight Decay Intuition [11:44]

Without weight decay, optimization can get trapped in an infinite loop — oscillating back and forth over the same values. With weight decay, the ball loses a bit of momentum each cycle and eventually settles at the center.

### Weight Decay in Excel [23:49]

```
updated_weight = old_weight - (lr * gradient) - (wd * old_weight)
```

- `wd` = weight decay coefficient (e.g., 0.01)
- Each step, weights decay slightly toward zero
- Only weights that are genuinely useful survive

---

## PyTorch Cheat Sheet [26:05]

```python
import torch.nn as nn
import torch.optim as optim

model = DeepDNN(layer_depth=20, has_residuals=True)

# Dropout
dropout = nn.Dropout(p=0.1)  # 10% dropout

# Gradient clipping (in training loop)
torch.nn.utils.clip_grad_norm_(model.parameters(), max_norm=1.0)

# Weight decay (built into AdamW)
optimizer = optim.AdamW(model.parameters(), lr=0.001, weight_decay=0.01)
```

---

## Training Results Comparison [27:45]

Without noise: model reaches 100% accuracy.

With 10% noise + no regularization:
- Test accuracy: ~80%
- Clear overfitting gap

With 10% noise + dropout + gradient clipping + weight decay:
- Test accuracy: improves
- Overfitting gap shrinks
- Smoother convergence

The dropout masks visualization shows which neurons get randomly turned off at each step. Gradient clipping prevents the loss spikes. Weight decay keeps weights small. Together, they make the model generalize instead of memorize.

---

## Key Takeaways

| Technique | What It Prevents | How |
|-----------|-----------------|-----|
| **Dropout** | Co-adaptation of neurons | Randomly turns off neurons during training |
| **Gradient clipping** | Exploding gradients | Scales gradient norm to a maximum |
| **Weight decay** | Excessively large weights | Subtracts a fraction of weight each update |

### GPT-2 Decisions

| Decision | Choice | Why |
|----------|--------|-----|
| Dropout | 10% | GPT-2 used it; modern LLMs skip it |
| Gradient clipping | Norm clipping (max=1.0) | Preserves direction |
| Weight decay | AdamW built-in (0.01) | Standard for most LLM training |

---

## Next Up: Softmax

We've now covered all the ML fundamentals. Next: **Softmax** — converting logits to probabilities. LLMs communicate in nothing but probabilities ("the cat sat on the ___ → mat 60%, car 15%..."). Softmax is the function that makes that possible. [39:50]

Then: tokenizers, embeddings, attention, and transformers — the language-specific components. We're getting close to building the full model.
