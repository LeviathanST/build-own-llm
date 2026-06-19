# Perceptrons: wx + b

**Build Your Own LLM Workshop — Chapter 3 of 23**

| | |
|---|---|
| **Duration** | 15m 51s |
| **Video** | https://www.youtube.com/watch?v=uaA8ChGcMwE |

---

## Workshop Roadmap

We've just finished reverse engineering a GPT-2 style model, which gave us our roadmap for the day: we're going to rebuild it component by component. But before we can build anything, we need to start with the most basic unit of all neural networks — the **perceptron**.

Our deliverable for this section is simple: a working perceptron.

If you want to follow along with the code and exercises, you can find them at:
- **Code:** [go.justinangel.ai/code-3](https://go.justinangel.ai/code-3)
- **Excel:** [go.justinangel.ai/excel-3](https://go.justinangel.ai/excel-3)

---

## What Is a Perceptron?

Before we dive into the math, let's think about what problem a perceptron is trying to solve. As we learn the English language, we constantly make decisions about which word is the right word to say. We store information, and based on that stored information, we make decisions. [0:47]

This is exactly the question that Frank Rosenblatt posed in 1958 when he first conceived of the perceptron [1:02]:

- How is information about the physical world sensed and detected by a biological system?
- In what form is information stored or remembered?
- How does stored information influence recognition and behavior?

A perceptron — or a neuron — is the basic unit that answers these questions. It's the smallest unit of a neural network. While saying "GPT is really just 100 billion perceptrons" is a gross oversimplification, it's also about 51% correct. Every complex neural network is built from these fundamental building blocks.

---

## The Perceptron Formula: f(x) = wx + b

Here's the core formula [2:03]:

> **f(x) = wx + b**

Or, in words: given an input *x*, we multiply it by a *weight* *w*, and add a *bias* *b*.

In code, it looks like this:

```python
def perceptron_math(weight, input, bias):
    return weight * input + bias
```

If we call `perceptron_math(1, 2, 3)`, we get 5. Simple enough.

### What Does a Perceptron Actually Do?

A perceptron holds behavioral information and performs linear math. "Linear" here means the output changes proportionally with the input — if you graph it, you get a straight line. (We'll contrast this with nonlinear math when we get to activation functions.)

One of the most useful properties of a perceptron is that it can detect **edges** — decision boundaries. A simple example: positive outputs can mean one thing, negative outputs another, and zero is the boundary between them.

---

## A Physical Perceptron Demo

Before we get lost in numbers, let's make this tangible. There's a wonderful physical analog perceptron built by Welsh Lab that I want to show you. The key insight: **all those weight and bias numbers are just knobs you get to turn.**

I built my own physical perceptron circuit to demonstrate this. Here's how it works:

- We set values for weight, bias, and input using physical controls.
- The formula `wx + b` runs through the circuit.
- The output is displayed — and it can be positive, negative, or zero.

For example:
- Weight = 2, Input = 1, Bias = 1 → Output = 3
- Weight = 2, Input = 2, Bias = 1 → Output = 5
- Weight = 2, Input = -1, Bias = 1 → Output = -1

You can adjust any of the three knobs — input, weight, or bias — and see the output change in real time. Bring the bias down to a negative value to suppress the signal. Adjust the weight to amplify or dampen the input's effect.

There's a linear relationship between weight, input, and bias. That linearity is both a feature (it's simple and predictable) and a limitation (we'll address the limitation in the next section on activation functions).

---

## Interactive Web Demo

You don't have a physical circuit to play with, so I built an interactive demo at **[go.justinangel.ai/neuralnet](https://go.justinangel.ai/neuralnet)**. We'll use this demo throughout the next several sections.

The demo shows the same thing as the physical circuit: an input, a bias, and a weight. With the default values (input = 1, weight = 1.5, bias = 2):

> 1.5 × 1 + 2 = 3.5

Wait, let me recalculate. The math shown in the demo gives:

> 1.5 × 1 + 2 = 1.7... 

Hmm, that doesn't look right. Let me check again. Actually, with weight = 1.5, input = 1, bias = 2:

> 1.5 × 1 + 2 = 3.5

But if I bring the input down to a negative value, the output also goes negative. Input of -1:

> 1.5 × (-1) + 2 = 0.5

And lower:

> 1.5 × (-1.5) + 2 = -0.25

You can play with the bias — bring it up or down — and adjust the weight, and watch the output swing between positive and negative values.

Why is this ability to find edges (the boundary between positive and negative) so important? Because we can use **zero as a decision boundary**. Positive output means one thing, negative output means another. Zero is the edge. That's not just a math trick — that's the beginning of how neural networks make decisions.

---

## Excel Perceptron Playground

Now let's open up the Excel sheet and work through the exercises.

### Single Perceptron

With weight = 1, input = 2, bias = 3:

> W × X + B = 1 × 2 + 3 = **5**

Increase the weight to 2, and the answer becomes 7. Push the weight to 100, and you get 203. Take it negative, and you might get 1. Push it even more negative, and if the bias is still positive, it gives you a floor. Experiment with the numbers — it builds intuition faster than reading about it.

### Multiple Inputs Through One Perceptron

Now let's run a sequence of inputs through the same perceptron (keeping weight and bias fixed):

| Input | Weight | Bias | Output |
|-------|--------|------|--------|
| 1 | 1 | 3 | 4 |
| 2 | 1 | 3 | 5 |
| 3 | 1 | 3 | 6 |
| 4 | 1 | 3 | 7 |
| 5 | 1 | 3 | 8 |

There's a clear linear relationship here. If you plot it, you get a straight line. The line intersects the Y-axis at the bias value (3), and its slope is determined by the weight (1).

### What Does the Bias Actually Do?

Set the bias to 0. The line now intersects at zero. Set it to 1, and it intersects at 1. The bias is simply the *offset* — it shifts the entire line up or down.

### What About the Weight?

Make the weight negative. The line flips direction — instead of rising as input increases, it falls. Make the weight very close to zero (but not zero), and the line becomes almost horizontal. The input barely affects the output. This is a linear system with very low sensitivity.

### Visualizing the Landscape

Here's where it gets interesting. Fix the weight at 1, but vary both the bias and the input. Create a 2D grid where:

- Rows represent different input values
- Columns represent different bias values
- Each cell computes wx + b

If you apply a color scale to this grid (say, green for positive, red for negative), you'll see something remarkable: **a clear decision boundary at zero**. There's a valley in the middle of the table — the zero line — separating positive and negative values.

This is how perceptrons influence behavior: positive values drive behavior in one direction, negative values in another. The decision boundary at zero is the edge we talked about earlier. We'll explore this much more when we get to activation functions in the next section.

---

## Coding a Perceptron

Let's implement what we've learned in Python.

### Option 1: A Simple Function

```python
def perceptron_math(weight, input, bias):
    return weight * input + bias
```

**Exercise:** Complete the `activate` method [12:48]. It's literally `weight * input + bias`. If you get stuck, the answer is in the notebook under "Show Code."

### Option 2: A Class

Since a perceptron holds fixed weight and bias values while processing multiple inputs, a class is more natural [12:35]:

```python
class Perceptron:
    def __init__(self, weight, bias):
        self.weight = weight
        self.bias = bias

    def activate(self, input):
        return self.weight * input + self.bias
```

**Exercise:** Complete the `activate` method above. It's literally `weight * input + bias`. If you get stuck, the answer is in the notebook under "Show Code."

### Running the Perceptron

Once you've implemented the class, run it with a sequence of inputs:

```python
p = Perceptron(weight=1, bias=3)
for x in range(-5, 6):
    result = p.activate(x)
    print(f"Input: {x}, Output: {result}")
```

Expected output:

| Input | Output |
|-------|--------|
| -5 | -2 |
| -4 | -1 |
| -3 | 0 |
| -2 | 1 |
| -1 | 2 |
| 0 | 3 |
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |
| 4 | 7 |
| 5 | 8 |

You can see the linear relationship: the output increases by exactly the weight (1) for each unit increase in input, and the line crosses the Y-axis at the bias value (3).

**Further exercises:**
- Change the weight and see how the slope changes
- Make the weight negative and observe the descending line
- Play with the bias to shift the line up and down
- Generate a chart — it will look exactly like the line chart from the Excel section

This might seem simple, but these charts build something called a **loss landscape**, and we'll see landscapes again in section 7 when we talk about loss functions.

---

## Wrap Up and Next Steps

Here's what we covered in this section:

- **The perceptron formula:** f(x) = wx + b — weight times input plus bias.
- **What a perceptron does:** It holds information and influences behavior through a simple linear calculation.
- **Physical metaphor:** A circuit where weight, bias, and input are knobs you turn.
- **Decision boundaries:** The zero crossing acts as an edge or classifier between positive and negative outputs.
- **Excel visualization:** We saw linear relationships, line charts, and 2D color-coded landscapes.
- **Python implementation:** A Perceptron class with an activate method.

You might be wondering: surely there's a framework that implements perceptrons for you? Yes — we'll get to PyTorch soon. But not just yet.

Why do we need activation functions on perceptrons? Because perceptrons alone aren't great at finding edges. We kind of faked it by declaring zero as the edge, but the result is very linear and not flexible enough for real-world problems. Activation functions — coming in the next section — solve that problem.

See you in section 4.
