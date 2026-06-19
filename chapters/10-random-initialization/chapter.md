# Random Initialization

**Build Your Own LLM Workshop — Chapter 10 of 23**

| | |
|---|---|
| **Duration** | 36m 30s |
| **Video** | https://www.youtube.com/watch?v=-pwr0RMhCg8 |

---

## The Problem: Training Collapse

We've finished building machine learning models. Now we're moving into **transformer architecture** — specifically, how to build deep neural networks whose training actually works. [0:20]

The shared problem for Sections 10–13: **training can either collapse or explode.** [0:59]

Imagine taking a bunch of randomly initialized numbers and matrix-multiplying them repeatedly. There are only two possible outcomes:

- **Vanishing gradients:** Numbers get very small, converging toward zero. All signal is lost — the transformer stops learning. [1:34]
- **Exploding gradients:** Numbers get very large, exceeding what floats can contain. Training fails catastrophically. [1:36]

Why should you care? GPU time costs money. Training collapse on a multimillion-dollar run gets people fired. [3:08]

---

## Distributions Crash Course [3:15]

We need a bit of statistics. Two key distributions:

### Uniform Distribution

`=RAND()` in Excel. Every number between 0 and 1 is equally likely. All values have the same probability of appearing. [3:48]

### Normal Distribution (Gaussian)

Follows a bell curve centered on the mean: [4:04]

- **±1 standard deviation:** 68% of values
- **±2 standard deviations:** 95% of values
- **±3 standard deviations:** 99.7% of values

This is why neural network values tend to fall between -4 and +4 — they're within a few standard deviations of the mean. [4:50]

---

## Why ReLU Creates Zeros [5:05]

ReLU zeroes out all negative values: [5:23]

```
normal distribution:  [-4, -3, -2, -1, 0, 1, 2, 3, 4]
after ReLU:           [ 0,  0,  0,  0, 0, 1, 2, 3, 4]
```

About half the values become zero. Since neural networks are just matrix multiplications (repeated multiplication and addition), multiplying by zero propagates zeros. Add zeros, nothing changes.

**ReLU is dangerous inside a system that's only doing matrix multiplication.** [5:50] It increases the likelihood of vanishing gradients.

---

## He Initialization (for ReLU) [6:07]

In 2015, Kaiming He proposed a standard deviation that compensates for ReLU's zeroing: [6:10]

```
He stddev = √(2 / fan_in)
```

Where `fan_in` is the number of input dimensions. For a layer with 5 inputs:

```
stddev = √(2 / 5) = √(0.4) ≈ 0.632
```

Instead of using standard deviation 1.0 (which causes collapse or explosion), we use this tailored value. The mathematical proof is in the paper, but the intuition is: by starting with a slightly wider distribution, we compensate for the fact that ReLU will cut half the values to zero. [6:25]

---

## Xavier Initialization (for Tanh/Sigmoid) [7:26]

Different activation functions need different initialization. Tanh and sigmoid **compress values toward their edges**: [6:55]

```
Tanh compresses:  [ -inf ,  0  , +inf  ]
                  → [-1,  0,  +1]
```

In 2010, Xavier Glorot proposed: [7:26]

```
Xavier stddev = √(2 / (fan_in + fan_out))
```

For a 5×5 layer:

```
stddev = √(2 / (5 + 5)) = √(0.2) ≈ 0.447
```

---

## Excel Demonstration

### Setup: RAND and NORM [8:09]

```excel
=RAND()                          # Uniform: 0 to 1
=NORMINV(RAND(), mean, stddev)   # Normal distribution
```

With 10,000 random values, the law of large numbers makes the distribution visible:
- **Uniform:** Even count across all buckets [10:18]
- **Normal (stddev=1):** Bell curve centered at 0, 68% between -1 and +1 [11:14]
- **Normal (stddev=0.4):** Most values between -1 and +1 [11:22]

### Uniform Distribution Explosion [11:55]

Matrix-multiply two 5×5 uniform random matrices, apply ReLU, repeat 10 times:

| Round | Average Value | 
|-------|---------------|
| 1 | 0.6 |
| 2 | 1.2 |
| 3 | 3.4 |
| 4 | 9.2 |
| 5 | 22.8 |
| 6 | 51.8 |
| 7 | 119.5 |
| 8 | 239.0 |

**Gradient explosion.** By round 8, values are 239× larger than the start. GPT-2 small has 72 consecutive matrix multiplications — these numbers would overflow any float. [13:50]

### Normal Distribution Still Fails [14:25]

Using normal distribution (stddev=1):

| stddev | Result |
|--------|--------|
| 1.0 | Variance oscillates wildly [14:12] |
| 0.4 | Gradient collapses to zero [15:00] |
| 2.0 | Gradient explodes [15:37] |
| 0.2 | Total collapse [15:54] |

Neither uniform nor naive normal distribution prevents training collapse.

### He Initialization in Sheets [16:45]

```
He stddev = √(2 / 5) ≈ 0.632
```

With this value:
- 10 rounds of matrix multiply + ReLU
- First try: collapsed (5×5 is too small for the law of large numbers)
- Second try: **stable** — variance holds steady [17:28]

He initialization doesn't guarantee stability on tiny matrices, but with larger dimensions (e.g., 100×100), it's dramatically more reliable.

### Xavier for Tanh/Sigmoid [18:10]

```
Xavier stddev = √(2 / (5 + 5)) = √(0.2) ≈ 0.447
```

With Tanh as the activation function:
- Standard deviation 0.447 keeps the values stable
- The compressed edges of Tanh/Sigmoid require a different correction factor than ReLU [18:33]

---

## One-Hot Encoding Setup [19:39]

For the exercise, we use one-hot encoding:

```python
def one_hot_encode(x, num_classes=100):
    vec = torch.zeros(num_classes)
    vec[x] = 1.0
    return vec
```

A+B mod 5 dataset: each input is one-hot encoded (two 100-element vectors = 200 inputs).

---

## Colab Data Pipeline [22:06]

```python
# Generate 10,000 random pairs
dataset = []
for _ in range(10000):
    a = random.randint(0, 99)
    b = random.randint(0, 99)
    x = torch.cat([one_hot_encode(a), one_hot_encode(b)])
    y = (a + b) % 5
    dataset.append((x, y))

train_loader = DataLoader(dataset[:8000], batch_size=64, shuffle=True)
val_loader = DataLoader(dataset[8000:], batch_size=64)
```

---

## Deep DNN Architecture [23:40]

| Layer | Size | Purpose |
|-------|------|---------|
| Input | 200 | One-hot A and B |
| Hidden 1 | 128 | Initial features |
| Hidden 2 | 64 | Compressed features |
| Hidden 3 | 32 | Higher-level patterns |
| Output | 5 | Class logits |

Training loop: standard forward → loss → backward → step pattern.

### Uniform vs He Initialization [28:31]

```python
# Uniform initialization (bad)
def init_weights_uniform(m):
    if isinstance(m, nn.Linear):
        nn.init.uniform_(m.weight, a=0, b=1)

# He initialization (good for ReLU)
def init_weights_he(m):
    if isinstance(m, nn.Linear):
        nn.init.kaiming_uniform_(m.weight, mode='fan_in', nonlinearity='relu')
```

With uniform init, training loss starts high and barely decreases. With He init, loss drops steadily to near-zero within a few epochs. [30:43]

### Xavier for Tanh

```python
# Xavier initialization (good for Tanh/Sigmoid)
def init_weights_xavier(m):
    if isinstance(m, nn.Linear):
        nn.init.xavier_uniform_(m.weight)
```

---

## Why Training Collapses Without Proper Init [31:25]

Without proper initialization, the gradients either:
- **Vanish:** Output → 0, no learning occurs, loss stays flat
- **Explode:** Output → NaN, training crashes

He and Xavier initialization give the model a fighting chance by keeping gradients in a stable range through deep networks.

---

## Exercises

1. Compare uniform vs He init on the deep DNN — see the loss curves diverge [32:04]
2. Try Xavier init with Tanh activations
3. Experiment with different standard deviations in the Excel sheet
4. Observe what happens with 10 layers vs 50 layers — deeper networks need better init

---

## Key Formulas Reference

| Activation | Init | Formula |
|------------|------|---------|
| ReLU / ReLU² | He | stddev = √(2 / fan_in) |
| Tanh / Sigmoid | Xavier | stddev = √(2 / (fan_in + fan_out)) |

---

## Next Up: Residuals [36:11]

Initialization alone won't fix training collapse if we keep adding more layers. Residual connections, coming in Section 11, address the deeper problem.
