# Comparison of Word Embedding Methods

## 1. Overview

Word2Vec, GloVe, and FastText are traditional word embedding techniques used to convert words into dense, low-dimensional numerical vectors.

They differ in how they learn word representations and how they handle rare words, unseen words, and subword information.

## 2. Overall Comparison

| Feature | CBOW | Skip-Gram | GloVe | FastText |
|---|---|---|---|---|
| Approach | Predictive | Predictive | Count-based | Predictive |
| Input | Context words | Target word | Co-occurrence matrix | Word + subwords |
| Prediction | Target word | Context words | No direct word prediction | Target/context prediction |
| Architecture | Word2Vec | Word2Vec | Matrix-based objective | Word2Vec-style |
| Main information | Local context | Local context | Global co-occurrence statistics | Context + character n-grams |
| Subword information | No | No | No | Yes |
| Static embeddings | Yes | Yes | Yes | Yes |
| OOV handling | Limited | Limited | Limited | Better |
| Polysemy handling | No | No | No | No |

**Note:** CBOW and Skip-Gram are two architectures of Word2Vec, not separate embedding algorithms.

## 3. CBOW vs Skip-Gram

Both are Word2Vec architectures.

### CBOW (Continuous Bag of Words)

- Uses surrounding context words to predict the target word.
- Combines context embeddings, usually through averaging.
- Generally faster to train.
- Often performs well for frequent words.

Example:

`[doctor, works, a] → hospital`

**When to use:**
- When training speed is important.
- When the corpus contains many frequent words.
- When a computationally efficient Word2Vec model is required.

### Skip-Gram

- Uses the target word to predict surrounding context words.
- Generates multiple training pairs from one target word occurrence.
- Often performs better for rare words.
- Can require more training time.

Example:

`hospital → doctor, works, a`

**When to use:**
- When rare-word representation is important.
- When the dataset is relatively small or medium-sized and more training time is acceptable.
- When learning detailed word-context relationships is important.

## 4. Word2Vec vs GloVe

| Aspect | Word2Vec | GloVe |
|---|---|---|
| Learning approach | Predictive | Count-based |
| Training mechanism | Predict words using context | Fit global co-occurrence statistics |
| Main objective | Prediction loss | Weighted least squares |
| Context information | Local prediction examples | Global co-occurrence statistics |
| Architectures | CBOW and Skip-Gram | Neither CBOW nor Skip-Gram |

### When to Use Word2Vec?

- When learning word relationships through context prediction.
- When CBOW or Skip-Gram architecture is suitable.
- When a predictive embedding approach is preferred.

### When to Use GloVe?

- When global word co-occurrence statistics are useful.
- When working with a sufficiently large corpus from which co-occurrence statistics can be collected.
- When a count-based embedding approach is preferred.

**Important:** Word2Vec also trains on the entire corpus. The difference is not that Word2Vec uses only local data and GloVe uses the entire corpus. The main difference is their learning objective and how they model co-occurrence information.

## 5. FastText vs Word2Vec

| Aspect | Word2Vec | FastText |
|---|---|---|
| Word representation | Whole-word embedding | Whole-word + subword embeddings |
| Character n-grams | No | Yes |
| Rare words | Limited handling | Better handling |
| OOV words | Cannot normally construct a learned vector | Can construct vectors using available subword embeddings |
| Morphological information | Not explicitly modeled | Captured through character n-grams |

### When to Use FastText?

- When the corpus contains many rare words.
- When unseen words are likely to appear during inference.
- When words have many morphological variations.
- When working with morphologically rich languages.

Example:

Words: `play`, `playing`, `played`, `player`

FastText can share information through their common character n-grams.

## 6. Which Problems Do These Methods Solve?

| Problem | CBOW | Skip-Gram | GloVe | FastText |
|---|---|---|---|---|
| One-hot encoding sparsity | Yes | Yes | Yes | Yes |
| Dense vector representations | Yes | Yes | Yes | Yes |
| Semantic relationships | Yes | Yes | Yes | Yes |
| Rare-word handling | Limited | Often better | Depends on counts | Better through subwords |
| OOV word representation | No | No | No | Yes, when useful subword information is available |
| Polysemy | No | No | No | No |
| Context-dependent embeddings | No | No | No | No |

### Understanding the Limitations

**1. OOV (Out-of-Vocabulary) Problem**

A word is OOV when it is not present in the model's training vocabulary.

- Word2Vec: Does not normally generate an embedding for an unseen word.
- GloVe: Does not normally generate an embedding for an unseen word.
- FastText: Can construct an embedding using character n-grams.

**2. Polysemy Problem**

Polysemy means a word has multiple meanings.

Example:

- I deposited money in the bank.
- He sat near the river bank.

All four methods use a static representation for the word `bank`. They do not generate separate contextual representations for its different meanings.

**3. Contextual Embeddings**

Models such as BERT generate word representations based on the surrounding sentence.

For example, the representation of `bank` can differ between financial and river-related contexts.

## 7. Practical Selection Guide

| Requirement | Recommended approach |
|---|---|
| Faster Word2Vec training | CBOW |
| Better handling of rare words in Word2Vec | Skip-Gram |
| Global co-occurrence-based learning | GloVe |
| Rare and unseen word handling | FastText |
| Morphological information | FastText |
| Context-dependent word meanings | BERT or other contextual embedding models |

These are general selection guidelines, not absolute rules. Actual performance depends on corpus size, language, vocabulary, hyperparameters, and the downstream task.
