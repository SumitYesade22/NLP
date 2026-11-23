# Part 1: POS Tagging (Part of Speech Tagging)

# 1. POS Tagging Fundamentals

## 1.1 What is POS Tagging?

Part of Speech (POS) Tagging is the process of assigning a grammatical category to each word in a sentence based on its role and context.

Common grammatical categories include:

- Noun
- Verb
- Adjective
- Adverb
- Pronoun
- Preposition
- Determiner
- Conjunction
- Interjection

**Example:**

Sentence: `The intelligent student studies regularly.`

| Word | POS Tag | Meaning |
|---|---|---|
| The | DT | Determiner |
| intelligent | JJ | Adjective |
| student | NN | Noun |
| studies | VBZ | Verb |
| regularly | RB | Adverb |
| . | . | Punctuation |

POS tagging helps a computer understand the grammatical structure of a sentence.

## 1.2 Why is POS Tagging Required?

Human language contains ambiguity. A word can perform different grammatical roles depending on its usage.

For example:

- `I read a book.` — Book is a noun.
- `I will book a ticket.` — Book is a verb.

The same word has different grammatical roles in different contexts.

POS tagging helps NLP systems:

1. Understand sentence structure.
2. Identify relationships between words.
3. Improve syntactic analysis.
4. Support Named Entity Recognition and information extraction.
5. Improve machine translation.
6. Assist text analysis and linguistic processing.

## 1.3 What is a POS Tag?

A POS tag is a grammatical label assigned to a word.

For example:

- NN represents a singular noun.
- NNS represents a plural noun.
- VB represents a base-form verb.
- VBD represents a past-tense verb.
- JJ represents an adjective.
- RB represents an adverb.

A POS tag provides grammatical information about a word rather than its complete meaning.

## 1.4 Common POS Tags (Penn Treebank)

The Penn Treebank tagset contains fine-grained grammatical labels.

| Tag | Meaning | Example |
|---|---|---|
| NN | Singular noun | book |
| NNS | Plural noun | books |
| NNP | Proper singular noun | India |
| NNPS | Proper plural noun | Indians |
| VB | Base-form verb | eat |
| VBD | Past-tense verb | played |
| VBG | Gerund / present participle | playing |
| VBN | Past participle | eaten |
| VBP | Non-3rd person singular present | play |
| VBZ | 3rd person singular present | plays |
| JJ | Adjective | beautiful |
| JJR | Comparative adjective | better |
| JJS | Superlative adjective | best |
| RB | Adverb | quickly |
| RBR | Comparative adverb | faster |
| RBS | Superlative adverb | fastest |
| DT | Determiner | the, a |
| IN | Preposition / subordinating conjunction | in, on |
| PRP | Personal pronoun | he, she |
| PRP$ | Possessive pronoun | his, her |
| CC | Coordinating conjunction | and, but |
| CD | Cardinal number | one, 100 |
| MD | Modal | can, should |
| TO | To | to |
| UH | Interjection | oh |
| . | Sentence-ending punctuation | . |
| , | Comma | , |

**Important:** The Penn Treebank tagset is more detailed than a coarse-grained tagset because it distinguishes grammatical variations such as singular/plural nouns and different verb forms.

## 1.5 Penn Treebank vs Universal POS Tagset

Different NLP libraries and models may use different tagsets.

| Penn Treebank | Universal POS | Meaning |
|---|---|---|
| NN | NOUN | Noun |
| NNP | PROPN | Proper noun |
| VB | VERB | Verb |
| VBD | VERB | Verb |
| JJ | ADJ | Adjective |
| RB | ADV | Adverb |
| DT | DET | Determiner |
| PRP | PRON | Pronoun |
| IN | ADP | Adposition |
| CC | CCONJ | Coordinating conjunction |

Penn Treebank provides detailed grammatical information, whereas Universal POS provides broader grammatical categories.

## 1.6 POS Ambiguity

POS ambiguity occurs when the same word can belong to different grammatical categories depending on its context.

**Example 1: Book**

- I bought a book. → NN
- I will book a flight. → VB

**Example 2: Fast**

- He drives fast. → RB
- He drives a fast car. → JJ

**Example 3: Light**

- Turn on the light. → NN
- This bag is light. → JJ

POS tagging algorithms use contextual information to determine the most appropriate grammatical category.

## 1.7 Applications of POS Tagging

- **Named Entity Recognition:** Helps identify grammatical context around names and entities.
- **Information Extraction:** Helps identify actions, objects, and relationships.
- **Machine Translation:** Provides grammatical information useful for translation.
- **Question Answering:** Helps analyze the structure of questions.
- **Text-to-Speech:** Provides grammatical information useful for pronunciation and language processing.
- **Sentiment Analysis:** Can help identify adjectives and other sentiment-bearing expressions.

## 1.8 Challenges in POS Tagging

1. **Lexical Ambiguity:** A word can have multiple grammatical roles.
2. **Unknown Words:** New or unseen words may not exist in the training vocabulary.
3. **Context Dependency:** Correct tagging may require understanding surrounding words.
4. **Morphological Variation:** Different word forms can have different grammatical roles.
5. **Domain Dependency:** A model trained on news articles may behave differently on social media text.
6. **Informal Language:** Slang, spelling errors, abbreviations, and incomplete sentences make tagging difficult.

---

# 2. Rule-Based POS Tagging

## 2.1 What is Rule-Based POS Tagging?

Rule-Based POS Tagging assigns grammatical categories using predefined linguistic rules.

These rules are manually designed using:

- Lexical information
- Morphological information
- Contextual and syntactic information

Unlike statistical approaches, a traditional rule-based tagger does not require learning its tagging rules from a large annotated corpus.

## 2.2 Lexical Rules

Lexical rules use a dictionary or lexicon containing known words and their possible grammatical categories.

For example:

| Word | Possible POS |
|---|---|
| book | NN / VB |
| beautiful | JJ |
| quickly | RB |
| and | CC |
| the | DT |

A lexical dictionary can identify possible grammatical categories, but it may not always determine the correct category.

For example:

- I read a book. → Book is NN.
- I book a ticket. → Book is VB.

The lexical information alone cannot resolve this ambiguity.

## 2.3 Morphological Rules

Morphological rules use the structure and formation of words to identify their grammatical categories.

Prefixes, suffixes, and word endings can provide useful clues.

Examples:

| Pattern | Possible POS | Example |
|---|---|---|
| -ly | Adverb | quickly |
| -ness | Noun | happiness |
| -tion | Noun | education |
| -able | Adjective | readable |
| -ing | Verb form / noun | running |
| -ed | Past-tense / past-participle verb | played |

These patterns are useful indicators, not guaranteed rules.

For example, `friendly` ends in `-ly` but is an adjective, not an adverb.

## 2.4 Contextual / Syntactic Rules

Contextual rules use neighboring words and sentence structure to determine the grammatical category.

Examples:

**Rule 1: Determiner followed by a noun**

- The book is interesting.
- The → DT
- book → NN

**Rule 2: Adjective before a noun**

- She bought a beautiful dress.
- beautiful → JJ
- dress → NN

**Rule 3: Modal followed by a base-form verb**

- He can swim.
- can → MD
- swim → VB

**Rule 4: Subject followed by a verb**

- The boy plays cricket.
- boy → NN
- plays → VBZ

Contextual rules help resolve ambiguities that cannot be solved using only lexical or morphological information.

## 2.5 How Rule-Based Tagging Works

A traditional rule-based POS tagger generally follows these steps:

1. Tokenize the sentence.
2. Identify possible POS categories using lexical information.
3. Apply morphological rules.
4. Apply contextual and syntactic rules.
5. Assign the most appropriate tag.

## 2.6 Advantages

- Easy to understand and interpret.
- Does not require a large annotated training corpus.
- Linguistic rules are explicitly defined.
- Can work well in restricted domains where rules are predictable.

## 2.7 Limitations

- Requires significant manual rule creation.
- Difficult to cover every grammatical situation.
- Rules may conflict with each other.
- Poor adaptability to new domains and language variations.
- Handling ambiguity is difficult when contextual rules are insufficient.
- Maintaining a large rule system becomes complicated.

---

# 3. Stochastic POS Tagging

## 3.1 What is Stochastic POS Tagging?

Stochastic POS tagging uses statistical probabilities learned from an annotated text corpus to assign grammatical categories to words.

Instead of relying entirely on manually written rules, it learns patterns from previously tagged sentences.

The main idea is:

**Choose the most probable POS tag or tag sequence based on observed language patterns.**

For example:

`I will book a ticket.`

The tagger should identify `book` as a verb rather than a noun based on the surrounding context.

## 3.2 Tagged Corpus

A tagged corpus is a collection of sentences in which every word has an associated grammatical label.

Example:

| Word | POS |
|---|---|
| The | DET |
| dog | NOUN |
| is | VERB |
| running | VERB |

A tagged corpus is used to estimate probabilities for statistical POS tagging models.

Examples of linguistic corpora include:

- Brown Corpus
- Penn Treebank
- Universal Dependencies treebanks

The quality and domain of the training corpus influence model performance.

## 3.3 Maximum Likelihood Estimation (MLE)

Maximum Likelihood Estimation estimates probabilities from observed frequencies in training data.

The general formula is:

`P(A) = Count(A) / Total Observations`

For example, if a word occurs 100 times and is tagged as a noun 80 times:

`P(NOUN | word) = 80 / 100 = 0.8`

This means that the word was tagged as a noun in 80% of its observed occurrences in that corpus.

MLE is used to estimate initial, transition, and emission probabilities in an HMM-based POS tagger.

## 3.4 Initial Probability

Initial probability represents the probability that a particular POS tag appears at the beginning of a sentence.

Formula:

`P(t1) = Count(t1 at sentence start) / Total Sentences`

Example:

Suppose a training corpus contains 100 sentences.

- 40 sentences start with a determiner.
- 30 sentences start with a pronoun.
- 20 sentences start with a proper noun.
- 10 sentences start with other tags.

Then:

`P(DET) = 40/100 = 0.4`

`P(PRON) = 30/100 = 0.3`

`P(PROPN) = 20/100 = 0.2`

## 3.5 Transition Probability

Transition probability represents the probability of a POS tag occurring after another POS tag.

Formula:

`P(ti | ti-1) = Count(ti-1, ti) / Count(ti-1 as previous tag)`

Example:

Suppose a noun is followed by a verb 60 times out of 100 observed noun-to-next-tag transitions.

`P(VERB | NOUN) = 60/100 = 0.6`

This probability helps a statistical tagger understand common grammatical sequences.

## 3.6 Emission Probability

Emission probability represents the probability of observing a particular word given a POS tag.

Formula:

`P(word | tag) = Count(tag, word) / Count(tag)`

Example:

Suppose the word `book` occurs 100 times as a noun out of 1200 noun occurrences.

`P(book | NOUN) = 100/1200 = 0.0833`

Emission probabilities help the model determine which words are likely to be associated with particular POS tags.

## 3.7 Numerical Example: Predicting POS Tags

Consider the sentence:

`Dogs bark`

Suppose the model has the following probabilities:

Initial probabilities:

- P(NOUN) = 0.6
- P(VERB) = 0.4

Transition probabilities:

- P(VERB | NOUN) = 0.8
- P(NOUN | VERB) = 0.2

Emission probabilities:

- P(Dogs | NOUN) = 0.5
- P(Dogs | VERB) = 0.01
- P(bark | VERB) = 0.6
- P(bark | NOUN) = 0.1

For the sequence NOUN → VERB:

`P = P(NOUN) × P(Dogs | NOUN) × P(VERB | NOUN) × P(bark | VERB)`

`P = 0.6 × 0.5 × 0.8 × 0.6`

`P = 0.144`

For the sequence VERB → NOUN:

`P = P(VERB) × P(Dogs | VERB) × P(NOUN | VERB) × P(bark | NOUN)`

`P = 0.4 × 0.01 × 0.2 × 0.1`

`P = 0.00008`

Therefore:

`P(NOUN → VERB) > P(VERB → NOUN)`

The model prefers:

`Dogs/NOUN bark/VERB`

**Important:** This example demonstrates how initial, transition, and emission probabilities contribute to the probability of a complete tag sequence.

## 3.8 Limitations of Basic Stochastic Tagging

- Requires an annotated training corpus.
- Unseen words create a data sparsity problem.
- MLE may assign zero probability to unseen events.
- Basic models may not capture long-range dependencies.
- Performance depends on the quality and domain of training data.

---

# 4. Hidden Markov Model (HMM)

## 4.1 What is HMM?

A Hidden Markov Model is a probabilistic generative model used to represent sequences where the actual states are hidden, but observable outputs are generated from those states.

In POS tagging:

- Hidden states = POS tags.
- Observations = Words.

The model observes words and attempts to determine the most probable sequence of hidden grammatical tags.

## 4.2 Hidden States vs Observations

Consider:

`The boy plays cricket.`

Observations:

`The, boy, plays, cricket`

Hidden states:

`DET, NOUN, VERB, NOUN`

The words are visible, but their grammatical states are not directly known. The HMM estimates those states using learned probabilities.

## 4.3 Why HMM is Used for POS Tagging

POS tagging is a sequence prediction problem.

The grammatical category of a word depends partly on:

- The word itself.
- The previous grammatical category.
- The probability of grammatical tag sequences.

HMM provides a probabilistic framework for modelling these relationships.

It combines:

1. Initial probability.
2. Transition probability.
3. Emission probability.

## 4.4 Markov Property

The Markov property states that the future state depends on the current state rather than the entire previous history.

In a first-order Markov model:

`P(ti | t1, t2, ..., ti-1) = P(ti | ti-1)`

This simplifies sequence modelling by considering only the immediately preceding state.

## 4.5 First-Order Markov Assumption

A first-order HMM assumes that the current POS tag depends only on the immediately previous POS tag.

For example:

`DET → NOUN → VERB → NOUN`

When predicting the next tag, the model considers the previous tag rather than the complete tag history.

This assumption makes computation more manageable.

## 4.6 HMM Assumptions

A basic HMM for POS tagging makes two major assumptions.

**1. Markov Assumption**

The current hidden state depends only on the previous hidden state.

`P(ti | t1, ..., ti-1) = P(ti | ti-1)`

**2. Observation Independence Assumption**

The current observed word depends only on the current hidden state.

`P(wi | t1, ..., ti, ..., tn, w1, ..., wi-1) = P(wi | ti)`

In other words, once the current POS tag is known, the model assumes that the current word is independent of the other words and tags.

This is a simplifying assumption, not a perfect representation of natural language.

## 4.7 Initial, Transition and Emission Probabilities

An HMM contains three important probability distributions.

| Probability | Meaning |
|---|---|
| Initial | Probability of the first hidden state |
| Transition | Probability of moving from one hidden state to another |
| Emission | Probability of observing a word from a hidden state |

These probabilities are generally estimated from a tagged training corpus using MLE.

## 4.8 Joint Probability of a Tag Sequence

For an observation sequence W and a tag sequence T, the HMM joint probability is:

`P(W, T) = P(t1) × P(w1 | t1) × ∏[P(ti | ti-1) × P(wi | ti)]`

Here:

- W = Observed word sequence.
- T = Hidden POS tag sequence.
- P(t1) = Initial probability.
- P(ti | ti-1) = Transition probability.
- P(wi | ti) = Emission probability.

The model uses this probability to evaluate possible tag sequences.

## 4.9 Finding the Most Probable Tag Sequence

The objective of HMM-based POS tagging is:

`T* = argmax_T P(T | W)`

Using Bayes' theorem:

`T* = argmax_T P(W, T)`

The denominator P(W) is the same for all possible tag sequences, so it does not affect which sequence has the maximum probability.

The challenge is that the number of possible tag sequences grows exponentially with sentence length.

Viterbi solves this efficiently using dynamic programming.

## 4.10 Advantages of HMM

- Provides a mathematical framework for sequence modelling.
- Uses probabilities learned from annotated data.
- Can handle ambiguity using both word emissions and tag transitions.
- Viterbi makes sequence decoding computationally efficient.
- Useful in speech recognition and other sequence modelling tasks.

## 4.11 Limitations of HMM

- Assumes limited dependence between consecutive hidden states.
- Assumes observations depend only on the current hidden state.
- Cannot naturally model rich, overlapping contextual features.
- Unseen words create emission probability problems.
- Long-range linguistic dependencies are difficult to capture.

---

# 5. Viterbi Algorithm

## 5.1 Why Do We Need Viterbi?

Suppose a sentence contains n words and the model has K possible POS tags.

The number of possible tag sequences is:

`K^n`

For example, if:

- Number of words = 5
- Number of possible tags = 10

Possible tag sequences:

`10^5 = 100,000`

Evaluating every possible sequence becomes computationally expensive as sentence length increases.

Viterbi finds the most probable sequence efficiently using dynamic programming.

## 5.2 Brute Force vs Dynamic Programming

**Brute Force:**

- Generates every possible tag sequence.
- Calculates the probability of each sequence.
- Selects the sequence with the highest probability.
- Becomes expensive for longer sequences.

Time complexity:

`O(K^n)`

**Dynamic Programming:**

- Solves smaller subproblems.
- Stores the best score for each state at each position.
- Reuses previously calculated results.
- Avoids repeatedly evaluating the same subproblems.

Viterbi uses dynamic programming to find the optimal sequence.

## 5.3 Viterbi Initialization

Initialization calculates the probability of starting with each possible POS tag and generating the first observed word.

For every possible tag:

`V1(tag) = P(tag) × P(word1 | tag)`

Here:

- P(tag) = Initial probability.
- P(word1 | tag) = Emission probability.

These values form the first column of the dynamic programming table.

## 5.4 Viterbi Recursion

For each subsequent word and each possible current tag, Viterbi evaluates all possible previous tags.

Formula:

`Vi(tag) = max_previous_tag [V(i-1)(previous_tag) × P(tag | previous_tag) × P(wordi | tag)]`

It stores:

1. The maximum probability score.
2. The previous tag responsible for that maximum score.

The second value is stored in a backpointer table.

This process continues until the final word.

## 5.5 Viterbi Termination

After processing the final word, the algorithm identifies the tag with the highest probability in the last column.

This represents the final state of the most probable tag sequence.

## 5.6 Viterbi Backtracking

The algorithm uses the stored backpointers to reconstruct the complete optimal tag sequence.

Starting from the best final tag:

1. Move to its stored previous tag.
2. Continue following backpointers.
3. Repeat until reaching the first word.
4. Reverse the recovered sequence if necessary.

This produces the most probable sequence of POS tags.

## 5.7 Numerical Example: Step-by-Step

Consider:

`Dogs bark`

Possible tags:

`NOUN, VERB`

Initial probabilities:

- P(NOUN) = 0.6
- P(VERB) = 0.4

Emission probabilities:

- P(Dogs | NOUN) = 0.5
- P(Dogs | VERB) = 0.01
- P(bark | NOUN) = 0.1
- P(bark | VERB) = 0.6

Transition probabilities:

- P(NOUN | NOUN) = 0.2
- P(VERB | NOUN) = 0.8
- P(NOUN | VERB) = 0.3
- P(VERB | VERB) = 0.7

**Step 1: Initialization**

For the first word `Dogs`:

`V1(NOUN) = 0.6 × 0.5 = 0.30`

`V1(VERB) = 0.4 × 0.01 = 0.004`

**Step 2: Recursion for the second word `bark`**

Calculate the score for current tag NOUN:

From previous NOUN:

`0.30 × 0.2 × 0.1 = 0.006`

From previous VERB:

`0.004 × 0.3 × 0.1 = 0.00012`

Choose the maximum:

`V2(NOUN) = 0.006`

Best previous tag = NOUN.

Now calculate the score for current tag VERB:

From previous NOUN:

`0.30 × 0.8 × 0.6 = 0.144`

From previous VERB:

`0.004 × 0.7 × 0.6 = 0.00168`

Choose the maximum:

`V2(VERB) = 0.144`

Best previous tag = NOUN.

**Step 3: Termination**

Compare the final scores:

- V2(NOUN) = 0.006
- V2(VERB) = 0.144

The best final tag is VERB.

**Step 4: Backtracking**

The backpointer for VERB points to NOUN.

Therefore:

`Dogs/NOUN bark/VERB`

This is the most probable tag sequence according to the given HMM probabilities.

## 5.8 Why Log Probabilities Are Used

When a sentence contains many words, multiplying several small probabilities can result in numerical underflow.

To avoid this, implementations commonly use logarithms.

Using the logarithm property:

`log(a × b) = log(a) + log(b)`

Therefore, multiplication of probabilities becomes addition of log probabilities.

The maximum-probability sequence remains unchanged because logarithm is a monotonically increasing function.

## 5.9 Time and Space Complexity

Let:

- n = Number of words.
- K = Number of possible hidden states (POS tags).

**Time Complexity:**

`O(n × K²)`

For each word, the algorithm considers transitions from every possible previous tag to every possible current tag.

**Space Complexity:**

`O(n × K)`

The algorithm stores the score table and backpointer table for every word and possible tag.

---

# 6. Other POS Tagging Approaches

## 6.1 Brill Tagger

Brill Tagger is a transformation-based learning approach for POS tagging.

It combines an initial tagging method with automatically learned correction rules.

Instead of directly predicting every tag independently, it improves an initial sequence of tags by applying transformation rules.

**Working:**

1. An initial tagger assigns POS tags.
2. Predictions are compared with the correct tags in training data.
3. The algorithm identifies useful correction rules.
4. Rules are selected based on how much they reduce tagging errors.
5. The learned rules are applied to improve future predictions.

Example:

Initial prediction:

`The/DT book/NN flights/NNS`

A learned contextual rule might correct `book` to VB when it appears before a noun in a particular context.

The actual correction depends on the learned rule templates and training corpus.

**Advantages:**

- Rules are interpretable.
- Combines statistical learning and linguistic rules.
- Can correct systematic tagging errors.

**Limitations:**

- Depends on the initial tagger.
- Rule learning can be computationally expensive.
- Performance depends on rule templates and training data.

## 6.2 Conditional Random Fields (CRF)

Conditional Random Field is a discriminative probabilistic model used for sequence labelling.

Unlike HMM, which models the joint probability of observations and hidden states, CRF directly models the conditional probability of a label sequence given an observation sequence.

HMM:

`P(W, T)`

CRF:

`P(T | W)`

In POS tagging:

- Input = Words in a sentence.
- Output = POS tag sequence.

CRF can use rich contextual features such as:

- Current word.
- Previous and next words.
- Prefixes and suffixes.
- Capitalization.
- Word shape.
- Previous and next label relationships.

**Advantages:**

- Supports multiple overlapping input features.
- Models dependencies between output labels.
- Does not require the same observation-independence assumption as a basic HMM.

**Limitations:**

- Requires feature engineering in traditional CRF implementations.
- Training can be computationally expensive.
- Requires annotated training data.

## 6.3 Traditional vs Neural POS Tagging

Traditional approaches use explicit probability models, linguistic rules, or engineered features.

Neural approaches learn useful representations automatically from training data.

| Aspect | Traditional Methods | Neural Methods |
|---|---|---|
| Examples | HMM, CRF, Brill | BiLSTM, Transformers |
| Features | Often manually designed | Often learned automatically |
| Context | Limited by model assumptions/features | Can capture richer contextual information |
| Training | Statistical estimation or feature-based learning | Neural network optimization |
| Data requirements | Varies by method | Often benefits from larger datasets |
| Interpretability | HMM and rule-based methods can be easier to inspect | Usually less interpretable |

Neither approach is universally best. Performance depends on the language, dataset, domain, and evaluation setup.

## 6.4 How Transformers / BERT Perform POS Tagging

BERT is a Transformer-based language model that learns contextual representations of words.

Unlike traditional HMM-based tagging, BERT uses self-attention to capture relationships between tokens across a sentence.

**Basic working:**

1. **Tokenization:** Input text is divided into tokens or subword units.
2. **Embedding:** Tokens are converted into numerical representations.
3. **Transformer Encoder:** Self-attention and feed-forward layers generate contextual representations.
4. **Token Classification Head:** A classification layer predicts a POS label for each relevant token.
5. **Output:** Predicted POS labels are mapped back to the original words.

**Example:**

Sentence:

`I will book a ticket.`

BERT considers the surrounding context to understand that `book` is being used as a verb.

For:

`I read a book.`

The contextual representation helps predict `book` as a noun.

### Subword Tokenization

BERT may divide a word into multiple subword tokens.

For example:

`playing` → `play`, `##ing`

A POS tagging system must handle the mapping between subword tokens and original word-level labels.

A common approach is to assign the word's label to its first subword and ignore or appropriately handle subsequent subwords during training and evaluation.

### Advantages

- Learns contextual representations.
- Captures relationships between distant tokens.
- Requires less manual feature engineering.
- Can achieve strong results when fine-tuned on suitable annotated data.

### Limitations

- Computationally expensive compared with simpler taggers.
- Requires careful token-to-label alignment.
- Fine-tuning requires annotated data.
- Predictions may be difficult to interpret.

---

# 7. Comparison of POS Tagging Approaches

| Approach | Main Idea | Important Technique |
|---|---|---|
| Rule-Based | Manually defined linguistic rules | Lexical, morphological, contextual rules |
| Stochastic | Probability-based tagging | MLE |
| HMM | Generative sequence modelling | Initial, transition, emission probabilities |
| Viterbi | Finds the most probable state sequence | Dynamic Programming |
| Brill | Learns correction rules | Transformation-based learning |
| CRF | Conditional sequence modelling | Feature functions and label dependencies |
| Neural POS | Learns contextual representations | Neural networks |
| BERT | Contextual Transformer representations | Self-attention and token classification |
