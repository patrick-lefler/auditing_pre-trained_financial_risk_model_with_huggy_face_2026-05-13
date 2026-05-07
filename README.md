# Auditing a Pre-Trained Financial Risk Model With Huggy Face
> A Practical Introduction to Model Governance Using `hfhub` and `tok`

**Author:** Patrick Lefler
**Published:** 2026-05-13
**Rendered:**

---

## Introduction

> Demonstrates how risk practitioners can programmatically audit open-source AI model metadata in R — producing a reproducible, SR 11-7-aligned governance record without inference code, a GPU, or a Python dependency.

## Overview

The project applies the `hfhub` and `tok` R packages to a structured metadata audit of FinBERT (`ProsusAI/finbert`), a BERT-based sentiment classifier widely deployed in fintech AI pipelines. Using `hub_download()` and vocabulary composition analysis, the workflow retrieves and parses model architecture parameters, tokenizer configuration, and context window constraints directly from the Hugging Face Hub. The result is a governance audit card aligned to SR 11-7 documentation expectations — a transferable template any risk team can adapt for third-party model due diligence. The project is designed for practitioners with intermediate R proficiency who need a board-ready entry point into AI model governance.

## Tech Stack

- **Language:** R
- **Framework:** [Quarto](https://quarto.org/)
- **Primary Libraries:** hfhub, tok, tidyverse, kableExtra, plotly, jsonlite
- **Deployment / Output:** Self-contained HTML (`embed-resources: true`)

## Repository Structure

```
├── data/                   # Raw and processed datasets (if applicable)
├── models/                 # Cached model artifacts from Hugging Face Hub
├── output/                 # Rendered HTML file
├── _brand.yml              # Brand configuration
├── _quarto.yml             # Project-level Quarto configuration
├── INSTRUCTIONS.md         # Project conventions and standards
└── finbert_model_audit.qmd # Main Quarto entry point
```

## Key Findings

**Truncation is silent and consequential.** FinBERT's 512-token context ceiling — roughly 380 words — is exceeded by most substantive financial documents. The model produces no error or flag when inputs are truncated; it returns a confidence score indistinguishable from one generated on complete input. Any production deployment must log token counts explicitly and route truncated documents to manual review.

**Training data provenance is narrower than the model's reputation suggests.** FinBERT was trained on approximately 4,840 Reuters and Bloomberg news articles. Performance on internal credit narratives, regulatory examination findings, or customer-facing disclosures is unvalidated. Domain drift between news headlines and operational risk text is a material limitation that the model card does not quantify.

**SR 11-7 classification is unambiguous.** An open-source model that informs a consequential financial decision is a model for purposes of model risk management — regardless of how it is described internally. Independent validation against firm-specific data and ongoing performance monitoring are not discretionary. The governance audit card produced here is a starting point for that documentation, not a substitute for it.

## License

This project is licensed under the MIT License. See the LICENSE file for details.

## Contact

Patrick Lefler — [LinkedIn](https://www.linkedin.com/in/patricklefler/) | [GitHub Pages](https://patrick-lefler.github.io) | [Substack](https://substack.com/@pflefler)
