# TF-IDF (Term Frequency–Inverse Document Frequency)

## 1. Introduction

TF-IDF (Term Frequency–Inverse Document Frequency) is a statistical feature extraction technique used in Natural Language Processing (NLP) to convert text documents into numerical representations based on the importance of words.

It assigns a numerical weight to each word in a document by considering:

1. How frequently the word appears in a particular document.
2. How common or rare the word is across the entire corpus.

### Intuition

Consider a collection of documents:

- Document 1: "I love machine learning"
- Document 2: "I love deep learning"
- Document 3: "I love Python"

Words such as `I` and `love` appear in multiple documents. Therefore, they may not be particularly useful for distinguishing one document from another.

However, words such as `machine`, `deep`, and `Python` are more distinctive because they appear in fewer documents.

TF-IDF gives:
- Higher importance to words that are frequent in a particular document but relatively rare across the corpus.
- Lower importance to words that appear frequently across many documents.

**Key Idea:** TF-IDF identifies words that are statistically important for distinguishing documents within a corpus.

---

## 2. Components of TF-IDF

TF-IDF consists of two components:

1. Term Frequency (TF)
2. Inverse Document Frequency (IDF)

### 2.1 Term Frequency (TF)

Term Frequency measures how frequently a particular word appears in a document relative to the total number of terms in that document.

**Formula:**

`TF(t, d) = Count of term t in document d / Total number of terms in document d`

Where:
- `t` = Term or word.
- `d` = Document.

**Example:**

Consider the document:

`I love machine learning and I love Python`

Total number of words = 8.

| Term | Frequency | TF |
|---|---:|---:|
| I | 2 | 2/8 = 0.25 |
| love | 2 | 2/8 = 0.25 |
| machine | 1 | 1/8 = 0.125 |
| learning | 1 | 1/8 = 0.125 |
| Python | 1 | 1/8 = 0.125 |

**Interpretation:**

A word that appears more frequently in a document generally receives a higher TF value.

However, TF alone cannot determine whether a word is important across the entire corpus.

For example, common words may have high TF values but may not help distinguish documents.

This is why IDF is required.

### 2.2 Inverse Document Frequency (IDF)

Inverse Document Frequency measures how rare or common a term is across the entire collection of documents (corpus).

**Formula:**

`IDF(t) = log(Total number of documents / Number of documents containing term t)`

Where:
- `t` = Term or word.
- Total number of documents = Number of documents in the corpus.
- Number of documents containing term t = Number of documents in which the term appears at least once.

**Example:**

Suppose a corpus contains 5 documents.

| Term | Documents containing term | IDF |
|---|---:|---:|
| learning | 5 | log(5/5) = 0 |
| Python | 1 | log(5/1) |
| machine | 2 | log(5/2) |
| data | 3 | log(5/3) |

**Interpretation:**

- If a word appears in every document, its IDF becomes 0 using this formula.
- If a word appears in fewer documents, its IDF becomes higher.
- Rare words receive higher IDF values than common words.

**Why is it called Inverse Document Frequency?**

Because the IDF value decreases as the number of documents containing a term increases.

Note: This is the basic unsmoothed IDF formula. Practical implementations often use smoothing to handle zero values and adjust the weighting.

---

## 3. TF-IDF Calculation

TF-IDF combines Term Frequency and Inverse Document Frequency to calculate the importance of a word in a particular document.

**Formula:**

`TF-IDF(t, d) = TF(t, d) × IDF(t)`

Where:
- TF measures the frequency of a term within a document.
- IDF measures how distinctive the term is across the corpus.

### Example

Suppose:
- Total documents = 5.
- The word `Python` appears in only 1 document.
- That document contains 10 words.
- `Python` appears once.

Therefore:

`TF = 1/10 = 0.1`

`IDF = log(5/1) = log(5)`

`TF-IDF = 0.1 × log(5)`

The resulting TF-IDF value represents the importance of `Python` in that document according to the selected weighting formula.

### Important Interpretation

A high TF-IDF score generally indicates that:
- The word appears relatively frequently in the document.
- The word appears in relatively few documents across the corpus.

A low TF-IDF score generally indicates that:
- The word is relatively uncommon in the particular document, or
- The word appears across many documents.

---

## 4. How TF-IDF Works

The overall workflow:

1. **Document Collection:** Collect a set of text documents forming a corpus.
2. **Preprocessing:** Perform required text preprocessing, such as tokenization and optional stopword removal.
3. **Vocabulary Creation:** Identify unique terms across the corpus.
4. **Term Frequency Calculation:** Calculate the frequency of each term in every document.
5. **Inverse Document Frequency Calculation:** Calculate how common or rare each term is across the corpus.
6. **TF-IDF Calculation:** Multiply TF and IDF to obtain the final weight for each term.
7. **Document Representation:** Represent each document as a numerical vector containing TF-IDF weights.

The resulting vectors can be used as input features for traditional machine learning algorithms.

---

## 5. Document-Term Matrix (DTM) in TF-IDF

TF-IDF represents a collection of documents using a weighted Document-Term Matrix.

- Rows represent documents.
- Columns represent unique terms in the vocabulary.
- Values represent TF-IDF weights instead of raw word counts.

For example:

| Document | Machine | Learning | Python |
|---|---:|---:|---:|
| D1 | 0.65 | 0.45 | 0.00 |
| D2 | 0.00 | 0.45 | 0.72 |
| D3 | 0.58 | 0.00 | 0.72 |

The values above are illustrative.

Each row represents one document as a fixed-length numerical vector.

**Vector Dimension = Vocabulary Size**

For example, if the vocabulary contains 5,000 unique terms, each document is represented by a vector containing 5,000 features.

### Important Point

TF-IDF creates a document-level vector, but it does not preserve the original positions or sequence of words when using unigram features.

---

## 6. TF-IDF and Word Ordering

Standard unigram TF-IDF does not maintain word order.

Consider:

- Document 1: `Dog bites man`
- Document 2: `Man bites dog`

Both documents contain the same words.

Their unigram TF-IDF vectors will be identical because the same terms receive the same weights.

TF-IDF represents the importance of terms, not their original positions in the sentence.

### How Can Word Order Be Captured?

TF-IDF can also work with N-Gram features.

| Feature Type | Example |
|---|---|
| Unigram | Dog, bites, man |
| Bigram | Dog bites, bites man |
| Trigram | Dog bites man |

Using bigrams or trigrams allows TF-IDF to capture local word-order patterns.

However, N-Grams still do not provide complete contextual or semantic understanding.

---

## 7. Advantages of TF-IDF

1. **Reduces the Impact of Common Words:** Words appearing across many documents receive lower weights, reducing their influence.

2. **Highlights Important Terms:** Identifies distinctive words that can help differentiate documents.

3. **Simple and Efficient:** Easy to understand and computationally efficient for many traditional NLP tasks.

4. **Useful for Document Similarity:** TF-IDF vectors can be compared using cosine similarity to identify similar documents.

5. **Useful for Text Classification:** Can be used as input features for algorithms such as Logistic Regression, Naive Bayes, SVM, and other traditional ML models.

---

## 8. Disadvantages of TF-IDF

1. **No Semantic Understanding:** TF-IDF cannot understand that words such as `car` and `automobile` have similar meanings. They are treated as separate features.

2. **No Contextual Understanding:** The same word receives the same corpus-level IDF and document-level TF calculation regardless of its intended meaning in different contexts.

   Example:
   - Bank of a river.
   - Bank where money is deposited.

   TF-IDF cannot distinguish these meanings by itself.

3. **Loss of Word Order:** Standard unigram TF-IDF ignores the sequence and grammatical structure of words.

   Example:
   - `Dog bites man`
   - `Man bites dog`

   Both can produce identical unigram representations.

4. **High Dimensionality:** The feature dimension depends on the vocabulary size. A large corpus can produce thousands or millions of features.

5. **Sparse Representation:** Most documents contain only a small subset of the complete vocabulary, resulting in many zero values.

6. **Rare but Unimportant Words Can Receive High Weights:** Misspellings, unusual terms, or irrelevant words appearing in very few documents may receive high IDF values.

7. **No Understanding of Relationships Between Words:** TF-IDF treats each vocabulary term as an independent feature and does not learn semantic relationships between terms.

---

## 9. Applications of TF-IDF

### 1. Information Retrieval
Used to represent documents and rank potentially relevant results for a search query.

### 2. Document Similarity
TF-IDF vectors can be compared using cosine similarity to identify documents containing similar terms with similar importance.

### 3. Search Engines
Can help identify and rank documents based on the importance of query terms.

### 4. Text Classification
Used as numerical input features for tasks such as spam detection, sentiment classification, and news categorization.

### 5. Document Clustering
Can be used with clustering algorithms to group documents based on their textual features.

### 6. Keyword Extraction
Words with relatively high TF-IDF scores can be considered candidate keywords for a document.

---

## 10. TF-IDF vs Bag of Words (BoW)

| Feature | Bag of Words | TF-IDF |
|---|---|---|
| Main idea | Represents word frequency or presence | Represents weighted word importance |
| Common words | Can receive high counts | Generally receive lower weights |
| Rare words | May have low frequency | Can receive higher weights |
| Values | Binary or integer counts | Usually decimal weights |
| Word order | Not preserved in unigram BoW | Not preserved in unigram TF-IDF |
| Semantic understanding | No | No |
| Contextual understanding | No | No |
| Document representation | Numerical vector | Weighted numerical vector |

**Key Difference:**

BoW represents documents using word presence or frequency, whereas TF-IDF adjusts word frequency based on how common or rare a word is across the corpus.

---

## 11. TF-IDF with Cosine Similarity

TF-IDF and cosine similarity are commonly used together in document similarity and information retrieval tasks.

Their responsibilities are different:

**TF-IDF:**
- Converts documents into numerical vectors.
- Assigns weights to terms based on their importance.

**Cosine Similarity:**
- Compares two numerical vectors.
- Measures the cosine of the angle between them.
- Helps determine how similar the document representations are.

**Formula:**

`Cosine Similarity(A, B) = (A · B) / (||A|| × ||B||)`

Where:
- A and B are document vectors.
- A · B represents the dot product.
- ||A|| and ||B|| represent the magnitudes of the vectors.

For non-negative TF-IDF vectors, cosine similarity generally ranges from 0 to 1.

### Applications of This Combination

- Document similarity.
- Search result ranking.
- Duplicate document detection.
- Article and content recommendation.
- Finding relevant documents for a user query.

**Important:** TF-IDF does not calculate similarity itself. It generates numerical representations, while cosine similarity compares those representations.

---

## 12. Limitations and Possible Improvements

| Limitation | Possible Improvement |
|---|---|
| Loss of word order | N-Gram features |
| No semantic understanding | Word embeddings |
| No contextual understanding | Contextual embeddings such as BERT |
| High dimensionality | Feature selection or dimensionality reduction |
| Large sparse vocabulary | Efficient sparse matrix representation |

TF-IDF remains useful for many traditional NLP applications, but it does not replace semantic or contextual text representations.

---

## 13. Key Takeaways

- TF-IDF stands for Term Frequency–Inverse Document Frequency.
- TF measures how frequently a word appears in a particular document.
- IDF measures how common or rare a word is across the corpus.
- TF-IDF combines both components to calculate term importance.
- Higher TF-IDF generally indicates a more distinctive term within a document.
- TF-IDF represents documents as weighted numerical vectors.
- Standard unigram TF-IDF does not preserve word order.
- N-Gram TF-IDF can capture local word-order patterns.
- TF-IDF does not understand semantic relationships or contextual meanings.
- TF-IDF vectors are commonly compared using cosine similarity.

**Final Intuition:**

BoW tells us how frequently words appear in a document, whereas TF-IDF tells us how statistically important those words are for distinguishing that document from the rest of the corpus.