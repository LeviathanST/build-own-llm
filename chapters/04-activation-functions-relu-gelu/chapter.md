# Activation Functions: ReLU, GELU

**Build Your Own LLM Workshop — Chapter 4 of 23**

| | |
|---|---|
| **Duration** | 25m 50s |
| **Video** | https://www.youtube.com/watch?v=G5gkYVB-P-Q |

---

## Why Nonlinearity Matters

Last time, we learned about perceptrons — the basic unit of work. One perceptron is simple, but 100 billion of them together create a GPT-style model. [0:13]

Now we need to talk about a limitation: perceptrons are *linear*. They produce outputs that change proportionally with inputs — a straight line when graphed. But the real world is nonlinear. [1:18]

Consider these examples:

- **Edge detection in vision:** Finding the edge of a building or a person requires determining where something *starts* and *stops*. Perceptrons alone aren't good at this. [1:52]
- **Absolute values:** There's no way to compute `|x|` using only linear math. `-3` does not equal `3` unless the weight happens to be zero. [2:08]
- **Sentiment intensity in text:** If someone says "the movie was great" vs "the movie was awful," those are opposites in sentiment. But the *intensity* of emotion is high for both. To measure intensity, you need to take the absolute value of sentiment — a nonlinear operation. [2:38]

**Activation functions introduce nonlinearity.** [0:21] They sit on top of perceptron outputs and transform them, allowing neural networks to model complex, nonlinear patterns — to find edges, to decide when things start and when they stop. [5:51]

---

## ReLU: The Original

ReLU (Rectified Linear Unit) was introduced in the landmark 2017 "Attention Is All You Need" paper that created transformers. [3:38]

The formula is simple:

```
ReLU(x) = max(0, x)
```

Choose the higher of two values: zero or x. If x is positive, pass it through. If x is negative, output zero. [4:26]

### What ReLU Does

**It compresses the signal.** Any negative signal is completely discarded — we only keep positive values. This introduces nonlinearity because there's no linear ratio between inputs of -4 and -1 (both produce 0), versus inputs of 1 and 4 (which produce 1 and 4). You can't reverse-engineer the original signal. [4:07]

**Activation functions allow models to know when things stop and start.** [5:51] Large language models must model the entirety of language — things start and stop at certain points. Temperature gets cold at a certain value. People are considered tall at a certain height. Even in language, there are edges.

### Physical ReLU Demo

In the physical perceptron circuit from the previous section, we added a ReLU component between the perceptron output and the final output. [6:57]

With weight = 1.5, input = 1, bias = 2:
- Perceptron output: 1.5 × 1 + 2 = 3.5
- ReLU output: max(0, 3.5) = 3.5 (positive, passes through)

Now bring the input down to -1:
- Perceptron output: 1.5 × (-1) + 2 = 0.5
- ReLU output: max(0, 0.5) = 0.5 (still positive)

Push the bias further negative:
- Perceptron output goes negative
- **ReLU blocks it — output becomes 0**

There's a ReLU indicator light on the physical circuit: when the perceptron output goes negative, the ReLU light turns on, and the output drops to zero. Positive values flow through; negative values are stopped. [9:06]

### The Numbers: -4 to +4

Many of the numbers we'll work with fall between -4 and +4. These represent **standard deviations in a normal distribution**. [4:44] 99.7% of values in a normal distribution live within three standard deviations of the mean. This will be covered in detail in Section 10 (Random Initialization). [5:12]

The outputs of machine learning models are called **logits**. [5:28] A single perceptron's output is a logit, and these tend to fall between -4 and +4 due to standard deviation.

---

## The Reality: Nobody Uses ReLU Anymore

I have to shatter your expectations. [9:28] In a 2025 survey of 53 open-source LLMs, **practically no one uses ReLU anymore.** [9:33]

| Era | Activation Function | Used In |
|-----|-------------------|---------|
| 2017 | ReLU | "Attention Is All You Need" |
| 2019 | GELU | GPT-2 |
| 2022+ | SwiGLU / Gated variants | Modern LLMs |

ReLU was used in the original transformer paper. It was possibly used in GPT-2 (2019). But a new family of **GELU** (Gaussian Error Linear Unit) took over soon after, and in the last three years **SwiGLU** (gated units) has become dominant in modern architectures. [10:15]

Since we're building a GPT-2 style transformer, we'll stick close to ReLU — specifically **ReLU²** (ReLU squared), which Karpathy found to work well for small models. [10:28] We'll touch on GELU more in Section 18.

A 2020 paper by Shazeer introduced SwiGLU and showed it outperformed ReLU, GELU, and Swish. [11:01] Why does it perform best? We'll have some version of an answer by the end of this section.

---

## The Activation Function Buffet

There are *many* activation functions. [11:32] Here's a sample:

ReLU, GELU, PReLU, ELU, Swish, CELU, Softplus, Mish, Sigmoid, Tanh, Hardtanh, Leaky ReLU...

The point of this overwhelming list: **there isn't a single correct activation function.** Machine learning is an empirical field — you choose the function that performs best for your specific problem. [12:17]

---

## Excel Walkthrough

Let's work through the activation functions in Google Sheets.

### ReLU in Excel

```
=MAX(0, A1)
```

Input 5 → output 5. Input -5 → output 0. Simple. [12:57]

Dragging this across a range of values shows all negatives become zero and positives pass through. Plotting it gives the classic ReLU shape: flat at zero for negatives, a 45° line for positives. [13:18]

### 2D and 3D ReLU Landscapes [14:01]

Extending to two dimensions: we create a grid where one axis is input values and the other has the same inputs multiplied by 2, then apply ReLU to the entire grid.

With **conditional formatting** (white for zero, green for positive), you can see a flat region where ReLU suppressed everything. A 3D rendering of this data shows the positive values have a distinct tilt — a landscape. [15:04]

Why does this matter? Loss functions (Section 7) are all about navigating landscapes. Activation functions shape those landscapes. This will make much more sense when we get there, but for now: **activation functions can be rendered as line charts, 2D landscapes, and 3D landscapes.** [15:26]

### ReLU² (ReLU Squared)

```
= MAX(0, x)^2
```

The formula: take max(0, x), then square it. [15:58]

ReLU and ReLU² behave differently at different magnitudes:
- Negative values → 0 (same as ReLU)
- Positive values → squared (the higher the input, the more amplified)

This **extenuates the differences** between outputs — a small positive value becomes moderately positive, a large positive value becomes very large. [16:46] This turns out to be useful, and we'll see why.

### Leaky ReLU

Leaky ReLU says: for values >= 0, use the input. For values < 0, multiply by a small factor (the "leak" alpha, typically 0.2). [17:20]

```
= IF(x >= 0, x, x * alpha)
```

The result: negative values are suppressed but not completely eliminated — there's a tiny slope on the negative side. [18:03]

Why is this useful? In large networks, ReLU can cause "dead neurons" — neurons that always output zero and never recover. Leaky ReLU keeps a small gradient flowing even for negative inputs, preventing neurons from dying entirely.

### GELU (Gaussian Error Linear Unit)

GELU is significantly more complex [18:49]:

```
GELU(x) ≈ 0.5 × x × (1 + tanh(√(2/π) × (x + 0.044715 × x³)))
```

You'll never need to memorize this formula, but you can see the implementation in the spreadsheet. [19:17]

GELU has a small bump in the region just before zero — it doesn't completely lose negative signals, only heavily suppresses them. [19:34] This smooth transition makes it easier for networks to learn compared to ReLU's hard cutoff.

### Comparing Functions [20:17]

In the spreadsheet, we can compare all the activation functions side by side on a chart:

- **ReLU:** Flat at zero, linear for positives — a hard cutoff
- **ReLU²:** Flat at zero, quadratic for positives — amplifies differences
- **Leaky ReLU:** Small negative slope, linear for positives — prevents dead neurons
- **GELU:** Smooth negative bump near zero, then linear — retains some negative signal

---

## Why Choose ReLU² for Our Model [21:54]

For our GPT-2 style model, we'll use **ReLU²**. This choice comes from Karpathy's results showing that ReLU² works well for small GPT-2 scale models. [22:16]

The higher magnitude sensitivity of ReLU² (amplifying larger positive values more than smaller ones) turns out to be beneficial attention-like properties. [22:30]

In modern large models, GELU or SwiGLU would be preferred. But for learning purposes and our small model, ReLU² is the right choice.

---

## The Lego Builder [24:07]

Before we wrap up, there's a tool called the **Lego Builder** at `go.justinangel.ai/lego`. [24:10]

You specify hyperparameters (model size, number of layers, activation function, etc.) and it generates a complete pre-training script for you. This is the same tool that generated the original training script we kicked off in Section 1.

It's useful for two reasons:
1. You can experiment with different architectural choices
2. You may not be able to write every line yourself — we live in 2026, tools exist to help

---

## Next Up: GPU Coding

Section 5 covers implementing activation functions in code. The reason it's a separate section is that there are *many* ways to write the code — from simple Python to highly optimized GPU kernels — and the performance differences are enormous. See you there.
