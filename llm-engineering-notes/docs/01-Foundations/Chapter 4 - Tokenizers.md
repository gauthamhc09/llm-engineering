# Tokenizers

**Difficulty:** 🟢 Beginner  
**Estimated Reading Time:** 10 minutes  
**Prerequisites:** Tokens vs Words  
**Last Updated:** July 2026

> "A tokenizer is the bridge between human language and machine language."

---

## Learning Objectives

By the end of this chapter, you will understand:

- What a tokenizer is
- Why LLMs need tokenizers
- Encoding vs Decoding
- Vocabulary and Token IDs
- Why every model has its own tokenizer

# Why should I care?

Large Language Models cannot understand text.

They only understand numbers.

A tokenizer is responsible for converting human-readable text into numerical token IDs that the model can process.

Without a tokenizer, an LLM cannot read your prompt or generate a response.

---

# The Big Idea

Think of the tokenizer as a translator.

```
Human Language

↓

Tokenizer

↓

Token IDs

↓

LLM

↓

Token IDs

↓

Tokenizer

↓

Human Language
```

The tokenizer works in **both directions**.

It converts:

```
Text → Token IDs
```

and

```
Token IDs → Text
```

---

# Why do we need a Tokenizer?

Suppose you ask:

```
What is Artificial Intelligence?
```

Humans understand this immediately.

The computer doesn't.

Instead, the tokenizer converts the sentence into something like:

```
"What"

↓

5231

"is"

↓

374

" Artificial"

↓

21075

" Intelligence"

↓

18823

"?"

↓

30
```

Now the LLM can process the input.

---

# The Two Main Jobs of a Tokenizer

## 1. Encoding

Encoding means:

```
Text

↓

Token IDs
```

Example:

```python
text = "Hello World"

tokenizer.encode(text)
```

Output:

```python
[9906, 4435]
```

---

## 2. Decoding

Decoding is the reverse.

```
Token IDs

↓

Text
```

Example:

```python
tokenizer.decode([9906,4435])
```

Output:

```
Hello World
```

---

# Tokenizer Pipeline

Whenever you chat with ChatGPT (or any LLM), something similar happens internally.

```
User Prompt

↓

Tokenizer

↓

Token IDs

↓

Embeddings

↓

Transformer

↓

Predicted Token IDs

↓

Tokenizer

↓

Readable Text
```

Notice that the transformer never receives plain text.

---

# Vocabulary

Every tokenizer contains a vocabulary.

Think of it as a dictionary.

Example:

| Token | Token ID |
|--------|---------:|
| Hello | 9906 |
| World | 4435 |
| AI | 15836 |
| Python | 12958 |

Every token has a unique ID.

---

# Special Tokens

Not every token represents normal text.

Some tokens help organize conversations.

Examples:

```
<BOS>
```

Beginning of Sentence

```
<EOS>
```

End of Sentence

```
<USER>
```

Marks the user's message.

```
<ASSISTANT>
```

Marks the model's response.

```
<SYSTEM>
```

System instruction.

These tokens are invisible to most users but are extremely important for chat models.

---

# Every Model Has Its Own Tokenizer

One of the most important facts about LLMs:

Different models use different tokenizers.

For example:

GPT

```
Hello

↓

[9906]
```

Llama

```
Hello

↓

[15043]
```

DeepSeek

```
Hello

↓

[2045]
```

The same word can have completely different token IDs depending on the model.

This is why you must always use the tokenizer that belongs to the model.

---

# Loading a Tokenizer

Using Hugging Face:

```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained(
    "meta-llama/Meta-Llama-3.1-8B"
)
```

What happens internally?

```
Hugging Face

↓

Download tokenizer files

↓

Vocabulary

↓

Special Tokens

↓

Chat Template

↓

Ready to tokenize text
```

Notice that this downloads only the tokenizer, **not the entire model**.

---

# Chat Templates

Modern chat models don't receive Python dictionaries directly.

Suppose we have:

```python
messages = [
    {"role":"system","content":"You are helpful"},
    {"role":"user","content":"Tell me a joke"}
]
```

The tokenizer converts this into the format expected by the model.

Example:

```
<System>

You are helpful.

<User>

Tell me a joke.

<Assistant>
```

Only after formatting does tokenization begin.

---

# Real-world Analogy

Imagine you're travelling to Japan.

You speak English.

The shopkeeper speaks Japanese.

A translator stands between both of you.

```
You

↓

Translator

↓

Japanese

↓

Shopkeeper
```

The tokenizer plays the exact same role.

```
You

↓

Tokenizer

↓

Numbers

↓

LLM
```

Without the translator, communication is impossible.

---

# Common Misconceptions

### ❌ The tokenizer is part of the transformer.

No.

The tokenizer runs **before** the transformer.

---

### ❌ Every LLM uses the same tokenizer.

False.

Every model has its own vocabulary and tokenizer.

---

### ❌ The tokenizer understands language.

No.

It simply converts between text and token IDs.

The understanding happens inside the transformer.

---

# Interview Questions

### What is a tokenizer?

A tokenizer converts text into token IDs and converts generated token IDs back into readable text.

---

### Why can't we feed text directly into an LLM?

Because neural networks operate on numbers rather than raw text.

---

### Why must we use the correct tokenizer?

Because every model has its own vocabulary and token IDs.

Using the wrong tokenizer produces incorrect inputs.

---

# Aha Moment 💡

When you type:

```
Explain Artificial Intelligence.
```

The LLM never actually sees those words.

It sees something conceptually like:

```
[9125, 294, 18392, 728]
```

Everything inside the transformer happens using numbers.

---

# Summary

- Tokenizers convert text into token IDs.
- They also convert generated token IDs back into text.
- Every model has its own tokenizer.
- Chat models use tokenizers to apply chat templates.
- Without tokenizers, LLMs cannot process human language.

---

# Next Chapter

➡️ Training vs Inference

Learn why ChatGPT stops learning after training and how inference differs from model training.