# Loss Functions

**Build Your Own LLM Workshop — Chapter 7 of 23**

| | |
|---|---|
| **Duration** | 25m 56s |
| **Video** | https://www.youtube.com/watch?v=bVz8i9EWEQw |

---

## Why Loss Functions?

In the previous section, we built an MLP — our second component that goes into the LLM. But how do we know if it's working? **Loss functions** measure the distance between where the model is and where it needs to be. [0:30]

Our deliverable: **cross-entropy loss**. [0:39]

A randomly initialized LLM is bad at English. Before training, given "Once upon a time in a small village," it might output "a soft drink Catalan captures 299 route Cincinnati solitaire manufacturing." After training: "an ancient man and woman lived there." [1:01]

**Loss functions quantify the distance from the goal.** Not the path — just how far away we are. [2:00] Their overall purpose is to **minimize future surprise**. [2:48]

---

## From Residual Error to RMSE

### Residual Error [2:17]

The simplest measure: `Y - Ŷ` (expected minus observed).

If you expected 7 and got 6, the residual error is 1. If your neural network output 3.1 and you expected 4, the residual is 0.9.

**Problem:** Positive and negative errors cancel out. If one prediction is +2 off and another is -2 off, the average error is 0 — even though the model is consistently wrong. [5:38]

### Mean Error

Sum all residuals and divide by N. For a dataset where most errors are negative, this gives a negative mean. But cancelling positives and negatives hides the true magnitude.

### Mean Squared Error (MSE)

Square the errors before summing: [6:09]

```
MSE = (1/N) × Σ(Y - Ŷ)²
```

Squaring solves the sign problem — all values become positive. But it also inflates the magnitude, making interpretation less intuitive.

### Root Mean Squared Error (RMSE)

Take the square root of MSE to bring the magnitude back down: [6:54]

```
RMSE = √(MSE)
```

Now we have a positive measure that reflects the typical error magnitude without being distorted by sign.

---

## Loss Landscapes [7:12]

When we plot loss values across different weights and biases, we get a **loss landscape**:

- **1D:** A single weight vs. loss — a curve with valleys at the lowest loss
- **2D:** Two weights vs. loss — a surface with a valley running through it
- **3D:** Multiple parameters — a landscape with peaks and valleys

In the Excel spreadsheet, we can create a 2D grid:
- Rows = different Y values
- Columns = different Ŷ values  
- Each cell = loss for that combination

With RMSE, the landscape shows a clear **valley** — shaped like a manta ray with its wings up. [9:21] The lowest point in the valley is where the model performs best. This is the first example of going from a single loss value to a full 3D landscape. [9:37]

---

## Why Residual Errors Don't Work for LLMs

Residual errors work when you have a single scalar target value. But **LLMs output probabilities over thousands of possible words.** [10:22]

For the prompt "The cat sat on the ___", the model might assign:
- mat: 60%
- car: 15%
- door: 10%
- floor: 8%
- ... (50,000+ other tokens)

We need a loss function that works with **multiple output probabilities**. That's **cross-entropy**. [10:47]

---

## Cross-Entropy Intuition

### First Digit Recognizer Demo [11:01]

We have a small neural network that predicts the first digit of a number. It has **10 output neurons**, each corresponding to a digit (0–9). For input 3.2, we want the "3" neuron to fire strongly and all others to be near zero.

The demo shows:
- Input 2.3 → correct prediction (highest probability on "2")
- Input 3.9 → wrong prediction (predicted "4")
- Adjusting weights and biases can improve accuracy, but there's always a trade-off

### Cross-Entropy in Excel [12:57]

For a given input (say 3.2, which should output "3"):

- **Y (expected):** 100% probability on digit 3, 0% on everything else
- **Ŷ (predicted):** the model's actual probabilities across all 10 digits

Cross-entropy formula:

```
H(Y, Ŷ) = -Σ Yᵢ × log(Ŷᵢ)
```

Since Y is 1 only for the correct class and 0 for everything else, only the correct class contributes: `-log(Ŷ_correct)`. [14:22]

If the model outputs 0.4 for the correct digit, cross-entropy is ~0.88. If we push that to 0.6, the loss drops. Higher confidence on the correct answer → lower loss. [15:02]

---

## Cross-Entropy in Code

### MSE Loss Example [15:46]

```python
import torch
import torch.nn as nn

# Perceptron
p = Perceptron(weight=0.5, bias=0.2)
y_pred = p.forward(torch.tensor(1.0))  # = 0.7
y_expected = torch.tensor(0.5)

# Manual MSE
residual = y_expected - y_pred  # = -0.2
mse = residual ** 2              # = 0.04

# PyTorch built-in MSE
mse_loss = nn.MSELoss()
loss = mse_loss(y_pred, y_expected)  # = 0.04
```

### Cross-Entropy Landscape [21:38]

For LLM-scale models, the loss landscape is astronomically complex — millions of dimensions. But the same principle applies: **navigate towards the valley**.

The code scans through all weight/bias combinations, calculates MSE for each, and renders the landscape. The manta-ray shape from Excel appears in code too.

---

## Optimizer Demo: Moving Towards the Minimum [23:43]

A quick preview of how optimizers work:

```python
optimizer = torch.optim.SGD(model.parameters(), lr=0.01)

for step in range(100):
    y_pred = model(x)
    loss = criterion(y_pred, y_expected)
    optimizer.zero_grad()
    loss.backward()       # Calculate gradients
    optimizer.step()      # Update weights
```

With **momentum**, the optimizer doesn't just follow the gradient at each point — it builds velocity, rolling past small bumps and settling in the deepest valley.

---

## Exercises

1. **Try different inputs and targets** in the loss landscape notebook — see how the landscape shape changes [18:32]
2. **Implement cross-entropy from scratch** in PyTorch
3. **Compare MSE vs cross-entropy** on the same problem — see why cross-entropy wins for classification

### Key Takeaways

| Loss Function | Best For | Formula |
|--------------|----------|---------|
| Residual Error | Single scalar targets | Y - Ŷ |
| Mean Squared Error | Avoiding sign cancellation | (1/N)Σ(Y - Ŷ)² |
| RMSE | Interpretable magnitude | √(MSE) |
| **Cross-Entropy** | **LLMs / multi-class** | **-ΣY·log(Ŷ)** |

For our GPT-2 style model, we'll use **cross-entropy loss**. All of those Excel demos and landscapes boil down to one line of code in PyTorch: [25:20]

```python
criterion = nn.CrossEntropyLoss()
```

This is exemplary of machine learning: 30 minutes of intuition-building to understand one line of code. [25:27]

Next up: **Backpropagation** — how do we actually walk down the loss landscape? How do we start from a high loss and navigate to the lowest point?
