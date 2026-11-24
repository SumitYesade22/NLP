# Named Entity Recognition (NER)

## 1. Introduction
Named Entity Recognition (NER) is an NLP task that identifies named entities in text and classifies them into predefined categories.

**Example:**

"Sundar Pichai works at Google in California."

- Sundar Pichai → PERSON
- Google → ORGANIZATION
- California → LOCATION

**Main tasks:**
- Entity Detection
- Entity Classification

## 2. Entity Types

| Entity | Description | Example |
|---|---|---|
| PERSON | Person's name | Virat Kohli |
| ORG | Organization | Google |
| GPE | Countries, cities, states | India, Mumbai |
| LOC | Non-GPE locations | Himalayas |
| DATE | Date | 24 November 2026 |
| TIME | Time | 10:30 AM |
| MONEY | Monetary value | ₹500 |
| PERCENT | Percentage | 25% |
| PRODUCT | Product | iPhone |
| EVENT | Event | FIFA World Cup |

*Entity labels depend on the dataset and model.*

## 3. NER vs POS Tagging

| POS Tagging | NER |
|---|---|
| Identifies grammatical roles | Identifies named entities |
| Noun, Verb, Adjective | Person, Organization, Location |
| Grammatical classification | Entity classification |

## 4. NER as a Sequence Labeling Problem

NER assigns labels to individual tokens while identifying entity boundaries.

**Example:**

| Token | BIO Label |
|---|---|
| Sundar | B-PER |
| Pichai | I-PER |
| works | O |
| at | O |
| Google | B-ORG |

## 5. BIO Tagging Scheme

BIO is a tagging scheme used to identify entity boundaries.

- **B (Beginning):** First token of an entity.
- **I (Inside):** Subsequent token belonging to the entity.
- **O (Outside):** Token that does not belong to an entity.

**Example:**

```text
New        → B-ORG
York       → I-ORG
University → I-ORG
```

BIO is a tagging scheme, not an NER algorithm.

## 6. Challenges in NER

- **Ambiguity:** The same word can represent different entities or meanings.
- **Context Dependency:** Entity identification depends on surrounding words.
- **OOV Entities:** Difficulty recognizing previously unseen entities.
- **Multi-word Entities:** Identifying complete entity boundaries.
- **Nested Entities:** Entities occurring inside other entities.
- **Boundary Detection:** Identifying the exact beginning and ending of entities.

## 7. Approaches to NER

### 7.1 Rule-Based NER

Uses predefined rules and dictionaries to identify entities.

**Techniques:**
- Gazetteers
- Dictionary Matching
- Regular Expressions
- Context-Based Rules

**Limitations:** Requires manual rule maintenance and struggles with unseen entities.

### 7.2 Traditional ML-Based NER

NER is formulated as a sequence labeling problem using annotated training data and manually engineered features.

**Common Features:**
- Current, previous and next words
- Capitalization
- Prefixes and suffixes
- POS tags
- Word shape

**HMM (Hidden Markov Model):**
- Hidden states represent NER labels.
- Observations represent words.
- Transition probabilities model label transitions.
- Emission probabilities model word generation.
- Viterbi finds the most probable label sequence.

**CRF (Conditional Random Field):**
- Uses input features and dependencies between neighboring labels.
- Predicts a globally consistent sequence of labels.
- Useful for sequence labeling tasks.

### 7.3 Deep Learning-Based NER

- **RNN:** Processes sequential information.
- **LSTM:** Handles long-term dependencies.
- **BiLSTM:** Uses both left and right context.
- **BiLSTM-CRF:** Combines contextual representations with sequence-level label prediction.

### 7.4 Transformer-Based NER

- **BERT:** Generates contextual representations of tokens.
- **Token Classification:** Predicts an entity label for each token.
- **BERT + Softmax:** Predicts token-level labels.
- **BERT + CRF:** Adds sequence-level label dependency modeling.

## 8. NER Evaluation

NER is commonly evaluated using entity-level metrics.

- **True Positive (TP):** Correctly predicted entity.
- **False Positive (FP):** Incorrectly predicted entity.
- **False Negative (FN):** Actual entity that was missed.

```text
Precision = TP / (TP + FP)

Recall = TP / (TP + FN)

F1-Score = 2 * (Precision * Recall) / (Precision + Recall)
```

**Exact Entity Match:** An entity is correct only when its start position, end position and entity type match the ground truth.

## 9. Practical Implementation

| Library | Important Functions / Features |
|---|---|
| NLTK | `ne_chunk()` |
| spaCy | `doc.ents`, `ent.text`, `ent.label_` |
| spaCy Visualization | `displacy.render()` |
| spaCy Custom Rules | `EntityRuler` |
| Hugging Face | Pretrained NER and token classification pipelines |

## 10. Key Takeaways

- NER identifies and classifies named entities.
- BIO tagging represents entity boundaries.
- Rule-based NER relies on predefined rules and dictionaries.
- HMM and CRF are traditional sequence-labeling approaches.
- BiLSTM and BERT are deep learning approaches.
- Entity-level Precision, Recall and F1 evaluate NER performance.