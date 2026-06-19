# Backpropagation

**Build Your Own LLM Workshop — Chapter 8 of 23**

| | |
|---|---|
| **Duration** | 56m 57s |
| **Video** | https://www.youtube.com/watch?v=Zf6RC6KZxKg |

---

## Overview

We just learned about loss functions — they measure the distance from the goal. Backpropagation is how we actually *traverse* the loss landscape to minimize that distance. [0:21]

Our deliverables: training loops, stochastic gradient descent, batch size, and learning rate. [0:30]

---

## Perceptron Update Demo

We start with a single perceptron: one input, one weight, one bias. Inputs aren't learnable — they change all the time. But the **weight and bias are learnable** — they're what training optimizes. [1:02]

**Scenario:** We want the output to be -1, but currently it's 0.7. The residual error is 1.7 (0.7 - (-1) = 1.7).

Can we use that 1.7 to update the weight and bias? Through the magic of calculus — yes. [1:55]

Clicking "update" once: the output drops from 0.7 to 0.3. Click again: it drops further. Within about 6-10 clicks, we arrive at -1. [2:42]

Backpropagation takes the accumulated loss, runs it through calculus derivatives, and determines exactly how much to change the weight and bias to reduce the loss. [2:55]

### Why Can't We Do It in One Step? [3:16]

If we set the learning rate to 1.0 and click update, the loss doesn't reduce — it *oscillates* between positive and negative. The derivative wants to make huge changes, but those overcorrect.

**Learning rate** is the discount factor. It controls how much of the derivative's recommendation we actually apply. [4:59]

- **Too high (1.0):** Oscillation, never converges [3:47]
- **Too low (0.001):** Takes forever, barely moves [5:05]
- **Just right (~0.1–0.5):** Steady descent to the target [4:14]

---

## Stochastic Gradient Descent (SGD)

Random updates won't teach a model English. We need a compass. SGD uses the loss function to optimize learnable parameters in the direction of **minimizing loss**. [6:17]

Metaphorically, it walks down a mountain in the direction that gets to the bottom fastest. [6:27]

### Derivatives and Slopes [6:44]

The derivative of x² is 2x. That "2" is the **slope**. In a loss landscape, the slope tells us:
- **Direction:** which way is downhill
- **Speed:** how steep the descent is

Derivatives determine both direction and speed. Before this, we only had direction (the loss value). Now we have the full picture. [7:43]

### Chain Rule Intuition [7:56]

You'll never need to compute this by hand for LLMs, but it's good to understand:

> **Chain rule:** How much Z changes in relation to X = (how much Z changes in relation to Y) × (how much Y changes in relation to X)

A concrete analogy: a muffin's taste relates to baking time through the browning level. Taste changes with browning, and browning changes with baking time. If we know both relationships, we can tune baking time to get the perfect muffin. [8:51]

In machine learning: we have the derivative of the loss. We have the current weight and bias values. Through the chain rule, we can determine exactly how to update the weights and biases to reduce the loss. [9:20]

The result of the chain rule derivation for residual errors simplifies to: **error × input**. Elegantly simple.

---

## Backprop in Excel [10:20]

### Simple Feedforward Network

We have a small feedforward network: two neurons, one output. The input is 1.5, the weight values are set, the bias gives us a current output of 3.1. We expect 4.0. Residual error: 0.9. [11:04]

Backpropagation walks up the tree using derivatives:
1. Compute the gradient at the output
2. Walk back through each weight and bias
3. Calculate how much each parameter contributed to the error
4. Apply the update (discounted by learning rate)

Every weight and bias has to be updated **individually**. [14:01]

### Complex Network with ReLU + Sigmoid [12:47]

With a two-neuron network, ReLU activation, and a sigmoid output:
- Current output: 0.84, expected: 0.3
- Backprop walks through each derivative: derivative of loss, derivative of sigmoid, derivative of the hidden layer weights and biases
- After one update at learning rate 0.1: output drops to 0.76

### Cross-Entropy with First Digit Recognizer [14:18]

Now with cross-entropy loss. Input is 9 (target class: 9):
- The network predicted class 8 instead of class 9
- Backprop recommends small changes to the weight and bias
- With learning rate 0.01: barely moves, still wrong
- With learning rate 0.1: the network now predicts 9 correctly! [16:24]

The key insight: you can see the direct impact of learning rate on how many update steps are needed.

---

## Autograd and Memory Costs [17:29]

In practice, you never do this calculus by hand. PyTorch's **autograd** handles it automatically: [17:45]

```python
loss.backward()  # Compute all gradients
optimizer.step() # Apply updates
```

But autograd stores:
- The entire forward pass in memory (needed for backward pass)
- Current gradients
- The optimizer state (history of all previous steps)

The optimizer state actually takes **more memory** than the model weights themselves. [18:48]

| Component | Memory Cost |
|-----------|-------------|
| Model weights (124M params) | ~500 MB |
| Gradients | ~500 MB |
| Optimizer state (Adam) | ~2 GB (momentum + variance buffers) |
| **Total** | **~3 GB per model** |

GPUs have finite memory (40/80 GB on H100/A100). Managing this efficiently is critical. [19:01]

---

## Train/Test Split Basics [19:37]

You don't test a model on the data it trained on — that would be like giving students the exam questions in advance. We split data into:

- **Training set** (80-90%): used to update weights
- **Test/Validation set** (10-20%): held out, used only for evaluation

---

## Learning Rate Schedules [21:38]

A single learning rate doesn't work for the entire training run. Instead, we use a **schedule**:

```
     learning rate
         ↑
   0.001 |   ╱〰〰〰〰〰〰〰→
         |  ╱
   0.0001| ╱
         |╱
         └────────────────────→ steps
           warmup    decay
```

1. **Warmup** (first ~1000 steps): gradually increase LR from near-zero to the target. Prevents early training instability.
2. **Cosine decay** (remaining steps): slowly decrease LR following a cosine curve. Allows fine-grained convergence.

---

## Optimizer Evolution [26:19]

| Era | Optimizer | Key Innovation |
|-----|-----------|----------------|
| Classic | SGD | Basic gradient descent |
| +Momentum | SGD+Momentum | Builds velocity, rolls past local minima |
| Adaptive | Adam | Per-parameter learning rates |
| Modern | AdamW | Fixed weight decay coupling |
| Latest | Muon | Newer alternative showing promise |

### Adam to AdamW [28:38]

**Adam** combines momentum (direction) with per-parameter adaptive learning rates (speed). It's been the dominant optimizer for years.

**AdamW** fixes a bug in Adam: weight decay (regularization) was incorrectly coupled with the adaptive learning rate. AdamW decouples them, leading to better generalization.

### Warmup in AdamW

```python
optimizer = torch.optim.AdamW(model.parameters(), lr=0.001, weight_decay=0.01)
scheduler = torch.optim.lr_scheduler.CosineAnnealingLR(optimizer, T_max=10000)
```

---

## Batch Size Basics [31:18]

- **Batch:** number of samples processed before updating weights
- **Larger batch:** more stable gradients, but more memory
- **Smaller batch:** noisier gradients (can help escape local minima), less memory

For our GPT-2 model: large batch during training, mini-batch for validation. [32:16]

---

## Training Loop Pattern [32:50]

```python
for epoch in range(num_epochs):
    for batch in train_loader:
        optimizer.zero_grad()       # Reset gradients
        y_pred = model(batch.x)     # Forward pass
        loss = criterion(y_pred, batch.y)  # Compute loss
        loss.backward()             # Backpropagation
        optimizer.step()            # Update weights
    
    # Validate
    with torch.no_grad():
        val_loss = evaluate(model, val_loader)
    
    print(f"Epoch {epoch}: train loss {loss:.4f}, val loss {val_loss:.4f}")
```

---

## A+B Mod 5 Dataset [34:59]

Let's work through a concrete example. Given two numbers A and B, predict `(A + B) % 5`.

**Data:** 10,000 rows of random A, B pairs (0–99 each)
**Encoding:** One-hot encoding → 200 input features (100 + 100)
**Architecture:** 200 → 32 → 16 → 5 output classes
**Task:** predict the remainder (0–4)

### Architecture Choices [35:50]

| Layer | Size | Purpose |
|-------|------|---------|
| Input | 200 | One-hot encoded A and B |
| Hidden 1 | 32 | Learn features |
| Hidden 2 | 16 | Higher-level features |
| Output | 5 | Class probabilities (0-4) |

### Training Loop in Code [39:29]

```python
model = MLP(input_dim=200, hidden_dims=[32, 16], output_dim=5)
criterion = nn.CrossEntropyLoss()
optimizer = torch.optim.AdamW(model.parameters(), lr=learning_rate)

for epoch in range(100):
    for x, y in train_loader:
        optimizer.zero_grad()
        outputs = model(x)
        loss = criterion(outputs, y)
        loss.backward()
        optimizer.step()
```

### Learning Rate Sweep [43:12]

Compare different learning rates:

| LR | Convergence | Notes |
|-----|-------------|-------|
| 0.1 | Fast but unstable | Oscillates |
| 0.01 | Good | Sweet spot for this model |
| 0.001 | Slow | Needs many epochs |

### Batch Size Sweep [44:46]

| Batch Size | Epochs to Converge | Memory |
|------------|-------------------|--------|
| 32 | 8 | Low |
| 64 | 5 | Medium |
| 128 | 3 | High |

Smaller batches need more steps per epoch but converge faster per step.

### What the Model Learned [48:14]

After training, the model can correctly compute `(A + B) % 5` for values it never saw during training. It learned modular arithmetic — a cyclic mathematical concept. This is analogous to how LLMs learn the cyclic structure of language.

---

## GPT-2 Training Decisions [55:01]

For our GPT-2 style model:
- **Optimizer:** AdamW [55:30]
- **Batch size:** Large during training, mini-batch during validation
- **Epochs:** 1 (one pass through the data — typical for LLMs) [55:01]
- **Learning rate schedule:** Warmup + cosine decay [56:06]
- **Model save:** Every 100 pre-training steps (checkpointing)

You don't need to implement the schedule yourself, but it's important to understand that we don't use a single learning rate — we bring it up during warmup, then slowly bring it down. [56:25]

---

## Next Up: Saving & Loading Models [56:36]

We've spent GPU time training a model. Now we need to save it to disk and load it back. Section 9 is shorter — join me there.
