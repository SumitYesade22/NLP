# Tokenization and Basic Terminologies

## 1. Tokenization

### What is Tokenization?

Tokenization is the process of breaking down raw text into smaller units called **tokens**.

These tokens can be:
- Words
- Subwords
- Characters
- Sentences

**Example:**

Original text:
```text
I love Natural Language Processing.
```

After word-level tokenization:
```python
["I", "love", "Natural", "Language", "Processing", "."]
```

Each individual element in the resulting list is called a token.

### Why is Tokenization Required?

Computers cannot directly process human language in the same way humans understand it.

Machine learning and deep learning models require numerical representations of text.

Tokenization helps divide raw text into smaller units that can subsequently be converted into numerical representations.

**Basic NLP Pipeline:**

```text
Raw Text
   |
   v
Tokenization
   |
   v
Tokens
   |
   v
Numerical Representation
   |
   v
NLP Model
   |
   v
Prediction / Output
```

**Important:** Tokenization itself does not convert text into numerical values. It only divides text into smaller units. Numerical representation happens in subsequent steps.

---

## 2. Basic NLP Terminologies

### 2.1 Corpus

A corpus is a collection of text documents used for NLP analysis or model training.

**Example:**

```text
Document 1: This movie is amazing.
Document 2: The movie was boring.
Document 3: I really enjoyed this movie.
```

The collection of all three documents is called a corpus.

### 2.2 Document

A document is an individual piece of text within a corpus.

A document can be:
- A sentence
- A Paragraph
- A Movie Review
- An Email
- A News Article

**Example:**

```text
This movie is amazing.
```

This is one individual document.

### 2.3 Sentence

A sentence is a linguistic unit that generally expresses a complete thought.

**Example:**

```text
I love Machine Learning.
NLP is interesting.
```

There are two sentences in the given text.

### 2.4 Token

A token is an individual unit generated after tokenization.

Depending on the tokenization technique, tokens can represent:
- Words
- Subwords
- Characters
- Punctuation marks

**Example:**

```text
NLP is interesting!
```

Tokens:

```python
["NLP", "is", "interesting", "!"]
```

### 2.5 Vocabulary

Vocabulary is the collection of unique tokens present in a corpus or defined by a tokenizer.

**Example:**

Corpus:

```text
Document 1: I love NLP
Document 2: I love Python
Document 3: NLP is amazing
```

All token occurrences:

```text
I, love, NLP, I, love, Python, NLP, is, amazing
```

Unique tokens:

```python
["I", "love", "NLP", "Python", "is", "amazing"]
```

Therefore:

```text
Vocabulary Size = 6
```

**Important:** Repeated tokens are counted only once when calculating vocabulary size.

### 2.6 Type vs Token

These terms are used to distinguish total token occurrences from unique tokens.

- **Token:** An individual occurrence of a token in the text.
- **Type:** A unique token in the text.

**Example:**

```text
I love NLP and I love Python.
```

Token occurrences:

```text
I, love, NLP, and, I, love, Python
```

Total Tokens = 7

Unique Types:

```text
I, love, NLP, and, Python
```

Total Types = 5

| Terminology | Count |
|---|---:|
| Total Tokens | 7 |
| Unique Types | 5 |
| Vocabulary Size | 5 |

**Note:** Token and type counts depend on the tokenization rules, including case sensitivity and punctuation handling.

### 2.7 Stop Words

Stop words are commonly occurring words that may contribute relatively little information to certain NLP tasks.

Examples:

- is
- the
- a
- an
- in
- of
- and

**Example:**

Original sentence:

```text
This is a very good movie.
```

After stop-word removal:

```text
very good movie
```

#### Why Remove Stop Words?

In some traditional NLP applications, removing frequent words can:
- Reduce the number of tokens.
- Reduce vocabulary size.
- Remove words that contribute relatively little to the task.
- Simplify text representations.

#### Important Limitation

Stop words should not be removed blindly because they can carry important contextual or grammatical information.

**Example:**

Original:
```text
I do not like this movie.
```

After removing `not`:

```text
I like this movie.
```

The meaning becomes completely opposite.

Therefore, stop-word removal is task-dependent.

---

## 3. N-Grams

### What are N-Grams?

N-grams are continuous sequences of N consecutive tokens in a text.

Here, N represents the number of consecutive tokens included in each sequence.

Consider the sentence:

```text
I love machine learning
```

### 3.1 Unigram (N = 1)

A unigram contains one token.

```text
I
love
machine
learning
```

Total Unigrams = 4

### 3.2 Bigram (N = 2)

A bigram contains two consecutive tokens.

```text
I love
love machine
machine learning
```

Total Bigrams = 3

### 3.3 Trigram (N = 3)

A trigram contains three consecutive tokens.

```text
I love machine
love machine learning
```

Total Trigrams = 2

### 3.4 General Formula

For a sequence containing L tokens, the number of possible contiguous N-grams is:

```text
Number of N-grams = L - N + 1
```

This formula applies when L >= N.

### Why are N-Grams Used?

Individual words do not always capture the complete meaning of a phrase.

For example:

```text
New York
```

The individual words `New` and `York` have separate meanings, but together they represent a specific geographical location.

N-grams help capture local word sequences and relationships.

**Applications:**
- Language modeling
- Text classification
- Sentiment analysis
- Text prediction
- Traditional NLP feature extraction

**Limitation:** As N increases, the number of possible combinations can grow significantly, leading to a larger feature space and data sparsity.

---

## 4. Types of Tokenization

Tokenization can be performed at different levels depending on the application and tokenizer.

### 4.1 Word-Level Tokenization

Breaks text into individual words.

**Example:**

```text
I love NLP
```

Output:

```python
["I", "love", "NLP"]
```

**Advantages:**
- Easy to understand and interpret.
- Words retain their individual identities.
- Useful for traditional NLP techniques.

**Limitations:**
- Large vocabulary size.
- Unseen words can create problems.
- Different word forms may be treated as separate tokens.

### 4.2 Character-Level Tokenization

Breaks text into individual characters.

**Example:**

```text
cat
```

Output:

```python
["c", "a", "t"]
```

**Advantages:**
- Small vocabulary.
- Can represent previously unseen words using known characters.
- Useful for handling spelling variations and certain character-level language tasks.

**Limitations:**
- Produces longer sequences.
- Requires the model to learn word structures from characters.
- Character-level processing can be computationally expensive for long documents.

### 4.3 Subword-Level Tokenization

Breaks words into smaller units called subwords.

These units can represent complete words, word fragments, or frequently occurring character sequences.

**Example:**

```text
playing
```

Possible tokenization:

```python
["play", "ing"]
```

The actual splitting depends on the tokenizer and its vocabulary.

**Advantages:**
- Balances vocabulary size and sequence length.
- Handles many previously unseen words through known subword units.
- Can represent morphological structures.
- Reduces the unknown-word problem.

**Limitations:**
- Tokenization is more complex.
- Tokens may not always correspond to meaningful linguistic units.
- Different models can tokenize the same text differently.

Subword tokenization is commonly used by modern Transformer-based models.

Examples include:
- BERT: WordPiece
- GPT-family tokenizers: BPE-based or other variants depending on the model
- T5: SentencePiece

### 4.4 Sentence-Level Tokenization

Breaks a paragraph or document into individual sentences.

**Example:**

Original text:

```text
I love NLP. It is interesting.
```

Output:

```python
[
    "I love NLP.",
    "It is interesting."
]
```

**Applications:**
- Sentence-level sentiment analysis.
- Text summarization.
- Document processing.
- Sentence classification.

---

## 5. Comparison of Tokenization Techniques

| Technique | Unit | Main Advantage |
|---|---|---|
| Word-Level | Words | Easy interpretation |
| Character-Level | Characters | Handles unseen words using known characters |
| Subword-Level | Word fragments | Balances vocabulary size and unknown words |
| Sentence-Level | Sentences | Preserves sentence boundaries |

---

## 6. Important Points to Remember

1. Tokenization is generally one of the initial steps in an NLP pipeline.
2. A token can represent a word, subword, character, or other unit.
3. A corpus is a collection of documents.
4. A document is an individual text unit within a corpus.
5. Vocabulary contains unique tokens.
6. Token count represents total token occurrences.
7. Type count represents unique token occurrences.
8. Stop-word removal is optional and depends on the NLP task.
9. N-grams capture sequences of consecutive tokens.
10. Modern Transformer models commonly use subword-based tokenization.

---

## 7. Key Takeaway

Tokenization converts raw text into smaller manageable units that can subsequently be represented numerically and processed by NLP models.

The choice of tokenization technique affects:
- Vocabulary size.
- Sequence length.
- Handling of unseen words.
- Model input representation.
- Computational requirements.

There is no universally best tokenization technique. The appropriate choice depends on the task, dataset, and model architecture.