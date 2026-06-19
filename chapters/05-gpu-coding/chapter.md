# GPU Coding

**Build Your Own LLM Workshop — Chapter 5 of 23**

| | |
|---|---|
| **Duration** | 21m 54s |
| **Video** | https://www.youtube.com/watch?v=VVk6N1_rFD0 |

---

## Why GPU Performance Matters

We just learned about activation functions (Section 4) — but we only saw them in Excel, not in code. There's a reason: writing activation functions for performance is a whole topic on its own. [0:19]

If you write GELU as plain Python code on a CPU, it will *work* — but it will be painfully slow. A modern CPU has around 4 physical cores (maybe 8 with hyperthreading). That's great for 8 parallel operations. [0:55]

But our small language model has **124 million parameters**. Running an activation function 124 million times on a CPU with only 8 cores is not practical. [1:16]

**We need GPUs.** Let's look at the levels of GPU coding, from slowest to fastest. [9:55]

---

## Level 1: CPU Code (Slow)

```python
def gelu_cpu(x):
    return 0.5 * x * (1 + tanh(sqrt(2/pi) * (x + 0.044715 * x**3)))
```

This works. But it runs on a CPU with limited cores. On a dataset of 32 million elements, CPU code takes roughly **12 seconds**. [3:23]

---

## Level 2: Custom PyTorch Module

PyTorch gives us two critical things: [1:54]
1. **Tensors** — arrays that can live on the GPU
2. **Math operations on the GPU** — run computations on thousands of cores

```python
class GELU(nn.Module):
    def forward(self, x):
        return 0.5 * x * (1 + torch.tanh(
            sqrt(2/pi) * (x + 0.044715 * x**3)))
```

We move data to the GPU with `.cuda()` and run it. An H100 GPU has **~15,000 parallel cores** — orders of magnitude more than a CPU. [3:47]

Result: ~**0.2 milliseconds** for 32 million elements, compared to 12 seconds on CPU. That's roughly **100x faster**. [3:23]

---

## Level 3: The Kernel Ping-Pong Problem

There's a catch. GELU has **9 math operations**: [4:17]

```
x³ → multiply → add x → tanh → add 1 → multiply → multiply by 0.5
```

Without optimization, each operation requires:
1. Transfer data from CPU → GPU
2. Execute on GPU
3. Send result back to CPU
4. Send to GPU for next operation

That's **9 CPU-GPU round trips**. The data transfer overhead dominates — the actual math on the GPU isn't the bottleneck anymore. [4:47]

---

## Level 4: Fused Kernels with torch.compile()

A **fused kernel** combines all operations into a single piece of code that runs sequentially on the GPU, eliminating the CPU-GPU round trips. [5:42]

The easiest way to get a fused kernel: **`torch.compile()`**. [6:17]

```python
model = GELU()
compiled_model = torch.compile(model)
```

This takes our 9 unfused kernels and fuses them into **1 kernel**. [6:25] At large tensor sizes (32K–32M elements), fused kernels are roughly **8x faster** than unfused. [11:50]

---

## Level 5: Built-in PyTorch Activations

Why write your own activation functions at all? PyTorch ships with built-in, optimized versions: [6:53]

```python
nn.ReLU(), nn.GELU(), nn.SiLU(), nn.Swish(), 
nn.LeakyReLU(), nn.Tanh(), nn.Sigmoid()
```

These are pre-compiled fused kernels. They'll run faster than your own code in most circumstances — **about 5.7x faster** than torch.compile at 32K elements. [13:35]

---

## Level 6: CUDA C++ Kernels

If you need maximal performance, you write your own **CUDA C++** kernel: [7:33]

```cpp
__global__ void gelu_kernel(float* x, float* out, int n) {
    int idx = blockIdx.x * blockDim.x + threadIdx.x;
    if (idx < n) {
        float val = x[idx];
        out[idx] = 0.5f * val * (1.0f + tanhf(
            sqrtf(2.0f/M_PI) * (val + 0.044715f * val*val*val)));
    }
}
```

CUDA is NVIDIA's GPU programming language. [7:53] This code works with blocks and threads — low-level GPU architecture concepts.

**Confession:** I don't write CUDA C++. I had Claude write this example. [8:50] And this is actually not great CUDA code — it's not optimized for tiling and other GPU architecture specifics. It's the simplest translation, not production-ready. [9:01]

---

## Level 7: Triton (Python → CUDA)

Triton lets you write Python code that gets compiled to CUDA C++: [9:24]

```python
@triton.jit
def gelu_kernel(x_ptr, out_ptr, n, BLOCK_SIZE: tl.constexpr):
    # Triton handles the GPU complexity
    # while you write Python-like code
```

You don't need to learn C++ or CUDA directly, but you still need a deep understanding of GPU architecture — blocks, tiling, memory alignment. [9:45]

---

## Performance Summary [11:23]

At large tensor sizes (32M elements), relative to torch.compile at 1x:

| Method | Speed vs torch.compile |
|--------|----------------------|
| Plain CPU code | ~100x slower (off the chart) |
| Custom PyTorch (unfused) | ~2x slower |
| torch.compile (fused) | **1x (baseline)** |
| Built-in PyTorch GELU | ~5.7x faster at 32K |
| CUDA C++ | ~6-8x faster |
| Triton | ~5-7x faster |

At massive sizes, CUDA C++, Triton, and built-in functions are all roughly comparable. CUDA C++ is slightly faster, but not by a dramatic margin. [14:10]

**Machine learning is an empirical field** — we use what works best. For this workshop, we'll use `torch.compile()` because it keeps our code readable. But if you're trying to save GPU bandwidth (and money), the optimized options are worth exploring. [14:17]

---

## Recommended Resources [15:04]

GPU programming for LLMs is a full workshop in itself. Here's where to start:

1. **"Inference Engineering" by Philip Key** — learning to work with GPUs at inference time (available as free PDF)
2. **"Ultra-Scale" by Hugging Face** — learning to work with GPUs at training time (free PDF)
3. **Chris's book** (released at NeurIPS) — practical GPU optimization techniques

Key concepts to learn: **tiling, memory coalescing, occupancy, block sizing, memory alignment**. Flash Attention and KV caching are GPU-specific optimizations not covered in today's workshop.

---

## Exercises

1. **Implement ReLU or ReLU²** — take the GELU notebook and adapt it [18:52]
2. **Benchmark each level** — compare CPU, custom PyTorch, torch.compile, and built-in across different tensor sizes
3. **Ask an AI for help** — you can download the notebook, give it to Claude, and say "generate a Colab notebook for activation function performance benchmarking" [19:09]

> **Important note on GPUs:** When running on a Colab A100, each background execution hour costs roughly $2. A 20-hour pre-training run costs ~$40. A T4 GPU is cheaper but takes longer, so your bill ends up roughly the same. [20:50]

Next up: **MLPs and Feedforward Networks**. We've only seen single perceptrons so far. Time to build layers.
