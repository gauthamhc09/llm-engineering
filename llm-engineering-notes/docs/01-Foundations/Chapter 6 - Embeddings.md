# Embeddings

> "Embeddings transform token IDs into meaningful vectors that capture semantic relationships."

**Difficulty:** 🟢 Beginner
**Estimated Reading Time:** 15 minutes
**Prerequisites:** Training vs Inference
**Last Updated:** July 2026

---

# Learning Objectives

By the end of this chapter, you will understand:

- Why token IDs are not enough for an LLM
- What embeddings are
- How embedding vectors are created
- Why similar words have similar embeddings
- How embeddings become the input to the Transformer

---

# Why Should I Care?

Earlier, we learned that the tokenizer converts text into token IDs.

For example:

```
"I love AI"

↓

[40, 3021, 15836]
```

But here's an important question:

> Can a neural network understand that token **15836** represents "AI"?

No.

To a neural network, **15836 is just an integer**.

Numbers like 1, 25, or 15836 have no meaning by themselves.

We need a richer numerical representation.

That representation is called an **embedding**.

---

# The Big Idea

A token ID is simply an index.

An embedding is a dense vector that captures the meaning of that token.

Think of it like this:

```
Text

↓

Tokenizer

↓

Token IDs

↓

Embeddings

↓

Transformer
```

The Transformer never works directly with token IDs.

It works with embedding vectors.

---

# Why Token IDs Are Not Enough

Imagine assigning IDs to fruits.

| Fruit | ID |
|--------|---:|
| Apple | 1 |
| Mango | 2 |
| Car | 3 |

Does the neural network know that Apple and Mango are more similar than Apple and Car?

No.

The IDs are arbitrary.

```
Apple → 1

Mango → 2

Car → 3
```

The numbers don't contain any semantic information.

---

# What is an Embedding?

An embedding is a list of floating-point numbers.

Example:

```
Token ID

15836

↓

Embedding

[0.23, -0.81, 1.14, 0.55, ...]
```

Real models typically use vectors with dimensions such as:

- 768
- 1024
- 4096
- 8192

Each value contributes to how the model represents the token.

---

# Embedding Matrix

Where do these vectors come from?

They are stored in an **Embedding Matrix**.

Imagine a table:

| Token ID | Embedding |
|----------:|-----------|
| 0 | [...] |
| 1 | [...] |
| 2 | [...] |
| 3 | [...] |
| ... | ... |
| 15836 | [...] |

When the tokenizer outputs:

```
15836
```

the model performs a lookup in this table.

No searching or calculation is needed.

It's simply:

```
Embedding = EmbeddingMatrix[15836]
```

---

# Example Pipeline

Input:

```
I love AI
```

Step 1:

```
Tokenizer

↓

[40, 3021, 15836]
```

Step 2:

```
Embedding Lookup

↓

[
 Vector1,
 Vector2,
 Vector3
]
```

These vectors become the input to the Transformer.

---

# Similar Words Have Similar Embeddings

One of the most powerful properties of embeddings is that similar concepts are located close together in vector space.

For example:

```
King
Queen
Prince
Princess
```

will have embeddings that are closer to each other than:

```
King
Banana
Car
Ocean
```

This helps the model recognize relationships between words.

---

# High-Dimensional Space

Humans think in 3D space.

Embeddings exist in hundreds or thousands of dimensions.

For example:

```
Embedding Dimension = 4096
```

You can't visualize 4096 dimensions directly, but mathematically the model can compare vectors and measure how similar they are.

---

# Visual Diagram

```
Text
 │
 ▼
Tokenizer
 │
 ▼
Token IDs
 │
 ▼
Embedding Lookup
 │
 ▼
Dense Vectors
 │
 ▼
Transformer
```

---

# Code Example

```python
from transformers import AutoTokenizer, AutoModel

tokenizer = AutoTokenizer.from_pretrained(
    "meta-llama/Meta-Llama-3.1-8B"
)

model = AutoModel.from_pretrained(
    "meta-llama/Meta-Llama-3.1-8B"
)

inputs = tokenizer("Hello", return_tensors="pt")

outputs = model(**inputs)
```

Here:

- `tokenizer()` converts text into token IDs.
- The model internally converts those IDs into embeddings before passing them through the Transformer.

---

# Engineering Notes

- The embedding layer is the first learnable layer of an LLM.
- Embeddings are learned during training and updated along with the rest of the model.
- The embedding matrix can contain millions of parameters.
- Models with larger hidden dimensions have larger embedding vectors.

---

# Common Misconceptions

### ❌ Token IDs contain meaning.

No.

Token IDs are simply identifiers.

The semantic information comes from the embedding vectors.

---

### ❌ Embeddings are created by the tokenizer.

No.

The tokenizer only outputs token IDs.

The embedding layer inside the model converts those IDs into vectors.

---

### ❌ Every model shares the same embeddings.

False.

Each model learns its own embedding matrix during training.

---

# Interview Questions

### What is an embedding?

An embedding is a dense vector representation of a token that captures semantic information and serves as input to the Transformer.

---

### Why can't we feed token IDs directly into the Transformer?

Because token IDs are arbitrary integers and do not encode semantic relationships.

---

### What is the embedding matrix?

It is a learnable lookup table that maps every token ID to a dense vector.

---

### Are embeddings learned or fixed?

Embeddings are learned during training and updated through backpropagation.

---

# 🧠 First Principles

The Transformer cannot understand integers like `15836`.

Its real input is a matrix of vectors.

Everything begins with converting token IDs into meaningful numerical representations.

---

# Aha Moment 💡

The tokenizer answers:

> "Which token is this?"

The embedding layer answers:

> "What does this token represent mathematically?"

Without embeddings, the Transformer would only see meaningless integers.

---

# Summary

- Token IDs are identifiers, not meaning.
- Embeddings convert token IDs into dense vectors.
- Similar words have similar embedding vectors.
- The embedding matrix is learned during training.
- The Transformer receives embeddings, not token IDs.

---

# Further Reading

- Attention Is All You Need (2017)
- Word2Vec
- GloVe
- FastText
- Llama 3 Technical Report

---

# Next Chapter

➡️ Positional Encoding

Learn how Transformers understand the order of words, since embeddings alone do not contain sequence information.