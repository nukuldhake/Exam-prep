# Unit IV: Machine Translation & Applications of NLP

## 1. Machine Translation (MT)
- **Classical MT Approaches (Vauquois Triangle)**:
    - **Direct**: Word-to-word translation with some reordering.
    - **Transfer**: Structural analysis of source, transfer to target structure, then generation.
    - **Interlingua**: Mapping source to a language-neutral representation, then generating target.
- **Statistical MT (SMT)**:
    - Uses the Noisy Channel Model.
    - Formula: $\hat{e} = \text{arg max}_e P(f|e)P(e)$.
    - $P(f|e)$ is the **Translation Model** (adequacy).
    - $P(e)$ is the **Language Model** (fluency).
- **Phrase-Based MT**: Translates small chunks of text (phrases) rather than individual words.
- **Alignment**: Mapping corresponding words/phrases between source and target sentences (e.g., IBM Models).

## 2. MT Evaluation
- **Human Evaluation**: Accuracy, Fluency, Post-editing effort.
- **Automatic Evaluation**:
    - **BLEU (Bilingual Evaluation Understudy)**: Measures n-gram overlap between machine output and human references.
    - **METEOR**: Considers synonyms and stemming.

## 3. Applications of NLP
- **Information Extraction (IE)**:
    - Named Entity Recognition (NER): Identifying names, dates, places.
    - Relation Extraction: Finding relations between entities (e.g., "CEO of").
- **Question Answering (QA)**:
    - Retrieving precise answers from a corpus.
    - Components: Question classification, passage retrieval, answer extraction.
- **Summarization**:
    - **Extractive**: Picking key sentences from the original text.
    - **Abstractive**: Generating new sentences to summarize the meaning.

## 4. Case Study: Indian Language MT Systems
- **Sampark**: A consortium project for MT between Indian languages.
- **Anusaaraka**: Focuses on "language access" by showing the mapping between source and target.
- **AnglaBharti**: Rule-based system for English to Indian language translation.
