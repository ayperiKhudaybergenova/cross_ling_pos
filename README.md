# Cross-Lingual POS Tagging for Karakalpak

## Project Overview

This project investigates cross-lingual part-of-speech (POS) tagging for Karakalpak, a low-resource Turkic language. The main objective is to examine whether NLP models trained on other Turkic languages can provide useful POS predictions for Karakalpak text without requiring a model trained from scratch on a large Karakalpak-annotated dataset.

The project uses Stanza pipelines for Turkish and Kazakh to assign Universal Part-of-Speech (UPOS) tags to Karakalpak text. These languages were selected because they provide different types of linguistic similarity: Kazakh and Karakalpak belong to the Kipchak branch of the Turkic language family, while Turkish belongs to the Oghuz branch and more  investigated. Comparing their predictions allows us to investigate how language relatedness may affect cross-lingual transfer.

The project also examines whether Karakalpak-specific lexical and suffix-based rules can correct errors in the transferred predictions. The results will be compared against manually annotated Karakalpak examples.

## Research Questions

1. How well can Stanza models trained for Turkish and Kazakh assign POS tags to Karakalpak text?
2. Does the Kazakh model perform differently from the Turkish model on the same Karakalpak examples?
3. Which POS-tagging errors are associated with Karakalpak vocabulary, agglutinative morphology, and differences in tokenization?
4. Can language-specific correction rules improve tagging performance?
5. How does TurkicNLP perform on the same manually annotated evaluation data?

## Methodological Approach

The project follows a comparative, cross-lingual approach:

1. **Corpus preparation:** Load Karakalpak text, inspect the data, and select sentences for analysis.
2. **Turkish baseline:** Apply the Turkish Stanza pipeline to Karakalpak text and save the predicted POS tags.
3. **Kazakh baseline:** Apply the Kazakh Stanza pipeline, using transliteration where required by the model's script, and examine its predictions.
4. **Error correction:** Apply selected Karakalpak lexical and morphological rules to investigate whether they correct model errors.
5. **Manual evaluation:** Compare model predictions against manually assigned UPOS tags.
6. **TurkicNLP comparison:** Evaluate the existing toolkit on the same eligible test examples and compare the results using consistent evaluation procedures.

The purpose is not to assume that a related language will automatically produce accurate results. Instead, the project tests how far cross-lingual transfer works for Karakalpak and identifies where language-specific information is needed.

## Current Work

The repository contains experimental outputs from Turkish and Kazakh Stanza tagging, a transliterated Kazakh input, a correction log, a Python lexical rules file, and a manually annotated dataset of 100 examples.

The current outputs provide a starting point for systematic evaluation. The next step is to verify the manual annotation format, ensure consistent token alignment, and calculate baseline accuracy before making claims about improvements.

## Scope and Limitations

The current work focuses on POS tagging, rather than full syntactic parsing or a complete morphological analyzer. The Turkish and Kazakh models are used as cross-lingual baselines; their predictions are not assumed to be correct for Karakalpak.

Karakalpak-specific rules are treated as experimental corrections. Their value must be measured on data that were not used to develop the rules. The project will report measured accuracy and error patterns rather than assuming that any model or correction method is better in advance.


## Methodology & Comparative Analysis

Our pipeline bridges the gap between neural performance and linguistic rigor:

| Language/Tool | Role | Improvement Method |
| --- | --- | --- |
| **Karakalpak** | Primary target language | Applied rule-based corrections for agglutinative structures. |
| **Kazakh** | Neural baseline | Utilized structural expectations from shared Kipchak features. |
| **Turkish** | Framework reference | Adapted established mature NLP treebank logic. |
| **FSTs (`.lexc`)** | Morphology Engine | Defined valid morphological transitions for word building. |
| **Stanza** | Neural Parser | Used for high-performance initial POS tagging. |


## Key Findings & Improvements

Our research demonstrates that neural models often default to generic tags (e.g., `NOUN`) for out-of-vocabulary agglutinative words. We improved accuracy through:

* **Rule-Based Correction Layer:** A Python script forces correct POS tags for known function words (e.g., *bul*, *hám*) to override neural misclassifications.
* **Input Normalization:** Pre-processing steps isolate punctuation (e.g., brackets, hyphens) to prevent tokenization errors.
* **Morphological Rigor:** Using `.lexc` files ensures that the system respects the formal grammatical rules of Karakalpak morphology alongside probabilistic tagging.

## Quick Start

To run the analysis pipeline:

1. **Upload Data:** Load your target text file into the environment.
2. **Apply Corrections:** Run the `fixer_script.py` to refine the output of the neural models:
```bash
python fixer_script.py --input final_tagged_data.txt

```
## Results 

| Model | Evaluation | Accuracy | Performance Level |
|-------|------------|---------:|-------------------|
| Turkish Stanza | Manual evaluation | **37.00%** | Low |
| Kazakh Stanza | Manual evaluation | **65.00%** | Moderate |
| Kazakh Stanza + Rule-Based Correction | Manual evaluation | **71.00%** | Good |
| TurkicNLP (Glot500) | Gold-standard evaluation | **73.89%** | Good |




## Performance by POS Tag (TurkicNLP)

| POS Tag | Precision | Recall | F1-score | Support |
|---------|----------:|-------:|---------:|--------:|
| NOUN   | 0.83 | 0.75 | 0.79 | 550 |
| VERB   | 0.73 | 0.89 | 0.80 | 184 |
| PUNCT  | 0.96 | 0.86 | 0.91 | 237 |
| ADJ    | 0.71 | 0.58 | 0.64 | 157 |
| PROPN  | 0.57 | 0.86 | 0.68 | 79 |
| NUM    | 0.58 | 0.89 | 0.70 | 37 |
| PRON   | 0.51 | 0.67 | 0.58 | 42 |
| CCONJ  | 0.47 | 0.60 | 0.53 | 43 |
| ADP    | 0.46 | 0.61 | 0.53 | 31 |
| ADV    | 0.57 | 0.37 | 0.45 | 46 |
| AUX    | 0.80 | 0.50 | 0.62 | 24 |
| DET    | 0.42 | 0.19 | 0.26 | 27 |
| PART   | 0.07 | 0.33 | 0.12 | 3 |


```
3. **Export:** The script will output a cleaned `corrected_tagged_data.txt` file ready for your UD treebank.

---
*Developed as part of an ongoing initiative to advance Karakalpak computational linguistics.*



```
