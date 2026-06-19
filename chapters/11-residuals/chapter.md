# Residuals

**Build Your Own LLM Workshop — Chapter 11 of 23**

| | |
|---|---|
| **Duration** | 27m 32s |
| **Video** | https://www.youtube.com/watch?v=e5V7QaHq5lQ |

---

## The Problem: Deep Networks Still Collapse

Initialization alone isn't enough. Our earlier A×B mod C example had about 7 layers. But GPT-2 small has **72 consecutive matrix multiplications**. [1:04]

With just initialization, we can survive maybe 10–20 layers. The 2015 ResNet paper solved this for really deep networks by introducing the **residual stream**. [1:36]

---

## The Residual Formula

It's deceptively simple:

```
residual_output = x + f(x)
```

Take the input x, run it through a function f (like two MLP layers), and **add x back** to the result. [1:50]

Think of residuals as **shortcuts** — a way for data to not get lost in the network. The network doesn't have to work hard to maintain information; it can just keep sending it through. [2:40]

---

## Types of Residuals

### Addition Residual (2015) [3:05]

The original and most common. Simply add the input to the output. Used in most papers and open-source models.

```
output = x + MLP(x)
```

### Scaled Residual [3:19]

Multiply by a small scalar to prevent magnitude growth:

```
output = x + 0.5 × MLP(x)
```

Without scaling, x + f(x) where both have similar magnitude doubles the signal. Scaled residuals prevent this.

### Highway / Gated Residual [3:50]

Uses learned weights instead of a fixed scalar:

```
output = x + gate(x) × MLP(x)
```

The gate learns when to let the residual through.

### Attention Residual (2026) [4:08]

Recently introduced by the KI team: instead of only looking at the previous layer, attention residuals can look at the **entire network** with learned parameters to decide where to pull information from. Expected to become common in open-source models by late 2026 / early 2027. [4:56]

For now, most people still use **additive residuals**. [5:07]

---

## Excel Demonstration

### Matrix Addition [5:28]

Residual is just matrix addition — same position, same size:

```
C[i][j] = A[i][j] + B[i][j]
```

In Excel: `=ARRAYFORMULA(A1:C3 + E1:G3)`

### Residual After One MatMul [7:04]

```
hidden = MMULT(input, weights)      # Matrix multiply
output = hidden + input              # Add residual
```

That's it. The simplest version of a residual addition.

### Residual After Two MatMuls (MLP-style) [7:48]

Closer to what real transformers use:

```
hidden1 = MMULT(input, W1)           # Grow
hidden2 = ReLU(hidden1)
hidden3 = MMULT(hidden2, W2)         # Shrink
output = hidden3 + input             # Residual
```

This is effectively the MLP layer that goes inside a transformer. [11:37]

### Concatenation Residual [9:00]

Used in attention mechanisms (covered in Section 17):

```
output = CONCATENATE(MMULT(input, W), input)
```

The signal is preserved at 100% since the input is kept verbatim.

### Scaled Residual [9:54]

```
scaled = MMULT(output, scale_factor)  # e.g., multiply by 0.5
output = scaled + input
```

Why scale? x + f(x) keeps increasing magnitude. Scaling prevents explosion.

---

## Code: Deep DNN with Residuals

```python
class DeepDNN(nn.Module):
    def __init__(self, layer_depth=20, has_residuals=True):
        super().__init__()
        self.has_residuals = has_residuals
        self.layers = nn.ModuleList([
            nn.Linear(128, 128) for _ in range(layer_depth)
        ])
    
    def forward(self, x):
        for layer in self.layers:
            out = F.relu(layer(x))
            if self.has_residuals:
                out = out + x  # The residual connection
            x = out
        return x
```

### Training: 32 Layers, No Residuals [14:59]

- Starts at 33% accuracy
- Gets to 57% after 50 epochs
- Slow, spiky convergence
- **Gradient explosion inside the network** — internal activations reach values of 10⁸ [18:08]

### Training: 32 Layers, With Residuals [15:35]

- Starts at lower initial accuracy
- **Reaches ~100% within 80 epochs**
- Smooth convergence curve
- Internal activations stay stable

With residuals: test accuracy goes up fast and plateaus at 100%. Without residuals: accuracy oscillates with big negative spikes. [16:28]

### Exercise: 72 Layers, No Residuals [18:28]

72 layers without residuals **never improves** — not even a tiny bit. Training is totally broken. Gradient explosion makes learning impossible.

---

## Why Residuals Work

Li et al. (2018) demonstrated something remarkable: [19:24]

- **Without residuals:** The loss landscape is spiky — lots of local minima and maxima. Easy to get trapped. Hard to navigate. [19:38]
- **With residuals:** The loss landscape smooths out. Harder to get stuck. Easier to find the global minimum. [19:50]

This is why we introduced loss landscapes in Section 7 — they're the key to understanding why residuals work.

### Gradients Flow Through Both Paths

With `output = x + f(x)`, gradients can flow through **both** paths during backpropagation: [21:52]
- Directly through x (the shortcut)
- Through f(x) (the learned transformation)

The direct path ensures gradients never vanish, even in very deep networks. The learned path still allows the network to learn complex transformations.

---

## Exercise

1. **Run 72 layers without residuals** — observe complete training collapse [18:28]
2. **Run 16 layers with growing-shrinking MLPs** (like the real transformer) — this is the closest to actual LLM code you'll write

---

## Next Up: Normalization [27:05]

Residuals prevent vanishing gradients, but they don't prevent gradient explosion entirely — especially as networks get deeper. Normalization is the next tool in the belt.
