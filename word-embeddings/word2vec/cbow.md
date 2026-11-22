# Word2Vec – CBOW (Continuous Bag of Words)

## 1. What is CBOW?

CBOW (Continuous Bag of Words) is one of the two architectures of Word2Vec.

It learns word embeddings by predicting a target (center) word using its surrounding context words.

In simple terms:

**Input:** Surrounding context words  
**Output:** Target word

The objective is to maximize the probability of predicting the correct target word given its context words.

`P(Target Word | Context Words)`

## 2. Basic Intuition

Consider the sentence:

`I love machine learning`

Assume the context window size is 1. 

For the target word `love`, its surrounding context words are:

- Left context: I
- Right context: machine

Therefore, the training example becomes:

`[I, machine] → love`

The model receives the context words `I` and `machine` and tries to predict the target word `love`.

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

## 4. CBOW Architecture

CBOW consists of three main components:

1. Input Layer
2. Projection Layer (Hidden Layer)
3. Output Layer

### 4.1 Input Layer

The input consists of the surrounding context words.

Each context word is represented using a one-hot encoded vector.

Consider the vocabulary:

`[I, love, machine, learning]`

Vocabulary size (V) = 4

For the training example:

`[I, machine] → love`

One-hot representations:

- I = [1, 0, 0, 0]
- machine = [0, 0, 1, 0]

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

The one-hot vector selects the corresponding row from W.

For example:

`One-hot(I) × W = Embedding(I)`

`One-hot(machine) × W = Embedding(machine)`

The same W matrix is shared across all training examples.

### 4.3 Projection Layer (Hidden Layer)

In CBOW, the embeddings of all context words are combined by taking their average.

Suppose:

`Embedding(I) = [0.2, 0.4, 0.6]`

`Embedding(machine) = [0.4, 0.2, 0.8]`

The combined context representation is:

`h = ([0.2, 0.4, 0.6] + [0.4, 0.2, 0.8]) / 2`

`h = [0.3, 0.3, 0.7]`

The resulting vector has D dimensions. 

**Why do we take the average?**

The model needs one fixed-size representation of all context words.

Averaging combines their embedding information into a single context representation, regardless of the number of context words.

This is why it is called a Bag of Words approach: the model combines context embeddings without preserving their original order.

### 4.4 Output Layer

The combined context vector is passed through the output weight matrix W'.

Its dimensions are:

`W' = D × V`

Where:

- D = Embedding dimension
- V = Vocabulary size

For example:

`W' = 3 × 4`

The multiplication is:

`h (1 × 3) × W' (3 × 4) = Scores (1 × 4)`

The output contains one score for each word in the vocabulary.

These scores are called logits.

### 4.5 Softmax Layer

The logits are passed through the Softmax function to convert them into probabilities.

Softmax formula:

`P(w_i) = exp(z_i) / Σ exp(z_j)`

Where:

- z_i = Logit of a particular word
- The denominator sums the exponentials of all vocabulary logits.

The resulting probabilities sum to 1.

The model predicts the word with the highest probability.

For our example, the target word is `love`.

The training objective is to increase:

`P(love | I, machine)`

## 5. Complete CBOW Training Pipeline

Consider:

`I love machine learning`

Target word: `love`

Context words: `I`, `machine`

The training process:

1. Convert context words into one-hot vectors.
2. Use the input embedding matrix W to retrieve their embeddings.
3. Average the context embeddings.
4. Pass the combined vector through W'.
5. Calculate logits for all vocabulary words.
6. Apply Softmax to obtain probabilities.
7. Calculate the loss using the actual target word.
8. Perform backpropagation to calculate gradients.
9. Update W and W' using an optimizer such as SGD or Adam.

The model repeats this process across training examples to learn useful word representations.

## 6. Loss Function

CBOW commonly uses categorical cross-entropy loss with Softmax.

For a single training example:

`Loss = -log(P(actual target word | context words))`

The objective is to minimize the loss.

If the model assigns a high probability to the correct target word, the loss is low.

If it assigns a low probability, the loss is high.

During training, backpropagation calculates gradients and the optimizer updates the model parameters to reduce the loss.

## 7. What Gets Updated During Training?

Both W and W' are trainable weight matrices.

For a single CBOW training example:

- The input embedding rows corresponding to the context words receive gradients.
- The output weight matrix receives gradients based on the prediction error.
- The target word's input embedding row is not directly updated merely because it is the target in that example.

For example:

`[I, machine] → love`

The input embedding rows for `I` and `machine` are involved in the input-side update.

The output-side weights are updated to improve the prediction of `love`.

**Important:** With full Softmax, gradients can affect all output vocabulary columns. With Negative Sampling, only the positive target and sampled negative output columns are involved in that training objective.

## 8. Why Is It Called Continuous Bag of Words?

**Bag of Words:**

The model considers the surrounding words as a collection and does not preserve their original order when combining their embeddings.

**Continuous:**

Instead of using sparse binary one-hot vectors as the learned representation, the model uses continuous-valued dense embedding vectors.

Therefore, the architecture is called Continuous Bag of Words.

## 9. Advantages of CBOW

1. **Computationally Efficient:** It generally requires fewer prediction operations than Skip-Gram because multiple context words are combined to predict one target.
2. **Faster Training:** It is often faster to train on large datasets.
3. **Works Well for Frequent Words:** It can learn useful representations for frequently occurring words.
4. **Multiple Context Words:** It uses information from multiple surrounding words to predict the target.

## 10. Limitations of CBOW

1. **Loss of Word Order:** Averaging context embeddings removes the original order of the context words.
2. **Rare Word Learning:** It may be less effective for rare target words because their input embeddings are not directly trained when they appear only as targets.
3. **Context Dilution:** Averaging can dilute the contribution of individual context words.
4. **Static Embeddings:** A word receives one learned embedding regardless of its sentence context.

## 11. Key Takeaways

- CBOW is a Word2Vec architecture.
- It predicts a target word using surrounding context words.
- Context embeddings are averaged to create one representation.
- W is the input embedding matrix with dimensions V × D.
- W' is the output weight matrix with dimensions D × V.
- Softmax converts output logits into probabilities.
- Cross-entropy loss measures the prediction error.
- Backpropagation and optimization update the trainable weights.
- CBOW does not preserve context word order.

