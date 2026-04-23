# Unit II: Part of Speech Tagging and Parsing

## 1. Word Classes and POS Tagging
- **Part-of-Speech (POS) Tagging**: The process of assigning a word class (noun, verb, adjective, etc.) to each word in a corpus.
- **Word Classes**:
    - **Open Class**: Nouns, Verbs, Adjectives, Adverbs (new words added frequently).
    - **Closed Class**: Prepositions, Pronouns, Conjunctions (fixed set).
- **Tagging Approaches**:
    1. **Rule-based POS Tagging**: Uses a dictionary and hand-written rules to disambiguate (e.g., if a word ends in "ing" and follows "is", it's a verb).
    2. **Transformation-Based Tagging (Brill Tagging)**:
        - Starts with a simple tagging (e.g., most frequent tag).
        - Applies "transformations" based on context to fix errors (e.g., change NN to VB if previous word is "to").

## 2. Formal Grammars
- **Context-Free Grammar (CFG)**:
    - Formalism for representing the structure of sentences.
    - Defined by $G = (V, \Sigma, R, S)$.
    - Uses non-terminals (NP, VP) and terminals (words).
- **Parsing with CFGs**:
    - **Top-Down Parsing**: Starts from the root symbol (S) and expands down to the words.
    - **Bottom-Up Parsing**: Starts from the words and aggregates up to the root.

## 3. Parsing Algorithms
- **Parsing as Search**: Finding the correct sequence of rules that derive the input sentence.
- **CKY Parsing (Cocke-Younger-Kasami)**:
    - A dynamic programming algorithm for parsing.
    - Requires the grammar to be in **Chomsky Normal Form (CNF)** ($A \rightarrow BC$ or $A \rightarrow a$).
    - Completes in $O(n^3 \cdot |G|)$ time.

## 4. Partial Parsing and Chunking
- **Chunking**: Grouping words into non-overlapping grammatical phrases (chunks), such as Noun Phrases (NP) or Verb Phrases (VP).
- **Finite-State Rule-Based Chunking**: Uses regular expressions over POS tags to identify chunks.
- **Machine Learning-Based Chunking**: Treats chunking as a sequence labeling task (often using IOB tagging: Inside, Outside, Beginning).

## 5. Case Study: Indian Language POS Tagger (IIIT Hyderabad)
- Developed for languages like Hindi, Marathi, Telugu.
- Uses a hierarchical tagset to handle the morphological richness of Indian languages.
- Often combines statistical models (HMM/CRF) with language-specific rules.
