# Tokens vs Words

**Difficulty:** 🟢 Beginner
**Prerequisites:** How ChatGPT Works
**Estimated Reading Time:** 8 minutes

---

> "LLMs do not think in words. They think in tokens."

---

# Why should I care?

One of the biggest misconceptions about Large Language Models is that they process text one word at a time.

They don't.

LLMs process **tokens**, which are smaller pieces of text.

Understanding tokens helps explain:

- Why APIs charge per token
- Why context windows are measured in tokens
- Why some words are split into multiple pieces
- Why different models count tokens differently

---

# The Big Idea

Humans read:

```
Words
```

LLMs read:

```
Tokens
```

A token is the smallest unit of text that a model processes.

A token can be:

- a whole word
- part of a word
- punctuation
- whitespace
- a special token

---

# What is a Word?

Words are what humans naturally read.

Example:

```
I love AI
```

Humans see:

```
I
love
AI
```

Three words.

---

# What is a Token?

A tokenizer breaks text into pieces called tokens.

Example:

```
I love AI
```

might become

```
"I"

" love"

" AI"
```

Notice something interesting.

The space belongs to the token.

Many modern tokenizers include leading spaces because they help the model represent language more efficiently.

---

# Words vs Tokens

Consider this sentence:

```
unbelievable
```

Humans see

```
1 word
```

A tokenizer may produce

```
un

believ

able
```

Now the model sees

```
3 tokens
```

---

# Another Example

Sentence:

```
ChatGPT is amazing!
```

Possible tokens:

```
"Chat"

"GPT"

" is"

" amazing"

"!"
```

Although this is only four words, it may become five tokens.

Different models may tokenize it differently.

---

# Why don't LLMs use words?

Imagine every possible word had to exist in the vocabulary.

What about:

- programming
- programmer
- programmable
- reprogramming

There would be millions of words.

Instead, models reuse pieces.

For example:

```
program

ming
```

These pieces can be combined to represent many different words.

This keeps the vocabulary manageable while still allowing the model to understand new words.

---

# Special Tokens

Not every token is human-readable.

Some tokens provide instructions to the model.

Examples:

```
<BOS>
```

Beginning of sentence.

```
<EOS>
```

End of sentence.

```
<USER>
```

Marks a user message.

```
<ASSISTANT>
```

Marks the assistant response.

These tokens help structure conversations.

---

# Why APIs charge per Token

When using an LLM API, billing is usually based on tokens.

For example:

```
Prompt

↓

120 Tokens

Response

↓

350 Tokens

Total

↓

470 Tokens
```

The model performs computation on every token, not every word.

---

# Context Window

LLMs have a maximum number of tokens they can process at one time.

For example:

```
8K Tokens

32K Tokens

128K Tokens
```

Notice:

These are token limits, not word limits.

Because words and tokens are different, a 128K-token model can usually process fewer than 128,000 words.

---

# Different Models = Different Tokens

The sentence

```
Portfolio Intelligence
```

may be split differently depending on the tokenizer.

Example:

Model A

```
Portfolio

 Intelligence
```

Model B

```
Port

folio

 Intelligence
```

Both are correct.

Each model has its own tokenizer and vocabulary.

---

# Real-world Analogy

Imagine building with LEGO bricks.

Humans think in complete houses.

LLMs think in LEGO bricks.

```
House

↓

Walls

↓

Doors

↓

Windows

↓

Bricks
```

Instead of memorizing every possible house, you reuse smaller pieces.

Tokens work exactly the same way.

---

# Common Misconceptions

### ❌ A token is always a word

False.

A token may be:

- part of a word
- a whole word
- punctuation
- whitespace

---

### ❌ Every model has the same tokens

False.

Each LLM has its own tokenizer.

GPT, Llama, DeepSeek, and Qwen all tokenize text differently.

---

### ❌ One word always equals one token

False.

Sometimes one word becomes several tokens.

Sometimes several short words become fewer tokens.

---

# Interview Questions

### What is a token?

A token is the smallest unit of text processed by an LLM.

---

### Why don't LLMs process words directly?

Because using subword tokens creates a smaller vocabulary and allows the model to represent unseen words efficiently.

---

### Why is API pricing measured in tokens?

Because every computation inside the model is performed on tokens.

---

# Aha Moment 💡

Humans write:

```
Words
```

LLMs process:

```
Token IDs

↓

Embeddings

↓

Vectors
```

The model never directly understands words.

It only understands numerical representations of tokens.

---

# Summary

- Words are for humans.
- Tokens are for LLMs.
- A token may be a whole word or part of a word.
- Every model has its own tokenizer.
- API pricing and context windows are measured in tokens, not words.

## Next Chapter

➡️ Tokenizers

Learn how tokens are converted into numbers that LLMs can understand.