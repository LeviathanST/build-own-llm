# Embeddings

**Build Your Own LLM Workshop — Chapter 16 of 23**

| | |
|---|---|
| **Duration** | 48m 42s |
| **Video** | https://www.youtube.com/watch?v=jyrgYjeVHBo |

---

## From Token IDs to Meaning

Tokenizers convert strings to integers (token IDs). But those integers are just indices — they carry no meaning. **Embeddings** convert token IDs into high-dimensional vectors that the network can reason with. [0:14]

A token ID like "995" (the token for "world") gets mapped to a vector of floating-point numbers in a high-dimensional space. For GPT-2 small, that's **768 dimensions** per token. [1:38]

---

## High-Dimensional Space

We think in 3 dimensions (x, y, z). Maybe 4 if you include time. GPT-2 small thinks in **768 dimensions**. [1:31]

I can't visualize 768 dimensions. But here's the key insight: **these seemingly random numbers mean something to an alien intelligence that thinks in high-dimensional space.** [6:19]

### Analogy Vectors

Using PCA (Principal Component Analysis), we can compress 768 dimensions down to 2 or 3 for visualization: [4:29]

When we embed the words **king, queen, man, woman** and project them to 2D:

```
    king ——— man
      |         |
      |         |
    queen —— woman
```

The vector from man → woman is roughly the same direction and distance as king → queen. The "royal gender" relationship is encoded in the embedding space. [5:12]

Similarly: Paris → France ≈ Berlin → Germany. Capital city relationships exist as directions in embedding space. [5:37]

**This is the key takeaway:** These high-dimensional vectors capture meaning — relationships, analogies, concepts. The model doesn't just store words; it stores a structured map of how concepts relate to each other. Large language models are alien intelligences that think in high-dimensional space. We don't fully understand how they work, and that's an active field of research. [6:34]

---

## Embedding Hyperparameters

### 1. Vocabulary Size

The number of tokens in the tokenizer. GPT-2 uses **50,257**. Claude 3.5 uses **150,000**. [7:38]

This determines how many **rows** the embedding matrix has — one row per token.

### 2. Hidden Size (d_model)

The number of dimensions in the embedding space. GPT-2 small uses **768**. [8:16]

This determines how many **columns** the embedding matrix has — the richness of representation per token.

More dimensions = more information per token. But doubling hidden size doubles the embedding matrix size — and embeddings already take up **31% of GPT-2 small's total parameters**. [9:00]

### 3. Context Size

The maximum number of tokens the model can process at once. GPT-2 uses **1,024 tokens** (~500–750 words). [10:55]

This determines how many **rows** flow through the model's internal matrices. Modern models have context sizes of 100K, 1M, or more — but that's much harder to build.

### 4. Batch Size

How many sequences to process in parallel. At inference time, batch size 2 means processing 2 sentences simultaneously to maximize GPU utilization. [11:31]

---

## The Three Matrices

| Matrix | Dimensions | Purpose |
|--------|-----------|---------|
| Input matrix | batch × context | Raw token IDs |
| Embedding matrix | vocab_size × hidden_size | Token → vector lookup table |
| Input embeddings | batch × context × hidden_size | Tokens in embedding space |

The embedding matrix is a **lookup table**. For each token ID in your input, you grab the corresponding row from the embedding matrix. [13:47]

You've actually seen this before — in Section 8, the A+B mod 5 model had a 200×32 embedding matrix (200 vocabulary, 32 hidden dimensions). The PCA visualization showed 5 points in a circle — the model learned a cyclic representation. [14:44]

---

## Positional Encoding

### The Problem [16:28]

Embeddings have no positional information. "Man bites dog" and "Dog bites man" produce the same embeddings — just the words man, bites, dog in no particular order. But these sentences have opposite meanings.

Without positional encoding, the LLM can't distinguish word order.

### The Solution: Rotating a Pug [18:40]

Imagine a pug in 3D space. Rotate it 10° — it's still a pug, but you know it was rotated. Rotate it 20° — still a pug, but you know it was rotated more.

**Positional encoding works the same way.** We add small values to each embedding that "rotate" it slightly in high-dimensional space — enough for the model to learn where the token was positioned, but not so much that the token's meaning is lost.

### Absolute Positional Encodings [20:02]

Uses sine and cosine waves at different frequencies:

```
PE(pos, 2i)   = sin(pos / 10000^(2i/d_model))
PE(pos, 2i+1) = cos(pos / 10000^(2i/d_model))
```

Each position gets a unique pattern of sine/cosine values added to its embedding. [20:49]

### Learned Positional Encodings [22:48]

Instead of fixed sine/cosine functions, let the network **learn** the positional values during training:

```python
self.position_embeddings = nn.Embedding(max_position, hidden_size)
```

This gives the model flexibility to learn whatever positional patterns are most useful. GPT-2 uses learned positional embeddings. [24:08]

### Relative Positional Encodings [24:25]

Instead of encoding absolute position ("I am token #5"), encode **relative distance** ("I am 2 positions after token #3"). The attention mechanism (Section 17) uses relative positions to determine which tokens to focus on.

### Rotary Positional Encodings (RoPE) [26:27]

Modern LLMs use RoPE: instead of adding positional values, it **rotates** the embedding vectors by an angle proportional to their position.

This gives better performance on long sequences and is used by most recent models.

---

## Code Implementation

### Token + Position Embeddings [28:04]

```python
class GPTEmbeddings(nn.Module):
    def __init__(self, vocab_size, hidden_size, max_position):
        super().__init__()
        self.token_embedding = nn.Embedding(vocab_size, hidden_size)
        self.position_embedding = nn.Embedding(max_position, hidden_size)
    
    def forward(self, input_ids):
        token_embeds = self.token_embedding(input_ids)
        positions = torch.arange(input_ids.shape[1]).to(input_ids.device)
        pos_embeds = self.position_embedding(positions)
        return token_embeds + pos_embeds
```

### Unembedding Matrix (LM Head) [39:30]

The reverse of the embedding matrix. At the output, we need to convert hidden states back to token probabilities:

```python
class GPTLMHead(nn.Module):
    def __init__(self, hidden_size, vocab_size):
        super().__init__()
        # Often weight-tied with the input embedding
        self.lm_head = nn.Linear(hidden_size, vocab_size, bias=False)
    
    def forward(self, hidden_states):
        logits = self.lm_head(hidden_states)
        return logits
```

**Weight tying:** The input embedding matrix and the output unembedding matrix often share the same weights. This saves memory and improves training. [42:41]

---

## Embedding Visualization with PCA [45:30]

After training, we can visualize embeddings:

```python
from sklearn.decomposition import PCA

embeddings = model.token_embedding.weight.detach().cpu().numpy()
pca = PCA(n_components=2)
reduced = pca.fit_transform(embeddings)

# Plot: each point is a token, colored by frequency or category
plt.scatter(reduced[:, 0], reduced[:, 1])
```

This shows the structure the model learned — tokens cluster by semantic similarity.

---

## Key Decisions for GPT-2

| Hyperparameter | Value | Notes |
|----------------|-------|-------|
| Vocabulary size | 50,257 | Matches GPT-2 BPE tokenizer |
| Hidden size | 768 | GPT-2 small |
| Context size | 1,024 | Tokens |
| Batch size | TBD | Depends on GPU memory |
| Positional encoding | Learned | GPT-2 style |
| Weight tying | Yes | Input embed = output embed |

---

## Next Up: Attention [48:34]

Attention is the secret sauce of transformers. It's how the model decides which tokens to focus on when predicting the next word. We'll finally see how all these components — embeddings, MLPs, residuals, normalization — come together.
