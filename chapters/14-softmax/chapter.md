# Softmax

**Build Your Own LLM Workshop — Chapter 14 of 23**

| | |
|---|---|
| **Duration** | 20m 13s |
| **Video** | https://www.youtube.com/watch?v=H2yV3jd4DKg |

---

## From Logits to Probabilities

This is the last deep neural network technique before we go into language-specific components. Softmax happens at the very end of a neural network — it converts **logits** (raw activations) into **probabilities**. [0:30]

**Logits** are just the output activations of a network. They tend to fall in the -4 to +4 range (if training hasn't collapsed). [1:12]

But logits aren't useful on their own. If our A×B mod C network outputs [3.5, 0.05, -9.8, ...], those numbers don't mean anything to us. We need probabilities — something that sums to 100% and tells us "token 6 has a 22% chance, token 8 has 25%." [2:03]

---

## Why Linear Ratios Fail

The naive approach: sum all logits, then divide each by the sum. Three problems: [3:04]

1. **Negative values cancel positives.** If logits include -9 and +7, summing them loses signal. You'd need to shift by the minimum first. [3:17]

2. **Bad for backpropagation.** Derivatives of a simple sum/division aren't clean for gradient computation. [3:33]

3. **Linear ratios produce flat probabilities.** All options converge to roughly equal percentages. We want a "winner takes all" effect — the most likely word should stand out. [3:58]

---

## Softmax Formula

Softmax solves all three problems using **exponents**: [5:26]

```
Softmax(xᵢ) = exp(xᵢ) / Σⱼ exp(xⱼ)
```

**Exponents** amplify differences: [5:47]
- Small numbers → pushed even smaller (e⁻⁵ ≈ 0.007)
- Large numbers → pushed much larger (e⁵ ≈ 148)
- Negative numbers → become positive (e⁻⁵ is still positive)

This creates a "winner takes all" effect. The highest logit gets a disproportionately large probability share. [11:07]

---

## Excel Demonstration

### Exponents [9:10]

Creating `=EXP(values)` for inputs from -2 to 10:
- Negative values hover between 0.1 and 1.0
- Values between 0 and 1 map to between 1.0 and 2.7
- Values above 1 grow exponentially

The gap between winners and losers gets dramatically larger.

### Softmax on a 1D Vector [10:07]

1. Take logits (e.g., 10 values from a normal distribution)
2. Compute `exp(logit)` for each
3. Sum all exponents
4. Divide each exponent by the sum

**Result:** One value at 99%, the next at 1%. The clearest winner dominates.

### Softmax vs Linear Ratio [11:13]

With the same logits:
- **Linear ratio:** All probabilities cluster around 10-15%. Hard to pick a winner. [8:50]
- **Softmax:** The leading logit breaks out dramatically. Clear winner.

### Softmax on a 2D Matrix (for Attention) [12:17]

In attention (Section 17), softmax operates per **row**:

1. Compute exponent of every cell
2. Sum each row
3. Divide each cell by its row sum

Each row now sums to 100%. This is how attention determines which tokens to focus on.

---

## Code Example

```python
import torch

logits = torch.tensor([3.5, 0.05, -9.8, 2.1, 0.5])
probabilities = torch.softmax(logits, dim=0)
# Result: [0.45, 0.14, 0.00, 0.33, 0.08]
```

The 8th token (index 6) might be the winner at 22.8%, but the 6th token (index 5) is close at 22%. Softmax preserves and enhances these differences, making the network's preference clear. [16:30]

---

## Exercise: Implement Softmax

```python
def softmax(logits):
    exp_logits = torch.exp(logits)
    sum_exp = torch.sum(exp_logits)
    return exp_logits / sum_exp
```

You'll need:
- `torch.exp()` for exponents
- `torch.sum()` for summing
- `torch.max()` to find the winning logit

---

## Key Decisions [17:58]

| Decision | Choice |
|----------|--------|
| Softmax type | LogSoftmax (standard) |
| Alternative | SparseMax (harder, less common) |

**Why standard softmax?** Remember loss landscapes from Section 7. Softmax has a gentle slope that's easy to navigate during optimization. SparseMax has a steep, intense slope — harder to traverse. [18:28]

---

## Softmax vs Sampling [19:20]

Softmax is the **first round** of selection — it converts logits to clean probabilities. Then sampling (temperature, top-K, top-P from Section 1) takes a **second pass** to choose the actual output token.

---

## Next Up: Tokenizers [19:46]

We're done with deep neural network techniques. Now: **language-specific components**. Tokenizers solve the problem of converting text into numbers that a neural network can process.
