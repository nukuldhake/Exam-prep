# AD32232: Natural Language Processing — Complete Course Guide

---

## 📋 Course Overview

| Detail | Info |
|---|---|
| **Credits** | 3 |
| **Lectures** | 2 Hrs/week |
| **Practical** | 2 Hrs/week |
| **ISE** | 20 Marks |
| **SCE** | 20 Marks |
| **ESE** | 40 Marks |
| **PR** | 20 Marks |

**Prerequisites:** Data Structures (AD21231), Probability Theory & Statistics (MDM20234)

---

## Course Outcomes (COs)

| CO | Description |
|---|---|
| CO1 | Comprehend the morphological aspects of NLP |
| CO2 | Identify PoS tags and explore parsing techniques |
| CO3 | Understand language semantics and Word Sense Disambiguation |
| CO4 | Explore IE, QA, Summarization, and MT systems |

---

---

# UNIT I: Introduction & Morphological Analysis (6 Hrs)

---

## 1.1 History of NLP

NLP is a subfield of AI and linguistics concerned with enabling computers to understand, interpret, and generate human language.

**Timeline:**

| Era | Period | Key Developments |
|---|---|---|
| **Foundational** | 1940s–1950s | Automata theory (Turing), Shannon's information theory, early MT efforts (Georgetown experiment 1954) |
| **Symbolic / Rule-Based** | 1957–1970s | Chomsky's generative grammar, ELIZA (1966), SHRDLU (1970) |
| **Stochastic / Statistical** | 1970s–1990s | HMMs, probabilistic parsing, corpus-based methods |
| **Empirical / ML** | 1990s–2010s | Statistical MT, SVMs, CRFs, Penn Treebank |
| **Deep Learning** | 2013–present | Word2Vec, seq2seq, attention, Transformers, BERT, GPT |

---

## 1.2 Stages in NLP

NLP processing is typically described in a **pipeline** of stages, progressing from surface text to deep meaning:

```
Raw Text
   │
   ▼
┌──────────────────────┐
│ 1. Phonological/      │  ← Sound/script analysis
│    Orthographic       │
│    Analysis           │
└──────────┬───────────┘
           ▼
┌──────────────────────┐
│ 2. Morphological      │  ← Word structure (stems, affixes)
│    Analysis           │
└──────────┬───────────┘
           ▼
┌──────────────────────┐
│ 3. Lexical Analysis   │  ← Word-level meaning, PoS
└──────────┬───────────┘
           ▼
┌──────────────────────┐
│ 4. Syntactic Analysis │  ← Sentence structure (parsing)
│    (Parsing)          │
└──────────┬───────────┘
           ▼
┌──────────────────────┐
│ 5. Semantic Analysis  │  ← Meaning representation
└──────────┬───────────┘
           ▼
┌──────────────────────┐
│ 6. Discourse Analysis │  ← Inter-sentence relationships
└──────────┬───────────┘
           ▼
┌──────────────────────┐
│ 7. Pragmatic Analysis │  ← Context, intent, world knowledge
└──────────────────────┘
```

**Detailed description of each stage:**

1. **Phonological/Orthographic Analysis:** Deals with sounds (speech) or characters (text). Maps speech signals to words or handles encoding/script issues.

2. **Morphological Analysis:** Analyzes internal structure of words — roots, prefixes, suffixes, inflections. E.g., "unhappiness" → un + happy + ness.

3. **Lexical Analysis:** Identifies individual words/tokens; assigns PoS tags; dictionary lookup.

4. **Syntactic Analysis (Parsing):** Determines grammatical structure of a sentence; produces parse trees using grammar rules (CFG).

5. **Semantic Analysis:** Extracts meaning from parsed structures; maps to meaning representations (logical forms, semantic roles).

6. **Discourse Analysis:** Interprets multi-sentence text; resolves coreferences; identifies discourse relations (coherence, structure).

7. **Pragmatic Analysis:** Understands intended meaning based on context, world knowledge, speaker intent. E.g., "Can you pass the salt?" is a request, not a question.

---

## 1.3 Ambiguity in Natural Language

Ambiguity is the **central challenge** of NLP — a single piece of text can have multiple valid interpretations.

### Types of Ambiguity

| Type | Description | Example |
|---|---|---|
| **Lexical Ambiguity** | A word has multiple meanings | "bank" → river bank vs. financial bank |
| **Syntactic Ambiguity** | A sentence has multiple parse trees | "I saw the man with a telescope" (Who has the telescope?) |
| **Semantic Ambiguity** | Multiple meaning interpretations | "Every student read a book" (same or different books?) |
| **Referential Ambiguity** | Pronoun reference is unclear | "John told Bill that he was wrong" (who is "he"?) |
| **Pragmatic Ambiguity** | Intent is unclear | "It's cold in here" (statement or request to close the window?) |

**Example of syntactic ambiguity — two parse trees:**

```
"I saw the man with a telescope"

Parse 1: I [saw [the man] [with a telescope]]
   → I used a telescope to see the man

Parse 2: I [saw [the man [with a telescope]]]
   → The man had a telescope
```

---

## 1.4 Challenges of NLP

1. **Ambiguity** (as above)
2. **Variability:** Same meaning can be expressed in many different ways
3. **Context dependence:** Meaning changes with context
4. **Idioms and metaphors:** "kick the bucket" ≠ literally kicking a bucket
5. **Sarcasm and irony:** "Oh great, another Monday"
6. **Spelling errors and noise:** Real-world text is messy
7. **Resource scarcity:** Many languages lack annotated corpora
8. **Morphological complexity:** Agglutinative languages (Turkish, Marathi) have rich morphology
9. **Word segmentation:** Languages without spaces (Chinese, Japanese)
10. **Domain specificity:** Medical, legal, technical texts have specialized vocabularies

---

## 1.5 Applications of NLP

| Application | Description |
|---|---|
| Machine Translation | Google Translate, DeepL |
| Sentiment Analysis | Opinion mining from reviews, social media |
| Information Extraction | Extracting structured data from unstructured text |
| Question Answering | Siri, Alexa, chatbots |
| Text Summarization | Automatic summary generation |
| Spell/Grammar Checking | Grammarly, MS Word |
| Speech Recognition | Converting speech to text |
| Text Generation | GPT-based content generation |
| Named Entity Recognition | Identifying persons, locations, organizations |
| Chatbots/Dialogue Systems | Customer service automation |

---

## 1.6 Finite-State Morphological Parsing

### Morphology Basics

**Morphology** is the study of the internal structure of words.

| Term | Definition | Example |
|---|---|---|
| **Morpheme** | Smallest meaningful unit | "un", "break", "able" |
| **Stem/Root** | Core morpheme | "break" in "unbreakable" |
| **Affix** | Attached morpheme | prefix ("un-"), suffix ("-able"), infix, circumfix |
| **Inflection** | Grammatical variation (same PoS) | walk → walks, walked, walking |
| **Derivation** | Creates new word (may change PoS) | happy (adj) → happiness (noun) |
| **Compounding** | Combining two stems | "blackboard", "sunflower" |

### Finite-State Morphological Parsing

The goal is to take a surface word form and produce its **lemma** (base form) + **morphological features**.

```
Input:  "cats"
Output: cat +N +PL (noun, plural)

Input:  "running"
Output: run +V +PresPart (verb, present participle)
```

This is done using **Finite-State Automata (FSA)** and **Finite-State Transducers (FST)**.

---

## 1.7 Building a Finite-State Lexicon

A **finite-state lexicon** encodes all valid stems and their categories using an FSA.

```
Example: Lexicon with words {cat, cats, dog, dogs}

States: q0 (start), q1, q2, q3, ...
```

The lexicon is represented as a **trie** (prefix tree) encoded as an FSA:

```
      c → a → t → (accept: N)
q0 ─┤                 └─→ s → (accept: N+PL)
     └─ d → o → g → (accept: N)
                  └─→ s → (accept: N+PL)
```

### Steps to build:
1. List all stems with their categories
2. Encode as a trie
3. Convert to a minimized FSA
4. Combine with morphological rules (via FSTs)

---

## 1.8 Finite-State Transducers (FSTs)

An **FST** is like an FSA but with **two tapes** — an input tape and an output tape. It maps one string to another.

**Formally:** An FST is a tuple (Q, Σ₁, Σ₂, δ, q₀, F) where:
- Q = set of states
- Σ₁ = input alphabet
- Σ₂ = output alphabet
- δ = transition function: Q × Σ₁ → Q × Σ₂
- q₀ = start state
- F = set of accept states

**Example:** FST mapping surface form to lexical form:

```
Input:  f o x e s
Output: f o x ^s
        (fox + plural)

Transition:  e:ε  (delete the 'e')
             s:^s (map 's' to morpheme boundary + s)
```

### Properties of FSTs:
- **Inversion:** Swap input and output → generation instead of analysis
- **Composition:** Chain multiple FSTs together
- **Sequential transducers:** Deterministic, efficient

---

## 1.9 FSTs for Morphological Parsing

Morphological parsing using FSTs involves **cascading** two components:

```
Surface Form  →  [Spelling Rules FST]  →  Intermediate  →  [Lexicon FST]  →  Lexical Form

Example:
"foxes" → [rule: e-insertion] → "fox^s" → [lexicon] → fox +N +PL
"cities" → [rule: y→ie] → "city^s" → [lexicon] → city +N +PL
```

**Architecture (Two-Level Morphology — Koskenniemi, 1983):**

```
  Lexical Level:    f o x   +N +PL
                    ↕ ↕ ↕     ↕
  Surface Level:    f o x e   s

  Rules apply simultaneously between levels
```

**Common spelling rules encoded as FSTs:**
- **E-insertion:** fox → foxes (insert 'e' before 's' after x, s, z, sh, ch)
- **E-deletion:** make + ing → making (delete silent 'e' before vowel suffix)
- **Y-replacement:** city + s → cities (y → ie before 's')
- **Consonant doubling:** stop + ing → stopping

---

## 1.10 The Porter Stemmer

The **Porter Stemming Algorithm** (Martin Porter, 1980) is a rule-based algorithm that strips suffixes from English words to produce stems.

### Key Concept: Measure (m)

A word is represented as: [C](VC){m}[V]

Where C = consonant sequence, V = vowel sequence, m = **measure** (number of VC pairs).

| Word | Pattern | m |
|---|---|---|
| TR | C | 0 |
| TREE | CV | 0 |
| TROUBLE | CVCV | 1 |
| TROUBLES | CVCCVC | 2 |
| PRIVATE | CVCVCV | 2 |

### Steps of Porter Stemmer (5 main steps):

**Step 1a: Plural and past participle**
```
SSES → SS     (caresses → caress)
IES  → I      (ponies → poni)
SS   → SS     (caress → caress)
S    → ε      (cats → cat)
```

**Step 1b: -ED and -ING**
```
(m>0) EED → EE   (agreed → agree)
(*v*) ED  → ε    (plastered → plaster)
(*v*) ING → ε    (motoring → motor)
```
*After removing -ED or -ING, apply cleanup rules (e.g., AT → ATE, BL → BLE, doubling)*

**Step 2: Map double suffixes (m>0)**
```
ATIONAL → ATE    (relational → relate)
TIONAL  → TION   (conditional → condition)
ENCI    → ENCE   (dependency → dependence)
FULNESS → FUL    (hopefulness → hopeful)
OUSLI   → OUS    (analogously → analogous)
```

**Step 3: More suffix mapping (m>0)**
```
ICATE → IC    (triplicate → triplic)
ATIVE → ε     (formative → form)
ALIZE → AL    (formalize → formal)
ICAL  → IC    (electrical → electric)
```

**Step 4: Remove suffixes (m>1)**
```
AL, ANCE, ENCE, ER, IC, ABLE, IBLE, ANT, EMENT, MENT, ENT, ION, OU, ISM, ATE, ITI, OUS, IVE, IZE → ε
```

**Step 5: Clean up**
```
(m>1) E → ε     (probate → probat)
(m=1 and not *o) E → ε
(m>1 and *d and *L) → remove last letter (controll → control)
```

### Limitations of Porter Stemmer:
- **Over-stemming:** "university" and "universe" both → "univers"
- **Under-stemming:** "alumnus" and "alumni" are not conflated
- Not linguistically motivated — purely heuristic
- Language-specific (designed for English)

### Stemming vs Lemmatization:

| Feature | Stemming | Lemmatization |
|---|---|---|
| Approach | Rule-based suffix stripping | Dictionary-based, morphological analysis |
| Output | Stem (may not be a valid word) | Lemma (valid dictionary word) |
| Example | "running" → "run" or "runn" | "running" → "run" |
| Speed | Faster | Slower |
| Accuracy | Lower | Higher |

---

## 1.11 Word and Sentence Tokenization

### Word Tokenization

**Tokenization** is the process of breaking text into individual tokens (words, punctuation, numbers).

**Challenges:**
- Contractions: "don't" → "do" + "n't" or "don't"?
- Hyphenated words: "state-of-the-art" — one token or four?
- Abbreviations: "U.S.A.", "Dr.", "etc."
- Numbers and dates: "3.14", "01/01/2024"
- Clitics: "I'm" → "I" + "'m"
- Multiword expressions: "New York", "ice cream"
- Non-space-separated languages: Chinese, Japanese, Thai

**Common approaches:**
1. **Simple whitespace/regex-based:** Split on spaces and punctuation
2. **Rule-based tokenizers:** Penn Treebank tokenizer
3. **Subword tokenization:** Byte Pair Encoding (BPE), WordPiece, SentencePiece

**Example (Penn Treebank style):**
```
Input:  "Don't you think Mr. Smith's car is well-maintained?"
Output: ["Do", "n't", "you", "think", "Mr.", "Smith", "'s", "car", "is", "well-maintained", "?"]
```

### Sentence Tokenization (Sentence Segmentation)

Breaking text into sentences, primarily by detecting sentence boundaries.

**Challenges:**
- Period is ambiguous: abbreviation ("Dr."), decimal ("3.14"), ellipsis ("..."), end-of-sentence
- "!" and "?" can appear in quotations mid-text

**Approaches:**
1. **Rule-based:** If period is followed by a capital letter and preceded by a non-abbreviation
2. **ML-based:** Binary classifier to determine if a period is end-of-sentence
3. **Tools:** NLTK `sent_tokenize()`, spaCy sentence segmenter

---

## 1.12 Spelling Error Detection and Correction

### Types of Spelling Errors

| Type | Description | Example |
|---|---|---|
| **Non-word errors** | Misspelled word not in dictionary | "graffe" (giraffe) |
| **Real-word errors** | Misspelled to another valid word | "there" instead of "three" |
| **Typographic errors** | Keyboard/typing mistakes | "teh" → "the" |
| **Cognitive errors** | Phonetic similarity | "piece" vs. "peace" |

### Common error patterns (Damerau-Levenshtein):
1. **Insertion:** "the" → "thhe"
2. **Deletion:** "the" → "th"
3. **Substitution:** "the" → "thr"
4. **Transposition:** "the" → "hte"

### Spelling Correction Approaches:

**1. Dictionary Lookup:**
- Check if word exists in dictionary
- If not, find closest dictionary words

**2. Minimum Edit Distance (see next section)**

**3. Noisy Channel Model:**
```
ŵ = argmax P(w|x) = argmax P(x|w) · P(w)
         w                    w

where:
- x = observed (misspelled) word
- w = candidate correct word
- P(x|w) = error model (how likely is typo x given intended word w)
- P(w) = language model (prior probability of word w)
```

**4. N-gram based:** Use surrounding context to detect real-word errors

---

## 1.13 Minimum Edit Distance

**Minimum Edit Distance (MED)** (also called **Levenshtein Distance**) is the minimum number of edit operations needed to transform one string into another.

### Edit Operations and Costs:

| Operation | Levenshtein Cost | Example |
|---|---|---|
| Insertion | 1 | "" → "a" |
| Deletion | 1 | "a" → "" |
| Substitution | 1 (or 2 in some variants) | "a" → "b" |

### Dynamic Programming Algorithm

Given source string `X` of length `n` and target string `Y` of length `m`:

**Recurrence:**
```
D[i, 0] = i                    (base case: delete all of X)
D[0, j] = j                    (base case: insert all of Y)

D[i, j] = min {
    D[i-1, j]   + 1,           (deletion)
    D[i, j-1]   + 1,           (insertion)
    D[i-1, j-1] + (0 if X[i]=Y[j], else 1)  (substitution or match)
}
```

**Time Complexity:** O(n × m)
**Space Complexity:** O(n × m)

### Worked Example: "INTENTION" → "EXECUTION"

```
        #  E  X  E  C  U  T  I  O  N
    #   0  1  2  3  4  5  6  7  8  9
    I   1  1  2  3  4  5  6  6  7  8
    N   2  2  2  3  4  5  6  7  7  7
    T   3  3  3  3  4  5  5  6  7  8
    E   4  3  4  3  4  5  6  6  7  8
    N   5  4  4  4  4  5  6  7  7  7
    T   6  5  5  5  5  5  5  6  7  8
    I   7  6  6  6  6  6  6  5  6  7
    O   8  7  7  7  7  7  7  6  5  6
    N   9  8  8  8  8  8  8  7  6  5
```

**MED("INTENTION", "EXECUTION") = 5**

### Backtrace:
The backtrace recovers the actual sequence of operations:
```
I→E (sub), N→X (sub), keep T→T, E→E, N→C (sub), T→U (sub), I→T (sub)...
```
(Actual alignment depends on tie-breaking)

---

## 1.14 N-Grams

### N-Gram Language Model

An **N-gram** is a contiguous sequence of N items (words/characters) from text.

| N | Name | Example ("I love NLP") |
|---|---|---|
| 1 | Unigram | "I", "love", "NLP" |
| 2 | Bigram | "I love", "love NLP" |
| 3 | Trigram | "I love NLP" |

### N-Gram Language Model

The **goal** is to compute the probability of a sentence (sequence of words):

$$P(w_1, w_2, ..., w_n) = \prod_{k=1}^{n} P(w_k | w_1, ..., w_{k-1})$$

**Markov Assumption:** Only the previous (N-1) words matter:

**Bigram Model (N=2):**
$$P(w_k | w_1, ..., w_{k-1}) \approx P(w_k | w_{k-1})$$

**Trigram Model (N=3):**
$$P(w_k | w_1, ..., w_{k-1}) \approx P(w_k | w_{k-2}, w_{k-1})$$

### Estimating Probabilities (MLE):

**Bigram:**
$$P(w_n | w_{n-1}) = \frac{C(w_{n-1}, w_n)}{C(w_{n-1})}$$

**Example:**
```
Corpus: "I am Sam. Sam I am. I like green eggs and ham."

P("am" | "I") = C("I am") / C("I") = 2/3
P("Sam" | "am") = C("am Sam") / C("am") = 1/2
```

### Sentence Probability (Bigram):
```
P("I am Sam") = P(I|<s>) × P(am|I) × P(Sam|am) × P(</s>|Sam)
```
where `<s>` and `</s>` are sentence boundary tokens.

### Smoothing Techniques

**Problem:** Zero probability for unseen n-grams.

**1. Laplace (Add-1) Smoothing:**
$$P_{Laplace}(w_n | w_{n-1}) = \frac{C(w_{n-1}, w_n) + 1}{C(w_{n-1}) + V}$$
where V = vocabulary size

**2. Add-k Smoothing:**
$$P_{add-k}(w_n | w_{n-1}) = \frac{C(w_{n-1}, w_n) + k}{C(w_{n-1}) + k \cdot V}$$

**3. Good-Turing Smoothing:**
Re-estimate counts based on frequency of frequencies.

**4. Backoff and Interpolation:**
- **Backoff:** Use lower-order n-gram if higher-order has zero count
- **Interpolation:** Weighted combination of different n-gram orders:
$$P(w_n | w_{n-2}, w_{n-1}) = \lambda_1 P(w_n) + \lambda_2 P(w_n|w_{n-1}) + \lambda_3 P(w_n|w_{n-2}, w_{n-1})$$
where $\lambda_1 + \lambda_2 + \lambda_3 = 1$

### Evaluation: Perplexity

$$PP(W) = P(w_1 w_2 ... w_N)^{-1/N} = \sqrt[N]{\frac{1}{\prod_{i=1}^{N} P(w_i|w_{i-1})}}$$

- **Lower perplexity = better model**
- Interpreted as the "average branching factor" — how many words the model is confused between

### N-Grams for Spelling Correction

N-grams help correct **real-word errors** by considering context:

```
"I went to the library to chick out a book"
→ Bigram P("chick out") is very low
→ Bigram P("check out") is much higher
→ Correct: "check"
```

**Approach:**
1. For each word, generate candidate corrections
2. Score each candidate in context using n-gram language model
3. Select candidate with highest probability

---

## 1.15 Case Study: Morphological Analyzer for Marathi

**Marathi** is an **agglutinative** language with extensive **affix stacking** — multiple suffixes can be added to a single stem.

**Example:**
```
घरांमधून (gharānmadhūn) → घर (ghar, house) + ā (plural) + madhūn (from among)
Meaning: "from among the houses"
```

**Challenges:**
- Multiple suffixes stack on each other
- Sandhi (phonological changes at morpheme boundaries)
- Extensive inflectional paradigms
- Irregular forms

**Approach:**
- Use **FST-based** morphological analyzer
- Build lexicon of stems
- Define suffix ordering rules
- Handle sandhi rules as spelling-change FSTs
- Cascade: Surface form → Spelling FST → Lexicon FST → Morphological features

---

---

# UNIT II: Part of Speech Tagging and Parsing (6 Hrs)

---

## 2.1 Word Classes and Part-of-Speech Tagging

### Word Classes (Parts of Speech)

| Class | Category | Examples |
|---|---|---|
| **Noun (NN)** | Open | dog, city, idea |
| **Verb (VB)** | Open | run, think, is |
| **Adjective (JJ)** | Open | big, red, happy |
| **Adverb (RB)** | Open | quickly, very, well |
| **Pronoun (PRP)** | Closed | he, she, it, they |
| **Preposition (IN)** | Closed | in, on, at, by |
| **Conjunction (CC)** | Closed | and, but, or |
| **Determiner (DT)** | Closed | the, a, this |
| **Interjection (UH)** | Closed | oh, wow, alas |

**Open class:** New words can be added (nouns, verbs, etc.)
**Closed class:** Fixed set, rarely changes (prepositions, determiners, etc.)

### Penn Treebank Tagset (45 tags — commonly used):

| Tag | Description | Example |
|---|---|---|
| NN | Noun, singular | dog |
| NNS | Noun, plural | dogs |
| NNP | Proper noun, singular | London |
| VB | Verb, base form | run |
| VBD | Verb, past tense | ran |
| VBG | Verb, gerund | running |
| VBN | Verb, past participle | run |
| VBZ | Verb, 3rd person singular | runs |
| JJ | Adjective | big |
| RB | Adverb | quickly |
| DT | Determiner | the |
| IN | Preposition | in |
| PRP | Personal pronoun | he |
| CC | Coordinating conjunction | and |

### Part-of-Speech Tagging

**PoS Tagging** is the task of assigning a part-of-speech tag to each word in a sentence.

```
Input:  "The dog runs quickly"
Output: "The/DT dog/NN runs/VBZ quickly/RB"
```

**Why is it hard?**
- **Ambiguity:** Many words can have multiple PoS tags:
  - "book" → NN (noun: "the book") or VB (verb: "book a flight")
  - "run" → VB, NN
  - "back" → RB, JJ, NN, VB

**Approaches:**
1. Rule-Based PoS Tagging
2. Transformation-Based Tagging (TBL / Brill Tagger)
3. Stochastic/Probabilistic (HMM-based)
4. Machine Learning-based (CRF, Deep Learning)

---

## 2.2 Rule-Based PoS Tagging

**Approach:**
1. Assign **all possible tags** to each word from a dictionary
2. Apply **hand-crafted disambiguation rules** to remove incorrect tags

**Example Rules:**
```
Rule 1: If a word is preceded by a determiner (DT) and followed by a noun (NN), 
        remove verb tags → it's likely an adjective (JJ)
        Example: "the light bulb" → light is JJ, not VB or NN

Rule 2: If a word follows a modal verb (MD), assign VB (base verb)
        Example: "can run" → run is VB

Rule 3: If word ends in "-ly", assign RB (adverb)
        Example: "quickly" → RB

Rule 4: If word ends in "-ing" and follows "is/am/are", assign VBG
        Example: "is running" → running is VBG
```

**Advantages:**
- Interpretable, linguistically motivated
- High precision for well-defined rules

**Disadvantages:**
- Requires extensive linguistic expertise
- Hard to scale; rules can conflict
- Language-specific; poor portability

---

## 2.3 Transformation-Based Tagging (TBL / Brill Tagger)

**Eric Brill (1995)** proposed a hybrid approach: start with simple assignment, then learn transformation rules from a tagged corpus.

### Algorithm:

```
Step 1: Initial tagging
   → Assign each word its MOST FREQUENT tag from training data
   → Unknown words: assign NN (or use suffix rules)

Step 2: Learn transformation rules
   → Compare with gold-standard tags
   → Find the rule that corrects the most errors
   → Apply that rule to the corpus
   → Repeat until no improvement

Step 3: Apply learned rules in sequence to new text
```

### Rule Templates:

Rules have the form: **Change tag A to tag B when CONDITION**

| Template | Example |
|---|---|
| Preceding word is tagged X | Change NN to VB if previous tag is MD |
| Following word is tagged X | Change VB to NN if next tag is DT |
| Preceding word is W | Change VB to NN if previous word is "the" |
| Current word suffix is S | Change NN to JJ if word ends in "-ous" |

### Example:

```
Training: "The/DT race/NN was/VBD fast/JJ"

Initial (most frequent tag): "The/DT race/NN was/VBD fast/RB"
                                                          ↑ error (should be JJ)

Error analysis reveals:
Rule: Change RB → JJ when previous tag is VBD
This corrects this error (and others like it)

Learned rules (ordered):
1. RB → JJ if prev tag is VBD
2. NN → VB if prev tag is TO
3. ... (more rules)
```

**Advantages over pure rule-based:**
- Rules are **automatically learned** from data
- Compact rule set
- More systematic and reproducible

**Advantages over HMMs:**
- Rules are interpretable
- Can use any feature (not just bigrams)

---

## 2.4 Introduction to Context-Free Grammars (CFG)

A **Context-Free Grammar (CFG)** is a formal system for generating/describing the syntactic structure of sentences.

### Formal Definition:

A CFG is a 4-tuple G = (N, Σ, R, S) where:
- **N** = set of non-terminal symbols (syntactic categories)
- **Σ** = set of terminal symbols (words)
- **R** = set of production rules of the form A → β (A ∈ N, β ∈ (N ∪ Σ)*)
- **S** = start symbol (usually S for "Sentence")

### Example CFG:

```
S  → NP VP
NP → DT NN | DT JJ NN | PRP | NP PP
VP → VB NP | VB NP PP | VB
PP → IN NP
DT → "the" | "a"
NN → "dog" | "cat" | "park" | "telescope"
JJ → "big" | "small"
VB → "saw" | "chased" | "ran"
PRP → "I" | "he"
IN → "in" | "with"
```

### Parse Tree Example:

Sentence: "The dog chased a cat"

```
            S
           / \
         NP   VP
        / \   / \
      DT  NN VB  NP
      |   |   |  / \
     The dog chased DT NN
                    |   |
                    a  cat
```

### Chomsky Normal Form (CNF)

A CFG is in **Chomsky Normal Form** if every rule is of one of these forms:
- A → B C (two non-terminals)
- A → a (one terminal)
- S → ε (only for start symbol)

**Why CNF?** Required for CKY parsing algorithm.

**Conversion to CNF:**
1. Eliminate ε-productions
2. Eliminate unit productions (A → B)
3. Convert long rules: A → B C D becomes A → B X, X → C D
4. Convert mixed rules: A → B a becomes A → B X, X → a

---

## 2.5 Parsing with Context-Free Grammars

**Parsing** = determining the syntactic structure (parse tree) of a sentence given a grammar.

### Parsing as Search

Parsing can be viewed as a **search problem**:
- **State space:** Partial parse trees
- **Initial state:** Start symbol S (top-down) or input words (bottom-up)
- **Goal state:** Complete parse tree spanning the entire input
- **Operators:** Grammar rules

---

## 2.6 Top-Down Parsing

**Strategy:** Start with S and try to derive the input sentence by expanding non-terminals.

```
Algorithm (Recursive Descent):
1. Start with S
2. Pick a rule S → α
3. Expand leftmost non-terminal in α
4. If terminal matches input word, advance
5. If no match, backtrack and try another rule
6. If all input consumed and no non-terminals remain → success
```

**Example:** Parse "the dog ran" with grammar:
```
S → NP VP,  NP → DT NN,  VP → VB,  DT → "the",  NN → "dog",  VB → "ran"
```

```
Step 1: S
Step 2: S → NP VP → [NP] VP
Step 3: NP → DT NN → [DT] NN VP
Step 4: DT → "the" ✓ → [NN] VP
Step 5: NN → "dog" ✓ → [VP]
Step 6: VP → VB → [VB]
Step 7: VB → "ran" ✓ → SUCCESS
```

**Advantages:**
- Goal-directed (always starts from S)
- Never builds subtrees that don't connect to S

**Disadvantages:**
- May pursue dead-end expansions
- Left recursion causes infinite loop (e.g., NP → NP PP)
- Can be exponential without memoization

---

## 2.7 Bottom-Up Parsing

**Strategy:** Start with input words and try to reduce them to S by finding applicable grammar rules.

```
Algorithm (Shift-Reduce):
1. Start with input words
2. SHIFT: Push next word onto stack
3. REDUCE: If top of stack matches RHS of a rule, replace with LHS
4. Repeat until stack has S and input is consumed
```

**Example:** Parse "the dog ran"

```
Stack            Input           Action
[]               the dog ran     SHIFT
[the]            dog ran         REDUCE: DT → "the"
[DT]             dog ran         SHIFT
[DT, dog]        ran             REDUCE: NN → "dog"
[DT, NN]         ran             REDUCE: NP → DT NN
[NP]             ran             SHIFT
[NP, ran]        (empty)         REDUCE: VB → "ran"
[NP, VB]         (empty)         REDUCE: VP → VB
[NP, VP]         (empty)         REDUCE: S → NP VP
[S]              (empty)         SUCCESS
```

**Advantages:**
- Never builds structures inconsistent with input
- No left recursion problem

**Disadvantages:**
- May build subtrees that don't lead to S
- Ambiguity: when to shift vs. reduce?
- Can be inefficient without guidance

---

## 2.8 Dynamic Programming Parsing: CKY Algorithm

**CKY (Cocke-Kasami-Younger)** is an efficient dynamic programming algorithm for parsing with CNF grammars.

### Prerequisites:
- Grammar must be in **Chomsky Normal Form (CNF)**
- All rules: A → B C or A → a

### Algorithm:

```
Input: words w1, w2, ..., wn
       Grammar G in CNF

Table: T[i][j] = set of non-terminals that can derive wi...wj

Initialization (single words):
  For i = 1 to n:
    T[i][i] = {A | A → wi ∈ R}

Fill table (bottom-up, increasing span length):
  For length = 2 to n:
    For i = 1 to n - length + 1:
      j = i + length - 1
      For k = i to j - 1:    (split point)
        For each rule A → B C:
          If B ∈ T[i][k] and C ∈ T[k+1][j]:
            Add A to T[i][j]

Accept if S ∈ T[1][n]
```

### Time Complexity: **O(n³ · |G|)**
### Space Complexity: **O(n² · |G|)**

### Worked Example:

**Grammar (CNF):**
```
S  → NP VP
VP → VB NP
NP → DT NN
DT → "the"
NN → "dog" | "cat"
VB → "chased"
```

**Input:** "the dog chased the cat"

**CKY Table (upper triangular):**

```
          the    dog    chased   the     cat
     ┌─────┬──────┬────────┬──────┬──────┐
the  │ {DT}│ {NP} │   ∅    │  ∅   │  {S} │  ← T[1][5]
     ├─────┼──────┼────────┼──────┼──────┤
dog  │     │ {NN} │   ∅    │  ∅   │  ∅   │
     ├─────┼──────┼────────┼──────┼──────┤
chased│    │      │  {VB}  │  ∅   │ {VP} │
     ├─────┼──────┼────────┼──────┼──────┤
the  │     │      │        │ {DT} │ {NP} │
     ├─────┼──────┼────────┼──────┼──────┤
cat  │     │      │        │      │ {NN} │
     └─────┴──────┴────────┴──────┴──────┘
```

**Filling T[1][5]:**
- Split at k=2: T[1][2]={NP}, T[3][5]=? → need to check T[3][5]
  - T[3][5]: Split at k=3: T[3][3]={VB}, T[4][5]={NP} → VP → VB NP → VP ∈ T[3][5]
- Back to T[1][5]: Split at k=2: T[1][2]={NP}, T[3][5]={VP} → S → NP VP ✓

**S ∈ T[1][5] → Sentence is grammatical!**

---

## 2.9 Partial Parsing (Chunking)

**Chunking** (also called **shallow parsing**) identifies non-overlapping phrases (chunks) without building a full parse tree.

```
Input:  "The big dog chased the small cat quickly"
Output: [NP The big dog] [VP chased] [NP the small cat] [ADVP quickly]
```

### Chunk Types:
| Chunk | Description | Example |
|---|---|---|
| NP | Noun Phrase | "the big dog" |
| VP | Verb Phrase (verb group) | "has been running" |
| PP | Prepositional Phrase | "in the park" |
| ADJP | Adjective Phrase | "very happy" |
| ADVP | Adverb Phrase | "very quickly" |

### IOB Tagging Scheme:

Chunking is often formulated as a **sequence labeling** task using IOB tags:

| Tag | Meaning |
|---|---|
| B-NP | Beginning of NP chunk |
| I-NP | Inside NP chunk |
| O | Outside any chunk |

**Example:**
```
The/DT  → B-NP
big/JJ  → I-NP
dog/NN  → I-NP
chased/VBD → B-VP
the/DT  → B-NP
cat/NN  → I-NP
```

### Finite-State Rule-Based Chunking

Use **regular expressions over PoS tags** to define chunk patterns:

```python
# NP Chunk pattern
NP: {<DT>?<JJ>*<NN.*>+}
# Matches: optional determiner, zero or more adjectives, one or more nouns

# VP Chunk pattern  
VP: {<MD>?<VB.*>+}
# Matches: optional modal, one or more verbs
```

**Example with NLTK:**
```python
import nltk
grammar = r"NP: {<DT>?<JJ>*<NN>+}"
cp = nltk.RegexpParser(grammar)
sentence = [("the","DT"), ("big","JJ"), ("dog","NN"), ("chased","VBD"), ("a","DT"), ("cat","NN")]
result = cp.parse(sentence)
```

### Machine Learning-Based Approaches to Chunking

**Formulate as sequence labeling:**
- Input: word + PoS tag
- Output: IOB chunk tag

**Features used:**
- Current word and PoS tag
- Surrounding words and tags (window)
- Word shape, prefixes, suffixes

**ML Models:**
1. **HMM:** Sequence model using tag bigrams
2. **Maximum Entropy (MaxEnt):** Discriminative classifier
3. **Conditional Random Fields (CRF):** State-of-the-art for sequence labeling
4. **SVM:** Multiclass classification
5. **Deep Learning:** BiLSTM-CRF, Transformers

**Evaluation Metrics:**
- **Precision** = correct chunks / predicted chunks
- **Recall** = correct chunks / actual chunks
- **F1-score** = 2 × P × R / (P + R)
- A chunk is correct only if **both boundaries and type** match

---

## 2.10 Case Study: POS Tagger for Indian Languages (IIIT Hyderabad)

**Context:** Indian languages have rich morphology, free word order, and limited annotated resources.

**Key Points:**
- Developed at IIIT Hyderabad for Hindi and other Indian languages
- Uses a **BIS (Bureau of Indian Standards) tagset** — standardized across Indian languages
- Combines:
  - Morphological analysis
  - Rule-based disambiguation
  - Statistical methods (HMM/CRF)
- Handles challenges specific to Indian languages:
  - **Free word order:** SOV vs. SVO (Hindi is typically SOV)
  - **Complex morphology:** Postpositions, case markers
  - **Lack of capitalization:** No distinction between proper and common nouns
  - **Compound verbs:** "खा लिया" (kha liya = ate up)

---

---

# UNIT III: Semantic Analysis & Word Sense Disambiguation (6 Hrs)

---

## 3.1 Fundamentals of Semantic Analysis

**Semantics** is the study of meaning in language.

### Levels of Meaning:
| Level | Focuses On | Example |
|---|---|---|
| **Lexical Semantics** | Word-level meaning | "bank" = financial institution or river edge |
| **Compositional Semantics** | How words combine to form phrase/sentence meaning | "big dog" vs. "dog big" |
| **Sentential Semantics** | Sentence truth conditions | "The cat is on the mat" |
| **Discourse Semantics** | Meaning across sentences | Coreference, coherence |

### Key Semantic Concepts:

1. **Synonymy:** Same meaning — "big" / "large"
2. **Antonymy:** Opposite meaning — "hot" / "cold"
3. **Hyponymy:** IS-A relationship — "dog" is a hyponym of "animal"
4. **Hypernymy:** Reverse of hyponymy — "animal" is a hypernym of "dog"
5. **Meronymy:** Part-whole relationship — "wheel" is meronym of "car"
6. **Polysemy:** One word, multiple related meanings — "head" (body part, leader)
7. **Homonymy:** One word, unrelated meanings — "bank" (river, financial)

---

## 3.2 Meaning Representation

### Why Represent Meaning?
To enable computers to:
- Answer questions
- Make inferences
- Translate between languages
- Detect paraphrases

### Meaning Representation Languages:

**1. First-Order Predicate Logic (FOPL):**
```
"Every dog likes a bone"
∀x (Dog(x) → ∃y (Bone(y) ∧ Likes(x,y)))
```

**2. Semantic Networks:**
```
     dog ──IS-A──→ animal
      │
   LIKES
      │
      ▼
     bone ──IS-A──→ object
```

**3. Frames:**
```
Frame: Restaurant-Visit
  Slots:
    Customer: person
    Restaurant: place
    Food-Ordered: food item
    Payment: amount
```

**4. Conceptual Dependency (CD):**
Primitive actions like ATRANS (transfer), PTRANS (physical transfer), MTRANS (mental transfer)

**5. AMR (Abstract Meaning Representation) — Modern:**
```
"The boy wants to go"
(w / want-01
   :ARG0 (b / boy)
   :ARG1 (g / go-02
      :ARG0 b))
```

### Desiderata for Meaning Representation:
1. **Verifiability** — Can check truth against the world
2. **Unambiguous** — Each representation has one interpretation
3. **Canonical form** — Same meaning = same representation
4. **Inferential support** — Supports reasoning
5. **Expressiveness** — Can represent all meanings needed

---

## 3.3 Computational Semantics: Syntax-Driven Semantic Analysis

### Principle of Compositionality (Frege's Principle):
> The meaning of a complex expression is determined by the meanings of its parts and the rules used to combine them.

### Syntax-Driven Approach:
Build semantic representation **alongside** syntactic parsing — each grammar rule has an associated semantic rule.

```
Syntactic Rule:        Semantic Rule:
S  → NP VP            S.sem = VP.sem(NP.sem)
VP → VB NP            VP.sem = λx.VB.sem(x, NP.sem)
NP → DT NN            NP.sem = NN.sem
```

---

## 3.4 Semantic Augmentations to CFG Rules

**Augmented CFG** attaches semantic actions/features to grammar rules.

### Example:

```
Rule: S → NP VP
Semantic: S.sem = VP.sem(NP.sem)

Rule: VP → VB NP
Semantic: VP.sem = λx. VB.sem(NP.sem, x)

Rule: NP → "John"
Semantic: NP.sem = John

Rule: VB → "likes"
Semantic: VB.sem = λy.λx. Likes(x, y)

Rule: NP → "Mary"
Semantic: NP.sem = Mary
```

**Parsing "John likes Mary":**

```
Parse tree:
        S
       / \
     NP   VP
      |   / \
    John VB  NP
          |   |
        likes Mary

Semantic computation (bottom-up):
NP₁.sem = John
NP₂.sem = Mary
VB.sem = λy.λx. Likes(x,y)
VP.sem = VB.sem(NP₂.sem) = λy.λx. Likes(x,y)(Mary) = λx. Likes(x, Mary)
S.sem = VP.sem(NP₁.sem) = λx. Likes(x, Mary)(John) = Likes(John, Mary)
```

**Result: Likes(John, Mary)** ✓

---

## 3.5 Lexical Semantics: Word Senses, Relations Between Senses

### Word Senses

A **word sense** is one specific meaning of a word.

```
"bank":
  Sense 1: Financial institution
  Sense 2: Sloping land beside water
  Sense 3: A supply or stock ("blood bank")
```

### Relations Between Senses:

| Relation | Definition | Example |
|---|---|---|
| **Synonymy** | Same meaning | "big" ↔ "large" |
| **Antonymy** | Opposite meaning | "hot" ↔ "cold" |
| **Hyponymy** | IS-A (more specific) | "dog" → "animal" |
| **Hypernymy** | IS-A (more general) | "animal" → "dog" |
| **Meronymy** | Part-of | "wheel" → "car" |
| **Holonymy** | Has-part (reverse of meronymy) | "car" → "wheel" |
| **Polysemy** | Related senses of same word | "head" (body, leader) |
| **Homonymy** | Unrelated senses of same word | "bank" (river, financial) |
| **Metonymy** | Using one entity to refer to another | "The White House said..." |

---

## 3.6 WordNet

**WordNet** (George Miller, Princeton, 1995) is a large lexical database of English.

### Structure:
- Words are organized into **synsets** (synonym sets)
- Each synset represents a distinct concept
- Synsets are linked by semantic relations

### Key Features:

| Feature | Description |
|---|---|
| **Synset** | Set of synonyms representing one concept: {car, auto, automobile, motorcar} |
| **Gloss** | Short definition + example |
| **Relations** | Hypernymy, hyponymy, meronymy, antonymy, etc. |

### WordNet Relations:

```
              entity
                │
             object
              / \
        animal   vehicle
          │        │
         dog      car
        / \      / \
     poodle collie sedan SUV
```

### Example WordNet Entry:
```
Word: "bank"
Synset 1: {bank, banking company, depository financial institution}
  Gloss: "a financial institution that accepts deposits and channels the money into lending"
  Hypernym: financial_institution
  
Synset 2: {bank}
  Gloss: "sloping land beside a body of water"
  Hypernym: slope, incline
```

### WordNet Statistics (English):
- ~117,000 synsets
- ~155,000 words
- Covers nouns, verbs, adjectives, adverbs

### Applications:
- Word Sense Disambiguation
- Information Retrieval
- Text similarity measurement
- Machine Translation

### WordNet-based Similarity Measures:
1. **Path length:** Inverse of shortest path between synsets
2. **Wu-Palmer:** Based on depth of LCS (Least Common Subsumer)
3. **Lesk Algorithm:** Overlap between glosses
4. **Resnik:** Information content of LCS
5. **Lin:** Normalized information content

---

## 3.7 Word Sense Disambiguation (WSD)

**WSD** is the task of determining which **sense** of a word is used in a given context.

```
"I went to the bank to deposit money"  → bank = financial institution
"The boat was near the bank of the river" → bank = river bank
```

### Approaches to WSD:

### 1. Dictionary/Knowledge-Based Methods:

**a) Lesk Algorithm (Simplified):**
- Compare the **dictionary definition (gloss)** of each sense with the **context** (surrounding words)
- Choose the sense whose gloss has the most **overlap** with context

```
Word: "bank"
Context: "I went to the bank to deposit money"

Sense 1 gloss: "a financial institution that accepts deposits and channels money into lending"
Overlap with context: {deposit, money} → 2 words

Sense 2 gloss: "sloping land beside a body of water"
Overlap with context: {} → 0 words

Choose Sense 1 ✓
```

**b) Extended Lesk Algorithm:**
- Also consider glosses of **related synsets** (hypernyms, hyponyms, etc.)

**c) Walker Algorithm / Graph-Based Methods:**
- Build a graph from WordNet
- Use random walks or PageRank to find the most "central" sense

### 2. Thesaurus-Based Methods:

Use a thesaurus (like Roget's) instead of WordNet:
- Group words by semantic categories
- A word's sense is determined by which category its context words fall into

### 3. Supervised ML Methods (not the main focus in this unit but relevant):
- Train classifiers on sense-annotated corpora (SemCor)
- Features: surrounding words, PoS tags, collocations

### 4. Unsupervised Methods:
- Clustering of word contexts
- Each cluster represents a sense

---

## 3.8 Coreference Resolution

**Coreference** occurs when two or more expressions in a text refer to the **same entity**.

### Types of Reference Phenomena:

**1. Anaphora:**
A reference that points **backward** to a previously mentioned entity (the **antecedent**).

```
"John went to the store. He bought milk."
                          ↑ "He" refers back to "John"
```

**2. Cataphora:**
A reference that points **forward** to an entity mentioned later.

```
"After he finished work, John went home."
       ↑ "he" refers forward to "John"
```

**3. Other Reference Phenomena:**

| Phenomenon | Example |
|---|---|
| **Pronominal reference** | "John... He..." (pronoun refers to noun) |
| **Definite NP reference** | "A dog entered. The dog barked." |
| **Demonstrative reference** | "I saw a movie. That was exciting." |
| **Zero anaphora** | "John entered and ∅ sat down." (subject omitted) |

### Types of Referring Expressions:
- **Indefinite NPs:** "a dog" (introduces new entity)
- **Definite NPs:** "the dog" (refers to known entity)
- **Pronouns:** "he", "she", "it" (refers to salient entity)
- **Proper names:** "John", "London"
- **Demonstratives:** "this", "that"

---

## 3.9 Features for Pronominal Anaphora Resolution

| Feature | Description | Example |
|---|---|---|
| **Number agreement** | Pronoun and antecedent must match in number | "The dogs... they" (not "it") |
| **Gender agreement** | Must match in gender | "Mary... she" (not "he") |
| **Person agreement** | Must match in person | "I... me" (1st person) |
| **Binding constraints** | Syntactic constraints on reflexives and pronouns | "John₁ saw himself₁" (reflexive binds locally) |
| **Recency** | More recent antecedents are preferred | Prefer closest matching NP |
| **Grammatical role** | Subjects are preferred antecedents | Subject > Object > Other |
| **Parallelism** | Prefer antecedent in same grammatical role | |
| **Selectional restrictions** | Semantic compatibility | "The table... it fell" (not "she") |

---

## 3.10 Hobbs Algorithm (Naive / Baseline Algorithm)

The **Hobbs Algorithm** (Jerry Hobbs, 1978) is a tree-search algorithm for resolving pronominal anaphora.

### Algorithm Steps:

```
Input: Parse tree containing the pronoun to be resolved

1. Begin at the NP node immediately dominating the pronoun
2. Go up the tree to the first NP or S node encountered. Call it X.
   Call the path from pronoun to X as path p.
3. Traverse all branches below X to the LEFT of path p,
   in left-to-right, breadth-first order.
   Propose any NP node encountered as antecedent.
   Check agreement (number, gender). If match → RETURN.
4. If no match, go up to next NP or S node. Call it X.
   If X is the highest S node, traverse previous sentences' trees.
5. If X is an S node, traverse branches to the LEFT of p.
   If X is an NP node, check if X itself is a valid antecedent.
6. Traverse branches to the RIGHT of p (for cataphora).
7. If still no match, go to previous sentence and repeat from root.
```

### Simplified intuition:
1. Start at the pronoun
2. Walk up the parse tree
3. At each node, search left subtrees first (preceding text)
4. Propose NPs that match in gender/number
5. Prefer closer, more prominent (subject) antecedents

### Example:

```
"John saw Mary. He waved to her."

Parse tree for second sentence:
        S
       / \
     NP    VP
     |    / \
    He  VB   PP
     |  |   / \
   waved TO  NP
          |   |
         to  her

Resolving "He":
- Go up to S
- Search left (no NPs in this sentence before "He")
- Go to previous sentence
- Find "Mary" (gender: female) → no match
- Find "John" (gender: male) → MATCH
- "He" → John ✓

Resolving "her":
- Go up to PP → S
- Search left: find "He" (already resolved to John, male) → no match
- Go to previous sentence
- Find "Mary" (female) → MATCH
- "her" → Mary ✓
```

---

## 3.11 Case Study: Role of Semantic Relations in Hindi WSD

**Challenges in Hindi WSD:**
- Hindi has rich polysemy
- Fewer lexical resources compared to English
- Hindi WordNet (developed at IIT Bombay) serves as the primary resource

**Approach:**
- Use semantic relations from Hindi WordNet:
  - Hypernymy-hyponymy
  - Meronymy
  - Synonymy
- Apply modified Lesk algorithm using Hindi glosses
- Leverage bilingual dictionaries (Hindi-English) for additional coverage
- Consider syntactic features (postpositions, verb frames) specific to Hindi

---

---

# UNIT IV: Machine Translation & Applications of NLP (6 Hrs)

---

## 4.1 Introduction to Machine Translation (MT)

**Machine Translation** is the automatic translation of text from one natural language (**source**) to another (**target**).

```
Source (French): "Le chat est sur le tapis"
Target (English): "The cat is on the mat"
```

### Brief History:
| Period | Approach | Key System |
|---|---|---|
| 1950s | Rule-based (Direct) | Georgetown-IBM experiment |
| 1960s-70s | Transfer-based | SYSTRAN |
| 1980s-90s | Interlingua, Knowledge-based | Various |
| 1990s-2000s | Statistical MT (SMT) | IBM Models, Moses |
| 2014-present | Neural MT (NMT) | Seq2Seq, Transformer, Google NMT |

---

## 4.2 Classical MT & The Vauquois Triangle

The **Vauquois Triangle** (Bernard Vauquois, 1968) represents different MT strategies arranged by their level of analysis:

```
                    Interlingua
                    /        \
                   /          \
            Analysis        Generation
               /                \
        Transfer (deep)          \
           /                      \
    Transfer (shallow)             \
        /                           \
  Direct Translation                 \
     /                                \
Source Language ─────────────────── Target Language
```

### MT Approaches (bottom to top):

**1. Direct Translation (Word-by-Word):**
- Simplest approach
- Dictionary-based word substitution
- Minimal analysis
- Poor quality — ignores word order, grammar, idioms

```
French: "Je suis un étudiant"
Direct: "I am a student" (works here, but often fails)
French: "Il fait froid" (literally "It makes cold")
Direct: "It makes cold" ✗ (should be "It is cold")
```

**2. Transfer-Based MT:**
- Analyze source into linguistic representation
- Transfer rules convert source representation to target representation
- Generate target text from target representation

```
Three phases:
Source text → [Analysis] → Source representation
Source representation → [Transfer] → Target representation
Target representation → [Generation] → Target text
```

**3. Interlingua-Based MT:**
- Analyze source into a **language-independent** meaning representation (interlingua)
- Generate target from the interlingua
- Advantage: Adding a new language requires only analysis + generation (not N² transfer rules)
- Challenge: Creating a true interlingua is extremely difficult

**Trade-offs:**

| Approach | Analysis Depth | Quality | Effort |
|---|---|---|---|
| Direct | None | Low | Low per pair |
| Transfer | Medium | Medium | Medium |
| Interlingua | Deep | High (theoretically) | Very high initially |

---

## 4.3 Statistical Machine Translation (SMT)

**Core Idea:** Use probability models trained on parallel corpora (aligned source-target text pairs).

### The Noisy Channel Model:

Given a French sentence **f**, find the best English sentence **e**:

$$\hat{e} = \arg\max_e P(e|f) = \arg\max_e P(f|e) \cdot P(e)$$

By Bayes' Rule:
- **P(f|e)** = **Translation Model** — how likely is French sentence f given English sentence e
- **P(e)** = **Language Model** — how likely is English sentence e (fluency)

### Components:

```
Source sentence (f) → [Decoder] → Target sentence (e)
                        ↑   ↑
              Translation  Language
                Model       Model
              P(f|e)        P(e)
```

---

## 4.4 P(F|E): The Phrase-Based Translation Model

### Word-Based Models (IBM Models 1-5):
- Translate word by word
- Learn word-to-word translation probabilities: P(f_j | e_i)
- IBM Model 1: Uniform alignment, only lexical translation
- IBM Models 2-5: Add alignment, fertility, distortion models

### Phrase-Based Translation Model:
Instead of translating word-by-word, translate **phrase-by-phrase**.

```
English phrase → French phrase
"does not"     → "ne ... pas"
"the house"    → "la maison"
"I would like" → "je voudrais"
```

**Key concepts:**
1. **Phrase table:** Maps source phrases to target phrases with probabilities
2. **Phrases** are not linguistic phrases — they are any contiguous word sequences
3. Learned automatically from word-aligned parallel corpora

**Phrase extraction:**
```
Given word alignment:
English: The | cat | sat | on | the | mat
French:  Le  | chat | est | assis | sur | le | tapis

Consistent phrase pairs (where alignment is consistent):
("The cat", "Le chat"), ("sat on", "est assis sur"), ("the mat", "le tapis"), etc.
```

**Scoring:**
$$P(\bar{f}|\bar{e}) = \frac{count(\bar{f}, \bar{e})}{count(\bar{e})}$$

**Decoding:** Find best segmentation and phrase translation:
$$\hat{e} = \arg\max_e \prod_i \phi(\bar{f}_i|\bar{e}_i) \cdot d(start_i - end_{i-1} - 1) \cdot P_{LM}(e)$$

where:
- φ = phrase translation probability
- d = distortion (reordering) penalty
- P_LM = language model score

---

## 4.5 Alignment in MT

**Alignment** is the correspondence between words/phrases in source and target sentences.

### Types of Alignment:

```
English:  The | boy | loves | the | girl
Hindi:    लड़का | लड़की | से | प्यार | करता | है

Alignment:
The boy  → लड़का
loves    → प्यार करता है
the girl → लड़की से
```

**Alignment challenges:**
- **One-to-many:** "the" → (no Hindi equivalent in some cases)
- **Many-to-one:** "kicked the bucket" → "मर गया" (died)
- **Null alignment:** Function words may have no counterpart
- **Reordering:** Hindi is SOV, English is SVO

### IBM Model 1 (Simplest Alignment Model):

$$P(f|e) = \frac{\epsilon}{(l_e + 1)^{l_f}} \prod_{j=1}^{l_f} \sum_{i=0}^{l_e} t(f_j|e_i)$$

where:
- t(f_j|e_i) = probability of translating English word e_i to French word f_j
- Uniform alignment probability
- Trained with **EM algorithm**

### EM Training for IBM Model 1:

```
Initialize t(f|e) uniformly

Repeat until convergence:
  E-step: For each sentence pair, compute expected counts
    For each (f_j, e_i) pair:
      count(f_j|e_i) += t(f_j|e_i) / Σ_k t(f_j|e_k)
  
  M-step: Normalize
    t(f|e) = count(f|e) / Σ_f count(f|e)
```

---

## 4.6 MT Evaluation Techniques

### Human Evaluation:
- **Adequacy:** Does the translation convey the meaning? (1-5 scale)
- **Fluency:** Is the translation grammatically correct and natural? (1-5 scale)
- Expensive, slow, subjective

### Automatic Evaluation:

**1. BLEU (Bilingual Evaluation Understudy) — Papineni et al., 2002:**

Most widely used automatic MT evaluation metric.

**Concept:** Measure n-gram overlap between MT output (candidate) and human reference translations.

$$BLEU = BP \cdot \exp\left(\sum_{n=1}^{N} w_n \log p_n\right)$$

where:
- $p_n$ = modified n-gram precision
- $w_n = 1/N$ (uniform weight, typically N=4)
- $BP$ = brevity penalty

**Modified n-gram precision:**
$$p_n = \frac{\sum_{ngram \in candidate} \min(count_{candidate}(ngram), max\_count_{reference}(ngram))}{\sum_{ngram \in candidate} count_{candidate}(ngram)}$$

**Brevity Penalty:**
$$BP = \begin{cases} 1 & \text{if } c > r \\ e^{1-r/c} & \text{if } c \leq r \end{cases}$$
where c = candidate length, r = reference length

**Example:**
```
Reference: "The cat is on the mat"
Candidate: "The the the the the the"

Unigram precision: "the" appears 2 times in reference
Modified count for "the" in candidate: min(6, 2) = 2
p1 = 2/6 = 0.33

Clearly poor translation → low BLEU score
```

**BLEU Properties:**
- Range: 0 to 1 (higher is better)
- Correlates well with human judgments at corpus level
- Not reliable for single sentences
- Does not capture meaning well — only surface overlap

**2. METEOR (Metric for Evaluation of Translation with Explicit ORdering):**
- Considers synonyms, stems, paraphrases
- Considers word order (via fragmentation penalty)
- Higher correlation with human judgments than BLEU

**3. TER (Translation Edit Rate):**
- Number of edits needed to change MT output to reference
- Lower is better

**4. NIST:**
- Variant of BLEU that gives more weight to less frequent (more informative) n-grams

---

## 4.7 Applications of NLP

### 4.7.1 Information Extraction (IE)

**Goal:** Extract structured information from unstructured text.

**Sub-tasks:**

**a) Named Entity Recognition (NER):**
Identify and classify named entities into categories:

```
Input:  "Apple Inc. was founded by Steve Jobs in Cupertino, California in 1976."
Output: [Apple Inc.]_ORG was founded by [Steve Jobs]_PER in [Cupertino]_LOC, [California]_LOC in [1976]_DATE
```

**Common entity types:**
| Tag | Type | Examples |
|---|---|---|
| PER | Person | Steve Jobs, Einstein |
| ORG | Organization | Apple, WHO, MIT |
| LOC | Location | Paris, India, Mount Everest |
| DATE | Date/Time | January 1, 2024, last week |
| MONEY | Monetary values | $50, €100 |

**Approaches:**
- Rule-based (regex patterns, gazetteers)
- ML: HMM, CRF, MaxEnt
- Deep Learning: BiLSTM-CRF, BERT-based

**b) Relation Extraction:**
Identify relationships between entities:

```
"Steve Jobs founded Apple"
→ (Steve Jobs, FOUNDED-BY, Apple)
```

**c) Event Extraction:**
```
"A magnitude 7.2 earthquake struck Nepal on April 25, 2015"
→ Event: Earthquake
  Location: Nepal
  Date: April 25, 2015
  Magnitude: 7.2
```

---

### 4.7.2 Question Answering (QA) Systems

**Goal:** Automatically answer questions posed in natural language.

**Types:**
| Type | Description | Example |
|---|---|---|
| **Factoid QA** | Answer is a fact | "What is the capital of France?" → "Paris" |
| **List QA** | Answer is a list | "Name all planets in the solar system" |
| **Definition QA** | Answer is a definition | "What is photosynthesis?" |
| **Complex/Why/How QA** | Answer requires reasoning | "Why is the sky blue?" |

**Architecture (IR-based QA):**

```
Question → [Question Analysis] → Question Type + Keywords
                                        │
                                        ▼
                               [Document Retrieval]
                                        │
                                        ▼
                               [Passage Retrieval]
                                        │
                                        ▼
                               [Answer Extraction]
                                        │
                                        ▼
                                     Answer
```

**Steps:**
1. **Question Processing:**
   - Determine question type (who, what, where, when, why, how)
   - Identify expected answer type (person, location, date, etc.)
   - Extract keywords for search

2. **Document/Passage Retrieval:**
   - Use IR techniques to find relevant documents
   - Rank passages by relevance

3. **Answer Extraction:**
   - Find the answer span in retrieved passages
   - Match expected answer type with NER
   - Rank candidate answers

---

### 4.7.3 Text Summarization

**Goal:** Produce a concise summary that captures the essential information.

**Types:**

| Type | Description |
|---|---|
| **Extractive** | Select important sentences from the original text |
| **Abstractive** | Generate new sentences that paraphrase key content |
| **Single-document** | Summarize one document |
| **Multi-document** | Summarize multiple related documents |

**Extractive Summarization Approaches:**

**a) Frequency-based:**
- Score sentences based on word frequency (TF-IDF)
- Select top-scoring sentences

**b) Graph-based (TextRank/LexRank):**
- Build a graph where sentences are nodes
- Edges represent similarity between sentences
- Apply PageRank to find most central sentences

```
S1 ──0.8── S2
│          │
0.3       0.6
│          │
S3 ──0.4── S4

PageRank gives importance scores → select top sentences
```

**c) Position-based:**
- First/last sentences of paragraphs tend to be important
- Title words indicate important content

**d) Machine Learning-based:**
- Train a binary classifier: include sentence in summary or not?
- Features: position, length, word frequency, named entities, cue phrases

**Abstractive Summarization:**
- More challenging — requires language generation
- Modern approaches: Seq2Seq models, Transformers (BART, T5, GPT)

**Evaluation of Summarization — ROUGE:**

**ROUGE (Recall-Oriented Understudy for Gisting Evaluation):**

$$ROUGE\text{-}N = \frac{\sum_{ref} \sum_{ngram \in ref} count_{match}(ngram)}{\sum_{ref} \sum_{ngram \in ref} count(ngram)}$$

| Metric | Description |
|---|---|
| ROUGE-1 | Unigram overlap |
| ROUGE-2 | Bigram overlap |
| ROUGE-L | Longest Common Subsequence |

---

## 4.8 Case Study: MT Systems for Indian Languages

**Key Indian Language MT Systems:**

| System | Description |
|---|---|
| **Anusaaraka** | Based on Panini's grammar; English → Hindi; uses rule-based transfer |
| **Shakti** | IIIT Hyderabad; English → Hindi; hybrid (rule-based + statistical) |
| **Sampark** | Consortium project; translates among 9 Indian languages; transfer-based |
| **Google Translate** | Statistical/Neural; supports Hindi, Bengali, Tamil, Telugu, etc. |
| **Microsoft Translator** | Neural MT for several Indian languages |
| **IndicTrans** | AI4Bharat; multilingual NMT for 11 Indian languages |

**Challenges for Indian Language MT:**
1. **Morphological richness:** Agglutinative languages (Dravidian family)
2. **Free word order:** SOV default but flexible
3. **Divergences:** Structural differences between source and target
4. **Resource scarcity:** Limited parallel corpora
5. **Script diversity:** Different scripts for different languages
6. **Postpositions vs. prepositions:** Hindi uses postpositions
7. **Pro-drop:** Subject pronouns often dropped in Hindi
8. **Compound verbs:** Extensive use in Hindi

---

---

# 📝 Lab Assignments Guide

---

## Assignment 1: Comparative Study of NLP Libraries

| Library | Language | Key Features | Pros | Cons |
|---|---|---|---|---|
| **NLTK** | Python | Tokenization, PoS, parsing, WordNet, corpora | Comprehensive, educational | Slower, not production-ready |
| **spaCy** | Python | NER, PoS, dependency parsing, pipelines | Fast, industrial-grade, pre-trained models | Less flexibility for research |
| **Stanford NLP / Stanza** | Java/Python | Full NLP pipeline, multi-lingual | Accurate, academic standard | Heavy, Java dependency |
| **Gensim** | Python | Topic modeling, Word2Vec, Doc2Vec | Excellent for unsupervised text modeling | Limited NLP pipeline |
| **TextBlob** | Python | Sentiment, PoS, translation | Simple API, beginner-friendly | Limited functionality |
| **OpenNLP** | Java | Tokenization, NER, parsing | Mature Java ecosystem | Less Python support |
| **Transformers (HuggingFace)** | Python | BERT, GPT, T5, all SOTA models | State-of-the-art, 100k+ models | Heavy compute, complex |
| **iNLTK** | Python | Indian language NLP | Hindi, Tamil, etc. support | Limited scope |
| **IndicNLP** | Python | Indian language processing | Tokenization, transliteration | Preprocessing focused |

---

## Assignment 2: Text Preprocessing

```python
import nltk
from nltk.tokenize import word_tokenize, sent_tokenize
from nltk.stem import PorterStemmer, WordNetLemmatizer
from nltk.corpus import stopwords
import re

text = "The cats are running quickly towards the beautiful garden. They couldn't stop!"

# 1. Sentence Tokenization
sentences = sent_tokenize(text)
print("Sentences:", sentences)

# 2. Word Tokenization
tokens = word_tokenize(text)
print("Tokens:", tokens)

# 3. Tokenization using Regular Expressions
tokens_re = re.findall(r'\b\w+\b', text.lower())
print("Regex Tokens:", tokens_re)

# 4. Stop Word Removal
stop_words = set(stopwords.words('english'))
filtered = [w for w in tokens if w.lower() not in stop_words]
print("After stopword removal:", filtered)

# 5. Stemming
stemmer = PorterStemmer()
stemmed = [stemmer.stem(w) for w in filtered]
print("Stemmed:", stemmed)

# 6. Lemmatization
lemmatizer = WordNetLemmatizer()
lemmatized = [lemmatizer.lemmatize(w, pos='v') for w in filtered]
print("Lemmatized:", lemmatized)
```

---

## Assignment 3: Minimum Edit Distance

```python
def min_edit_distance(source, target):
    n = len(source)
    m = len(target)
    
    # Create DP table
    D = [[0] * (m + 1) for _ in range(n + 1)]
    
    # Base cases
    for i in range(n + 1):
        D[i][0] = i
    for j in range(m + 1):
        D[0][j] = j
    
    # Fill table
    for i in range(1, n + 1):
        for j in range(1, m + 1):
            if source[i-1] == target[j-1]:
                sub_cost = 0
            else:
                sub_cost = 1  # or 2 for Levenshtein variant
            
            D[i][j] = min(
                D[i-1][j] + 1,      # deletion
                D[i][j-1] + 1,      # insertion
                D[i-1][j-1] + sub_cost  # substitution
            )
    
    # Print table
    print("   ", "  ".join(["#"] + list(target)))
    for i in range(n + 1):
        row_label = "#" if i == 0 else source[i-1]
        print(f"{row_label}  {'  '.join(str(D[i][j]) for j in range(m+1))}")
    
    return D[n][m]

# Example
source = "INTENTION"
target = "EXECUTION"
distance = min_edit_distance(source, target)
print(f"\nMinimum Edit Distance: {distance}")
```

---

## Assignment 4: PoS Tagging

```python
import nltk
from nltk import pos_tag, word_tokenize, RegexpTagger

text = "The quick brown fox jumps over the lazy dog"
tokens = word_tokenize(text)

# 1. Using NLTK's default PoS tagger
tagged = pos_tag(tokens)
print("NLTK Tagger:", tagged)

# 2. Regex-based PoS tagger
patterns = [
    (r'.*ing$', 'VBG'),         # gerunds
    (r'.*ed$', 'VBD'),          # past tense
    (r'.*es$', 'VBZ'),          # 3rd person singular
    (r'.*ly$', 'RB'),           # adverbs
    (r'.*tion$', 'NN'),         # nouns ending in -tion
    (r'.*ness$', 'NN'),         # nouns ending in -ness
    (r'.*ful$', 'JJ'),          # adjectives ending in -ful
    (r'^(The|the|A|a|An|an)$', 'DT'),  # determiners
    (r'.*', 'NN'),              # default: noun
]
regexp_tagger = RegexpTagger(patterns)
tagged_regex = regexp_tagger.tag(tokens)
print("Regex Tagger:", tagged_regex)

# 3. Using spaCy
import spacy
nlp = spacy.load("en_core_web_sm")
doc = nlp(text)
spacy_tags = [(token.text, token.pos_, token.tag_) for token in doc]
print("spaCy Tagger:", spacy_tags)
```

---

## Assignment 5: Chunking

```python
import nltk
from nltk import pos_tag, word_tokenize, RegexpParser

text = "The big brown dog quickly chased the very small cat in the park"
tokens = word_tokenize(text)
tagged = pos_tag(tokens)
print("PoS Tagged:", tagged)

# Define chunk grammar
grammar = r"""
    NP: {<DT>?<JJ>*<NN.*>+}       # Noun Phrase
    VP: {<MD>?<VB.*>+}             # Verb Phrase
    ADJP: {<RB>?<JJ>+}            # Adjective Phrase
    ADVP: {<RB>+}                  # Adverb Phrase
    PP: {<IN><NP>}                 # Prepositional Phrase
"""

chunker = RegexpParser(grammar)
tree = chunker.parse(tagged)
print("Chunk Tree:")
print(tree)
tree.draw()  # Visual display
```

---

## Assignment 6: CYK Parsing

```python
def cyk_parse(grammar, sentence):
    """CYK Parsing Algorithm for CNF grammar"""
    words = sentence.split()
    n = len(words)
    
    # Initialize table
    table = [[set() for _ in range(n)] for _ in range(n)]
    
    # Fill diagonal (single words)
    for i in range(n):
        for lhs, rhs_list in grammar.items():
            for rhs in rhs_list:
                if len(rhs) == 1 and rhs[0] == words[i]:
                    table[i][i].add(lhs)
    
    # Fill upper triangle (increasing span)
    for length in range(2, n + 1):           # span length
        for i in range(n - length + 1):      # start
            j = i + length - 1               # end
            for k in range(i, j):            # split point
                for lhs, rhs_list in grammar.items():
                    for rhs in rhs_list:
                        if len(rhs) == 2:
                            B, C = rhs
                            if B in table[i][k] and C in table[k+1][j]:
                                table[i][j].add(lhs)
    
    # Print table
    print("\nCYK Table:")
    for i in range(n):
        row = []
        for j in range(n):
            if j >= i:
                row.append(str(table[i][j]) if table[i][j] else "∅")
            else:
                row.append("")
        print(f"  {words[i]:>8}: {row}")
    
    # Check if sentence is valid
    if 'S' in table[0][n-1]:
        print(f"\n'{sentence}' is VALID according to the grammar")
    else:
        print(f"\n'{sentence}' is NOT VALID according to the grammar")
    
    return table

# Grammar in CNF
grammar = {
    'S':  [('NP', 'VP')],
    'VP': [('VB', 'NP')],
    'NP': [('DT', 'NN')],
    'DT': [('the',), ('a',)],
    'NN': [('dog',), ('cat',), ('mouse',)],
    'VB': [('chased',), ('saw',)]
}

cyk_parse(grammar, "the dog chased a cat")
```

---

## Assignment 7: Sentiment Analysis

```python
from textblob import TextBlob
from nltk.sentiment import SentimentIntensityAnalyzer
import nltk

# 1. Single-word sentiment (using a lexicon)
positive_words = {'good', 'great', 'excellent', 'amazing', 'wonderful', 'love', 'happy'}
negative_words = {'bad', 'terrible', 'awful', 'hate', 'sad', 'poor', 'worst'}

word = "excellent"
if word in positive_words:
    print(f"'{word}' → Positive")
elif word in negative_words:
    print(f"'{word}' → Negative")
else:
    print(f"'{word}' → Neutral/Unknown")

# 2. Multi-word / sentence sentiment using TextBlob
text = "The movie was absolutely wonderful and the acting was superb"
blob = TextBlob(text)
print(f"\nTextBlob Polarity: {blob.sentiment.polarity}")  # -1 to 1
print(f"TextBlob Subjectivity: {blob.sentiment.subjectivity}")  # 0 to 1

# 3. Polarity-based using VADER (NLTK)
sia = SentimentIntensityAnalyzer()
sentences = [
    "I love this product, it's amazing!",
    "This is the worst experience ever.",
    "The weather is okay, nothing special.",
    "I'm not unhappy with the results."
]

for sent in sentences:
    scores = sia.polarity_scores(sent)
    compound = scores['compound']
    if compound >= 0.05:
        label = "Positive"
    elif compound <= -0.05:
        label = "Negative"
    else:
        label = "Neutral"
    print(f"\n'{sent}'")
    print(f"  Scores: {scores}")
    print(f"  Sentiment: {label}")
```

---

## Assignment 8: Language Model — Next Word Prediction

```python
from collections import defaultdict, Counter
import random

def build_bigram_model(corpus):
    """Build a bigram language model"""
    bigram_counts = defaultdict(Counter)
    unigram_counts = Counter()
    
    for sentence in corpus:
        tokens = ['<s>'] + sentence.lower().split() + ['</s>']
        for i in range(len(tokens) - 1):
            bigram_counts[tokens[i]][tokens[i+1]] += 1
            unigram_counts[tokens[i]] += 1
    
    # Convert to probabilities
    bigram_probs = {}
    for w1 in bigram_counts:
        bigram_probs[w1] = {}
        for w2 in bigram_counts[w1]:
            bigram_probs[w1][w2] = bigram_counts[w1][w2] / unigram_counts[w1]
    
    return bigram_probs

def predict_next_word(model, word, top_n=5):
    """Predict next word given previous word"""
    word = word.lower()
    if word not in model:
        return "Word not in vocabulary"
    
    candidates = sorted(model[word].items(), key=lambda x: x[1], reverse=True)
    return candidates[:top_n]

# Training corpus
corpus = [
    "I love natural language processing",
    "I love machine learning",
    "natural language processing is fascinating",
    "I study natural language processing at university",
    "machine learning and natural language processing are related",
    "I enjoy studying language and processing text",
]

model = build_bigram_model(corpus)

# Predict
test_words = ["i", "natural", "language", "machine"]
for word in test_words:
    predictions = predict_next_word(model, word)
    print(f"\nAfter '{word}': {predictions}")
```

---

## Assignment 9: Named Entity Recognition

```python
import spacy
import nltk
from nltk import ne_chunk, pos_tag, word_tokenize

text = """Apple Inc. was founded by Steve Jobs, Steve Wozniak, and Ronald Wayne 
in Cupertino, California on April 1, 1976. The company is now worth over 
$2 trillion and is headquartered in the United States."""

# Method 1: Using NLTK
print("=== NLTK NER ===")
tokens = word_tokenize(text)
tagged = pos_tag(tokens)
tree = ne_chunk(tagged)
for subtree in tree:
    if hasattr(subtree, 'label'):
        entity = " ".join(word for word, tag in subtree)
        print(f"  {subtree.label():>12}: {entity}")

# Method 2: Using spaCy
print("\n=== spaCy NER ===")
nlp = spacy.load("en_core_web_sm")
doc = nlp(text)
for ent in doc.ents:
    print(f"  {ent.label_:>12}: {ent.text}")
```

---

# 📚 Quick Revision Summary

| Unit | Key Topics | Key Algorithms/Concepts |
|---|---|---|
| **Unit I** | NLP intro, Morphology, N-grams | FST, Porter Stemmer, MED (DP), N-gram LM, Smoothing, Perplexity |
| **Unit II** | PoS Tagging, Parsing, Chunking | Rule-based tagger, Brill Tagger, CFG, Top-down/Bottom-up parsing, CKY, IOB chunking |
| **Unit III** | Semantics, WSD, Coreference | WordNet, Lesk Algorithm, Semantic relations, Hobbs Algorithm |
| **Unit IV** | MT, IE, QA, Summarization | Vauquois Triangle, SMT, Phrase-based MT, BLEU, NER, TextRank |

---

This comprehensive guide covers all four units of the AD32232 NLP course with detailed explanations, algorithms, examples, and practical code for all nine assignments. Use this as your primary study and revision resource!
