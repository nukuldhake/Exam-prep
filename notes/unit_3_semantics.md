# Unit III: Semantic Analysis and Word Sense Disambiguation

## 1. Fundamentals of Semantic Analysis
- **Semantic Analysis**: Creating a representation of the meaning of an utterance.
- **Meaning Representation**:
    - FOPC (First Order Predicate Calculus).
    - Semantic Networks.
    - Frames.
- **Requirements**: Veridicality, Unambiguity, Canonicity, Inference.

## 2. Computational Semantics
- **Syntax-Driven Semantic Analysis**: Meaning is constructed recursively based on the syntactic structure (Principle of Compositionality).
- **Semantic Augmentations to CFG**: Attaching semantic rules to grammar rules (e.g., $NP \rightarrow ProperNoun \ \{ProperNoun.sem\}$).

## 3. Lexical Semantics
- **Word Senses**: Different meanings of the same lemma.
- **Relations**:
    - **Synonymy**: Same meaning.
    - **Antonymy**: Opposite meaning.
    - **Hyponymy**: IS-A relation (General -> Specific).
    - **Meronymy**: Part-whole relation.
- **WordNet**: A large lexical database for English organizing words into **Synsets**.

## 4. Word Sense Disambiguation (WSD)
- **Task**: Determining which sense of a word is used in context.
- **Lesk Algorithm**:
    - Chooses the sense whose definition has the most word overlap with the context of the target word.
- **Selectional Preferences**: Using constraints (e.g., "eat" expects something "edible").

## 5. Coreference Resolution
- **Anaphora**: Referring back (e.g., "John saw a movie. **He** liked it.").
- **Cataphora**: Referring forward (e.g., "Because **he** was cold, John put on a coat.").
- **Hobbs Algorithm**:
    - A syntax-based algorithm for resolving pronouns.
    - It searches the parse tree for a matching noun phrase candidate using specific traversal rules.

## 6. Case Study: Hindi WSD
- Focuses on using semantic relations (synonymy, hypernymy) from IndoWordNet to disambiguate Hindi words.
- Handles complexities like multi-word expressions and free word order in Hindi.
