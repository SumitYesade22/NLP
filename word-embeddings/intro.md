# Introduction to Word Embeddings

## 1. What Are Word Embeddings?

Word Embeddings are dense, low-dimensional vector representations of words in a continuous vector space.

They represent words as numerical vectors in such a way that words with similar meanings or usage patterns tend to have similar vector representations.

Machine learning models cannot directly understand text. They require numerical representations of the input. Word embeddings help convert textual data into meaningful numerical representations.

**Example:**

Consider the following words:

- King
- Queen
- Apple
- Banana

A model learns numerical representations for these words, such as:

| Word | Embedding (Illustrative) |
|---|---|
| King | [0.82, 0.45, 0.91] |
| Queen | [0.79, 0.48, 0.88] |
| Apple | [0.12, 0.91, 0.24] |
| Banana | [0.15, 0.87, 0.29] |

These are illustrative values, not actual pretrained embeddings.

Notice that King and Queen have relatively similar representations, as do Apple and Banana.

The objective is to learn vector representations that capture useful relationships between words.

## 2. Why Do We Need Word Embeddings?

Before word embeddings, one commonly used technique was One-Hot Encoding.

### 2.1 One-Hot Encoding

One-Hot Encoding represents each word using a binary vector whose length equals the vocabulary size.

Only the position corresponding to that word is 1; all other positions are 0.

**Example:**

Vocabulary:

`["cat", "dog", "apple", "banana"]`

One-hot representations:

| Word | One-Hot Vector |
|---|---|
| cat | [1, 0, 0, 0] |
| dog | [0, 1, 0, 0] |
| apple | [0, 0, 1, 0] |
| banana | [0, 0, 0, 1] |

### 2.2 Limitations of One-Hot Encoding

**1. High Dimensionality**

The vector size is equal to the vocabulary size.

For example, if the vocabulary contains 50,000 unique words, every word is represented using a 50,000-dimensional vector.

This creates high-dimensional and sparse representations.

**2. Sparse Representation**

Most values in a one-hot vector are zero.

For a vocabulary of 50,000 words, only one value is 1 and the remaining 49,999 values are 0.

**3. No Semantic Relationship**

One-hot encoding does not capture relationships between words.

For example:

- Cat = [1, 0, 0, 0]
- Dog = [0, 1, 0, 0]

The similarity between these vectors is zero, even though cat and dog are semantically related.

Every pair of different one-hot vectors is orthogonal.

**4. No Similarity Information**

One-hot encoding cannot naturally represent how closely two words are related in meaning or usage.

It treats every distinct word as an independent category.

## 3. Dense vs Sparse Representations

### Sparse Representation

A sparse vector contains mostly zero values.

Example:

`[0, 0, 0, 1, 0, 0, 0, 0]`

One-hot encoding is a sparse representation.

### Dense Representation

A dense vector contains meaningful numerical values across most of its dimensions.

Example:

`[0.24, 0.81, -0.36, 0.57]`

Word embeddings are generally dense representations.

Instead of requiring one dimension per vocabulary word, embeddings represent words using a relatively small number of learned dimensions.

## 4. Semantic and Syntactic Information

Word embeddings can capture different types of linguistic relationships.

### 4.1 Semantic Information

Semantic information relates to the meaning and conceptual relationships between words.

Examples:

- King and Queen
- Doctor and Nurse
- Cat and Dog
- Apple and Banana

Words with similar meanings or usage patterns may have similar vector representations.

### 4.2 Syntactic Information

Syntactic information relates to grammatical and structural properties of language.

Examples:

- Play, Playing, Played
- Walk, Walking, Walked
- Run, Runs, Running

Word embeddings can learn patterns associated with tense, plurality, and other grammatical relationships.

## 5. Distributional Hypothesis

The Distributional Hypothesis is a fundamental idea behind many word embedding techniques.

**"Words that occur in similar contexts tend to have similar meanings."**

In simple terms, we can understand a word's usage by examining the words that frequently appear around it.

**Example:**

Sentence 1: The cat is drinking milk.

Sentence 2: The dog is drinking milk.

Here, cat and dog appear in similar contexts:

- The
- is
- drinking
- milk

Since they appear in similar linguistic contexts, an embedding model can learn similar representations for them.

This does not mean that the words have exactly the same meaning. It means their usage patterns have similarities.

## 6. How Are Word Embeddings Learned?

Word embeddings are generally learned from large text corpora.

A simplified training process:

1. **Corpus Collection:** Collect a large amount of text.
2. **Tokenization:** Split the text into individual tokens.
3. **Vocabulary Creation:** Build a vocabulary of unique words.
4. **Initialization:** Initialize word vectors, often with small random values.
5. **Training:** Learn vector representations using word-context relationships or co-occurrence statistics.
6. **Optimization:** Update the model's parameters to improve its learning objective.
7. **Embedding Extraction:** Extract the learned word vectors.

Unlike manually assigning meanings to words, the model learns numerical representations from patterns in the training data.

## 7. Important Characteristics of Word Embeddings

| Characteristic | Description |
|---|---|
| Dense | Contains relatively few zero values |
| Low-dimensional | Uses fewer dimensions than vocabulary size |
| Learned | Values are learned during training |
| Continuous | Represents words using real-valued numbers |
| Distributed | Information about a word is represented across multiple dimensions |
| Similarity-aware | Can capture relationships between words through vector similarity |

**Important:** Individual embedding dimensions generally do not have directly interpretable meanings. A dimension does not necessarily represent a specific concept such as gender, age, or emotion.

## 8. Common Word Embedding Techniques

We will study three important approaches:

### 8.1 Word2Vec

A predictive approach that learns word representations by predicting words from their surrounding context or predicting context from a given word.

It has two main architectures:

- CBOW (Continuous Bag of Words)
- Skip-Gram

### 8.2 GloVe (Global Vectors for Word Representation)

A count-based approach that learns word vectors using global word co-occurrence statistics from a corpus.

### 8.3 FastText

An extension of the Word2Vec approach that incorporates subword information using character n-grams.

It can represent words using their constituent character n-grams, which helps with rare and previously unseen words.

## 9. Static vs Contextual Word Embeddings

Traditional Word2Vec, GloVe, and FastText embeddings are generally static.

This means a word has the same learned embedding regardless of the sentence in which it appears.

**Example:**

Consider the word "Bank":

1. I deposited money in the bank.
2. He sat near the river bank.

The word bank has different meanings in these sentences, but a traditional static embedding model generally provides the same word vector for both occurrences.

Contextual embedding models, such as BERT, generate representations based on the surrounding context.

Therefore, the representation of "bank" can differ depending on its usage in a sentence.

## 10. Key Takeaways

- Word embeddings convert words into dense, low-dimensional numerical vectors.
- They overcome several limitations of one-hot encoding.
- They can capture semantic and syntactic relationships.
- The Distributional Hypothesis provides an important foundation for learning word representations.
- Word2Vec, GloVe, and FastText are important traditional word embedding techniques.
- Traditional word embeddings are generally static, whereas contextual models generate representations based on sentence context.

---
