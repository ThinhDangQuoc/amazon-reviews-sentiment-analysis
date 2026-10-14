# Repository Setup Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Transform the CS221 NLP project into a clean, reproducible, standard ML/NLP repository with organized directories, git ignores, dependencies, and full documentation.

**Architecture:** Standard Data Science structure separating documentation (`docs/`), notebooks (`notebooks/`), and dataset placeholders (`data/`), configured with comprehensive `.gitignore` rules and pinned `requirements.txt`.

**Tech Stack:** Git, Python 3.11, PyTorch, Hugging Face Transformers, Scikit-learn, Jupyter Notebooks.

## Global Constraints
- Target workspace directory: `/home/thinh/KHMT/XLNNTN`
- Default branch: `main`
- Existing notebook `amazon-reviews-sentiment_analysis.ipynb` and report `BaoCaoNLP.pdf` must be moved safely without data loss.
- Commit messages must follow conventional commits (`feat:`, `docs:`, `chore:`).

---

### Task 1: Directory Restructuring & Asset Relocation

**Files:**
- Create: `notebooks/` (directory)
- Create: `docs/` (directory)
- Create: `data/.gitkeep`
- Move: `amazon-reviews-sentiment_analysis.ipynb` -> `notebooks/amazon-reviews-sentiment_analysis.ipynb`
- Move: `BaoCaoNLP.pdf` -> `docs/BaoCaoNLP.pdf`

**Interfaces:**
- Consumes: Current root files `amazon-reviews-sentiment_analysis.ipynb` and `BaoCaoNLP.pdf`.
- Produces: Standard ML directory layout with assets safely moved into `notebooks/` and `docs/`, plus empty `data/` folder tracked by `.gitkeep`.

- [x] **Step 1: Create directories and move existing files**

```bash
mkdir -p notebooks docs data
git mv amazon-reviews-sentiment_analysis.ipynb notebooks/
git mv BaoCaoNLP.pdf docs/
touch data/.gitkeep
git add data/.gitkeep
```

- [x] **Step 2: Verify file relocation and integrity**

```bash
ls -la notebooks/amazon-reviews-sentiment_analysis.ipynb docs/BaoCaoNLP.pdf data/.gitkeep
git status --short
```
Expected output:
- `R  amazon-reviews-sentiment_analysis.ipynb -> notebooks/amazon-reviews-sentiment_analysis.ipynb`
- `R  BaoCaoNLP.pdf -> docs/BaoCaoNLP.pdf`
- `A  data/.gitkeep`

- [x] **Step 3: Commit relocation**

```bash
git commit -m "chore: organize files into notebooks, docs, and data directories"
```

---

### Task 2: Configuration & Dependencies (`.gitignore` and `requirements.txt`)

**Files:**
- Create: `.gitignore`
- Create: `requirements.txt`

**Interfaces:**
- Consumes: None
- Produces: Complete git ignore rules preventing unwanted artifacts from tracking, and reproducible dependency list.

- [x] **Step 1: Create `.gitignore`**

Create `.gitignore` containing rules for Python byte code, checkpoints, virtual environments, large data files, and logs:

```gitignore
# Byte-compiled / optimized / DLL files
__pycache__/
*.py[cod]
*$py.class

# C extensions
*.so

# Distribution / packaging
.Python
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
wheels/
share/python-wheels/
*.egg-info/
.installed.cfg
*.egg

# Virtual Environments
.env
.venv
env/
venv/
ENV/
env.bak/
venv.bak/

# Jupyter Notebook checkpoints
.ipynb_checkpoints
*/.ipynb_checkpoints/*

# PyTorch & Hugging Face checkpoints and outputs
results/
logs/
checkpoints/
checkpoint-*/
*.pt
*.pth
*.bin
*.safetensors

# Datasets and cache files (except .gitkeep)
data/*
!data/.gitkeep
*.csv
*.parquet
*.h5
*.pkl

# IDE & Editor files
.vscode/
.idea/
*.swp
*.swo
.DS_Store

# Antigravity & AI agent artifacts
.agents/
```

- [x] **Step 2: Create `requirements.txt`**

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

- [x] **Step 3: Verify git ignore behavior**

Test git ignore rules with temporary file:
```bash
touch results_test.pt .venv_test
git status --ignored
rm results_test.pt .venv_test
```
Verify that `.gitignore` and `requirements.txt` are staged/tracked properly.

- [x] **Step 4: Commit configuration and dependencies**

```bash
git add .gitignore requirements.txt
git commit -m "feat: add .gitignore and requirements.txt"
```

---

### Task 3: Comprehensive Project Documentation (`README.md`)

**Files:**
- Create: `README.md`

**Interfaces:**
- Consumes: Project details, model comparison results, course information.
- Produces: User-facing documentation detailing problem formulation, models, benchmarks, and reproducibility guide.

- [x] **Step 1: Write `README.md`**

Include:
- Project title, course (CS221 - Xử lý ngôn ngữ tự nhiên, UIT - VNU-HCM), author info.
- Problem overview: Amazon review multi-class sentiment analysis (1-5 stars).
- Methods compared: TF-IDF + Logistic Regression, TF-IDF + Random Forest, RoBERTa Fine-tuning.
- Results table (Accuracy & Macro F1).
- Repository structure tree.
- Setup & Execution instructions.

- [x] **Step 2: Verify markdown formatting**

```bash
head -n 40 README.md
git status --short
```

- [x] **Step 3: Commit documentation**

```bash
git add README.md
git commit -m "docs: add comprehensive README with benchmarks and setup guide"
```

---

### Task 4: Final Repository Verification

**Files:**
- Verify: All files in repository tree

- [x] **Step 1: Check git log and tree**

```bash
git log --oneline
git status
```
Verify that working tree is clean and commits are organized.

- [x] **Step 2: Check repository directory tree**

Verify all target files exist in their expected paths:
- `notebooks/amazon-reviews-sentiment_analysis.ipynb`
- `docs/BaoCaoNLP.pdf`
- `data/.gitkeep`
- `.gitignore`
- `requirements.txt`
- `README.md`
