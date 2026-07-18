# What is an LLM?

# What is a Large Language Model (LLM)?

> "A Large Language Model (LLM) is a neural network trained on massive amounts of text to predict the next token in a sequence."

---

# Why should I care?

Large Language Models power applications like:

- ChatGPT
- Claude
- Gemini
- DeepSeek
- Llama
- Qwen

As an AI Engineer, understanding how an LLM works is far more important than simply knowing how to call an API.

---

# The Big Idea

An LLM is **not** a search engine.

It does **not** search the internet every time you ask a question.

Instead, it has already learned language patterns during training and generates text by predicting the most likely next token.

For example:

Input:

```
The capital of France is
```

The model predicts:

```
Paris
```

It doesn't "look up" Paris.

It predicts that "Paris" is the most probable next token.

---

# How an LLM Works

```
User Prompt
      │
      ▼
Tokenizer
(Text → Token IDs)
      │
      ▼
Embeddings
(Token IDs → Vectors)
      │
      ▼
Transformer
(Billions of mathematical operations)
      │
      ▼
Predict Next Token
      │
      ▼
Repeat until complete
      │
      ▼
Tokenizer
(Token IDs → Text)
      │
      ▼
Response
```

---

# The Two Phases of an LLM

## 1. Training

During training, the model learns patterns from huge amounts of text.

```
Books
Wikipedia
Research Papers
GitHub
News
Web Pages
```

For every sentence, the model repeatedly performs:

```
Forward Pass

↓

Prediction

↓

Loss Calculation

↓

Backpropagation

↓

Optimizer

↓

Update Weights
```

This process repeats trillions of times.

At the end of training, the model has learned billions of language patterns.

---

## 2. Inference

Inference is what happens when you use ChatGPT.

```
Your Question

↓

Tokenizer

↓

Transformer

↓

Predict Next Token

↓

Predict Next Token

↓

Predict Next Token

↓

Response
```

No learning happens during inference.

The model only uses the knowledge it already learned.

---

# Training vs Inference

| Training | Inference |
|-----------|-----------|
| Learns | Uses learned knowledge |
| Updates weights | Does not update weights |
| Requires huge GPU clusters | Can run on a laptop or API |
| Takes weeks/months | Takes milliseconds or seconds |

---

# What is "Large"?

"Large" refers to the number of parameters (weights) in the neural network.

Examples:

| Model | Parameters |
|--------|-----------:|
| Tiny Model | 100 Million |
| Phi-4 Mini | ~4 Billion |
| Llama 3.1 8B | 8 Billion |
| GPT-4 Class Models | Hundreds of billions or more (exact size undisclosed) |

More parameters generally allow the model to capture more complex language patterns, but they also require more memory and computation.

---

# Real-world Analogy

Imagine teaching a child English.

The child reads millions of books.

Eventually you ask:

```
The capital of France is ____
```

The child answers:

```
Paris
```

The child isn't searching Google.

The child remembers patterns learned during years of reading.

An LLM learns in a very similar way, except it learns using mathematics instead of biological neurons.

---

# Key Terminology

**Token**
> The basic unit processed by an LLM (word, subword, or punctuation).

**Parameter**
> A learned numerical value inside the neural network.

**Prompt**
> The input provided by the user.

**Inference**
> Using the trained model to generate responses.

**Training**
> The process of learning by updating model parameters.

---

# Interview Questions

### What is an LLM?

A neural network trained on massive text corpora that generates text by predicting the next token.

---

### Does ChatGPT search the internet?

Not by default.

It generates responses using patterns learned during training.

(Some versions can additionally use web search tools.)

---

### Does an LLM understand language?

Not in the human sense.

It learns statistical relationships between tokens and uses those relationships to generate coherent text.

---

# Aha Moment 💡

The biggest misconception is:

```
Question

↓

LLM

↓

Answer
```

What actually happens is:

```
Question

↓

Tokenizer

↓

Numbers

↓

Transformer

↓

Next Token Prediction

↓

Text

↓

Answer
```

The model never directly reads or writes text.

It operates on numbers.

---

# Summary

- LLMs are neural networks trained to predict the next token.
- They learn patterns during training.
- During inference, they do not learn.
- Every response is generated one token at a time.
- Internally, an LLM works entirely with numbers rather than text.