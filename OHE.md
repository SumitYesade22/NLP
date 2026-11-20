# One-Hot Encoding (OHE)

## 1. What is One-Hot Encoding?

One-Hot Encoding (OHE) is a technique used to convert categorical data into numerical binary vectors so that machine learning algorithms can process categorical information.

Each unique category is represented by a separate binary column. Only one column gets the value `1`, while all remaining columns get `0` for that category.

### Example

Suppose we have a categorical feature called `Color`:

| Color |
|---|
| Red |
| Blue |
| Green |
| Red |

After applying One-Hot Encoding:

| Color_Red | Color_Blue | Color_Green |
|---:|---:|---:|
| 1 | 0 | 0 |
| 0 | 1 | 0 |
| 0 | 0 | 1 |
| 1 | 0 | 0 |

Each category is represented by a unique binary vector.

- Red → `[1, 0, 0]`
- Blue → `[0, 1, 0]`
- Green → `[0, 0, 1]`

## 2. Why Do We Need One-Hot Encoding?

Machine learning algorithms generally require numerical input. However, categorical features contain labels rather than numerical values.

For example:

```text
Color = ["Red", "Blue", "Green"]
```

We could assign numerical labels:

```text
Red   = 0
Blue  = 1
Green = 2
```

But this can introduce an artificial ordinal relationship.

An algorithm might interpret:

- Green (2) as greater than Blue (1).
- The distance between Green and Red as twice the distance between Blue and Red.

However, colors do not have any inherent numerical ordering.

OHE solves this problem by representing each category independently using binary values.

**Important:** Integer encoding is not automatically wrong for every algorithm. Some tree-based algorithms can work with integer-coded categories, but arbitrary numerical ordering can still affect their splits.

## 3. One-Hot Encoding in NLP

In NLP, One-Hot Encoding can represent individual words as binary vectors.

Consider the following vocabulary:

```text
Vocabulary = ["I", "Love", "NLP", "Python"]
```

Vocabulary size = 4.

Each word gets a vector of length 4.

| Word | OHE Vector |
|---|---|
| I | `[1, 0, 0, 0]` |
| Love | `[0, 1, 0, 0]` |
| NLP | `[0, 0, 1, 0]` |
| Python | `[0, 0, 0, 1]` |

### Dimensionality

If vocabulary size is `V`, then:

```text
Dimension of each word's OHE vector = V
```

For example, if a vocabulary contains 20,000 unique words, each word's OHE vector has 20,000 dimensions.

### Sentence Representation

Consider:

```text
"I Love NLP"
```

Its individual word vectors are:

```text
I     = [1, 0, 0, 0]
Love  = [0, 1, 0, 0]
NLP   = [0, 0, 1, 0]
```

If we combine these vectors using element-wise addition:

```text
[1, 1, 1, 0]
```

This is a multi-hot representation when each word occurs only once.

If a word repeats, its count can become greater than 1. A binary presence representation would keep the value as 1.

**Important distinction:**
- One-hot vector: Represents one category or token with exactly one active position.
- Multi-hot vector: Represents multiple categories or tokens with multiple active positions.
- Count vector: Represents how many times each word occurs.

## 4. Advantages of One-Hot Encoding

### 4.1 No Artificial Ordinal Relationship

OHE does not assign arbitrary numerical ordering to categories.

For example, Red, Blue and Green are represented independently rather than as 0, 1 and 2.

### 4.2 Simple and Easy to Understand

It is straightforward to implement and interpret. Each binary column represents a specific category.

### 4.3 Compatible with Many ML Algorithms

OHE provides numerical input suitable for algorithms such as:

- Logistic Regression
- Linear Regression
- Support Vector Machines
- Neural Networks
- Naive Bayes

### 4.4 Preserves Category Identity

Each category receives a unique representation, so different categories are not confused with one another.

## 5. Disadvantages of One-Hot Encoding

### 5.1 High Dimensionality

The number of dimensions increases with the number of unique categories.

For example:

```text
Vocabulary size = 50,000
OHE vector dimension = 50,000
```

For large NLP vocabularies, this creates extremely high-dimensional feature representations.

### 5.2 Sparse Representation

Most values in an OHE vector are zero.

For example, with a vocabulary of 10,000 words, an individual word's OHE vector contains:

- One `1`
- 9,999 `0`s

This is called a sparse representation.

Storing these vectors as ordinary dense arrays can waste memory. Sparse matrix formats can reduce storage requirements.

### 5.3 No Semantic Relationship

OHE cannot represent semantic similarity between words.

For example:

```text
King   = [1, 0, 0, 0]
Queen  = [0, 1, 0, 0]
Apple  = [0, 0, 1, 0]
```

All three vectors are equally distant under common distance measures such as Euclidean distance.

However, semantically, King and Queen are more closely related than King and Apple.

OHE does not capture this relationship.

### 5.4 Unseen Categories

Suppose the training vocabulary contains:

```text
["I", "Love", "NLP"]
```

But a new document contains:

```text
"Python"
```

Python is not part of the existing vocabulary, so it has no predefined OHE position.

An NLP system needs an explicit strategy, such as an unknown-token (`UNK`/`OOV`) representation or a tokenizer that can handle unseen words.

### 5.5 Computational Cost

High-dimensional representations can increase memory consumption and computational requirements, especially when dense vectors are used.

## 6. One-Hot Encoding vs Word Embeddings

| Property | One-Hot Encoding | Word Embeddings |
|---|---|---|
| Representation | Binary vector | Dense numerical vector |
| Dimensionality | Vocabulary size | Fixed embedding size |
| Values | Mostly 0s, one 1 | Usually continuous values |
| Semantic meaning | Not captured | Can capture semantic relationships |
| Sparsity | Sparse | Dense |
| Example |  `[0, 1, 0, 0]` | `[0.21, -0.45, 0.78, ...]` |

Word embeddings represent words in a lower-dimensional continuous vector space. They can capture relationships and similarities between words.

Examples of embedding approaches include Word2Vec, GloVe and FastText. Transformer models later introduced contextual representations, where a word's representation can depend on its surrounding context.

## 7. When Should We Use One-Hot Encoding?

OHE is useful when:

- A categorical feature has a relatively small number of unique categories.
- We need a simple numerical representation.
- We do not want to introduce artificial ordinal relationships.
- We are working with traditional ML models that require numerical features.

For NLP, OHE is useful for understanding basic numerical text representations, but it is generally not the preferred approach for representing large vocabularies in modern NLP systems.

## 8. Key Takeaways

1. One-Hot Encoding converts categories into binary vectors.
2. Each category gets a separate position in the vector.
3. Each individual OHE vector contains exactly one `1`.
4. Vector dimensionality equals the number of unique categories.
5. OHE does not introduce an artificial numerical ordering.
6. OHE produces sparse, potentially high-dimensional representations.
7. OHE does not capture semantic similarity between words.
8. Multi-hot and count vectors can represent multiple words in a document.
9. Word embeddings address some of OHE's limitations by learning dense vector representations.
10. OHE is useful for categorical data with manageable cardinality, but can be inefficient for large NLP vocabularies.