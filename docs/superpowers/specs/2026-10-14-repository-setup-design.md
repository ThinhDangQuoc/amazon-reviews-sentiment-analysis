# Repository Setup & Structure Design

- **Date:** 2026-10-14
- **Project:** CS221 - Sentiment Analysis for Amazon Reviews
- **Author:** Đặng Quốc Thịnh (MSSV: 23521494)
- **Institution:** University of Information Technology (UIT - VNU-HCM)

---

## 1. Objectives & Scope
Transform the existing project directory into a well-structured, reproducible, and professional Machine Learning Git repository.
- Provide clear separation of concerns (notebooks, reports, data).
- Ensure reproducibility through dependency declarations (`requirements.txt`).
- Prevent accidental check-in of temporary checkpoints, environments, or heavy datasets (`.gitignore`).
- Document problem statement, model implementations, benchmarks, and run instructions in `README.md`.

---

## 2. Target Directory Structure
```
amazon-reviews-sentiment-analysis/
├── .gitignore              # Python, PyTorch, Jupyter, cache, and virtualenv ignores
├── README.md               # Project overview, architecture, benchmark results, setup guide
├── requirements.txt        # Pinned Python package dependencies
├── notebooks/
│   └── amazon-reviews-sentiment_analysis.ipynb # Core experiments and fine-tuning notebook
├── docs/
│   ├── BaoCaoNLP.pdf       # Full academic project report (UIT CS221)
│   └── superpowers/specs/  # Design specifications
└── data/
    └── .gitkeep            # Data placeholder directory (raw datasets ignored)
```

---

## 3. Git Configuration & Repository Initialization
- **Branch:** `main` as the default branch.
- **Git User:** Retain existing user configuration (`Thinh Dang <dangquocthinh2005@gmail.com>`).
- **Initial Commit:** Structured initial commit including project files and documentation.

---

## 4. Configuration & Dependencies

### 4.1 `.gitignore`
Includes rules covering:
- Python bytecode (`__pycache__/`, `*.pyc`)
- Python virtual environments (`.venv/`, `venv/`, `env/`)
- Jupyter notebook checkpoints (`.ipynb_checkpoints/`)
- Hugging Face / PyTorch model artifacts & logs (`results/`, `logs/`, `checkpoint-*/`, `*.pt`, `*.bin`, `*.safetensors`)
- Data caches (`data/*`, except `!data/.gitkeep`)
- System & IDE files (`.DS_Store`, `.vscode/`, `.idea/`)

### 4.2 `requirements.txt`
Dependencies extracted from notebook:
```txt
torch>=2.0.0
transformers>=4.30.0
datasets>=2.14.0
accelerate>=0.20.0
scikit-learn>=1.2.0
pandas>=2.0.0
numpy>=1.24.0
matplotlib>=3.7.0
seaborn>=0.12.0
xgboost>=1.7.0
nltk>=3.8.0
ipykernel>=6.20.0
```

---

## 5. Documentation (`README.md`)
The `README.md` will contain:
1. **Header & Context:** Course CS221 (Xử lý ngôn ngữ tự nhiên), UIT, student name and supervisor.
2. **Project Overview:** Multi-class sentiment classification on Amazon reviews (1-5 stars).
3. **Methods Implemented:**
   - TF-IDF + Logistic Regression (baseline)
   - TF-IDF + Random Forest
   - RoBERTa Fine-Tuning (`roberta-base` via Hugging Face Trainer)
4. **Benchmark Results:**
   | Model | Accuracy | Macro F1-Score |
   |---|:---:|:---:|
   | Logistic Regression | 46% | 45% |
   | Random Forest | 44% | 42% |
   | **RoBERTa (Fine-tuned)** | **58%** | **58%** |
5. **Setup & Execution Guide:** Virtual environment setup, dependency installation, and running the notebook.
