# Saving & Loading Models

**Build Your Own LLM Workshop — Chapter 9 of 23**

| | |
|---|---|
| **Duration** | 11m 40s |
| **Video** | https://www.youtube.com/watch?v=riCiHjVEqXc |

---

## Why Saving Matters

We just trained a model on A+B mod 5 — about 5 million parameters. Training took minutes to an hour. We need to save it to disk so we don't lose that work. [0:22]

---

## PTH (PyTorch Default)

The simplest way to save is `torch.save`:

```python
# Saving
torch.save(model.state_dict(), "model.pth")

# Loading
model = MLP()
model.load_state_dict(torch.load("model.pth"))
```

`model.state_dict()` contains just the learnable parameters (weights and biases). If you're still training, you should also save the optimizer state (momentum buffers, etc.) to resume training later: [0:47]

```python
checkpoint = {
    'model_state_dict': model.state_dict(),
    'optimizer_state_dict': optimizer.state_dict(),
    'epoch': epoch,
    'loss': loss,
}
torch.save(checkpoint, "checkpoint.pth")
```

### PTH Security Warning [1:44]

PTH files are **insecure** for web downloads. The entire file is loaded through a custom instruction set that can easily take over your machine. [1:57]

**Rule of thumb:** Only use PTH if you saved the file yourself and are loading it yourself. Never download a PTH from the internet and run it. [2:05]

---

## SafeTensors (The Modern Standard) [2:50]

SafeTensors is the format that has taken over Hugging Face. [2:17]

**Advantages over PTH:**
- Secure (uses JSON serialization)
- Supports lazy loading (load only what you need)
- Supports quantization (reduced precision models)
- Most widely used format on Hugging Face today

---

## Other Export Formats

| Format | Best For | Compatibility |
|--------|----------|---------------|
| **PTH** | Local PyTorch training | PyTorch only |
| **SafeTensors** | Sharing models | Multi-framework, secure |
| **ONNX** | Cross-platform inference | PyTorch + TensorFlow [2:52] |
| **GGML** | Production inference | Heavily optimized for inference [3:27] |
| **Core ML** | iOS | Apple's native format [4:04] |
| **Android format** | Android | Platform-native |

For our workshop, we'll use **PTH** for local training checkpoints. [4:17]

---

## Publishing Models

Hugging Face is where the community stores datasets and models. Our workshop model is at `justinangel/workshop-v1-pretraining.pth`. [4:27]

---

## Saving Code Walkthrough [4:46]

The full save pipeline:

```python
MODEL_PATH = "workshop-v1-pretraining.pth"

# Train
model = MLP(input_dim=200, hidden_dim=16, output_dim=5)
train_model(model, train_loader, val_loader, epochs=10)

# Save
torch.save(model.state_dict(), MODEL_PATH)
```

### Persistent Storage Options [7:20]

| Storage | Persistent? | When to Use |
|---------|-------------|-------------|
| Colab local | ❌ Lost after session | Temporary only |
| Google Drive | ✅ | Colab + persistent |
| Modal volume | ✅ | Modal platform |
| Local filesystem | ✅ | Your machine |

The code tries each option in sequence: Google Drive first, then modal volume, then fallback. [7:28]

### Loading from the Internet [8:07]

We can load our GPT-2 model directly from Hugging Face:

```python
model = GPT2Model.from_pretrained("justinangel/workshop-v1-pretraining")
output = model.generate("The meaning of life is", max_length=100, temperature=0.8)
```

Expected output: "The meaning of life is to live as a human being. The goal of life is to achieve the highest level of happiness." [9:28]

---

## Checkpointing Strategy [9:56]

- **File format:** PTH
- **Location:** `/workshop` folder on Google Drive (or `/mnt/workshop` on Modal)
- **Naming:** `workshop-v1-{stage}.pth` (pre-training, instruct-tuning, RL)
- **Frequency:** Save latest PTH every **100 pre-training steps** [10:33]
- **Retention:** Only keep the latest — a full model file is ~1.4 GB. Keeping them all gets expensive fast. [10:45]

---

## Next Up: Transformer Architecture

We're now officially done with basic machine learning. The next sections (10–13) cover keeping deep neural network training stable — gradients vanish, gradients explode, and how to prevent both. [11:05]
