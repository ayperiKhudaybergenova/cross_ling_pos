
# Addressing Agglutinative Complexity: A Cross-Lingual Pipeline for Karakalpak NLP.

A computational linguistics project dedicated to building robust NLP resources for the Karakalpak language using Universal Dependencies (UD) and finite-state morphology.

## Overview

This project addresses the linguistic resource gap for Karakalpak, a Turkic language of the Kipchak branch. By integrating rule-based finite-state transducers (FSTs) with neural models, we provide a reproducible pipeline for morphological analysis and POS tagging.

## Research Purpose

The objective is to establish standardized linguistic data for Karakalpak. By adhering to the **Universal Dependencies (UD) CoNLL-U standard**, we ensure our annotations are interoperable with global linguistic research, facilitating comparative studies across the Turkic language family.

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



```
3. **Export:** The script will output a cleaned `corrected_tagged_data.txt` file ready for your UD treebank.

---
*Developed as part of an ongoing initiative to advance Karakalpak computational linguistics.*



```
