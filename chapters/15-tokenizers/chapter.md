# Tokenizers

**Build Your Own LLM Workshop — Chapter 15 of 23**

| | |
|---|---|
| **Duration** | 30m 47s |
| **Video** | https://www.youtube.com/watch?v=TPPhTqPu_Yg |

---

## The Problem: Text to Numbers

From Section 15 onward, everything is about large language models specifically — no more general ML. [0:27]

LLMs and neural networks use numbers. Language uses strings. **Tokenizers** convert between the two, bidirectionally: [0:45]

```
"hello world" → [31373, 995] → "hello world"
```

A token can be: [1:55]
- A single character (`a`, `!`)
- A whole word (`hello`, `world`)
- A subword (`hell`, `o`)

---

## Tiktokenizer Demo

GPT-2 uses a tokenizer called **Tiktoken**. Let's see it in action at [tiktokenizer.vercel.app](https://tiktokenizer.vercel.app). [2:24]

Typing "hello world" shows the token IDs. "Justin" happens to be a single token — it's common enough in the training data. A misspelled word like "message" (with one 's') splits into two subword tokens. [3:10]

Most words are subword combinations. This is the key insight: BPE tokenizers operate at a **subword level**, merging common character sequences into tokens.

---

## Character Tokenizers

The simplest approach: **every character is a token**. [4:31]

- Vocabulary size: ~140 (lowercase, uppercase, numbers, punctuation)
- "Hello" (5 characters) → 5 tokens

**Compression ratio:** 6.12 — the tokenized output is 6× larger than the input. **Negative compression.** [6:27]

Why this is bad: [6:44]
- The model's context window fills up 6× faster (can only process ~1/6 as many words)
- The first layers have to waste compute recombining characters into words before they can even start reasoning

---

## Word Tokenizers

The opposite extreme: **every word is a token**. [7:36]

- Vocabulary size: ~21,000 unique words in a 100,000 word sample
- Compression ratio: ~5:1 — **80% reduction** in size
- Context window can now hold 5× more content

**Compression ratio:** 0.19 — the tokenized output is 5× smaller than the input.

Why this is bad: the **embedding matrix** (Section 16) would be huge. [9:00]

In GPT-2 small, token embeddings are already **31% of all learnable parameters**. A word-level tokenizer would make this even larger — and most of those words would be uncommon (like the longest English word that almost nobody uses). We'd waste massive memory on rare words that don't need dedicated embeddings. [9:50]

---

## BPE: The Compromise

**Byte Pair Encoding (BPE)** is the compromise between character and word tokenizers. [10:54]

It starts at the character level and **builds up** — merging the most frequently occurring character pairs into subwords, then subwords into larger subwords, up to whole words. [11:02]

### BPE Visualizer Walkthrough [12:05]

At [bpe-visualizer.com](https://bpe-visualizer.com):

Starting with "merge me!":
1. The most common co-occurrence is "me" — merged first
2. Then "mr" gets merged
3. And so on, building up from characters to meaningful subword units

With "the quick brown fox jumps over the lazy dog":
- BPE finds frequent pairs and merges them
- It stops when it hits the maximum number of merges or runs out of pairs
- The result: a vocabulary of common subwords + characters for everything else

### Alternatives to BPE

**SentencePiece** handles languages where words can't be split by simple character boundaries — Japanese, Korean, Chinese. It operates on a different tokenization principle for these scripts. [11:45]

---

## GPT-2 Tokenizer in Code [14:10]

```python
from transformers import GPT2Tokenizer

tokenizer = GPT2Tokenizer.from_pretrained('gpt2')
tokens = tokenizer.encode("Hello world. I'm supercalifragilisticexpialidocious!")
```

The vocabulary:
- First tokens: punctuation marks (!, (, ), etc.)
- Then uppercase letters, lowercase letters
- Then subwords like "inter", "interdependency"
- The word "world" is at token index 995 [15:09]

Encoding "hello world" produces a mix of full-word tokens and subword tokens — this is the "compromised" nature of BPE. [16:24]

---

## Building Tokenizers from Scratch

### Character Tokenizer [17:23]

```python
class CharTokenizer:
    def __init__(self, corpus):
        chars = sorted(list(set(corpus)))
        self.stoi = {ch: i for i, ch in enumerate(chars)}
        self.itos = {i: ch for i, ch in enumerate(chars)}
    
    def encode(self, text):
        return [self.stoi[ch] for ch in text]
    
    def decode(self, ids):
        return ''.join([self.itos[i] for i in ids])
```

From 100,000 words → 612,000 characters → 140 unique chars → compression ratio 6.12.

Encoding "hello world" → every character is its own token. [18:35]

### Word Tokenizer [19:15]

```python
class WordTokenizer:
    def __init__(self, corpus):
        words = corpus.split()
        vocab = sorted(list(set(words)))
        self.stoi = {w: i for i, w in enumerate(vocab)}
        self.itos = {i: w for i, w in enumerate(vocab)}
```

From 100,000 words → 21,000 unique words → compression ratio 0.19. But vocabulary is too large — wastes embedding space on rare words.

### BPE Tokenizer [20:41]

```python
class BPETokenizer:
    def __init__(self, corpus, vocab_size=5000):
        # Start with character-level tokens
        # Find most frequent adjacent pairs
        # Merge them into new tokens
        # Repeat until vocab_size is reached
        ...
```

BPE training loop: [20:55]
1. Start with all unique characters
2. Find the most frequent pair of adjacent tokens
3. Merge them into a single token
4. Repeat until vocabulary reaches target size

### Special Tokens [23:13]

| Token | Purpose |
|-------|---------|
| `<|endoftext|>` | End of sequence / separator |
| `<|pad|>` | Padding to fill context window |
| `<|unk|>` | Unknown/unseen token |

---

## Custom BPE Exercise [23:43]

Train your own BPE tokenizer on fineweb-edu data:

```python
bpe = BPETokenizer(corpus, vocab_size=5000)
encoded = bpe.encode("hello world")
decoded = bpe.decode(encoded)
```

Compare character, word, and BPE tokenizers on the same text:
- **Character:** 612K tokens from 100K words — terrible compression
- **Word:** 21K tokens — great compression, huge embedding
- **BPE (5K vocab):** ~50% compression — balanced

---

## Using OpenAI's Tiktoken [26:58]

For production, use the official implementation:

```python
import tiktoken

enc = tiktoken.get_encoding("gpt2")
tokens = enc.encode("hello world")
# [31373, 995]
text = enc.decode(tokens)
# "hello world"
```

---

## Key Decisions [28:23]

| Decision | Choice | Why |
|----------|--------|-----|
| Tokenizer type | GPT-2 BPE | Matches our model |
| Vocabulary size | 50,257 | Standard GPT-2 vocab |
| Special tokens | `<|endoftext|>` | Separator for our model |
| Training data | FineWeb-Edu | Education-focused dataset |

---

## Next Up: Embeddings [30:19]

Tokenizers convert text to integers. Embeddings convert those integers into high-dimensional vectors that the model can actually reason with. This is where the magic of "meaning in high-dimensional space" begins.
