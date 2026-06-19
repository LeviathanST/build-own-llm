# Normalization

**Build Your Own LLM Workshop — Chapter 12 of 23**

| | |
|---|---|
| **Duration** | 35m 2s |
| **Video** | https://www.youtube.com/watch?v=ZqSbev8Y-ys |

---

## The Problem: Even with Residuals, Training Still Collapses

We've added residuals and He initialization. But GPT-2 small still needs **72 consecutive matrix multiplications**, and they still don't converge. [0:34]

Training A×B mod C with 72 layers, even with residuals and He init: accuracy barely moves from 23% to 30% in 200 epochs. [2:04]

Why? Residuals prevent vanishing gradients (x + f(x) is always ≥ x in magnitude), but they don't prevent **exploding** gradients. He initialization assumes a simple MLP+ReLU pattern, but our transformer uses growing-shrinking MLPs with ReLU in the middle — the assumptions don't hold. [1:08]

**The tool we need: normalization.** [2:31]

---

## What Normalization Does

Normalization has two operations: [3:31]

**Scaling:** Pull values toward a stable boundary. Values inside the boundary get pulled out; values outside get pulled in. Everything stays within a predictable range.

**Centering:** Shift the average back to zero. If the mean of your values drifted to 2.0, centering brings it back to 0.0.

The goal: maintain a single coherent set of statistics within the residual stream. No explosion, no collapse, no shifting. [1:49]

---

## Types of Normalization

| Type | Operates On | Does | Used in LLMs? |
|------|-------------|------|---------------|
| **LayerNorm** | Rows | Scale + center | Early LLMs |
| **BatchNorm** | Columns | Scale + center | No |
| **RMSNorm** | Rows | Scale only | **Modern LLMs** |

### Why RMSNorm Won [5:28]

LayerNorm needs to calculate **variance**: `Var(x) = E[x²] - E[x]²`. Computing variance is expensive — it's a statistic over the entire array.

RMSNorm only needs **mean of squares**: `RMS(x) = √(E[x²])`. No variance calculation.

Since GPUs are compute-constrained, and RMSNorm doesn't lose anything meaningful by skipping the centering step, **RMSNorm has supplanted LayerNorm in modern LLMs.** [5:28]

### Why BatchNorm Doesn't Work for LLMs [7:04]

BatchNorm operates on columns, not rows. In the context of language model embeddings, averaging across columns doesn't make sense. (This will be clearer when we cover embeddings in Section 16.)

---

## Excel Walkthrough

### LayerNorm in Sheets [9:17]

Formula:

```
LayerNorm(x) = (x - mean) / √(variance + ε) × λ + β
```

Where:
- `mean` = average of the row
- `variance` = VAR of the row
- `ε` = small epsilon (prevents division by zero)
- `λ` = learned scale parameter
- `β` = learned shift parameter

Step by step:
1. Calculate mean per row: `=AVERAGE(row)` [9:31]
2. Calculate variance per row: `=VAR(row)` [9:48]
3. Center: `=value - mean` [10:08]
4. Scale: `=centered / √(variance + ε)` [10:31]
5. Apply learned parameters: `=scaled × λ + β` [10:56]

After LayerNorm, values are centered around 0 with consistent scale.

### BatchNorm [12:43]

Same formula as LayerNorm, but calculated per **column** instead of per row. Not useful for LLMs but good to know exists.

```
BatchNorm(x) = (x - col_mean) / √(col_variance + ε) × λ + β
```

### RMSNorm [14:32]

Formula (simpler — no centering):

```
RMSNorm(x) = x / √(mean(x²) + ε) × λ
```

1. Calculate mean of squares: `=AVERAGE(row^2)` [14:50]
2. Divide: `=x / √(mean_squares + ε)` [15:43]
3. Scale: `=result × λ` [15:21]

RMSNorm pulls values into the -1 to +1 range, preventing them from drifting.

### Single-Line Formulas [16:36]

These are the versions you'd actually use:

```excel
# LayerNorm (single cell)
=LAMBDA(x, (x - AVERAGE(x)) / SQRT(VAR(x) + ε) * λ + β)(range)

# RMSNorm (single cell)
=LAMBDA(x, x / SQRT(AVERAGE(x^2) + ε) * λ)(range)
```

---

## Normalization in MLP Blocks [17:01]

Our MLP has: grow → ReLU → shrink → residual. Even with residuals, the values trend more green and more red — magnitude is increasing. [17:47]

Normalization fixes this by keeping each layer's output within a stable range.

### Condensed MLP Notation [19:03]

```
hidden = MMULT(input, W1)           # Grow: 5→8
hidden = ReLU(hidden)
hidden = MMULT(hidden, W2)          # Shrink: 8→5
output = hidden + input             # Residual
```

### Pre-Norm vs Post-Norm [19:23]

The key question: **when** do we apply normalization?

**Post-Norm** (original 2017 approach):

```
hidden = MLP(x)
output = LayerNorm(hidden + x)
```

**Pre-Norm** (modern approach):

```
hidden = LayerNorm(x)
output = MLP(hidden) + x
```

### Which Wins? Pre-Norm [21:24]

Research (Xiong et al., 2020) showed that **pre-norm consistently outperforms post-norm** for transformers. [21:24]

Why? Pre-norm stabilizes the input to each layer, preventing the buildup of large activations in deep networks. Post-norm normalizes after the residual addition — by which point the damage is done.

**Our choice: Pre-RMSNorm.**

---

## PyTorch Implementation [22:57]

```python
# LayerNorm
nn.LayerNorm(hidden_dim)

# RMSNorm (not built-in, easy to implement)
class RMSNorm(nn.Module):
    def __init__(self, dim, eps=1e-6):
        super().__init__()
        self.eps = eps
        self.scale = nn.Parameter(torch.ones(dim))
    
    def forward(self, x):
        mean_sq = x.pow(2).mean(-1, keepdim=True)
        x_norm = x * torch.rsqrt(mean_sq + self.eps)
        return self.scale * x_norm
```

### Baseline Training (72 layers, no norm) [26:01]

Accuracy gets from 23% to 30% in 200 epochs. Essentially stuck.

### With Pre-RMSNorm [26:47]

**Converges to high accuracy within ~50 epochs.** The yellow line on the chart (no norm) barely moves. Pre-RMSNorm in green zooms up. [28:09]

### LayerNorm vs RMSNorm [28:47]

| | LayerNorm | RMSNorm |
|--|-----------|---------|
| Operations | Mean + variance | Mean of squares only |
| Speed | Slower (variance is expensive) | Faster |
| Parameters | Scale (λ) + shift (β) | Scale (λ) only |
| Performance | Good | **Comparable or better** |

RMSNorm is faster, simpler, and performs just as well. That's why modern LLMs (LLaMA, etc.) use it.

---

## Key Decisions for GPT-2 [32:50]

| Decision | Choice |
|----------|--------|
| Normalization type | RMSNorm |
| Placement | Pre-norm |
| Epsilon | 1e-6 |
| Scale parameter | Learned per dimension |

---

## Code Exercise [33:17]

```python
class TransformerBlock(nn.Module):
    def __init__(self, dim):
        super().__init__()
        self.norm1 = RMSNorm(dim)
        self.attn = Attention(dim)  # Section 17
        self.norm2 = RMSNorm(dim)
        self.mlp = MLP(dim)         # Section 6
        
    def forward(self, x):
        # Pre-norm pattern
        x = x + self.attn(self.norm1(x))
        x = x + self.mlp(self.norm2(x))
        return x
```

This is the pre-norm + residual pattern used in every modern transformer.

---

## Next Up: Regularization [34:39]

Even with normalization, things are still a bit wonky. Regularization handles overfitting — the next and final tool before we start building the actual transformer components.
