# Word2Vec – Skip-Gram Architecture

## 1. What is Skip-Gram?

Skip-Gram is one of the two architectures of Word2Vec.

It learns word embeddings by predicting the surrounding context words given a target (center) word.

In simple terms:

**Input:** Target word  
**Output:** Surrounding context words

The objective is to maximize the probability of predicting the actual context words given the target word.

`P(Context Words | Target Word)`

## 2. Basic Intuition

Consider the sentence:

`I love machine learning`

Assume the context window size is 1.

For the target word `love`, its surrounding context words are:

- Left context: I
- Right context: machine

Unlike CBOW, Skip-Gram uses the target word as input and predicts its surrounding context words.

Therefore, the training pairs become:

- `love → I`
- `love → machine`

Each target-context pair represents an individual prediction task.

## 3. Understanding the Context Window

The context window determines how many words surrounding the target word are considered during training.

For example:

`I love machine learning`

If the target word is `love`:

| Window Size | Context Words |
|---|---|
| 1 | I, machine |
| 2 | I, machine, learning |

A larger window considers more surrounding words.

**Important:** The window size is a hyperparameter selected before training.

## 4. Skip-Gram Architecture

Skip-Gram consists of three main components:

1. Input Layer
2. Projection Layer (Hidden Layer)
3. Output Layer

### 4.1 Input Layer

The input consists of a single target word.

Each target word is represented using a one-hot encoded vector.

Consider the vocabulary:

`[I, love, machine, learning]`

Vocabulary size (V) = 4.

For the training pair:

`love → I`

The one-hot representation of `love` is:

`[0, 1, 0, 0]`

Each input vector has V dimensions.

### 4.2 Input Embedding Matrix (W)

The model contains an input embedding matrix W.

Its dimensions are:

`W = V × D`

Where:

- V = Vocabulary size
- D = Embedding dimension

For example, if V = 4 and D = 3:

`W = 4 × 3`

Each row of W represents the input embedding of one vocabulary word.

The one-hot input vector selects the corresponding row from W.

For example:

`One-hot(love) × W = Embedding(love)`

The same W matrix is shared across all training examples.

### 4.3 Projection Layer (Hidden Layer)

The selected embedding of the target word is passed to the projection layer.

For example:

`Embedding(love) = [0.2, 0.4, 0.6]`

This becomes the hidden representation:

`h = [0.2, 0.4, 0.6]`

Unlike CBOW, Skip-Gram does not average multiple context embeddings because it has only one target word as input.

The hidden representation has D dimensions.

### 4.4 Output Layer

The hidden representation is multiplied by the output weight matrix W'.

Its dimensions are:

`W' = D × V`

For example:

`W' = 3 × 4`

The multiplication is:

`h (1 × 3) × W' (3 × 4) = Scores (1 × 4)`

The result contains one score for every possible context word in the vocabulary.

These scores are called logits.

### 4.5 Softmax Layer

The logits are passed through the Softmax function to convert them into probabilities.

Softmax formula:

`P(w_i) = exp(z_i) / Σ exp(z_j)`

Where:

- z_i = Logit of a particular word
- The denominator sums the exponentials of all vocabulary logits.

The resulting probabilities sum to 1.

For the training pair:

`love → I`

The objective is to increase:

`P(I | love)`

Similarly, for the second training pair:

`love → machine`

The objective is to increase:

`P(machine | love)`

## 5. Complete Skip-Gram Training Pipeline

Consider:

`I love machine learning`

Target word: `love`

Context words: `I`, `machine`

The training process:

1. Select a target word from the corpus.
2. Identify its surrounding context words using the context window.
3. Generate individual target-context training pairs.
4. Convert the target word into a one-hot vector.
5. Use the input embedding matrix W to retrieve its embedding.
6. Pass the embedding through W'.
7. Calculate logits for all vocabulary words.
8. Apply Softmax to obtain probabilities.
9. Calculate the loss using the actual context word.
10. Perform backpropagation to calculate gradients.
11. Update W and W' using an optimizer.

The process repeats across training pairs to learn useful word representations.

## 6. Loss Function

Skip-Gram commonly uses categorical cross-entropy loss with Softmax.

For one target-context pair:

`Loss = -log(P(actual context word | target word))`

For example:

`love → I`

The model tries to maximize the probability of predicting `I` given `love`.

If multiple context words exist, each target-context pair contributes an individual prediction loss.

The total loss can be calculated by summing or averaging the losses across the context pairs.

The objective is to minimize the loss.

## 7. What Gets Updated During Training?

Both W and W' are trainable weight matrices.

For a single Skip-Gram training pair:

`love → I`

- The input embedding row corresponding to `love` receives gradients.
- The output weight matrix receives gradients based on the prediction error.
- The input embedding row corresponding to `I` is not directly updated merely because it is the output target in this pair.

For example, consider:

`love → I`

The input embedding row for `love` is involved in the input-side update.

The output-side weights are updated to improve the prediction of `I`.

For the next pair:

`love → machine`

The same input embedding row for `love` receives another learning signal.

**Important:** With Full Softmax, gradients can affect all output vocabulary columns. With Negative Sampling, only the positive context word and sampled negative output columns are involved in that training objective.

## 8. Why Is Skip-Gram Often Better for Rare Words?

Skip-Gram can be effective for rare words because each occurrence of a target word can generate multiple target-context training pairs.

Consider:

`The cat guzzles milk`

Assume the target word is `guzzles` and window size is 1.

The training pairs are:

- `guzzles → cat`
- `guzzles → milk`

Both prediction tasks train the input embedding of `guzzles`.

Therefore, even one occurrence of a rare word can provide multiple learning signals to its input embedding.

In CBOW, the same word appearing as a target does not directly update its input embedding row for that example.

This is one reason Skip-Gram can perform well on rare words.

## 9. Advantages of Skip-Gram

1. **Rare Word Learning:** Can learn useful representations for rare words because one target occurrence generates multiple context prediction tasks.
2. **Individual Context Learning:** Each context word provides a separate prediction signal.
3. **Flexible Context Learning:** Learns relationships between a target word and its surrounding words.
4. **Useful Semantic Relationships:** Can learn meaningful word relationships from large text corpora.

## 10. Limitations of Skip-Gram

1. **More Training Examples:** Each target word can generate multiple target-context pairs.
2. **Slower Training:** It can require more computation than CBOW, particularly with Full Softmax.
3. **Static Embeddings:** A word generally has one learned embedding regardless of its sentence context.
4. **Context Independence:** It does not explicitly preserve the order of surrounding context words in its prediction objective.

## 11. Key Takeaways

- Skip-Gram is a Word2Vec architecture.
- It predicts surrounding context words using a target word.
- Each target-context pair represents an individual prediction task.
- W is the input embedding matrix with dimensions V × D.
- W' is the output weight matrix with dimensions D × V.
- Softmax converts output logits into probabilities.
- Cross-entropy loss measures prediction error.
- Backpropagation and optimization update the trainable weights.
- Skip-Gram can be effective for rare words because one target occurrence generates multiple training pairs.
