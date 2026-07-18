# Training vs Inference

**Difficulty:** 🟢 Beginner  
**Estimated Reading Time:** 12 minutes  
**Prerequisites:** Tokenizers  
**Last Updated:** July 2026

---

> "Training is when an LLM learns. Inference is when an LLM uses what it has already learned."

---
# Learning Objectives

By the end of this chapter, you will understand:

- What training is
- What inference is
- How GPT is trained
- Why ChatGPT does not learn from your questions
- The difference between forward pass and backward pass
- Why training is expensive while inference is comparatively fast

---

# Why Should I Care?

One of the biggest misconceptions about ChatGPT is:

> "Every time I ask a question, ChatGPT learns from me."

This is **not true**.

Understanding the difference between **training** and **inference** is fundamental to understanding how LLMs work.

---

# The Big Idea

An LLM has **two completely different phases**.

```
Training

↓

Learn Patterns

↓

Save Knowledge

↓

Inference

↓

Use Knowledge
```

Think of it like a student.

```
School

↓

Learning

↓

Graduation

↓

Job

↓

Applying Knowledge
```

Training is the school.

Inference is the job.

---

# What is Training?

Training is the process of teaching a model using massive amounts of text.

Sources include:

- Books
- Wikipedia
- GitHub
- Research Papers
- News Articles
- Public Websites
- Documentation

The model learns language patterns by repeatedly predicting the next token.

Example:

Input:

```
The capital of France is
```

Correct Answer:

```
Paris
```

If the model predicts:

```
London
```

It made a mistake.

The training process teaches the model how to reduce that mistake.

---

# How Training Works

Every training example follows the same cycle.

```
Input Text

↓

Tokenizer

↓

Token IDs

↓

Forward Pass

↓

Prediction

↓

Loss

↓

Backward Pass

↓

Optimizer

↓

Update Weights

↓

Repeat
```

This process happens **trillions of times**.

---

# Step 1 — Forward Pass

The model receives the input.

Example:

```
The capital of France is
```

The transformer predicts probabilities.

| Token | Probability |
|--------|------------:|
| Paris | 12% |
| London | 18% |
| Rome | 8% |
| Berlin | 4% |

The prediction is compared with the correct answer.

---

# Step 2 — Loss

Loss measures how wrong the prediction was.

Imagine taking an exam.

```
100%

↓

Correct

↓

Loss = Low
```

```
30%

↓

Wrong

↓

Loss = High
```

Lower loss means better predictions.

---

# Step 3 — Backward Pass

Now the model asks:

> "Which parameters caused the mistake?"

Using **backpropagation**, gradients are calculated for billions of parameters.

These gradients tell the optimizer how each weight should change.

---

# Step 4 — Optimizer

The optimizer slightly updates the model's weights.

Example:

```
Old Weight

↓

0.218

↓

New Weight

↓

0.221
```

Tiny updates happen billions of times during training.

Over time, the model becomes better at predicting language.

---

# What is Inference?

Inference begins **after training is complete**.

This is what happens when you use:

- ChatGPT
- Claude
- Gemini
- Llama
- DeepSeek

The model no longer learns.

Instead, it simply predicts the next token.

---

# Inference Pipeline

```
Your Prompt

↓

Tokenizer

↓

Embeddings

↓

Transformer

↓

Next Token

↓

Repeat

↓

Response
```

Notice something missing?

```
Loss

Backward Pass

Optimizer
```

These steps do **not** exist during inference.

---

# Training vs Inference

| Training | Inference |
|-----------|-----------|
| Learns | Uses learned knowledge |
| Updates weights | No weight updates |
| Requires datasets | Requires a prompt |
| Uses forward + backward pass | Uses only forward pass |
| Expensive | Much cheaper |
| Takes weeks or months | Takes milliseconds or seconds |

---

# Why Doesn't ChatGPT Learn During a Conversation?

Suppose you ask:

```
2 + 2 = 5
```

ChatGPT may correct you.

But even if you repeatedly insist:

```
No.

2 + 2 = 5.
```

The model's internal weights do not change.

Tomorrow, another user will still receive:

```
2 + 2 = 4
```

The model generates responses using the knowledge learned during training.

It does not update that knowledge during inference.

---

# Real-world Analogy

Imagine becoming a doctor.

```
Medical School

↓

Years of Study

↓

Graduation

↓

Hospital

↓

Treat Patients
```

While treating patients, the doctor's medical knowledge does not instantly change after every conversation.

Similarly:

```
Training

↓

Learning

↓

Inference

↓

Answer Questions
```

---

# Visual Diagram

```
                 TRAINING

Books + Internet
        │
        ▼
Tokenizer
        │
        ▼
Transformer
        │
        ▼
Prediction
        │
        ▼
Loss
        │
        ▼
Backward Pass
        │
        ▼
Optimizer
        │
        ▼
Update Weights

====================================

                INFERENCE

User Prompt
        │
        ▼
Tokenizer
        │
        ▼
Transformer
        │
        ▼
Next Token
        │
        ▼
Response
```

---

# Engineering Notes

- Training usually requires thousands of GPUs.
- Training may take weeks or even months.
- Inference only performs a forward pass.
- Quantization is primarily used during inference.
- Fine-tuning is a new training phase that starts from an already-trained model.

---

# Common Misconceptions

### ❌ ChatGPT learns from every conversation.

No.

The model generates responses using already-trained weights.

---

### ❌ Inference updates model parameters.

False.

Inference never updates weights.

---

### ❌ Training and inference are the same process.

No.

Training learns.

Inference predicts.

---

# Interview Questions

### What is training?

Training is the process of learning language patterns by minimizing prediction errors and updating model parameters.

---

### What is inference?

Inference is the process of generating predictions using a trained model without updating its parameters.

---

### What happens during the backward pass?

Gradients are computed to determine how the model's weights should change in order to reduce prediction error.

---

### Why is training much more expensive than inference?

Because training requires forward passes, backward passes, gradient calculations, and weight updates over massive datasets.

Inference performs only forward passes.

---

# Aha Moment 💡

Every time you chat with ChatGPT:

```
No learning happens.
```

The model is simply using knowledge that was learned during training.

This single idea explains why ChatGPT can answer questions instantly while training GPT requires enormous computing resources.

---

# Summary

- Training teaches the model.
- Inference uses the learned knowledge.
- Training updates weights.
- Inference never updates weights.
- Training requires forward and backward passes.
- Inference only requires forward passes.

---

# Further Reading

- Attention Is All You Need (2017)
- GPT-3 Paper
- Llama 3 Technical Report
- Deep Learning by Ian Goodfellow

---

# Next Chapter

➡️ Embeddings

Learn how token IDs are converted into vectors that capture semantic meaning before entering the transformer.