# Multi-Layer Perceptrons & Feedforward Networks

**Build Your Own LLM Workshop — Chapter 6 of 23**

| | |
|---|---|
| **Duration** | 40m 14s |
| **Video** | https://www.youtube.com/watch?v=6BU9Gj2yoSw |

---

## From One Perceptron to Many

We've been working with a single perceptron: `wx + b`. But a real neural network has *layers* of perceptrons, each with multiple inputs and multiple outputs. Our deliverable for this section: a **feedforward network with ReLU²** working as it would in a transformer. [0:25]

This is our first real component that we'll carry into the full model. [0:32]

---

## Multiple Inputs, One Perceptron

If a perceptron has multiple inputs, each input gets its own weight, and there's one global bias: [0:53]

```
f(x₁, x₂) = w₁·x₁ + w₂·x₂ + b
```

In code:

```python
weighted_sum = 0
for i in range(len(inputs)):
    weighted_sum += weights[i] * inputs[i]
output = weighted_sum + bias
```

If weights are [3, 0.1], inputs are [1, 100], and bias is some value, then the weighted sum is `3×1 + 0.1×100 + bias`. [1:42]

### Interactive Demo

In the interactive demo, we see this in action: [2:01]

- **Two inputs**, each with its own weight
- Input 1 has weight 1.5, Input 2 has weight -0.8
- One global bias

Each input can be up-regulated or down-regulated independently. A high bias means a higher overall output; a more negative bias suppresses the output. [3:33]

---

## Two Perceptrons, Two Inputs — The Weight Explosion

When we have **two neurons** and **two inputs**, we get a Cartesian product of weights: [4:00]

| | Neuron A Weight | Neuron B Weight |
|---|---|---|
| **Input 1** | w₁ₐ | w₁ᵦ |
| **Input 2** | w₂ₐ | w₂ᵦ |

**4 weights total.** Each neuron also has its own bias.

The more inputs and the more neurons, the more weights we have to learn. [4:44] Each perceptron has its own relationship to each input in the previous layer. Changing the weight for Input→Neuron B doesn't affect Neuron A at all.

---

## Adding an Output Layer

Two neurons produce two outputs. But a system might need only one output. The solution: **another neuron at the end** that combines them. [5:32]

This gives us:

```
Input Layer → Hidden Layer (2 neurons) → Output Layer (1 neuron)
```

We've moved from a single-layer network to a **multi-layer network**. [5:46] A neuron that's producing a very negative value gets blocked by ReLU and doesn't contribute to the output. Other neurons "wake up" and contribute. This ability to selectively activate or suppress neurons is critical.

### Terminology [9:22]

- **Input layer** — the first layer
- **Output layer** — the last layer
- **Hidden layer** — any layer in between
- **Fully connected / FFN** — every neuron connects to every neuron in the next layer
- **MLP** and **FFN** are used synonymously in the context of LLMs [10:00]

---

## XOR: Why Multiple Layers Are Necessary

The **XOR gate** (exclusive or) is a logic gate that outputs true only when exactly one input is true: [6:54]

| Input A | Input B | Output |
|---------|---------|--------|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

There is **no way to implement XOR with a single perceptron** or even a single layer of perceptrons. The inputs need to be daisy-chained through multiple layers. [7:25]

In the interactive demo, you can see how:
- When only Neuron A is active, it contributes positive value → output is true
- When only Neuron B is active, Neuron A still contributes → output is still true
- When **both** are active, the second neuron's strong negative weight cancels everything out → output is false

This interaction — turning neurons on and off — is how MLPs learn complex, nonlinear patterns like "either but not both."

---

## Matrix Multiplication in Excel

Now let's move from manual calculations to **matrix multiplication** (matmul / MMULT). [10:10]

### Single Neuron with Matmul

Instead of `w₁×x₁ + w₂×x₂ + b`, we can use:

```
=MMULT(weights_array, inputs_array) + bias
```

Matmul is just a function that does all the multiplications and additions for us. [12:20]

### Multi-Neuron with Matmul

With 2 inputs and 2 hidden neurons:

```
Inputs: [x₁, x₂]
Weights: [[w₁ₐ, w₁ᵦ], [w₂ₐ, w₂ᵦ]]
Biases: [bₐ, bᵦ]

Hidden = MMULT(inputs, weights) + biases
Hidden_activated = ReLU(Hidden)
Output = MMULT(Hidden_activated, output_weights) + output_bias
```

**Array formulas** allow us to compute multiple neurons in a single matmul call — much cleaner than computing each neuron manually. [13:58]

### The Transpose Trick [15:49]

Matrix dimensions must match: for `MMULT(A, B)`, the second dimension of A must equal the first dimension of B.

To keep things readable, we often use **TRANSPOSE** to flip a column into a row (or vice versa):

```
=MMULT(inputs, TRANSPOSE(weights)) + biases
```

### Folding Bias into Weights [15:49]

Instead of adding bias separately, we can **add a column of 1s to the input** and fold the bias into the weight matrix:

```
Inputs with bias column: [x₁, x₂, 1]
Weights with bias: [[w₁ₐ, w₁ᵦ], [w₂ₐ, w₂ᵦ], [bₐ, bᵦ]]
```

This keeps the operation as a single matmul. The `1` in the input means the bias passes through without modification.

### XOR with Matmul [17:06]

We can implement the XOR truth table entirely with matrix operations:

```
Inputs: all 4 combinations [0,0], [0,1], [1,0], [1,1]
Hidden weights: 2×4 matrix (16 values total)
Output weights: [2, -6]
Bias: 0
```

Running this through matmul + ReLU + another matmul yields exactly `[0, 1, 1, 0]` — the correct XOR truth table. [18:41]

---

## Growing and Shrinking Arrays [20:37]

A key property of MLPs: **they can expand and contract dimensions**.

```
Input (4 values) × Weights (4×16 matrix) → Hidden (16 neurons)
Hidden (16 neurons) × Weights (16×1 matrix) → Output (1 value)
```

The network "grows" from 4 inputs to 16 hidden neurons (learning multiple representations), then "shrinks" back to 1 output. This is exactly how a GPT-2 FFN works:

```
768 → 3072 (expand 4x) → ReLU² → 768 (shrink back)
```

The expansion gives the network a "scratchpad" to work with — higher-dimensional representations where it can separate and combine concepts before projecting back down. [20:37]

### Matmul Dimension Rules [22:15]

```
If matrix A is (M × N) and matrix B is (N × P),
then MMULT(A, B) produces a (M × P) matrix.
```

The inner dimensions (N) must match. The outer dimensions (M, P) determine the output shape. This rule governs everything in MLP design.

---

## PyTorch Implementation [26:47]

In PyTorch, an MLP is straightforward:

```python
class MLP(nn.Module):
    def __init__(self, input_dim, hidden_dim, output_dim):
        super().__init__()
        self.fc1 = nn.Linear(input_dim, hidden_dim)
        self.relu = nn.ReLU()
        self.fc2 = nn.Linear(hidden_dim, output_dim)
    
    def forward(self, x):
        x = self.fc1(x)
        x = self.relu(x)
        x = self.fc2(x)
        return x
```

### XOR in PyTorch

```python
import torch
import torch.nn as nn

model = MLP(input_dim=2, hidden_dim=4, output_dim=1)
criterion = nn.MSELoss()
optimizer = torch.optim.SGD(model.parameters(), lr=0.1)

X = torch.tensor([[0,0],[0,1],[1,0],[1,1]], dtype=torch.float32)
y = torch.tensor([[0],[1],[1],[0]], dtype=torch.float32)

for epoch in range(10000):
    y_pred = model(X)
    loss = criterion(y_pred, y)
    optimizer.zero_grad()
    loss.backward()
    optimizer.step()
```

### Exercise: Build a GPT-2 Style FFN [32:54]

Build a feedforward network with:
- Input: 768 dimensions
- Hidden: 3072 dimensions (4x expansion)
- Activation: ReLU²
- Output: 768 dimensions (back to original size)
- **Typically no biases** in the FFN layers of GPT-2

```python
class GPT2FFN(nn.Module):
    def __init__(self, d_model=768, d_ff=3072):
        super().__init__()
        self.fc1 = nn.Linear(d_model, d_ff, bias=False)
        self.fc2 = nn.Linear(d_ff, d_model, bias=False)
    
    def forward(self, x):
        return self.fc2(torch.relu(self.fc1(x)) ** 2)
```

---

## Recommended Resource

If you want to learn linear algebra deeply, **"Linear Algebra for Dummies"** by Stephen wrote a full linear algebra code example. Available at the workshop links. [39:39]

---

## Next Up: Loss Functions

Why do we need loss functions? We're trying to learn good weights and biases that will help the model learn English. Loss functions measure *how far off* we are. See you in Section 7. [39:54]
