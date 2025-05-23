# 🧬 Drug-Drug Interaction Classification Using XGBoost and Morgan Fingerprints

## 📚 Overview

This project presents a machine learning pipeline to classify **Drug-Drug Interactions (DDIs)** using the **DrugBank dataset** via the [TDC (Therapeutics Data Commons)](https://tdcommons.ai/). The objective is to predict the type of pharmacological interaction between two chemical compounds, using structural information encoded as **Morgan fingerprints** and a **multi-class XGBoost classifier**.

---

## 🧪 Dataset

- Source: **DrugBank (via TDC DDI task)**
- Classes: **86 distinct interaction types**
- Features: **SMILES** (Simplified Molecular-Input Line-Entry System) strings for Drug 1 and Drug 2
- Label: Integer from 1 to 86, each representing a DDI category (e.g., increased serum level, decreased effect, etc.)

---

## 🧰 Methodology

1. **Data Sampling**:
   - Training set: 10,000 samples randomly selected from the full dataset
   - Validation set: An additional 10,000 samples, disjoint from the training data

2. **Featurization**:
   - Molecules were converted from SMILES to **RDKit Mol objects**
   - Generated **2048-bit Morgan fingerprints** (radius=2) for each molecule
   - Final feature vector: Concatenation of Drug1 and Drug2 fingerprints

3. **Model**:
   - Classifier: `XGBoostClassifier`
   - Objective: `multi:softprob`
   - Evaluation metric: `mlogloss`
   - Labels encoded using `LabelEncoder`

---

## 📈 Results

### 🏋️‍♂️ Training Set (n=9997)

| Metric        | Value |
|---------------|-------|
| Accuracy      | 0.85  |
| Macro F1      | 0.78  |
| Weighted F1   | 0.85  |

---

### ✅ Validation Set (n=10000)

| Metric        | Value |
|---------------|-------|
| Micro F1      | 0.87  |
| Macro F1      | 0.80  |
| Weighted F1   | 0.87  |
| Accuracy      | 0.86  |

---

### 🔍 Binary Confusion Matrix (Correct vs Incorrect Predictions)

|               | Predicted Correct | Predicted Incorrect |
|---------------|-------------------|---------------------|
| **Actual**    | **8633**          | **1367**            |

- **Sensitivity (Recall)**: `0.863`
- **Precision (PPV)**: `0.863`
- **Overall Accuracy**: `0.863`

> This binary view simplifies the multi-class problem to evaluate the model's ability to distinguish between right and wrong predictions.

---

## 📊 Visualizations

- Confusion Matrix (multi-class and binary)
- ROC AUC curves (micro-average and top classes)

![confusion_matrix](path/to/confusion_matrix.png)
![roc_auc_curve](path/to/roc_auc.png)

---

## 🧠 Future Work

- Address class imbalance via oversampling, reweighting, or focal loss
- Explore graph-based approaches (e.g., GNNs on molecular graphs)
- Expand model evaluation to include clinical significance metrics

---

## 🚀 How to Run

```bash
git clone https://github.com/yourusername/ddi-xgboost.git
cd ddi-xgboost
pip install -r requirements.txt
python train.py
