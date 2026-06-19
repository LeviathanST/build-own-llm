# Transformers

**Build Your Own LLM Workshop — Chapter 18 of 23**

| | |
|---|---|
| **Duration** | 53m 52s |
| **Video** | https://www.youtube.com/watch?v=mKAW7cYYwQs |

---

## The Culmination

We've spent 17 sections learning individual components. This section **pulls everything together** into the GPT-2 style transformer architecture. [0:49]

By the end, we'll be complete with the architecture. The remaining sections cover training, evaluation, and post-training. [1:04]

**The key insight:** Transformers contain no new concepts. Every component is something we've already learned. Transformers are just composition. [17:57]

---

## Architecture Overview

GPT-2's architecture follows this flow: [2:17]

```
Input text → Tokenizer → Token Embeddings → Positional Embeddings → Dropout
    → 12× Transformer Blocks
        → Pre-LayerNorm → Multi-Head Attention → Dropout → Residual
        → Pre-LayerNorm → MLP (grow → activation → shrink) → Dropout → Residual
    → Final LayerNorm → Unembedding → Softmax → Output
```

### The Flow Step by Step [2:09]

1. **Tokenize** the input text (Section 15)
2. **Token embeddings** — look up the 768-dimensional vector for each token (Section 16)
3. **Positional embeddings** — add position information (Section 16)
4. **Dropout** — 10% regularization (Section 13)
5. **12× Transformer blocks** — the core
6. **Final LayerNorm** — one last normalization (Section 12)
7. **Unembedding** — project back to vocabulary space (Section 16)
8. **Softmax** → sample next token (Sections 14, 1)

---

## Inside a Transformer Block

Each block has two sub-layers, each following the **pre-norm** pattern:

### Sub-layer 1: Attention

```
x → LayerNorm → Multi-Head Attention → Dropout → + (residual from pre-norm input)
```

1. Pre-LayerNorm on the input [2:57]
2. Multi-Head Attention (Section 17)
3. Dropout (Section 13)
4. Add the pre-norm input as a residual connection (Section 11)

### Sub-layer 2: MLP [3:12]

```
x → LayerNorm → Linear (grow 4×) → Activation (ReLU²) → Linear (shrink) → Dropout → + (residual)
```

1. Pre-LayerNorm
2. Linear layer: expand from 768 → 3072 (4×) — gives the network a "scratchpad" [3:19]
3. ReLU² activation (Section 4)
4. Linear layer: shrink from 3072 → 768
5. Dropout
6. Residual connection from the pre-norm input

This block repeats **12 times**. [3:40] The residual stream flows through all blocks untainted — each block only *adds* its output to the stream. [14:47]

---

## Excel Walkthrough

### Step 1: Tokenize [4:34]

Input: "the brown fox the brown dog jumped over the lazy fox"

Using the GPT-2 tokenizer vocabulary (50,257 tokens), we convert each word to its token ID. [4:52]

### Step 2: Token Embeddings [5:23]

Look up each token ID in the embedding matrix (vocab_size × hidden_dim = 50,257 × 768). The result is a context_size × hidden_dim matrix.

### Step 3: Positional Encoding [6:20]

Add sinusoidal positional encodings to the embeddings. Each position gets a unique sine/cosine pattern added to its embedding vector. [6:43]

```
input_embeddings = token_embeddings + positional_encodings
```

### Step 4: Dropout [7:36]

Apply 10% dropout mask — element-wise multiply by a binary mask. [7:44]

### Step 5–16: Transformer Blocks (×12) [8:21]

Each block follows the same pattern. In the spreadsheet, we trace through one block step by step:

1. **LayerNorm** (pre-norm) [8:41]
2. **Multi-Head Attention** (12 heads, 64 dimensions each) [9:13]
   - Compute QKV per head
   - Scale, mask, softmax
   - Multiply by V
   - Concatenate heads, project with W_O
3. **Dropout** [11:52]
4. **Residual connection** — add the pre-norm input [12:02]
5. **LayerNorm** (pre-norm for MLP) [12:49]
6. **MLP** [12:59]
   - Linear: 768 → 3072 (grow)
   - Activation: ReLU²
   - Linear: 3072 → 768 (shrink)
7. **Dropout** [14:16]
8. **Residual connection** [14:30]

Repeat 11 more times.

### Step 17: Final LayerNorm [15:34]

### Step 18: Unembedding [15:41]

Multiply by the transpose of the embedding matrix (weight-tied):

```python
logits = torch.matmul(hidden_states, embedding_weights.T)
```

### Step 19: Softmax + Sampling [16:21]

Apply softmax to the logits, then use ArgMax or sampling (temperature, top-K, top-P) to pick the next token.

---

## Code: The Full GPT-2 Model [18:32]

```python
class GPT2Model(nn.Module):
    def __init__(self, config):
        super().__init__()
        self.token_embedding = nn.Embedding(config.vocab_size, config.hidden_size)
        self.position_embedding = nn.Embedding(config.max_position, config.hidden_size)
        self.dropout = nn.Dropout(config.dropout_rate)
        self.blocks = nn.ModuleList([
            TransformerBlock(config) for _ in range(config.num_layers)
        ])
        self.ln_f = nn.LayerNorm(config.hidden_size)
        self.lm_head = nn.Linear(config.hidden_size, config.vocab_size, bias=False)
        
        # Weight tying
        self.lm_head.weight = self.token_embedding.weight
    
    def forward(self, input_ids):
        B, T = input_ids.shape
        positions = torch.arange(T, device=input_ids.device)
        
        x = self.token_embedding(input_ids) + self.position_embedding(positions)
        x = self.dropout(x)
        
        for block in self.blocks:
            x = block(x)
        
        x = self.ln_f(x)
        logits = self.lm_head(x)
        return logits
```

### The Transformer Block [20:12]

```python
class TransformerBlock(nn.Module):
    def __init__(self, config):
        super().__init__()
        self.ln1 = nn.LayerNorm(config.hidden_size)
        self.attn = CausalSelfAttention(config)
        self.ln2 = nn.LayerNorm(config.hidden_size)
        self.mlp = MLP(config)
        self.dropout = nn.Dropout(config.dropout_rate)
    
    def forward(self, x):
        # Pre-norm attention sub-layer
        x = x + self.dropout(self.attn(self.ln1(x)))
        # Pre-norm MLP sub-layer
        x = x + self.dropout(self.mlp(self.ln2(x)))
        return x
```

### The MLP [20:44]

```python
class MLP(nn.Module):
    def __init__(self, config):
        super().__init__()
        self.fc1 = nn.Linear(config.hidden_size, config.hidden_size * 4)
        self.fc2 = nn.Linear(config.hidden_size * 4, config.hidden_size)
        self.dropout = nn.Dropout(config.dropout_rate)
    
    def forward(self, x):
        x = self.fc1(x)
        x = torch.relu(x) ** 2  # ReLU²
        x = self.dropout(x)
        x = self.fc2(x)
        return x
```

---

## Interactive Transformer Demo [45:50]

The "Transformer Explained" demo loads real GPT-2 small weights and lets you:
- Step through each layer
- See attention patterns visually
- Watch how tokens change through attention and MLP
- Compare nanoGPT to GPT-2 small

Available at the workshop links.

---

## Modern Transformer Variants [46:22]

GPT-2 (2019) was just the beginning. Key differences in modern models:

| Feature | GPT-2 (2019) | Modern (2025/26) |
|---------|--------------|------------------|
| Normalization | Post-norm LayerNorm | **Pre-norm RMSNorm** |
| Activation | GELU | **SwiGLU** |
| Attention | MHA | **GQA / Flash Attention** |
| Positional encodings | Learned absolute | **RoPE (rotary)** |
| Context window | 1,024 | **100K–1M+** |
| Embedding | Separate | **Weight-tied** |

---

## Next Up: Pre-training [53:17]

The architecture is done. Now we need to train it. Pre-training covers:
- The dataset (FineWeb-Edu)
- Binning and data loading
- The full pre-training script
- Actually training the model to speak English
