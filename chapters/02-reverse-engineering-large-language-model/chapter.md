# Reverse Engineering Large Language Models

**Build Your Own LLM Workshop — Chapter 2 of 23**

| | |
|---|---|
| **Duration** | 15m 32s |
| **Video** | https://www.youtube.com/watch?v=E0rkgxwhz5g |

---

## The Goal: Extract a Roadmap

In the previous section, we ran GPT-2 inside a Colab notebook. Now we're going to reverse engineer that model to figure out what components we need to build our own. [0:09]

The key insight: we can inspect the model in memory — calling `print(model)` and `summary()` — to discover all the inference-time components that make up a GPT-2 style transformer. [0:36] These components become our workshop roadmap.

---

## Loading GPT-2 and Counting Parameters

We load GPT-2 into memory and check its size. [1:28]

```python
from transformers import GPT2Model
model = GPT2Model.from_pretrained('gpt2')
```

**GPT-2 small has about 124 million parameters.** [1:52] Is that a lot? It's more than a few million and a lot less than a few billion — roughly the size of a small test model by modern standards. [2:00]

A *parameter* is a unit of size for a model (we'll learn more about what they actually are when we cover perceptrons).

---

## print(model) — The Component Tree [2:13]

Calling `print(model)` reveals a tree of modules:

```
GPT2Model(
  (transformer): GPT2Model(
    (wte): Embedding(…)
    (wpe): Embedding(…)
    (drop): Dropout(…)
    (h): ModuleList(
      (0-11): 12 x GPT2Block(
        (ln_1): LayerNorm(…)
        (attn): GPT2Attention(…)
        (ln_2): LayerNorm(…)
        (mlp): GPT2MLP(
          (c_fc): Conv1D(…)
          (act): NewGELUActivation()
          (c_proj): Conv1D(…)
          (dropout): Dropout(…)
        )
      )
    )
    (ln_f): LayerNorm(…)
  )
)
```

The modules we see: [2:28]
- **Transformer** — the overall architecture
- **Embedding** — how tokens become vectors
- **Dropout** — a regularization technique
- **LayerNorm** — normalization between layers
- **Linear / Conv1D** — weight matrix operations
- **Attention** — the core mechanism that relates tokens to each other
- **MLP** — the feedforward network within each block
- **GELU activation** — the nonlinearity function

All of these will become sections of our workshop.

### torchinfo.summary() [3:02]

Using `torchinfo.summary()` gives a cleaner view and reveals that **GPT-2 has 12 repeated GPT2 blocks** — that's 12 layers within the transformer. [3:16]

The difference between 124M and 163M parameters depends on whether you count the embeddings. In this workshop, we count them. [3:33]

---

## From Components to a Workshop Roadmap [4:39]

Each component we discovered maps to a workshop section:

| Component | Section |
|-----------|---------|
| Transformer | Section 18 |
| Embedding | Section 16 |
| Dropout | Section 13 (Regularization) |
| LayerNorm | Section 12 (Normalization) |
| Residuals | Section 11 |
| MLP / Feedforward | Section 6 |
| GELU Activation | Section 4 |
| Attention | Section 17 |
| Softmax | Section 14 |

Beyond the module tree, there are also **functions** that are invisible in the module printout: [5:35]
- Activation functions
- Initialization
- Normalization
- Softmax

The function call tree shows that a transformer is essentially **attention → MLP → attention → MLP — repeated 12 times.** [6:19]

---

## Exercise: Reverse Engineer Any Model [6:44]

Go to [Hugging Face](https://huggingface.co), choose a text generation model (6B–12B parameters, no more than 32B), and run the same `print(model)` / `summary()` commands.

For example, load Tiny LLaMA (1.1B parameters — about 10x bigger than GPT-2 small) [7:14]:

```python
from transformers import AutoModel
model = AutoModel.from_pretrained("TinyLlama/TinyLlama-1.1B-Chat-v1.0")
print(model)
```

You'll see familiar components — attention layers, embedding layers, linear layers, MLPs — plus some differences like **RMSNorm** (instead of LayerNorm) and **rotary positional embeddings**. [7:55]

Try it with different models. It's empowering to see that the architecture is recognizable across model families. [8:17]

---

## Ablation Tests [8:48]

Why do we use these specific components? **Machine learning is an empirical field** [9:34] — we use the components that work. The components we use outperformed the alternatives in controlled experiments.

An **ablation test** means taking something away and comparing performance. [10:01] If the system works better with a component than without it, the component "won" the ablation test. The reverse engineering we just did is meaningful because it tells us these are the components that worked.

---

## LLMs Are Grown, Not Built [10:10]

Three metaphors for how LLMs work:

> **Chris Olah (2020):** "LLMs are grown, not built." [10:14]
> We build the architecture, but the model learns the language itself. We don't teach grammar rules — we expose it to English and it picks them up.

> **Andrej Karpathy:** LLMs are like "summoning ghosts" — we show it the entire English language and its foggy recollection is what it learns. [10:45]

> **Justin Angel:** Farmers build the farm, but the tomatoes do the growing. We set up the trellises (the architecture); the model does the growing (learning). [11:10]

---

## The Full Roadmap [11:27]

Here's the complete workshop roadmap we derived from reverse engineering GPT-2:

**Architecture components** (from the model tree):
- Activation functions → Section 4
- MLP / Feedforward networks → Section 6
- Residuals → Section 11
- Normalization → Section 12
- Regularization (Dropout) → Section 13
- Softmax → Section 14
- Tokenizers → Section 15
- Embeddings → Section 16
- Attention → Section 17
- Transformers → Section 18

**Training fundamentals** (needed to actually train a model):
- Perceptrons → Section 3
- GPU coding → Section 5
- Loss functions → Section 7
- Backpropagation → Section 8
- Saving & loading models → Section 9
- Random initialization → Section 10

**LLM-specific training:**
- Pre-training → Section 19
- Evaluation → Section 20
- Instruction tuning → Section 21
- Reinforcement learning → Section 22

---

## Every Section in One Line of Code [12:08]

Every section in this workshop can be summarized in roughly one line of code. [12:35] If you just want the code, it's all in the Colab notebooks at `go.justinangel.ai/code-0`.

Our goal for the day is not just to copy those lines, but to understand them intuitively — to know *why* each component exists and *how* it works.

---

## Interactive 3D Demo [13:14]

There's an excellent interactive 3D model (created by Shawn, whose name I'm forgetting — my apologies) that visualizes all the components we just discovered in non-linear-algebra form. [13:25]

You can:
- See embeddings, layer norms, projections, MLPs, and softmax in a visual hierarchy
- Click through and watch attention flow across layers
- Compare models from nanoGPT (80K parameters) to GPT-2 small (124M) to GPT-3 (175B)
- Deep dive into individual blocks like the MLP [14:17]

I highly recommend spending time with this demo — it's one of the most useful tools for building intuition about how all these components fit together. [14:24]

---

## Next Up: Perceptrons

Our next section starts building from the ground up. Perceptrons are the basic unit of work within any neural network. [14:55] From there, we'll build up to:

- Activation functions
- GPU performance
- MLPs and feedforward networks
- Loss functions
- Backpropagation (how we train)

That's the entire machine learning fundamentals module. See you in section 3.
