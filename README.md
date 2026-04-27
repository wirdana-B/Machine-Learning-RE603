# Machine-Learning-RE603
## 📚 Daftar Isi

- [Apa itu Machine Learning?](#-apa-itu-machine-learning)
- [Sejarah Singkat](#-sejarah-singkat)
- [Bagaimana ML Bekerja?](#-bagaimana-ml-bekerja)
- [Jenis-Jenis Machine Learning](#-jenis-jenis-machine-learning)
- [Algoritma Populer](#-algoritma-populer)
- [Alur Kerja ML (ML Pipeline)](#-alur-kerja-ml-ml-pipeline)
- [Konsep Penting](#-konsep-penting)
- [Aplikasi Nyata](#-aplikasi-nyata)
- [Tools & Library](#-tools--library)
- [Perbedaan AI, ML, dan Deep Learning](#-perbedaan-ai-ml-dan-deep-learning)
- [Memulai Belajar ML](#-memulai-belajar-ml)
- [Referensi](#-referensi)

---

## 🧠 Apa itu Machine Learning?

**Machine Learning (ML)** adalah cabang dari kecerdasan buatan (Artificial Intelligence) yang memungkinkan komputer untuk **belajar dari data** dan **membuat keputusan** tanpa harus diprogram secara eksplisit untuk setiap tugas.

> *"Machine Learning adalah ilmu yang memberi komputer kemampuan untuk belajar tanpa diprogram secara eksplisit."*
> — **Arthur Samuel, 1959**

### Analogi Sederhana

Bayangkan kamu mengajari anak kecil mengenali kucing:
- **Cara Konvensional 🔴:** Kamu jelaskan satu per satu — "kucing punya 4 kaki, berbulu, berekor, bertelinga lancip..."
- **Cara ML 🟢:** Kamu tunjukkan **ribuan foto** kucing dan bukan kucing, lalu biarkan anak tersebut **menemukan polanya sendiri**

Itulah inti dari Machine Learning — menemukan **pola tersembunyi dalam data** secara otomatis.

### Definisi Formal

```
Machine Learning = Data + Algoritma + Model

                   Data
                    │
                    ▼
              [ Algoritma ML ]
                    │
                    ▼
                  Model
                    │
          ┌─────────┴─────────┐
          │                   │
       Input Baru          Prediksi
```

---

## 📖 Sejarah Singkat

| Tahun | Peristiwa |
|:-----:|-----------|
| **1950** | Alan Turing mengusulkan "Turing Test" — bisakah mesin berpikir? |
| **1957** | Frank Rosenblatt menciptakan **Perceptron** — neuron buatan pertama |
| **1959** | Arthur Samuel menciptakan istilah **"Machine Learning"** |
| **1986** | Algoritma **Backpropagation** dipopulerkan untuk neural network |
| **1997** | IBM Deep Blue mengalahkan juara catur dunia Garry Kasparov |
| **2006** | Geoffrey Hinton memperkenalkan **Deep Learning** |
| **2012** | AlexNet memenangkan ImageNet — kebangkitan deep learning |
| **2016** | AlphaGo mengalahkan juara dunia Go, Lee Sedol |
| **2017** | Google memperkenalkan arsitektur **Transformer** |
| **2022** | **ChatGPT** diluncurkan, ML masuk ke kehidupan mainstream |
| **2024+** | Era **Large Language Models (LLM)** dan AI generatif |

---

## ⚙️ Bagaimana ML Bekerja?

ML bekerja dalam 3 fase utama:

### Fase 1: Training (Pembelajaran)
```
Data Training ──► Algoritma ──► Model Terlatih
```
Model "belajar" dengan mencari pola dari data yang ada.

### Fase 2: Validation (Validasi)
```
Data Validasi ──► Model ──► Evaluasi Performa
```
Model diuji dengan data yang belum pernah dilihat untuk mengukur kualitasnya.

### Fase 3: Prediction (Prediksi)
```
Data Baru ──► Model Terlatih ──► Prediksi / Output
```
Model digunakan untuk membuat prediksi pada data dunia nyata.

---

## 🗂️ Jenis-Jenis Machine Learning

Machine Learning dibagi menjadi **3 kategori utama** berdasarkan cara belajarnya:

---

### 1. 🎓 Supervised Learning (Pembelajaran Terarah)

Model belajar dari data yang sudah **berlabel** (ada jawaban benarnya).

```
Input (X) + Label (Y) ──► Model ──► Prediksi label baru
```

**Analogi:** Seperti belajar dengan buku soal yang sudah ada kunci jawabannya.

**Dibagi menjadi:**
- **Klasifikasi** — output berupa kategori (ya/tidak, spam/bukan spam)
- **Regresi** — output berupa nilai numerik (harga rumah, suhu)

**Contoh Algoritma:**
| Algoritma | Jenis | Contoh Penggunaan |
|-----------|-------|-------------------|
| Linear Regression | Regresi | Prediksi harga rumah |
| Logistic Regression | Klasifikasi | Deteksi spam email |
| Decision Tree | Keduanya | Diagnosa medis |
| Random Forest | Keduanya | Prediksi kredit |
| SVM | Klasifikasi | Pengenalan wajah |
| KNN | Keduanya | Sistem rekomendasi |
| Naive Bayes | Klasifikasi | Filter spam |
| Neural Network | Keduanya | Pengenalan gambar |

---

### 2. 🔍 Unsupervised Learning (Pembelajaran Mandiri)

Model belajar dari data yang **tidak berlabel** — mencari pola sendiri.

```
Input (X) tanpa Label ──► Model ──► Pola / Kelompok / Struktur
```

**Analogi:** Seperti mengelompokkan buku di perpustakaan tanpa diberitahu kategorinya.

**Dibagi menjadi:**
- **Clustering** — mengelompokkan data yang mirip
- **Dimensionality Reduction** — menyederhanakan data berdimensi tinggi
- **Association Rule** — menemukan hubungan antar item

**Contoh Algoritma:**
| Algoritma | Tipe | Contoh Penggunaan |
|-----------|------|-------------------|
| K-Means | Clustering | Segmentasi pelanggan |
| DBSCAN | Clustering | Deteksi anomali |
| PCA | Dim. Reduction | Kompresi gambar |
| Apriori | Association | Market basket analysis |
| Autoencoder | Dim. Reduction | Deteksi fraud |

---

### 3. 🎮 Reinforcement Learning (Pembelajaran Penguatan)

Model (agent) belajar melalui **trial and error** dengan sistem reward dan punishment dari lingkungan.

```
Agent ──► Aksi ──► Lingkungan ──► Reward/Punishment
  ▲                                       │
  └───────────── Belajar ◄────────────────┘
```

**Analogi:** Seperti melatih anjing dengan memberikan hadiah jika melakukan hal benar dan hukuman jika salah.

**Contoh Penggunaan:**
- 🎮 Game AI (AlphaGo, OpenAI Five)
- 🤖 Robotika dan kontrol otomatis
- 🚗 Mobil otonom
- 📈 Trading saham otomatis

---

### 4. 🔄 Semi-Supervised Learning *(Bonus)*

Kombinasi supervised dan unsupervised — menggunakan **sedikit data berlabel** dan **banyak data tidak berlabel**.

**Cocok ketika:** Pelabelan data sangat mahal atau membutuhkan banyak waktu.

---

## 🛠️ Algoritma Populer

```
Machine Learning
│
├── Supervised
│   ├── Linear Regression
│   ├── Logistic Regression
│   ├── Decision Tree
│   ├── Random Forest
│   ├── Gradient Boosting (XGBoost, LightGBM)
│   ├── Support Vector Machine (SVM)
│   ├── K-Nearest Neighbors (KNN)
│   └── Naive Bayes
│
├── Unsupervised
│   ├── K-Means Clustering
│   ├── Hierarchical Clustering
│   ├── DBSCAN
│   ├── PCA
│   └── t-SNE
│
└── Deep Learning (Neural Network)
    ├── ANN (Artificial Neural Network)
    ├── CNN (Convolutional Neural Network)
    ├── RNN / LSTM
    └── Transformer (BERT, GPT)
```

---

## 🔄 Alur Kerja ML (ML Pipeline)

Setiap proyek ML mengikuti alur kerja yang sistematis:

```
1. Definisi Masalah
        │
        ▼
2. Pengumpulan Data
        │
        ▼
3. Eksplorasi Data (EDA)
        │
        ▼
4. Preprocessing Data
   ├── Handling missing values
   ├── Encoding categorical data
   ├── Feature scaling
   └── Feature engineering
        │
        ▼
5. Pemilihan Model
        │
        ▼
6. Training Model
        │
        ▼
7. Evaluasi Model
   ├── Accuracy, Precision, Recall, F1
   └── Cross-validation
        │
        ▼
8. Tuning Hyperparameter
        │
        ▼
9. Deployment
        │
        ▼
10. Monitoring & Maintenance
```

---

## 💡 Konsep Penting

### Overfitting vs Underfitting

```
Underfitting          Good Fit           Overfitting
(Terlalu Sederhana)   (Ideal)            (Terlalu Kompleks)

    *  *                *  *               * *
  *      *            *      *           *     *
*          *         *        *         *       *
─────────────       ──────────────     ─────────────

Model terlalu        Model seimbang    Model "hafal"
umum, akurasi        bias & variance   data training,
training & test      tinggi            buruk di data baru
sama-sama rendah
```

| Kondisi | Training Acc | Test Acc | Solusi |
|---------|:---:|:---:|--------|
| Underfitting | Rendah | Rendah | Tambah kompleksitas model, lebih banyak fitur |
| Good Fit | Tinggi | Tinggi | ✅ Model ideal |
| Overfitting | Sangat Tinggi | Rendah | Regularisasi, lebih banyak data, dropout |

---

### Bias vs Variance

- **Bias tinggi** → model terlalu sederhana → underfitting
- **Variance tinggi** → model terlalu kompleks → overfitting
- **Tujuan:** menemukan titik keseimbangan keduanya (**Bias-Variance Tradeoff**)

---

### Feature Engineering

Proses membuat atau memodifikasi fitur agar model dapat belajar lebih baik.

```python
# Contoh: dari tanggal, buat fitur hari, bulan, tahun
df['hari'] = df['tanggal'].dt.day
df['bulan'] = df['tanggal'].dt.month
df['tahun'] = df['tanggal'].dt.year
df['hari_minggu'] = df['tanggal'].dt.dayofweek
```

---

### Cross-Validation

Teknik evaluasi model yang lebih reliabel dari sekedar train-test split.

```
Data ──► Bagi jadi K bagian (fold)

Iterasi 1: [Test][Train][Train][Train][Train]
Iterasi 2: [Train][Test][Train][Train][Train]
Iterasi 3: [Train][Train][Test][Train][Train]
...
Hasil akhir: rata-rata akurasi dari semua iterasi
```

---

## 🌍 Aplikasi Nyata

| Bidang | Contoh Penggunaan |
|--------|-------------------|
| 🏥 **Kesehatan** | Deteksi kanker dari MRI, prediksi diabetes, drug discovery |
| 🏦 **Keuangan** | Deteksi fraud kartu kredit, prediksi harga saham, credit scoring |
| 🚗 **Transportasi** | Mobil otonom, optimasi rute, prediksi permintaan ojol |
| 🛒 **E-Commerce** | Rekomendasi produk, prediksi churn pelanggan |
| 📱 **Teknologi** | Face ID, Google Translate, spam filter, voice assistant |
| 🌾 **Pertanian** | Prediksi panen, deteksi penyakit tanaman dari foto |
| ⚡ **Energi** | Prediksi konsumsi listrik, optimasi panel surya |
| 🎬 **Hiburan** | Rekomendasi Netflix, filter konten, subtitle otomatis |

---

## 🧰 Tools & Library

### Bahasa Pemrograman
| Bahasa | Keterangan |
|--------|------------|
| **Python** 🐍 | Paling populer untuk ML, ekosistem terlengkap |
| **R** | Populer di kalangan statistisi dan peneliti |
| **Julia** | Performa tinggi untuk komputasi numerik |

### Library Python Utama

```python
# Data Manipulation
import numpy as np          # operasi array & matematika
import pandas as pd         # manipulasi data tabular

# Visualisasi
import matplotlib.pyplot as plt  # plotting dasar
import seaborn as sns            # visualisasi statistik

# Machine Learning
from sklearn import *            # algoritma ML lengkap

# Deep Learning
import tensorflow as tf          # framework deep learning Google
import torch                     # framework deep learning Meta (PyTorch)

# Gradient Boosting
import xgboost as xgb            # XGBoost
import lightgbm as lgb           # LightGBM
```

### Platform & Tools
| Tool | Fungsi |
|------|--------|
| **Jupyter Notebook** | Eksperimen & eksplorasi data interaktif |
| **Google Colab** | Jupyter gratis dengan GPU di cloud |
| **Kaggle** | Kompetisi ML + dataset publik |
| **Hugging Face** | Model pre-trained & NLP |
| **MLflow** | Tracking eksperimen ML |
| **Streamlit** | Deploy model ML sebagai web app |

---

## 🔺 Perbedaan AI, ML, dan Deep Learning

```
┌─────────────────────────────────────────────┐
│          Artificial Intelligence (AI)        │
│   Semua teknik yang membuat mesin "cerdas"  │
│                                             │
│   ┌─────────────────────────────────────┐   │
│   │       Machine Learning (ML)         │   │
│   │  Belajar dari data tanpa            │   │
│   │  diprogram eksplisit                │   │
│   │                                     │   │
│   │   ┌───────────────────────────┐     │   │
│   │   │     Deep Learning (DL)    │     │   │
│   │   │  ML dengan Neural Network │     │   │
│   │   │  berlapis-lapis (deep)    │     │   │
│   │   └───────────────────────────┘     │   │
│   └─────────────────────────────────────┘   │
└─────────────────────────────────────────────┘
```

| Aspek | AI | ML | Deep Learning |
|-------|:--:|:--:|:-------------:|
| Lingkup | Luas | Lebih spesifik | Paling spesifik |
| Butuh data | Tidak selalu | Ya | Ya, sangat banyak |
| Butuh GPU | Tidak selalu | Tidak selalu | Ya |
| Interpretasi | Mudah | Sedang | Sulit (black box) |
| Contoh | Chatbot rules-based | Random Forest | GPT, ResNet |

---

## 🚀 Memulai Belajar ML

### Roadmap Belajar

```
Tahap 1 — Fondasi (1-2 bulan)
├── Matematika: Statistik, Probabilitas, Aljabar Linear
└── Python: NumPy, Pandas, Matplotlib

Tahap 2 — ML Dasar (2-3 bulan)
├── Supervised Learning: Regresi, Klasifikasi
├── Unsupervised Learning: Clustering
└── Scikit-learn & Evaluasi Model

Tahap 3 — ML Lanjutan (2-3 bulan)
├── Ensemble Methods: Random Forest, XGBoost
├── Feature Engineering & Selection
└── Hyperparameter Tuning

Tahap 4 — Deep Learning (3-6 bulan)
├── Neural Network Dasar
├── CNN untuk Computer Vision
├── RNN/LSTM untuk Time Series & NLP
└── Transfer Learning

Tahap 5 — Spesialisasi & Proyek
├── Pilih bidang: NLP / Computer Vision / Time Series
├── Buat proyek portfolio
└── Deploy model ke production
```

### Dataset untuk Berlatih
- 🌸 **Iris Dataset** — klasifikasi bunga (pemula)
- 🏠 **Boston Housing** — prediksi harga rumah (regresi)
- 🚢 **Titanic** — klasifikasi survival (pemula)
- 🖼️ **MNIST** — pengenalan tulisan tangan (computer vision)
- 📊 **Kaggle Datasets** — ribuan dataset publik

---

## 📌 Ringkasan

| Konsep | Penjelasan Singkat |
|--------|-------------------|
| **Machine Learning** | Komputer belajar dari data tanpa diprogram eksplisit |
| **Supervised Learning** | Belajar dari data berlabel (ada jawaban benar) |
| **Unsupervised Learning** | Mencari pola dari data tidak berlabel |
| **Reinforcement Learning** | Belajar dari reward & punishment |
| **Overfitting** | Model terlalu "hafal" data training, gagal generalisasi |
| **Underfitting** | Model terlalu sederhana, tidak bisa menangkap pola |
| **Feature Engineering** | Proses memilih & membuat fitur yang relevan |
| **Cross-Validation** | Teknik evaluasi model yang lebih reliabel |

---

## 📚 Referensi

- Géron, A. (2022). *Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow* (3rd ed.). O'Reilly.
- Mitchell, T. M. (1997). *Machine Learning*. McGraw-Hill.
- Bishop, C. M. (2006). *Pattern Recognition and Machine Learning*. Springer.
- Scikit-learn Documentation: [https://scikit-learn.org](https://scikit-learn.org)
- Google ML Crash Course: [https://developers.google.com/machine-learning/crash-course](https://developers.google.com/machine-learning/crash-course)
- Kaggle Learn: [https://www.kaggle.com/learn](https://www.kaggle.com/learn)

---

