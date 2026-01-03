# 💰 Loan Status Classification (Credit Risk Prediction)

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/Library-Scikit_Learn-orange?logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Library-Pandas-150458?logo=pandas&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-success)

> **A Machine Learning project to predict credit default risk based on applicant financial profiles.**

## 📌 Background
Financial institutions face significant risks of financial loss due to customers failing to repay loans (default). This project aims to build an intelligent system capable of classifying whether a customer is eligible for a loan (**Non-Default/Safe**) or poses a risk (**Default**) based on their demographic and financial history.

## 📂 Dataset
The dataset used in this project is sourced from Kaggle: **[Dataset Klasifikasi Status Pinjaman](https://www.kaggle.com/datasets/faisalwp/dataset-klasifikasi-status-pinjaman/data)**.

* **Total Records:** ~50,000 rows.
* **Target Variable:** `status_pinjaman` (0: Non-Default, 1: Default).
* **Key Features:** Age, Annual Income, Credit Score, Total Debt, Credit History Length, etc.

## 🛠️ Methodology & Preprocessing

This project implements an end-to-end data science pipeline:

1.  **Data Cleaning:**
    * Removed the `id_pelanggan` column (irrelevant unique identifier).
    * **Handling Missing Values:** Dropped rows containing nulls (percentage was < 5%).
    * **Label Encoding:** Applied to categorical features such as `status_pekerjaan` (Job Status), `tipe_produk` (Product Type), and `tujuan_pinjaman` (Loan Purpose).

2.  **Handling Skewed Data (Crucial Step):**
    * Identified highly skewed distributions in numerical features (e.g., `pendapatan_tahunan`, `aset_tabungan`).
    * Applied **Log Transformation (`np.log1p`)** to normalize the data distribution, optimizing it for linear and distance-based algorithms.

3.  **Data Splitting:**
    * **Ratio:** 80% Train : 10% Validation : 10% Test.
    * **Stratification:** Used `stratify=y` to maintain the ratio of the target classes across all splits.

## 🤖 Modeling

Three Machine Learning algorithms were trained and evaluated:

1.  **Naive Bayes (GaussianNB)** - Used as the baseline model.
2.  **K-Nearest Neighbors (KNN)** - Optimized using `GridSearchCV` to find the best *k* and distance metric.
3.  **Decision Tree** - Optimized using `GridSearchCV` (tuning `max_depth`, `criterion`, etc.).

## 📊 Evaluation Results

The models were evaluated using the **Test Set** (unseen data). The performance comparison is as follows:

| Model | Accuracy | Precision | Recall | Observation |
| :--- | :--- | :--- | :--- | :--- |
| **Naive Bayes** | 72.07% | 66.65% | **98.61%** | Very high Recall, but suffers from high False Positives. |
| **KNN (Tuned)** | 78.69% | 76.61% | 88.23% | Moderate and balanced performance. |
| **Decision Tree (Tuned)** | **88.29%** | **87.76%** | **91.48%** | **🏆 Best Model** |

### Confusion Matrix Analysis (Decision Tree)
The **Decision Tree** was selected as the final model because it offered the optimal balance between Accuracy and Recall.
* **True Positive:** Successfully detected the majority of default cases.
* **False Negative (Bank Risk):** Very minimal (~233 cases out of the total test set), significantly reducing the risk of granting loans to defaulters.

## 💻 Installation & Usage

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/faisalsuryasaputra/klasifikasi-status-pinjaman.git](https://github.com/faisalsuryasaputra/klasifikasi-status-pinjaman.git)
    cd klasifikasi-status-pinjaman
    ```

2.  **Install dependencies:**
    ```bash
    pip install pandas numpy scikit-learn matplotlib seaborn kagglehub
    ```

3.  **Run the Notebook:**
    Open `notebook.ipynb` (or your specific filename) using Jupyter Notebook, VS Code, or Google Colab.

## 👥 Credits
* **Faisal Surya Saputra** - *End-to-End Analysis (Preprocessing, Modeling, & Evaluation)*

---
*Created as a Final Project for the Artificial Intelligence / Machine Learning Course.*
