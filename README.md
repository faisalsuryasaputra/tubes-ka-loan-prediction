# TUBES-KA-klasifikasi-status-pinjaman

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Scikit-Learn](https://img.shields.io/badge/Library-Scikit--Learn-orange)
![Pandas](https://img.shields.io/badge/Library-Pandas-150458)
![Status](https://img.shields.io/badge/Status-Completed-success)

> **Projek Machine Learning untuk memprediksi risiko gagal bayar (default) pada pengajuan pinjaman nasabah.**

## 📌 Latar Belakang
Lembaga keuangan menghadapi risiko kerugian finansial akibat nasabah yang gagal bayar (*default*). Proyek ini bertujuan membangun sistem cerdas yang dapat mengklasifikasikan apakah seorang nasabah layak menerima pinjaman (Lancar) atau berisiko macet (Gagal Bayar) berdasarkan profil demografis dan finansial mereka.

## 📂 Dataset
Dataset yang digunakan berasal dari Kaggle: **[Dataset Klasifikasi Status Pinjaman](https://www.kaggle.com/datasets/faisalwp/dataset-klasifikasi-status-pinjaman/data)**.

* **Total Data:** ~50,000 baris.
* **Target Variable:** `status_pinjaman` (0: Lancar, 1: Kredit Macet/Default).
* **Fitur Utama:** Usia, Pendapatan Tahunan, Skor Kredit, Total Hutang, Lama Riwayat Kredit, dll.

## 🛠️ Metodologi & Preprocessing

Proyek ini mencakup pipeline *end-to-end* data science:

1.  **Data Cleaning:**
    * Menghapus kolom `id_pelanggan` (irrelevant).
    * Handling Missing Values (drop rows karena jumlah missing value < 5%).
    * Label Encoding untuk fitur kategorikal (`status_pekerjaan`, `tipe_produk`, `tujuan_pinjaman`).
2.  **Handling Skewed Data (Penting):**
    * Mengidentifikasi distribusi miring pada fitur numerik (seperti `pendapatan_tahunan`, `aset_tabungan`).
    * Melakukan transformasi logaritma (`np.log1p`) untuk menormalkan distribusi data agar optimal bagi algoritma *linear* dan *distance-based*.
3.  **Data Splitting:**
    * Rasio: **80% Train : 10% Validation : 10% Test**.
    * Menggunakan `stratify` untuk menjaga keseimbangan rasio target.

## 🤖 Pemodelan (Modeling)

Tiga algoritma Machine Learning diuji dan dievaluasi kinerjanya:

1.  **Naive Bayes (GaussianNB)** - Sebagai baseline.
2.  **K-Nearest Neighbors (KNN)** - Dioptimasi menggunakan `GridSearchCV` (mencari *k* dan *metric* terbaik).
3.  **Decision Tree** - Dioptimasi menggunakan `GridSearchCV` (tuning `max_depth`, `criterion`, dll).

## 📊 Hasil Evaluasi

Evaluasi dilakukan menggunakan data Test (unseen data). Berikut perbandingan performanya:

| Model | Akurasi | Precision | Recall | Keterangan |
| :--- | :--- | :--- | :--- | :--- |
| **Naive Bayes** | 72.07% | 66.65% | **98.61%** | Recall sangat tinggi, namun banyak False Positive. |
| **KNN (Tuned)** | 78.69% | 76.61% | 88.23% | Performa moderat/seimbang. |
| **Decision Tree (Tuned)** | **88.29%** | **87.76%** | **91.48%** | **🏆 Best Model** |

### Analisis Confusion Matrix (Decision Tree)
Model Decision Tree dipilih sebagai model terbaik karena memberikan keseimbangan optimal antara Akurasi dan Recall.
* **True Positive:** Berhasil mendeteksi mayoritas kredit macet.
* **False Negative (Risiko Bank):** Sangat minim (~233 kasus dari total test set).

## 📈 Visualisasi Project
*(Disarankan untuk menaruh screenshot grafik dari notebook di sini, misalnya:)*
* [Image: Distribusi Data setelah Log Transformation]
* [Image: Confusion Matrix Decision Tree]
* [Image: Decision Tree Rules Visualization]

## 💻 Cara Menjalankan (Installation)

1.  Clone repositori ini:
    ```bash
    git clone [https://github.com/username-kamu/klasifikasi-status-pinjaman.git](https://github.com/username-kamu/klasifikasi-status-pinjaman.git)
    ```
2.  Install library yang dibutuhkan:
    ```bash
    pip install pandas numpy scikit-learn matplotlib seaborn kagglehub
    ```
3.  Jalankan notebook:
    Buka `notebook.ipynb` (atau nama file kamu) menggunakan Jupyter Notebook atau Google Colab.

## 👥 Kredit
Project ini dikerjakan oleh:
* **Faisal** - *Data Preprocessing, Modeling, & Evaluation.*

---
*Dibuat untuk memenuhi Tugas Besar Mata Kuliah Kecerdasan Buatan/Machine Learning.*
