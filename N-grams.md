# N-Grams in NLP

## 1. Introduction

N-Grams are a text representation technique that captures sequences of `N` consecutive words from a text document.

They extend the Bag of Words (BoW) model by capturing local word order and short-range relationships between consecutive words.

In standard BoW, individual words are treated as independent features, and their original order is ignored. N-Grams introduce word combinations as additional features.

**Example:**

Sentence: `I love machine learning`

### Unigram (N = 1)

Each individual word is treated as a feature.

- I
- love
- machine
- learning

### Bigram (N = 2)

Every consecutive sequence of two words is treated as a feature.

- I love
- love machine
- machine learning

### Trigram (N = 3)

Every consecutive sequence of three words is treated as a feature.

- I love machine
- love machine learning

### Four-Gram (N = 4)

- I love machine learning

---

## 2. Types of N-Grams

| Type | N | Description |
|---|---:|---|
| Unigram | 1 | Sequence of one word |
| Bigram | 2 | Sequence of two consecutive words |
| Trigram | 3 | Sequence of three consecutive words |
| Four-Gram | 4 | Sequence of four consecutive words |

### Number of N-Grams Formula

For a document containing `L` words, the number of N-Grams generated for a particular N is:

`Number of N-Grams = L - N + 1`

**Example:**

Sentence: `I love machine learning`

Total words = 4

- Unigrams = 4 - 1 + 1 = 4
- Bigrams = 4 - 2 + 1 = 3
- Trigrams = 4 - 3 + 1 = 2
- Four-Grams = 4 - 4 + 1 = 1

---

## 3. Why Do We Need N-Grams?

### Limitation of Bag of Words

Consider two sentences:

- Sentence 1: `Dog bites man`
- Sentence 2: `Man bites dog`

In a standard Unigram BoW representation, both sentences produce the same word-frequency representation because they contain the same words with the same frequencies.

BoW does not preserve the original word order.

### How Bigrams Solve This Problem

Sentence 1:

- Dog bites
- bites man

Sentence 2:

- Man bites
- bites dog

The Bigram representations are different.

Therefore, N-Grams capture local word order and help distinguish text sequences that have identical individual word frequencies.

---

## 4. Advantages of N-Grams

### 4.1 Captures Local Word Order

Unlike standard Unigram BoW, N-Grams capture the order of consecutive words.

For example:

- `Dog bites man`
- `Man bites dog`

Their Bigram representations are different.

### 4.2 Captures Phrase-Level Information

N-Grams identify commonly occurring word combinations.

Examples:

- Machine learning
- Deep learning
- Credit card
- New York

These combinations can carry more useful information than considering individual words independently.

### 4.3 Helps in Sentiment Analysis

Consider:

- `good`
- `not good`

Unigram features represent `not` and `good` separately.

Bigram features can additionally represent `not good` as a combined feature.

This helps traditional ML models identify certain sentiment-related patterns.

### 4.4 Useful for Text Classification

N-Grams can provide useful features for:

- Spam detection
- Sentiment analysis
- News classification
- Topic classification
- Text categorization

---

## 5. Disadvantages of N-Grams

### 5.1 High Dimensionality

As N increases, the number of possible word combinations increases.

For example:

- Unigrams generate individual word features.
- Bigrams introduce additional two-word combinations.
- Trigrams introduce additional three-word combinations.

This can significantly increase the feature space.

### 5.2 Increased Sparsity

Most possible N-Gram combinations do not occur in every document.

Consequently, the document-term matrix can contain a large number of zero values.

### 5.3 Data Sparsity

Consider these sentences:

- `I love machine learning`
- `I enjoy machine learning`

Their Trigrams are:

First sentence:
- I love machine
- love machine learning

Second sentence:
- I enjoy machine
- enjoy machine learning

Even though both sentences communicate a similar idea, their exact Trigram features differ.

A model trained on one combination may not have learned the other combination.

### 5.4 Limited Long-Range Context

N-Grams capture only consecutive sequences of a fixed length.

They cannot directly capture relationships between words separated by many other words.

Example:

`I am not saying this product is bad.`

A Bigram can capture `not saying`, but cannot directly capture the relationship between `not` and `bad`.

Therefore, N-Grams provide local context rather than complete contextual understanding.

---

## 6. N-Grams in Scikit-Learn

Scikit-learn provides N-Gram functionality through `CountVectorizer` using the `ngram_range` parameter.

| Parameter | Representation |
|---|---|
| `ngram_range=(1,1)` | Unigrams only |
| `ngram_range=(2,2)` | Bigrams only |
| `ngram_range=(3,3)` | Trigrams only |
| `ngram_range=(1,2)` | Unigrams and Bigrams |
| `ngram_range=(1,3)` | Unigrams, Bigrams and Trigrams |

**Important:** `ngram_range=(1,2)` includes both Unigrams and Bigrams, not only Bigrams.

---

## 7. Difference Between BoW and N-Grams

| Feature | Unigram BoW | N-Gram BoW |
|---|---|---|
| Individual word frequency | Yes | Yes, when unigrams are included |
| Local word order | No | Yes |
| Phrase-level information | No | Yes |
| Contextual understanding | No | Limited local patterns |
| Vocabulary size | Generally smaller | Generally larger |
| Sparsity | Can be high | Often higher |

---

## 8. N-Grams vs Contextual Embeddings

N-Grams capture fixed-length consecutive word combinations but do not understand the complete meaning of a sentence.

Contextual embedding models such as BERT generate word representations based on surrounding context.

For example:

- `I read a book.`
- `I will book a flight.`

The word `book` has different meanings in these sentences.

A static N-Gram feature representation does not dynamically generate different contextual representations for the same word. Contextual models can represent these different usages.

---

## 9. Applications of N-Grams

1. **Sentiment Analysis:** Identifying phrases such as `not good` and `very bad`.
2. **Spam Detection:** Identifying common spam-related word combinations.
3. **Text Classification:** Using word combinations as additional classification features.
4. **Search Engines:** Matching phrases and consecutive word sequences.
5. **Language Modeling:** Estimating the probability of a word based on preceding words.

---

## 10. Key Takeaways

- N-Grams represent sequences of N consecutive words.
- Unigrams represent individual words.
- Bigrams represent two consecutive words.
- Trigrams represent three consecutive words.
- N-Grams capture local word order and phrase-level information.
- They help distinguish sentences that have identical individual word frequencies but different word orders.
- Increasing N can increase vocabulary size, dimensionality and sparsity.
- N-Grams capture local patterns, not complete semantic or contextual understanding.
- `CountVectorizer` supports N-Grams through its `ngram_range` parameter.
