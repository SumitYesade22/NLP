# Text Preprocessing: Stemming and Lemmatization

## 1. Introduction

Stemming and Lemmatization are text normalization techniques used in Natural Language Processing (NLP).

Their primary objective is to convert different grammatical forms of a word into a common base representation.

### Why Do We Need Them?

Consider the following words:

- play
- plays
- playing
- played

These words represent different grammatical forms of the same underlying word.

Treating every form as an entirely different word can increase vocabulary size and create unnecessary variations in text representation.

Stemming and Lemmatization help address this problem by normalizing related word forms.

### Benefits

- Reduce vocabulary size.
- Normalize different grammatical forms.
- Improve word matching in information retrieval systems.
- Reduce feature sparsity in traditional NLP models.
- Simplify text representation.

**Note:** Stemming and Lemmatization are not necessary for every NLP task. Their usefulness depends on the application.

---

# 2. Stemming

## 2.1 What is Stemming?

Stemming is a text normalization technique that removes prefixes or suffixes from words to obtain their approximate root form, called a **stem**.

It generally uses predefined heuristic rules rather than requiring complete linguistic or dictionary knowledge.

### Examples

| Original Word | Stem |
|---|---|
| playing | play |
| played | play |
| plays | play |
| studies | studi |
| studying | studi |
| connected | connect |
| connection | connect |
| happiness | happi |

Notice that some stems, such as `studi` and `happi`, are not valid English dictionary words.

This is an important characteristic of stemming.

## 2.2 How Does Stemming Work?

Stemming algorithms apply predefined rules to remove or modify word endings.

For example:

- playing → play
- played → play
- studies → studi

The algorithm examines suffix patterns and applies rules according to conditions such as word length and character patterns.

Stemming does not necessarily understand the grammatical meaning of a word.

## 2.3 Types of Stemming Algorithms

### A. Porter Stemmer

- Introduced by Martin Porter in 1980.
- One of the widely known English stemming algorithms.
- Uses multiple rule-based stages to remove suffixes.
- Relatively conservative compared with more aggressive stemming approaches.

Examples:

| Word | Porter Stem |
|---|---|
| caresses | caress |
| ponies | poni |
| relational | relat |
| running | run |
| studies | studi |

### B. Snowball Stemmer

Snowball is a stemming algorithm framework that provides language-specific stemming algorithms.

- Commonly associated with Porter2 for English.
- Supports multiple languages.
- Provides language-specific stemming rules.
- Designed as an improved and extended approach to stemming.

### C. Lancaster Stemmer (Paice-Husk)

- An aggressive stemming algorithm.
- Applies extensive suffix-removal rules.
- Can produce shorter stems than other algorithms.
- May sometimes remove too much of a word.

Example:

| Word | Possible Stem |
|---|---|
| maximum | maxim |
| running | run |
| studies | study |

Exact outputs depend on the algorithm implementation and its rules.

## 2.4 Advantages of Stemming

1. Reduces vocabulary size.
2. Can improve computational efficiency.
3. Helps match related word forms in search engines.
4. Useful in traditional Bag of Words and TF-IDF pipelines.
5. Provides a relatively simple text normalization approach.

## 2.5 Disadvantages of Stemming

### 1. Over-stemming

Occurs when unrelated words are reduced to the same stem.

This can incorrectly merge words that have different meanings.

### 2. Under-stemming

Occurs when related words are not reduced to the same stem.

This reduces the effectiveness of normalization.

### 3. Non-dictionary Outputs

Stemming may generate outputs that are not valid English words.

Example:

`studies` → `studi`

The output is a stem, not necessarily a linguistically valid word.

---

# 3. Lemmatization

## 3.1 What is Lemmatization?

Lemmatization is a text normalization technique that converts a word into its linguistically valid base form, called a **lemma**.

Unlike stemming, lemmatization considers linguistic information such as vocabulary, morphology, and grammatical category (Part of Speech).

### Examples

| Original Word | Lemma |
|---|---|
| playing | play |
| played | play |
| studies | study |
| better | good |
| mice | mouse |
| am | be |
| are | be |
| was | be |
| running | run |

Lemmatization does not simply remove suffixes.

For example:

`better` → `good`

This transformation requires linguistic knowledge rather than simple suffix removal.

## 3.2 How Does Lemmatization Work?

Lemmatization generally considers the following factors:

### 1. Vocabulary / Dictionary

The system uses lexical information to identify valid base forms.

Example:

`mice` → `mouse`

A simple suffix-removal rule cannot reliably identify this transformation.

### 2. Part of Speech (POS)

POS identifies the grammatical role of a word, such as:

- Noun
- Verb
- Adjective
- Adverb

The grammatical category can affect the correct lemma.

### 3. Morphological Analysis

Morphological analysis examines the internal structure and grammatical variations of words.

Examples:

- cars → car
- running → run
- was → be

## 3.3 Importance of POS in Lemmatization

Consider the word `saw`.

**Sentence 1:**

"I saw a movie."

Here, `saw` is a verb.

Lemma: `see`

**Sentence 2:**

"The carpenter used a saw."

Here, `saw` is a noun.

Lemma: `saw`

Therefore, grammatical context can change the correct lemma.

A lemmatization system that considers POS information can produce more accurate results.

**spaCy Connection:** spaCy supports POS tagging and lemmatization. POS information is useful for understanding how contextual grammatical information influences lemmatization.

## 3.4 Advantages of Lemmatization

1. Produces linguistically valid base forms.
2. Considers grammatical information.
3. Handles irregular word forms.
4. Generally provides more linguistically accurate normalization.
5. Useful in applications where word meaning and grammatical structure matter.

## 3.5 Disadvantages of Lemmatization

1. More computationally expensive than simple stemming in many implementations.
2. Requires linguistic resources such as vocabulary and morphological information.
3. Accuracy depends on language resources and contextual analysis.
4. Incorrect POS information can lead to incorrect lemmas.
5. May not improve performance for every NLP task.

---

# 4. Stemming vs Lemmatization

| Parameter | Stemming | Lemmatization |
|---|---|---|
| Approach | Heuristic-based suffix/prefix removal | Linguistic normalization |
| Output | Stem | Lemma |
| Dictionary | Generally not required | Usually uses lexical resources |
| POS consideration | Generally no | Often yes |
| Linguistic accuracy | Lower | Generally higher |
| Speed | Generally faster | Generally slower |
| Output validity | May not be a real word | Valid dictionary form |
| Complexity | Relatively simple | More complex |

### Examples

| Original Word | Stemming | Lemmatization |
|---|---|---|
| studies | studi | study |
| caring | care | care |
| better | better | good |
| mice | mice | mouse |
| running | run | run |

---

# 5. Applications: When to Use Stemming and Lemmatization?

The choice depends on the NLP task and the importance of preserving linguistic information.

| Use Case | Possible Approach |
|---|---|
| Basic search engines | Stemming or Lemmatization |
| Information retrieval | Both can be useful |
| Traditional text classification | Either, depending on evaluation |
| Sentiment analysis | Carefully evaluate; often lemmatization or neither |
| Chatbots | Lemmatization may help, depending on the pipeline |
| Modern Transformer models | Usually neither as a separate preprocessing step |

### Why Should We Not Always Apply Them?

Consider:

- good
- not good

If preprocessing removes the word `not`, the sentiment of the sentence changes.

Similarly, incorrectly normalizing words such as `unhappy` may destroy important sentiment information.

Therefore, preprocessing should preserve relevant information rather than simply reduce text size.

---

# 6. Stemming and Lemmatization in Modern NLP

Traditional NLP pipelines frequently use stemming and lemmatization.

Modern Transformer-based models, such as BERT and GPT, generally use subword tokenization to process text.

For these models, manually applying stemming or lemmatization is usually unnecessary and may be harmful.

Reasons:

1. It can remove useful grammatical information.
2. Transformer models learn contextual language representations.
3. Unnecessary normalization can alter the input distribution expected by the pretrained model.

This does not mean stemming and lemmatization are outdated. They remain useful in traditional machine learning NLP pipelines, information retrieval, search systems, and specific linguistic applications.

---

# 7. Key Takeaways

### Stemming

- Heuristic-based normalization.
- Removes or modifies prefixes and suffixes.
- Does not guarantee valid dictionary words.
- Example: `studies` → `studi`.
- Common algorithms: Porter, Snowball, Lancaster.

### Lemmatization

- Linguistic normalization.
- Uses vocabulary and morphological information.
- POS information can improve accuracy.
- Produces linguistically valid base forms.
- Example: `studies` → `study`.

### Most Important Difference

Stemming focuses on reducing words through heuristic rules, whereas Lemmatization focuses on identifying their linguistically correct base forms.

---

# 8. Practical Implementation Plan

| Concept | Library |
|---|---|
| Porter Stemming | NLTK |
| Snowball Stemming | NLTK |
| Lancaster Stemming | NLTK |
| Lemmatization | spaCy |
| POS Tagging | spaCy |
