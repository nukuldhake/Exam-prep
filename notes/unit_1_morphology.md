# Unit I: Introduction & Morphological Analysis

## 1. Introduction to NLP
- **History of NLP**: 
    - **1940s-50s**: Weaver's Memorandum (1949), Alan Turing's "Computing Machinery and Intelligence" (1950), Georgetown-IBM experiment (1954 - early MT demo).
    - **1960s-70s**: ALPAC report (1966 - highlighted MT difficulties), Lighthill report (1973), Rule-based systems (ELIZA, SHRDLU).
    - **1980s-90s**: Shift to Statistical NLP, introduction of large corpora and probabilistic models.
    - **2000s-Present**: Deep Learning Era, Word Embeddings (Word2Vec), RNNs/LSTMs, and the Transformer revolution (BERT, GPT).
- **Levels of Language Processing**:
    1. **Phonology**: Study of speech sounds and their patterns.
    2. **Morphology**: Study of word structure and formation (morphemes).
    3. **Lexical**: Identifying distinct words and their grammatical categories.
    4. **Syntactic**: Determining the structural relationship between words (parsing).
    5. **Semantic**: Determining the literal meaning of sentences.
    6. **Discourse**: Understanding meaning across multiple sentences/context.
    7. **Pragmatic**: Understanding how context affects the interpretation of meaning.
- **Ambiguity in Natural Language**:
    - **Lexical**: One word, multiple meanings (e.g., "bank").
    - **Syntactic**: Multiple parse trees (e.g., "I saw the man with the telescope").
    - **Semantic**: Multiple meanings for a sentence.
    - **Anaphoric**: Pronoun reference ambiguity.
- **Challenges**: Diversity of languages, evolving slang, context dependence, irony/sarcasm.
- **Applications**: Machine Translation, Sentiment Analysis, Chatbots, Text Summarization.

## 2. Morphological Analysis
- **Morphology**: The study of how words are formed from basic units called **morphemes**.
    - **Free Morphemes**: Can stand alone (e.g., "book").
    - **Bound Morphemes**: Must be attached (e.g., "-s" in "books").
- **Finite-State Morphological Parsing**:
    - Uses Finite State Automata (FSA) to recognize valid word forms.
- **Finite-State Transducers (FSTs)**:
    - Extends FSA to map input strings to output strings.
    - Used for mapping surface forms (e.g., "cats") to lexical forms (e.g., "cat + N + PL").
- **Porter Stemmer**:
    - A rule-based algorithm for suffix stripping to find the word root (stem).
    - Uses a series of 5 stages of rules (e.g., "sses" -> "ss", "ies" -> "i").

## 3. Tokenization & Basic Tasks
- **Word Tokenization**: Splitting text into individual words.
- **Sentence Tokenization**: Splitting text into sentences (handles "." vs abbreviations).
- **Spelling Detection & Correction**:
    - **Minimum Edit Distance (Levenshtein Distance)**: The minimum number of operations (insert, delete, substitute) required to transform one string into another.
    - **N-Grams**:
        - Sequence of $n$ items from a given text.
        - Unigram (1), Bigram (2), Trigram (3).
        - Used for language modeling and spelling correction (predicting the next word or checking the probability of a sequence).

## 4. Case Study: Marathi Morphological Analyzer
- **Affix Stacking**: Marathi is an agglutinative language where multiple suffixes can be added to a root (e.g., "gharatilach" -> house-in-from-only).
- **Analysis**: Requires handling complex inflectional and derivational morphology using FSTs or rule-based engines.
