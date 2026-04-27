# 🤖 Naive Bayes Classification

## Daftar Isi
- [Pengertian](#pengertian)
- [Teorema Bayes](#teorema-bayes)
- [Asumsi Naive Bayes](#asumsi-naive-bayes)
- [Cara Kerja](#cara-kerja)
- [Jenis-Jenis Naive Bayes](#jenis-jenis-naive-bayes)
- [Contoh Kasus](#contoh-kasus)
- [Kelebihan dan Kekurangan](#kelebihan-dan-kekurangan)
- [Implementasi Python](#implementasi-python)
- [Evaluasi Model](#evaluasi-model)

---

## Pengertian

**Naive Bayes Classification** adalah algoritma klasifikasi berbasis probabilistik yang menggunakan **Teorema Bayes** sebagai dasarnya. Algoritma ini disebut *"naive"* (naif) karena mengasumsikan bahwa setiap fitur/atribut bersifat **independen satu sama lain**, padahal dalam dunia nyata hal tersebut jarang terjadi.

Meskipun asumsinya sederhana, Naive Bayes sangat efektif dalam banyak kasus nyata, terutama pada:
- 📧 Klasifikasi email spam
- 📰 Analisis sentimen teks
- 🏥 Diagnosa medis
- 🔍 Kategorisasi dokumen

---

## Teorema Bayes

Naive Bayes dibangun di atas **Teorema Bayes**, yang dinyatakan sebagai:

```
P(C | X) = P(X | C) × P(C) / P(X)
```

| Notasi | Nama | Keterangan |
|--------|------|------------|
| `P(C \| X)` | **Posterior** | Probabilitas kelas C, diberikan data X |
| `P(X \| C)` | **Likelihood** | Probabilitas data X muncul jika kelasnya C |
| `P(C)` | **Prior** | Probabilitas awal kelas C (sebelum melihat data) |
| `P(X)` | **Evidence** | Probabilitas data X (sama untuk semua kelas, bisa diabaikan) |

Karena `P(X)` konstan untuk semua kelas, rumus disederhanakan menjadi:

```
P(C | X) ∝ P(X | C) × P(C)
```

**Prediksi** dilakukan dengan memilih kelas dengan nilai posterior tertinggi:

```
Ŷ = argmax [ P(C) × ∏ P(xᵢ | C) ]
```

---

## Asumsi Naive Bayes

> ⚠️ **Asumsi utama:** Setiap fitur diasumsikan **kondisional independen** satu sama lain, diberikan label kelas.

Artinya:

```
P(X | C) = P(x₁ | C) × P(x₂ | C) × ... × P(xₙ | C)
```

Meskipun asumsi ini sering tidak sepenuhnya terpenuhi dalam data nyata, algoritma ini tetap memberikan hasil yang baik karena model ini fokus pada **arah probabilitas** bukan nilai absolutnya.

---

## Cara Kerja

### Langkah-langkah Naive Bayes:

**1. Hitung Prior Probability**
```
P(C) = Jumlah sampel kelas C / Total seluruh sampel
```

**2. Hitung Likelihood**
```
P(xᵢ | C) = Jumlah kemunculan xᵢ pada kelas C / Total sampel kelas C
```

**3. Hitung Posterior untuk setiap kelas**
```
P(C | X) ∝ P(C) × P(x₁ | C) × P(x₂ | C) × ... × P(xₙ | C)
```

**4. Prediksi**
Pilih kelas dengan nilai **posterior tertinggi**.

---

## Jenis-Jenis Naive Bayes

### 1. 🔢 Gaussian Naive Bayes
Digunakan ketika fitur bersifat **kontinu** dan diasumsikan mengikuti distribusi normal (Gaussian).

```
P(xᵢ | C) = (1 / √(2π σ²)) × exp(-(xᵢ - μ)² / 2σ²)
```
- `μ` = rata-rata fitur pada kelas C
- `σ²` = variansi fitur pada kelas C

**Cocok untuk:** data numerik kontinu (tinggi badan, berat badan, suhu, dll.)

---

### 2. 📊 Multinomial Naive Bayes
Digunakan untuk fitur berupa **frekuensi/hitungan** (count data).

**Cocok untuk:** klasifikasi teks — dimana fitur adalah frekuensi kemunculan kata (word count / TF-IDF).

---

### 3. ✅ Bernoulli Naive Bayes
Digunakan ketika fitur bersifat **biner** (0 atau 1).

**Cocok untuk:** klasifikasi teks dengan representasi binary (ada/tidak ada kata).

---

## Contoh Kasus

### Studi Kasus: Klasifikasi Email Spam

**Dataset Latih:**

| Email | Kata "gratis" | Kata "menang" | Kata "klik" | Label |
|-------|:---:|:---:|:---:|:---:|
| 1 | Ya | Ya | Ya | Spam |
| 2 | Tidak | Ya | Tidak | Spam |
| 3 | Ya | Tidak | Tidak | Ham |
| 4 | Tidak | Tidak | Tidak | Ham |
| 5 | Tidak | Tidak | Ya | Ham |

**Hitung Prior:**
```
P(Spam) = 2/5 = 0.4
P(Ham)  = 3/5 = 0.6
```

**Email baru:** mengandung kata "gratis" = Ya, "menang" = Ya, "klik" = Tidak

**Hitung Likelihood:**
```
P(gratis=Ya | Spam) = 1/2 = 0.5
P(menang=Ya | Spam) = 2/2 = 1.0
P(klik=Tidak | Spam) = 1/2 = 0.5

P(gratis=Ya | Ham)  = 1/3 ≈ 0.33
P(menang=Ya | Ham)  = 0/3 = 0.0 → gunakan Laplace Smoothing
P(klik=Tidak | Ham) = 2/3 ≈ 0.67
```

> 💡 **Laplace Smoothing** digunakan untuk menghindari probabilitas bernilai nol:
> ```
> P(xᵢ | C) = (Jumlah xᵢ pada C + 1) / (Total sampel C + Jumlah kelas)
> ```

**Hitung Posterior:**
```
P(Spam | X) ∝ 0.4 × 0.5 × 1.0 × 0.5 = 0.100
P(Ham  | X) ∝ 0.6 × 0.33 × 0.1 × 0.67 ≈ 0.013
```

**Prediksi:** Email diklasifikasikan sebagai **SPAM** ✅

---

## Kelebihan dan Kekurangan

### ✅ Kelebihan
- **Cepat dan efisien** — pelatihan dan prediksi sangat cepat
- **Bekerja baik dengan data kecil** — tidak memerlukan banyak data training
- **Skalabel** — cocok untuk data berdimensi tinggi (teks)
- **Mudah diimplementasikan** — sederhana secara matematis
- **Multi-class** — secara natural mendukung lebih dari 2 kelas
- **Robust terhadap fitur tidak relevan** — tetap memberikan performa yang wajar

### ❌ Kekurangan
- **Asumsi independensi** — jarang terpenuhi dalam data nyata
- **Zero probability problem** — jika suatu fitur belum pernah muncul di data latih (diatasi dengan Laplace Smoothing)
- **Estimasi probabilitas kurang akurat** — meskipun klasifikasi benar, probabilitasnya bisa tidak presisi
- **Tidak cocok untuk fitur kontinu yang tidak berdistribusi normal** (pada Gaussian NB)

---

## Implementasi Python

### Menggunakan scikit-learn

```python
from sklearn.naive_bayes import GaussianNB, MultinomialNB, BernoulliNB
from sklearn.model_selection import train_test_split
from sklearn.metrics import classification_report, accuracy_score
import numpy as np

# ========================
# Gaussian Naive Bayes
# ========================
from sklearn.datasets import load_iris

# Load dataset
data = load_iris()
X, y = data.data, data.target

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Inisialisasi dan training model
gnb = GaussianNB()
gnb.fit(X_train, y_train)

# Prediksi
y_pred = gnb.predict(X_test)

# Evaluasi
print("Accuracy:", accuracy_score(y_test, y_pred))
print("\nClassification Report:")
print(classification_report(y_test, y_pred, target_names=data.target_names))
```

### Multinomial Naive Bayes untuk Klasifikasi Teks

```python
from sklearn.naive_bayes import MultinomialNB
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.pipeline import Pipeline

# Data contoh
corpus = [
    "gratis menang hadiah besar",    # spam
    "klik link menangkan sekarang",  # spam
    "rapat besok pukul sembilan",    # ham
    "laporan keuangan bulan ini",    # ham
    "promo diskon hari ini saja",    # spam
]
labels = ["spam", "spam", "ham", "ham", "spam"]

# Pipeline: Vectorizer + Classifier
pipeline = Pipeline([
    ("vectorizer", CountVectorizer()),
    ("classifier", MultinomialNB(alpha=1.0))  # alpha = Laplace smoothing
])

# Training
pipeline.fit(corpus, labels)

# Prediksi email baru
email_baru = ["dapatkan hadiah gratis klik sekarang"]
prediksi = pipeline.predict(email_baru)
probabilitas = pipeline.predict_proba(email_baru)

print(f"Prediksi: {prediksi[0]}")
print(f"Probabilitas: {dict(zip(pipeline.classes_, probabilitas[0].round(3)))}")
```

### Implementasi dari Nol (Scratch)

```python
import numpy as np
from collections import defaultdict

class NaiveBayesClassifier:
    def __init__(self, alpha=1.0):
        self.alpha = alpha  # Laplace smoothing
        self.class_priors = {}
        self.likelihoods = {}
        self.classes = []

    def fit(self, X, y):
        self.classes = list(set(y))
        n_samples = len(y)

        for c in self.classes:
            # Prior probability
            X_c = [X[i] for i in range(n_samples) if y[i] == c]
            self.class_priors[c] = len(X_c) / n_samples

            # Likelihood untuk setiap fitur
            self.likelihoods[c] = defaultdict(float)
            total = len(X_c) + self.alpha * 2  # Laplace smoothing

            for sample in X_c:
                for feature, value in enumerate(sample):
                    self.likelihoods[c][(feature, value)] += 1

            for key in self.likelihoods[c]:
                self.likelihoods[c][key] = (
                    self.likelihoods[c][key] + self.alpha
                ) / total

    def predict(self, X):
        return [self._predict_single(x) for x in X]

    def _predict_single(self, x):
        posteriors = {}
        for c in self.classes:
            log_prior = np.log(self.class_priors[c])
            log_likelihood = sum(
                np.log(self.likelihoods[c].get((i, v), self.alpha / 2))
                for i, v in enumerate(x)
            )
            posteriors[c] = log_prior + log_likelihood
        return max(posteriors, key=posteriors.get)
```

---

## Evaluasi Model

### Metrik Evaluasi Umum

```python
from sklearn.metrics import (
    accuracy_score,
    precision_score,
    recall_score,
    f1_score,
    confusion_matrix,
    ConfusionMatrixDisplay
)
import matplotlib.pyplot as plt

# Hitung metrik
accuracy  = accuracy_score(y_test, y_pred)
precision = precision_score(y_test, y_pred, average='weighted')
recall    = recall_score(y_test, y_pred, average='weighted')
f1        = f1_score(y_test, y_pred, average='weighted')

print(f"Accuracy  : {accuracy:.4f}")
print(f"Precision : {precision:.4f}")
print(f"Recall    : {recall:.4f}")
print(f"F1-Score  : {f1:.4f}")

# Confusion Matrix
cm = confusion_matrix(y_test, y_pred)
disp = ConfusionMatrixDisplay(confusion_matrix=cm)
disp.plot(cmap='Blues')
plt.title("Confusion Matrix - Naive Bayes")
plt.show()
```

### Penjelasan Metrik

| Metrik | Rumus | Keterangan |
|--------|-------|------------|
| **Accuracy** | TP + TN / Total | Proporsi prediksi yang benar |
| **Precision** | TP / (TP + FP) | Dari yang diprediksi positif, berapa yang benar? |
| **Recall** | TP / (TP + FN) | Dari yang positif sebenarnya, berapa yang terdeteksi? |
| **F1-Score** | 2 × (P × R) / (P + R) | Harmonic mean dari Precision dan Recall |

---

## Referensi

- Bayes, T. (1763). *An Essay towards Solving a Problem in the Doctrine of Chances*
- Mitchell, T. M. (1997). *Machine Learning*. McGraw-Hill
- Scikit-learn Documentation: [Naive Bayes](https://scikit-learn.org/stable/modules/naive_bayes.html)

---

> 📌 **Catatan:** Naive Bayes sangat cocok sebagai **baseline model** karena cepat, sederhana, dan sering kali memberikan performa yang kompetitif bahkan dibandingkan model yang lebih kompleks.
