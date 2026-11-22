# FastText

## 1. What is FastText?

FastText is a word embedding technique developed by Facebook AI Research (FAIR).

It is an extension of the Word2Vec approach that learns word representations using both:

- Whole-word information.
- Subword information (character n-grams).

Its main advantage is that it can generate representations for unseen words using their character n-grams.

## 2. Character N-grams

FastText divides words into smaller character groups called character n-grams.

Example:

Word: `where`

After adding boundary markers:

`<where>`

For n = 3, character n-grams are:

- `<wh`
- `whe`
- `her`
- `ere`
- `re>`

Here, n represents the number of characters in each n-gram.

## 3. How Does FastText Work?

1. A word is divided into character n-grams.
2. Embeddings are learned for these subword units.
3. The word's own embedding and its subword embeddings are combined to create its representation.
4. The resulting representation is used for word prediction.
5. Prediction errors are used to update the embeddings through backpropagation.

**Architecture:** FastText uses Word2Vec-style predictive architectures:

- CBOW: Context words predict the target word.
- Skip-Gram: Target word predicts context words.

The key difference is that FastText incorporates character n-gram embeddings into the word representation.

## 4. Handling Out-of-Vocabulary (OOV) Words

Suppose the training vocabulary contains:

- playing
- played
- player

But the word `playingly` is not present in the training vocabulary.

Word2Vec and GloVe generally cannot provide a learned vector for this unseen word.

FastText can generate its character n-grams and combine their learned embeddings to construct a representation.

This works because some of its subword patterns may have appeared during training.

## 5. Advantages

- Better handling of unseen words.
- Captures subword and morphological information.
- Useful for rare words.
- Particularly useful for morphologically rich languages.

## 6. Limitations

- Produces static embeddings.
- Does not independently solve the polysemy problem.
- Requires additional storage for character n-gram embeddings.
- Similar spelling does not necessarily mean similar semantics.

## 7. Word2Vec vs GloVe vs FastText

| Feature | Word2Vec | GloVe | FastText |
|---|---|---|---|
| Approach | Predictive | Count-based | Predictive |
| Main information | Word context | Global co-occurrence | Word context + subwords |
| Representation | Whole-word embedding | Whole-word embedding | Whole-word + subword embeddings |
| OOV handling | Limited | Limited | Better |
| Static embeddings | Yes | Yes | Yes |

## 8. Key Takeaway

FastText extends the Word2Vec approach by incorporating character n-gram information into word representations.

It is especially useful for rare and unseen words because it can construct their representations using learned subword embeddings.