# Named Entity Recognition for High Energy Physics Literature Using SciBERT

## Overview

This project presents a transformer-based Named Entity Recognition (NER) system designed for High Energy Physics (HEP) scientific literature. The system uses SciBERT, a language model pretrained on scientific text, to automatically identify and extract domain-specific entities from HEP research abstracts.

The work focuses on extracting important scientific entities such as:

- Particles
- Detector systems
- Experiments
- Research facilities
- Collision types
- Energy measurements

A custom annotated HEP-NER dataset was constructed using abstracts collected from arXiv categories . The dataset was manually annotated using the BIO tagging scheme and used to fine-tune SciBERT for token classification.

The final model achieved a weighted F1-score of **0.97** on the custom HEP-NER dataset.

---

# Research Paper

The full research paper is available in the `paper/` directory.

**Paper Title:**

> Named Entity Recognition for High Energy Physics Literature Using SciBERT

---

# Abstract

High Energy Physics (HEP) research produces a large volume of scientific literature containing complex and domain-specific terminology related to particles, detectors, experiments, and energy measurements. Extracting useful information from these papers manually is both time-consuming and prone to inconsistency.

This project presents a Named Entity Recognition (NER) system designed to automatically identify and extract key scientific terms from HEP research abstracts using SciBERT. A custom annotated dataset was constructed from arXiv abstracts and labeled using the BIO tagging scheme.

The system recognizes entities including:

- Higgs boson
- CMS
- ATLAS
- CERN
- Energy values such as 13 TeV

The results demonstrate that transformer-based scientific language models can effectively perform domain-specific entity extraction for HEP literature.

---

# Project Structure

```bash
HEP-NER-SciBERT/
│
├── paper/
│   └── research_paper.pdf
│
├── dataset/
│   ├── hep_raw.csv
│   ├── hep_bio.csv
│   └── label_mapping.json
│
├── notebooks/
│   └── train_scibert_hep_ner.ipynb
│
├── results/
│   ├── entity_confusionmatrix.png
│   ├── loss_and_f(1).png
│   ├── comparision_graph.png
|   └── BIO_label.png
|   └── entity_mention.png
|   └── performance_compare.png
│
├── requirements.txt
└── README.md
```

---

# Dataset Description

## Dataset Source

The dataset was constructed using scientific abstracts collected from arXiv categories:

- `hep-ex`
- `hep-ph`

A total of **400 HEP abstracts** were manually annotated.

---

# Entity Classes

The dataset contains six domain-specific entity categories:

| Entity Type | Description |
|---|---|
| PARTICLE | Particle names such as Higgs boson, proton |
| DETECTOR | Detector systems such as CMS tracker |
| EXPERIMENT | Experimental collaborations such as CMS |
| FACILITY | Research facilities such as CERN |
| ENERGY | Energy values such as 13 TeV |
| COLLISION | Collision process terminology |

---

# BIO Tagging Scheme

The dataset uses the BIO tagging format.

| Tag | Meaning |
|---|---|
| B | Beginning of entity |
| I | Inside entity |
| O | Outside any entity |

Example:

```text
Higgs      B-PARTICLE
boson      I-PARTICLE
at          O
CERN       B-FACILITY
```

---

# Model Architecture

The project fine-tunes:

- SciBERT (`allenai/scibert_scivocab_uncased`)

for token classification using the Hugging Face Transformers framework.

---

# Technologies Used

| Tool | Purpose |
|---|---|
| Python | Programming language |
| PyTorch | Deep learning framework |
| Hugging Face Transformers | Model training |
| Hugging Face Datasets | Dataset handling |
| Google Colab | Training environment |
| SciBERT | Scientific language model |
| seqeval | NER evaluation |
| scikit-learn | Metrics and analysis |
| Matplotlib | Visualization |
| Pandas | Data processing |

---

# Training Configuration

| Hyperparameter | Value |
|---|---|
| Learning Rate | 2e-5 |
| Epochs | 3 |
| Train Batch Size | 8 |
| Eval Batch Size | 16 |
| Weight Decay | 0.01 |
| Warmup Ratio | 0.1 |
| Gradient Accumulation | 2 |
| Mixed Precision | fp16 |
| Random Seed | 42 |

---

# Experimental Results

## Transformer Model Comparison

| Model | Precision | Recall | F1-Score |
|---|---|---|---|
| BERT-base-uncased | 0.8773 | 0.9112 | 0.8939 |
| SciBERT (Ours) | 0.9562 | 0.9756 | 0.9658 |

---

# Entity-Level Results

| Entity | Precision | Recall | F1-Score |
|---|---|---|---|
| COLLISION | 1.00 | 1.00 | 1.00 |
| DETECTOR | 0.90 | 0.92 | 0.91 |
| ENERGY | 1.00 | 1.00 | 1.00 |
| EXPERIMENT | 0.83 | 0.92 | 0.88 |
| FACILITY | 1.00 | 1.00 | 1.00 |
| PARTICLE | 1.00 | 1.00 | 1.00 |

Weighted F1-score: **0.97**

---

# Key Findings

- Scientific pretraining significantly improves HEP entity extraction.
- SciBERT outperformed general-domain BERT on the custom HEP-NER dataset.
- DETECTOR and EXPERIMENT classes showed semantic ambiguity due to overlapping terminology.
- Transformer-based models can effectively learn domain-specific scientific vocabulary even with relatively small annotated datasets.

---

# Running the Project

## 1. Clone Repository

```bash
git clone https://github.com/yourusername/HEP-NER-SciBERT.git
cd HEP-NER-SciBERT
```

---

## 2. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## 3. Run Notebook

Open:

```bash
notebooks/train_scibert_hep_ner.ipynb
```

using:

- Jupyter Notebook
- VS Code
- or Google Colab

---

# Example Prediction

## Input

```text
The Higgs boson was detected at CERN using the CMS detector at 13 TeV.
```

## Output

```text
Higgs boson    → PARTICLE
CERN           → FACILITY
CMS            → DETECTOR
13 TeV         → ENERGY
```

---

# Limitations

- The dataset contains only 400 annotated abstracts.
- Astro-HEP-BERT was not directly fine-tuned on the dataset.
- Nested NER and relation extraction were outside the scope of the current study.

---

# Future Work

Future extensions may include:

- Larger HEP datasets
- Full-paper scientific NER
- Nested Named Entity Recognition
- Scientific relation extraction
- Knowledge graph construction
- Controlled evaluation of Astro-HEP-BERT

---

# Acknowledgements

This project makes use of:

- Hugging Face Transformers
- SciBERT by AllenAI
- arXiv scientific abstracts
- Google Colab GPU resources

---
