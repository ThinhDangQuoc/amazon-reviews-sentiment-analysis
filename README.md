# Amazon Reviews Sentiment Analysis

[![Python 3.11](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?logo=pytorch&logoColor=white)](https://pytorch.org/)
[![Hugging Face](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Transformers-yellow)](https://huggingface.co/)
[![Course](https://img.shields.io/badge/UIT-CS221%20NLP-orange)](https://www.uit.edu.vn/)

An end-to-end sentiment classification project for Amazon customer reviews, comparing classical machine learning approaches (TF-IDF with Logistic Regression and Random Forest) against transfer learning using **RoBERTa** (`roberta-base`).

---

## 📌 Project Information

- **Institution:** University of Information Technology (UIT) – Vietnam National University, Ho Chi Minh City (VNU-HCM)
- **Faculty:** Faculty of Computer Science (Khoa Khoa học Máy tính)
- **Course:** Natural Language Processing - CS221 (Xử lý ngôn ngữ tự nhiên)
- **Supervisor:** Dr. Nguyễn Trọng Chỉnh (TS. Nguyễn Trọng Chỉnh)
- **Team Name:** WRONG TIMES
- **Student:** Đặng Quốc Thịnh (MSSV: `23521494`)

---

## 🎯 Problem Statement

Online customer reviews play a critical role in consumer decision-making and business analytics. While 1-to-5 star ratings provide a high-level summary, sentiment can be nuanced:
- Reviews with intermediate ratings (2, 3, or 4 stars) often contain mixed sentiments.
- Textual semantics (e.g., sarcasm, domain-specific terminology, subtle praise or complaints) challenge traditional n-gram and bag-of-words models.

**Objective:** Build and evaluate multi-class sentiment classifiers that map review texts to their corresponding star rating classes ($[0, 4]$ remapped from 1 to 5 stars).

---

## 🔬 Approaches & Architectures

1. **TF-IDF + Logistic Regression (Baseline 1)**:
   - Text preprocessing: Lowercasing, punctuation stripping, tokenization via NLTK, stopword removal.
   - Feature representation: N-gram TF-IDF vectorization.
   - Classification: Multinomial Logistic Regression with L2 regularization.

2. **TF-IDF + Random Forest (Baseline 2)**:
   - Ensemble decision tree classifier trained on TF-IDF vectors to capture non-linear feature interactions.

3. **RoBERTa Fine-Tuning (Proposed Method)**:
   - Base model: `roberta-base` (12-layer Transformer, 768 hidden dimension, 12 attention heads, 125M parameters).
   - Tokenization: Byte-level Byte-Pair Encoding (BPE) with maximum sequence length capped at 128 tokens.
   - Optimization: Hugging Face `Trainer` API with AdamW optimizer, linear warmup, weight decay (0.01), evaluation loss checkpointing, and GPU acceleration.

---

## 📊 Benchmark Results

Evaluated on the held-out test split of Amazon reviews across all 5 sentiment classes:

| Model | Feature / Architecture | Accuracy | Macro F1-Score |
|---|---|:---:|:---:|
| **Logistic Regression** | TF-IDF (N-grams) | 46% | 45% |
| **Random Forest** | TF-IDF (N-grams) | 44% | 42% |
| **RoBERTa (Fine-tuned)** | Transformer (`roberta-base`) | **58%** | **58%** |

### Key Observations:
- **Transformer Superiority:** RoBERTa outperforms traditional bag-of-words baselines by **+12% to +14%** in both Accuracy and F1-score.
- **Polar vs. Intermediate Sentiments:** Classical baselines achieve reasonable recall only on extreme polarities (1-star and 5-star ratings) but severely degrade on intermediate ratings (2, 3, and 4 stars with recall $< 37\%$). In contrast, RoBERTa maintains consistent classification performance across all classes ($49\% - 70\%$ recall).

For the in-depth theoretical analysis, confusion matrices, and qualitative error cases, see the full academic project report in [docs/BaoCaoNLP.pdf](docs/BaoCaoNLP.pdf).

---

## 📂 Repository Structure

```
├── README.md               # Project overview, benchmark results, and setup guide
├── requirements.txt        # Pinned Python package dependencies
├── .gitignore              # Git ignore rules for environments, caches, and checkpoints
├── notebooks/
│   └── amazon-reviews-sentiment_analysis.ipynb # End-to-end data processing, training & evaluation
├── docs/
│   ├── BaoCaoNLP.pdf       # Full academic project report (UIT CS221)
│   └── superpowers/        # Project designs and implementation plans
└── data/
    └── .gitkeep            # Data placeholder directory (raw datasets ignored)
```

---

## 🚀 Getting Started

### 1. Prerequisites
- Python 3.10+ (Python 3.11 recommended)
- CUDA-compatible GPU (optional but strongly recommended for RoBERTa fine-tuning)

### 2. Clone and Setup Environment

```bash
# Clone the repository (if hosted remotely) or enter project directory
cd XLNNTN

# Create and activate a virtual environment
python3 -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# Upgrade pip and install dependencies
pip install --upgrade pip
pip install -r requirements.txt
```

### 3. Launch Notebook

```bash
# Register the kernel (optional)
python -m ipykernel install --user --name=nlp-cs221 --display-name "Python (NLP CS221)"

# Start Jupyter Lab / Notebook
jupyter lab
```

Open `notebooks/amazon-reviews-sentiment_analysis.ipynb` and run the cells sequentially to reproduce preprocessing, baseline model training, and RoBERTa fine-tuning.

---

## 📜 References

1. Liu, Y., et al. (2019). *RoBERTa: A Robustly Optimized BERT Pretraining Approach*. arXiv:1907.11692.
2. Vaswani, A., et al. (2017). *Attention Is All You Need*. NeurIPS.
3. Hugging Face Transformers & Datasets documentation.
