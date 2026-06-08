---
title: "Inference Optimization"
aliases:
  - "TTFT"
  - "TPOT"
  - "KV cache"
  - "model serving"
  - "latency optimization"
tags:
  - wiki
  - "context-reliability"
domain: "context-reliability"
sources:
  - "AI Engineer Chapter 9 (Chip Huyen, 2025).md"
status: stable
confidence: high
---

Created: Monday, 8 June 2026, 22:00
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# Inference Optimization

**Summary**: Inference optimization reduces the cost and latency of running a model in production. Techniques split into model-level (change the model) and service-level (change how it's served). The four highest-impact techniques across most workloads are quantization, tensor parallelism, replica parallelism, and attention optimization.

**Sources**: [[raw/AI Engineer Chapter 9 (Chip Huyen, 2025).md|AI Engineering Chapter 9]]

---

## Why It Matters

A model's usability depends heavily on inference cost and latency:
- **Cheaper inference** → more affordable AI-powered decisions
- **Faster inference** → enables AI in more latency-sensitive applications

For API consumers (most application developers), the cloud provider handles these optimizations. But understanding what's possible helps you evaluate and choose between model APIs intelligently.

## Key Metrics

### Latency

Inference latency for language models breaks into two phases:

| Metric | Full Name | What Drives It |
|--------|-----------|----------------|
| **TTFT** | Time to First Token | Prefilling phase — processing the input prompt |
| **TPOT** | Time per Output Token | Decoding phase — generating each output token |

**TTFT** matters most for interactive applications — how quickly the user sees the first word.
**TPOT** matters most for long-form generation — how quickly the full response arrives.

### Throughput

Throughput measures how many tokens/requests the system handles per unit time. It is directly tied to cost — higher throughput = lower cost per token.

### The Latency/Throughput Tradeoff

```txt
Low latency ←————————————————→ High throughput
(allocate more resources per request)   (batch more requests per machine)
```

- You can reduce cost by tolerating higher latency (batch more requests together)
- You can reduce latency by throwing more resources at each request (higher cost)
- This tradeoff governs most serving infrastructure decisions

## The Two Inference Phases

### Prefilling

Processes the entire input prompt in parallel. Influences TTFT. Computationally intensive but parallelizable — longer prompts increase TTFT.

### Decoding

Generates output tokens one at a time (autoregressive). Influences TPOT. Inherently sequential — each token depends on the previous one. This is the main bottleneck for long outputs.

Many optimization techniques exist specifically to address the autoregressive decoding bottleneck.

## Model-Level Techniques

These change the model itself — may affect model behavior.

### Quantization

Reduces the numerical precision of model weights:

| Precision | Bits | Memory Usage | Accuracy Impact |
|-----------|------|--------------|-----------------|
| FP32 | 32-bit | Baseline | None |
| FP16 / BF16 | 16-bit | ~50% reduction | Minimal |
| INT8 | 8-bit | ~75% reduction | Small |
| INT4 | 4-bit | ~87% reduction | Moderate |

**Inference quantization** (reducing precision at serving time) is distinct from [[finetuning#Quantized Training|quantized training]] (reducing precision during model training), though they use similar underlying techniques.

Quantization is **model-agnostic** — works across architectures.

### Distillation

Trains a smaller "student" model to mimic a larger "teacher" model. The student inherits the teacher's behavior at a fraction of the inference cost. Unlike quantization, distillation produces a genuinely smaller model with fewer parameters.

### KV Cache Management

The **KV (key-value) cache** stores intermediate attention computations so they don't need to be recomputed on every decoding step.

- Critical for long-context workloads — saves recomputing attention over the full history on every token
- KV cache grows with context length — memory management becomes a bottleneck at scale
- Less important for short-context, stateless workloads

### Attention Kernel Optimization

Custom GPU kernels (e.g., FlashAttention) rewrite the attention computation to be more memory-efficient. Can significantly accelerate transformer models — attention is the main computational bottleneck.

## Service-Level Techniques

These change how the model is served — model weights stay intact.

### Batching

Groups multiple requests together and processes them in one forward pass:
- **Static batching**: Fixed batch size, simple to implement
- **Dynamic batching**: Accumulates requests until batch is full or a timeout fires
- **Continuous batching**: Interleaves requests at the token level — the most efficient for LLMs

### Tensor Parallelism

Splits model weights across multiple GPUs within a single machine. Reduces latency (more compute per request) and enables serving models too large for a single GPU.

### Replica Parallelism

Runs multiple full copies (replicas) of the model in parallel. Each replica handles different requests independently.
- Relatively straightforward to implement
- Increases throughput linearly with replicas
- Each replica gets more resources per request → lower latency per request

### Prefilling/Decoding Decoupling

Separates the prefilling and decoding phases onto different machines optimized for each. Since prefilling is compute-bound and decoding is memory-bound, specialized hardware per phase improves overall efficiency.

### Prompt Caching

Caches the KV state of a repeated prompt prefix so it doesn't need to be reprocessed on each request. Especially valuable for:
- Long system prompts reused across many requests
- Multi-turn conversations (each turn re-sends the full history)
- RAG workloads where the same retrieved documents appear repeatedly

Anthropic exposes this as `cache_control` in the API — see [[context-reliability]] for implementation details.

## The Four Most Impactful Techniques

Chip Huyen explicitly identifies these as highest-impact across most workloads:

| Technique | Why It's High-Impact |
|-----------|---------------------|
| **Quantization** | Works across all model architectures; large memory savings |
| **Tensor parallelism** | Reduces latency AND enables larger models |
| **Replica parallelism** | Simple to implement; linear throughput scaling |
| **Attention optimization** | Addresses the core transformer bottleneck |

## Choosing Techniques by Workload

| Workload | Key Technique |
|----------|--------------|
| Long context | KV cache management |
| Long overlapping prompts / multi-turn | Prompt caching |
| Low latency priority | Replica parallelism (more replicas, fewer requests per machine) |
| Cost reduction priority | Quantization + dynamic batching |
| Very large models | Tensor parallelism |

## Related Pages

- [[context-reliability]] — prompt caching (`cache_control`) from the API perspective
- [[finetuning]] — quantized training vs inference quantization; distillation produces finetuned smaller models
- [[build-vs-buy-ai]] — inference cost is a key axis in API vs self-host decisions
- [[transformer-limitations]] — attention mechanism is the bottleneck that optimization targets
- [[rag-retrieval]] — RAG workloads especially benefit from prompt caching of repeated retrieved docs
