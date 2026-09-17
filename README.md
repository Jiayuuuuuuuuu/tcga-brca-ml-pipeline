# TCGA-BRCA Subtype Classifier

**End-to-end machine learning pipeline for multi-class breast cancer molecular subtype classification from RNA-seq gene expression data.**

This project takes raw TCGA-BRCA clinical and RNA-seq data through a full ML workflow — preprocessing, feature engineering, class-imbalance handling, model selection, hyperparameter tuning, and rigorous evaluation — to classify breast cancer patients into molecular subtypes (Luminal, HER2-enriched, Basal-like, etc.).

## Highlights

- **Full pipeline, not just a model**: data ingestion → cleaning/merging → EDA → feature engineering → SMOTE balancing → model training → hyperparameter search → evaluation, each stage checkpointed to disk for reproducibility.
- **Multi-model comparison**: Logistic Regression, Random Forest, SVM, and XGBoost trained and tuned under identical conditions for a fair head-to-head comparison.
- **Systematic tuning**: `GridSearchCV` / `RandomizedSearchCV` with stratified 5-fold cross-validation (`StratifiedKFold`) to avoid class-imbalance leakage into model selection.
- **Class imbalance handling**: SMOTE applied to address skewed subtype distribution common in clinical genomics data.
- **Rigorous evaluation**: accuracy, precision, recall, F1, ROC-AUC, Matthews correlation coefficient, confusion matrices, and per-class breakdowns — not just a single headline metric.

## Pipeline

| Stage | Notebook | What it does |
|---|---|---|
| 1. Data prep & feature engineering | `TCGA_BRCA_Methodology.ipynb` | Loads and merges clinical + RNA-seq data, EDA, preprocessing, feature engineering, SMOTE-based class balancing |
| 2. Model training & tuning | `TCGA_BRCA_Model_Training.ipynb` | Trains Logistic Regression, Random Forest, SVM, and XGBoost with cross-validated hyperparameter search |
| 3. Evaluation | `TCGA_BRCA_Evaluation.ipynb` | Computes final metrics, confusion matrices, ROC curves, and comparison visualizations across all models |

Run in order — each notebook checkpoints its output (`preprocessed_data.pkl`, `trained_models.pkl`) for the next stage.

## Skills Demonstrated

- ML pipeline design and reproducible experiment structure
- Feature engineering on high-dimensional genomic data (thousands of gene expression features)
- Handling severe class imbalance (SMOTE) in a clinical multi-class setting
- Hyperparameter optimization and cross-validation methodology
- Comparative model evaluation across classical ML and gradient-boosted approaches
- Applied ML on real-world biomedical/genomics data (TCGA)

## Dataset

- **Name:** TCGA-BRCA (The Cancer Genome Atlas Breast Invasive Carcinoma)
- **Source:** [https://portal.gdc.cancer.gov](https://portal.gdc.cancer.gov)
- **Required files** (place in the same directory as the notebooks):
  - `data_clinical_patient.txt`
  - `data_clinical_sample.txt`
  - `data_mrna_seq_v2_rsem.txt`

## Setup

Python 3.8+ (tested on 3.11).

```bash
pip install numpy==1.26.4 pandas==2.2.3 scikit-learn==1.5.2 imbalanced-learn==0.14.1 xgboost==3.2.0 matplotlib==3.9.2 seaborn==0.13.2 scipy==1.14.1 joblib==1.4.2
```

## Running

Run the three notebooks in order, top to bottom, without interruption:

```
1. TCGA_BRCA_Methodology.ipynb
2. TCGA_BRCA_Model_Training.ipynb
3. TCGA_BRCA_Evaluation.ipynb
```

> **Note:** Notebooks may contain hardcoded file paths from development. Update path variables at the top of each notebook to match your local directory structure before running.
