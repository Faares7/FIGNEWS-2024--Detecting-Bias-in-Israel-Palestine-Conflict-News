# FIGNEWS-2024: Bias Detection in Conflict News

Automatic detection of political bias in news articles about the Israel-Palestine conflict using a mixture of AI experts.

---

## 📌 What Is This Project?

This project detects bias in news articles written in **Arabic** and **English** about the Israel-Palestine conflict.

**Input:** A news article  
**Output:** Bias classification (Unbiased, Biased Against Palestine, Biased Against Israel, Others)

---

## 🎯 The Problem

- News articles can be politically biased
- Articles are in two different languages (Arabic & English)
- Most articles are unbiased (>40%), few are biased (<15%)
- Bias is subtle - not just keywords, but how things are framed

---

## 💡 Our Solution

We built **two systems** and compared them:

### System 1: Team of Experts (Our Approach)
- 5 different AI models work together
- Language-specific specialists:
  - **Arabic experts**: MARBERT + Random Forest
  - **English experts**: DeBERTa + Random Forest
  - **Multilingual bridge**: XLM-RoBERTa
- Models **vote** on the final answer (majority wins)

### System 2: One Smart Model (Baseline)
- Single multilingual model (XLM-RoBERTa)
- Handles both languages at once

---

## 🏗️ The 5-Stage Pipeline

1. **Stage 1**: Train classical models (Random Forests)
2. **Stage 2**: Train MARBERT (Arabic specialist)
3. **Stage 3**: Train DeBERTa (English specialist)
4. **Stage 4**: Train XLM-RoBERTa (multilingual model)
5. **Stage 5**: Combine all models with voting

Each stage saves a model → All models loaded in Stage 5 for ensemble voting.

---

## 📊 Results

| Model | Performance (Macro F1) |
|-------|------------------------|
| Arabic Random Forest | 0.88 🏆 |
| English Random Forest | 0.78 |
| **System 1 (Our Team)** | **0.75** |
| MARBERT | 0.50 |
| DeBERTa | 0.47 |
| **System 2 (Baseline)** | **0.35** |

**Key Finding:** Simple models beat advanced AI! System 1 is 2x better than System 2.

---

## 🛠️ Installation
```bash
# Clone the repository
git clone https://github.com/yourusername/fignews-2024.git
cd fignews-2024

# Install dependencies
pip install -r requirements.txt

# Download FastText embeddings (for Arabic)
wget https://dl.fbaipublicfiles.com/fasttext/vectors-crawl/cc.ar.300.bin.gz
gunzip cc.ar.300.bin.gz
```

---

## 🚀 How to Use

### Train All Models

Run the notebooks in order:
```bash
Ar_En_classical_model_RF.ipynb       # Train Random Forests
MarBERT.ipynb         # Train Arabic specialist
DeBERTa.ipynb        # Train English specialist
XLM-RoBERTa.ipynb      # Train multilingual model
Ensemble and inference.ipynb     # Run ensemble voting
```

**⭐ Star this repo if you find it helpful!**
