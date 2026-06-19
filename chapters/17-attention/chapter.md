# Attention

**Build Your Own LLM Workshop — Chapter 17 of 23**

| | |
|---|---|
| **Duration** | 58m 28s |
| **Video** | https://www.youtube.com/watch?v=CvGf-Eu2sl0 |

---

## The Secret Sauce of Transformers

Attention is the core mechanism that makes transformers work. It correlates every input token with every other input token using learned concepts. [1:04]

Why is this important? Before attention, models had a fixed context window and limited ability to look at relationships between distant words. Attention lets each token "look at" every other token and decide which ones matter.

**The catch:** Computing these correlations is O(n²) — quadratic in the sequence length. Every token looks at every other token. That's why longer contexts are expensive. [1:22]

---

## QKV: The Three Matrices

Attention uses three matrices derived from the input: [2:21]

```
Q = input × W_Q    (Query — what am I looking for?)
K = input × W_K    (Key — what do I contain?)
V = input × W_V    (Value — what information do I carry?)
```

Each is computed by multiplying the input by a learned weight matrix: [2:33]

```python
Q = torch.matmul(input, W_Q)
K = torch.matmul(input, W_K)  
V = torch.matmul(input, W_V)
```

The Q and K matrices form the **QK circuit** (which tokens pay attention to which). The V matrix combines with it to form the **OV circuit** (what information flows through). [3:12]

---

## Masked Self-Attention Steps

The full formula:

```
Attention(Q, K, V) = softmax(Q × Kᵀ / √(d_k) + mask) × V
```

Step by step: [3:07]

### Step 1: Q × Kᵀ (Query-Key Product)

Multiply Q by the transpose of K. This creates a matrix where cell [i][j] represents "how much should token i pay attention to token j?"

### Step 2: Scale by √(d_k)

Divide by the square root of the key dimension. [3:49] This prevents the dot products from growing too large and pushing softmax into extreme gradients.

```python
scores = torch.matmul(Q, K.transpose(-2, -1)) / math.sqrt(d_k)
```

### Step 3: Causal Mask [3:22]

In autoregressive language modeling, a token should only attend to tokens *before* it, not after. The mask sets all future positions to -infinity so softmax gives them zero probability:

```
mask = [
  [0,  -∞, -∞, -∞],
  [0,   0, -∞, -∞],
  [0,   0,  0, -∞],
  [0,   0,  0,  0]
]
```

After softmax, each token's attention weights only apply to itself and preceding tokens.

### Step 4: Softmax

Apply softmax per row (as in Section 14) so each row sums to 100%. This converts the scores into attention probabilities.

### Step 5: Multiply by V (OV Circuit)

```
output = softmax(scores) × V
```

This produces the final attention output — a weighted combination of the value vectors, where the weights come from the attention scores.

---

## Multi-Head Attention [4:54]

Instead of one attention mechanism, transformers use **multiple heads** running in parallel, each learning different relationships:

```
output = concatenate(head₁, head₂, ..., headₕ) × W_O
```

Where each head is:

```
headᵢ = Attention(Qᵢ, Kᵢ, Vᵢ)
```

With 12 heads in GPT-2 small, each head operates on 64 dimensions (768 / 12). [5:00]

The outputs are concatenated and projected through a final weight matrix W_O to produce the multi-head attention output. This is what gets fed into the residual stream.

---

## Excel Walkthrough

### Compute QKV [7:46]

```
Q = MMULT(input, W_Q)   # 5×5 × 5×5 = 5×5
K = MMULT(input, W_K)   # 5×5 × 5×5 = 5×5
V = MMULT(input, W_V)   # 5×5 × 5×5 = 5×5
```

### QK Scale Softmax [10:06]

```
scores = MMULT(Q, TRANSPOSE(K))    # QK circuit
scaled = scores / √(d_k)           # Scale by √5
masked = scaled + mask             # Apply causal mask
attn = SOFTMAX(masked, dim=1)      # Per-row softmax
```

Each row of `attn` sums to 100%. The causal mask ensures future tokens get ~0%.

### OV Circuit Output [15:51]

```
output = MMULT(attn, V)  # Weighted combination of values
```

This is the final attention output for a single head.

### End-to-End Self-Attention [16:47]

Combining all steps in one formula:

```excel
=MMULT(SOFTMAX(
    (MMULT(Q, TRANSPOSE(K)) / √(d_k)) + mask
, dim=1), V)
```

### Parallel Heads in Sheets [19:14]

For multi-head attention, compute multiple QKV sets in parallel and concatenate:

```
head₁ = attention(input, W_Q₁, W_K₁, W_V₁)  # 5×5
head₂ = attention(input, W_Q₂, W_K₂, W_V₂)  # 5×5
MHA_output = MMULT(CONCAT(head₁, head₂), W_O)  # 5×5
```

### Output Projection W_O [22:14]

The concatenated heads (which would be very wide) get projected back to the model dimension:

```python
MHA_output = torch.matmul(concat_heads, W_O)  # Back to d_model
```

---

## GQA and MQA [24:21]

Multi-head attention is expensive. Two optimizations:

| Variant | Key/Value Heads | Use Case |
|---------|----------------|----------|
| **MHA** (Multi-Head) | Full K/V per head | Original transformer |
| **GQA** (Grouped Query) | Shared K/V per group of Q heads | LLaMA 2 |
| **MQA** (Multi-Query) | Single shared K/V for all Q heads | Fast inference |

GQA and MQA reduce memory and compute by sharing key/value projections across query heads. GQA is the most common in modern models. [24:35]

---

## Attention Variants [29:39]

| Variant | Description |
|---------|-------------|
| **Self-attention** | Tokens attend to all tokens in the same sequence |
| **Cross-attention** | Tokens attend to tokens in a different sequence (encoder-decoder) |
| **Causal attention** | Self-attention with future masking (used in GPT) |
| **Sliding window** | Only attend to nearby tokens (reduces O(n²)) |
| **Flash attention** | GPU-optimized attention that avoids materializing the full attention matrix |

---

## Interpreting Heads [32:32]

Different attention heads learn different concepts:

- Some heads learn **positional** patterns (token i attends to token i-1)
- Some heads learn **syntactic** patterns (subjects attend to their verbs)
- Some heads learn **semantic** patterns (entities attend to related entities)

Tools like **Neuronpedia** let you explore what individual heads learn. [39:37]

---

## Code Implementation

### Causal Self-Attention [42:34]

```python
class CausalSelfAttention(nn.Module):
    def __init__(self, config):
        super().__init__()
        self.num_heads = config.num_heads
        self.head_dim = config.hidden_size // config.num_heads
        
        self.qkv = nn.Linear(config.hidden_size, 3 * config.hidden_size)
        self.proj = nn.Linear(config.hidden_size, config.hidden_size)
    
    def forward(self, x):
        B, T, C = x.shape
        qkv = self.qkv(x).reshape(B, T, 3, self.num_heads, self.head_dim)
        q, k, v = qkv.unbind(2)
        
        # Attention scores
        att = (q @ k.transpose(-2, -1)) * (1.0 / math.sqrt(self.head_dim))
        
        # Causal mask
        mask = torch.tril(torch.ones(T, T)).view(1, 1, T, T)
        att = att.masked_fill(mask == 0, float('-inf'))
        
        # Softmax + apply values
        att = F.softmax(att, dim=-1)
        y = (att @ v).transpose(1, 2).reshape(B, T, C)
        
        # Output projection
        return self.proj(y)
```

---

## Key Decisions for GPT-2 [53:45]

| Hyperparameter | Value |
|----------------|-------|
| Number of heads | 12 |
| Head dimension | 64 (768 / 12) |
| Attention type | Causal self-attention (MHA) |
| KV sharing | None (full MHA) |
| Output projection | W_O: 768×768 |

---

## Next Up: Transformers [58:00]

Attention is one component. The transformer is the composition of *all* the components we've learned — embeddings, attention, MLPs, residuals, normalization — arranged in a specific architecture. Section 18 puts it all together.
