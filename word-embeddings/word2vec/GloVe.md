# GloVe (Global Vectors for Word Representation)

## 1. What is GloVe?

GloVe is a **count-based word embedding technique** that learns dense, low-dimensional vector representations of words using global word co-occurrence statistics from a corpus.

The main idea is:

> Words that frequently appear in similar contexts tend to have related vector representations.

Unlike Word2Vec, which learns embeddings through a prediction task, GloVe learns embeddings by analyzing word co-occurrence statistics across the corpus.

## 2. Distributional Information

GloVe is based on the Distributional Hypothesis:

**Words appearing in similar contexts tend to have similar meanings.**

For example:

- Doctor frequently appears with hospital, patient, nurse, and medicine.
- Nurse frequently appears with hospital, patient, doctor, and medicine.
- Player frequently appears with football, team, match, and ground.

Doctor and nurse have similar context patterns. GloVe uses these patterns to learn meaningful word representations.

## 3. Co-occurrence Matrix

The first step in GloVe is constructing a co-occurrence matrix.

A co-occurrence matrix stores how frequently two words appear together within a predefined context window in a corpus.

### Example

Consider the following corpus:

- The doctor works in a hospital.
- The nurse works in a hospital.
- The doctor treats a patient.
- The player plays football.

After processing the corpus using a context window, suppose we obtain the following illustrative matrix:

| Word | Hospital | Patient | Football |
|---|---:|---:|---:|
| Doctor | 40 | 30 | 2 |
| Nurse | 35 | 25 | 1 |
| Player | 1 | 2 | 45 |

Interpretation:

- Doctor and hospital have a co-occurrence count of 40.
- Doctor and patient have a count of 30.
- Player and football have a count of 45.

These counts represent how frequently the corresponding word pairs occur within the chosen context window.

**Important:**
- Rows represent center words.
- Columns represent context words.
- Values represent co-occurrence counts.
- The exact matrix depends on the corpus, vocabulary, context window, and counting strategy.

### Why is the Co-occurrence Matrix Important?

The matrix captures the contextual relationships between words.

For example:

- Doctor and nurse have similar co-occurrence patterns.
- Player has a very different co-occurrence pattern.

GloVe uses these global patterns to learn word embeddings.

## 4. How Does GloVe Learn Word Embeddings?

Once the co-occurrence matrix is constructed, GloVe learns a vector representation for every word in the vocabulary.

Suppose we want to represent every word using a 2-dimensional vector.

Initially, the word vectors are randomly initialized.

Example:

| Word | Dimension 1 | Dimension 2 |
|---|---:|---:|
| Doctor | 0.2 | 0.8 |
| Nurse | 0.7 | 0.1 |
| Player | 0.3 | 0.4 |

These are illustrative initial values and do not yet represent meaningful relationships.

GloVe repeatedly adjusts these vectors during training so that they capture information from the co-occurrence matrix.

The objective is to make the learned word representations reflect the observed co-occurrence patterns.

## 5. GloVe Objective Function

GloVe tries to learn word vectors such that their dot product, along with bias terms, approximates the logarithm of their co-occurrence count.

The objective is:

`w_i · w̃_j + b_i + b̃_j ≈ log(X_ij)`

Where:

- `w_i` = Vector of the center word.
- `w̃_j` = Vector of the context word.
- `b_i` = Bias associated with the center word.
- `b̃_j` = Bias associated with the context word.
- `X_ij` = Co-occurrence count of word i and word j.
- `log(X_ij)` = Logarithm of the co-occurrence count.
- `·` = Dot product between two vectors.

### Why Use Logarithm?

Co-occurrence counts can vary significantly.

For example:

- Word pair A has a count of 10.
- Word pair B has a count of 1,000.
- Word pair C has a count of 100,000.

Using raw counts can create a very large numerical range.

Taking the logarithm compresses this range:

`log(10) ≈ 2.30`

`log(1000) ≈ 6.91`

`log(100000) ≈ 11.51`

This makes the learning objective easier to optimize and reduces the influence of extremely large counts.

### Why Are Bias Terms Used?

Bias terms allow the model to account for individual word-related effects that are not captured by the vector dot product alone.

They provide additional flexibility when fitting the co-occurrence statistics.

## 6. Weighted Least Squares Objective

GloVe does not treat every co-occurrence count equally.

It uses a weighting function to reduce the influence of extremely frequent and very rare word pairs.

The loss function is:

`J = Σ f(X_ij) [w_i · w̃_j + b_i + b̃_j - log(X_ij)]²`

Where:

- `J` = Total training loss.
- `f(X_ij)` = Weighting function.
- The expression inside the square measures the difference between the learned value and the observed log co-occurrence count.

The model learns by minimizing this loss.

### Why Use a Weighting Function?

- Very frequent word pairs should not dominate the training process.
- Extremely rare word pairs may contain unreliable information.
- The weighting function balances the contribution of different co-occurrence counts.

The original GloVe weighting function is:

`f(x) = (x / x_max)^α` if `x < x_max`

`f(x) = 1` otherwise.

Here, `x_max` and `α` are hyperparameters controlling the weighting behavior.

## 7. Training Process Summary

The complete GloVe training process:

1. Collect a text corpus.
2. Build a vocabulary.
3. Define a context window.
4. Construct the word co-occurrence matrix.
5. Initialize center-word and context-word vectors.
6. Calculate the objective using dot products, bias terms, and log co-occurrence counts.
7. Apply the weighting function.
8. Minimize the loss using an optimization algorithm.
9. Extract the learned word vectors.

The resulting vectors are dense, low-dimensional representations of words.

## 8. Word2Vec vs GloVe

Both Word2Vec and GloVe learn dense word embeddings, but their learning approaches differ.

| Aspect | Word2Vec | GloVe |
|---|---|---|
| Approach | Predictive | Count-based |
| Main idea | Predict words using context | Learn from co-occurrence statistics |
| Learning objective | Prediction objective | Weighted least squares objective |
| Information | Local context prediction examples | Global co-occurrence statistics |
| Architectures | CBOW and Skip-Gram | No CBOW or Skip-Gram architecture |
| Output | Dense word vectors | Dense word vectors |
