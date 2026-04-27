# 🔍 K-Nearest Neighbors (KNN) Classification

## Daftar Isi
- [Pengertian](#pengertian)
- [Cara Kerja](#cara-kerja)
- [Perhitungan Jarak](#perhitungan-jarak)
- [Memilih Nilai K](#memilih-nilai-k)
- [Contoh Kasus](#contoh-kasus)
- [Kelebihan dan Kekurangan](#kelebihan-dan-kekurangan)
- [Implementasi Python](#implementasi-python)
- [Evaluasi Model](#evaluasi-model)

---

## Pengertian

**K-Nearest Neighbors (KNN)** adalah algoritma klasifikasi (dan regresi) yang bekerja berdasarkan prinsip sederhana:

> *"Suatu data akan memiliki kelas yang sama dengan mayoritas tetangga terdekatnya."*

KNN termasuk algoritma **lazy learning** atau **instance-based learning**, artinya:
- ❌ Tidak ada proses "training" yang eksplisit
- ✅ Model langsung menyimpan seluruh data training
- ✅ Prediksi dilakukan saat ada data baru masuk

KNN banyak digunakan dalam:
- 🏥 Diagnosa penyakit berdasarkan gejala
- 🎬 Sistem rekomendasi film/produk
- 🖼️ Pengenalan gambar dan wajah
- 📊 Deteksi anomali / fraud

---

## Cara Kerja

### Algoritma KNN (Step by Step):

```
1. Tentukan nilai K (jumlah tetangga yang diperhitungkan)
2. Hitung jarak antara data baru dengan SEMUA data training
3. Urutkan jarak dari yang terkecil ke terbesar
4. Ambil K data dengan jarak terkecil (K tetangga terdekat)
5. Lakukan voting mayoritas dari kelas K tetangga tersebut
6. Kelas dengan suara terbanyak = hasil prediksi
```

### Ilustrasi:

```
Data Training:
  ● Kelas A: (1,2), (2,3), (1,4)
  ■ Kelas B: (5,5), (6,4), (7,6)

Data Baru: ★ (3,3), K=3

Jarak ke setiap titik:
  → (1,2): 2.83  ← tetangga
  → (2,3): 1.00  ← tetangga terdekat
  → (1,4): 2.24  ← tetangga
  → (5,5): 2.83
  → (6,4): 3.61
  → (7,6): 5.00

3 Tetangga Terdekat: semua Kelas A
Prediksi: ★ = Kelas A ✅
```

---

## Perhitungan Jarak

KNN menggunakan berbagai metode perhitungan jarak. Pemilihan metrik jarak berpengaruh besar terhadap performa model.

### 1. 📐 Euclidean Distance (paling umum)

Jarak garis lurus antara dua titik.

```
d(p, q) = √ Σ (pᵢ - qᵢ)²
```

**Contoh** (2D):
```
p = (1, 2), q = (4, 6)
d = √((4-1)² + (6-2)²)
d = √(9 + 16)
d = √25 = 5
```

---

### 2. 🏙️ Manhattan Distance

Jarak berdasarkan jalur grid (seperti jalan di kota).

```
d(p, q) = Σ |pᵢ - qᵢ|
```

**Contoh:**
```
p = (1, 2), q = (4, 6)
d = |4-1| + |6-2|
d = 3 + 4 = 7
```

---

### 3. 🔢 Minkowski Distance (generalisasi)

Menggabungkan Euclidean dan Manhattan dalam satu rumus.

```
d(p, q) = (Σ |pᵢ - qᵢ|^r)^(1/r)
```

- `r = 1` → Manhattan Distance
- `r = 2` → Euclidean Distance
- `r → ∞` → Chebyshev Distance

---

### 4. 📊 Cosine Similarity

Mengukur sudut antara dua vektor (bukan jarak absolut).

```
cos(θ) = (p · q) / (||p|| × ||q||)
```

**Cocok untuk:** data teks, dokumen, rekomendasi.

---

### Perbandingan Metrik Jarak

| Metrik | Formula | Cocok Untuk |
|--------|---------|-------------|
| Euclidean | √Σ(pᵢ-qᵢ)² | Data numerik umum |
| Manhattan | Σ\|pᵢ-qᵢ\| | Data dengan outlier |
| Minkowski | (Σ\|pᵢ-qᵢ\|^r)^(1/r) | Fleksibel |
| Cosine | (p·q)/(‖p‖‖q‖) | Data teks/vektor |
| Hamming | Proporsi bit berbeda | Data kategorikal/biner |

---

## Memilih Nilai K

Nilai **K** adalah hyperparameter terpenting dalam KNN.

### Efek Nilai K:

```
K terlalu kecil (K=1):
  → Sangat sensitif terhadap noise
  → Overfitting
  → Batas keputusan terlalu kompleks

K terlalu besar (K=N):
  → Semua data menjadi tetangga
  → Underfitting
  → Selalu prediksi kelas mayoritas

K optimal:
  → Seimbang antara bias dan variance
  → Batas keputusan lebih halus
```

### Tips Memilih K:

1. **Gunakan K ganjil** untuk menghindari seri/draw pada klasifikasi biner
2. **Aturan praktis:** K = √n, di mana n = jumlah data training
3. **Gunakan Cross-Validation** untuk mencari K terbaik
4. **Coba range K:** biasanya antara 1–20

### Mencari K Optimal dengan Cross-Validation:

```python
from sklearn.model_selection import cross_val_score
import numpy as np

k_values = range(1, 21)
cv_scores = []

for k in k_values:
    knn = KNeighborsClassifier(n_neighbors=k)
    scores = cross_val_score(knn, X_train, y_train, cv=5, scoring='accuracy')
    cv_scores.append(scores.mean())

best_k = k_values[np.argmax(cv_scores)]
print(f"K terbaik: {best_k}, Accuracy: {max(cv_scores):.4f}")
```

---

## Contoh Kasus

### Studi Kasus: Klasifikasi Penyakit Diabetes

**Dataset (sebagian):**

| # | Glukosa | BMI | Usia | Label |
|---|:-------:|:---:|:----:|:-----:|
| 1 | 85 | 26.6 | 31 | Tidak Diabetes |
| 2 | 183 | 23.3 | 32 | Diabetes |
| 3 | 89 | 28.1 | 21 | Tidak Diabetes |
| 4 | 137 | 43.1 | 33 | Diabetes |
| 5 | 116 | 25.6 | 30 | Tidak Diabetes |

**Data Baru:** Glukosa=120, BMI=32, Usia=29, K=3

**Langkah 1: Normalisasi data** (penting sebelum hitung jarak!)
```
Gunakan Min-Max Scaling atau Standard Scaler
agar semua fitur berada dalam skala yang sama
```

**Langkah 2: Hitung Euclidean Distance**
```
d(baru, #1) = √((120-85)² + (32-26.6)² + (29-31)²) = √(1225 + 29.16 + 4) = 35.64
d(baru, #2) = √((120-183)² + (32-23.3)² + (29-32)²) = √(3969 + 75.69 + 9) = 63.92
d(baru, #3) = √((120-89)² + (32-28.1)² + (29-21)²) = √(961 + 15.21 + 64) = 32.67
d(baru, #4) = √((120-137)² + (32-43.1)² + (29-33)²) = √(289 + 123.21 + 16) = 20.78
d(baru, #5) = √((120-116)² + (32-25.6)² + (29-30)²) = √(16 + 40.96 + 1) = 7.60
```

**Langkah 3: Urutkan & ambil K=3 terdekat**
```
1. #5 → jarak 7.60  → Tidak Diabetes
2. #4 → jarak 20.78 → Diabetes
3. #3 → jarak 32.67 → Tidak Diabetes
```

**Langkah 4: Voting Mayoritas**
```
Tidak Diabetes: 2 suara ✅
Diabetes      : 1 suara

Prediksi: TIDAK DIABETES
```

---

## Kelebihan dan Kekurangan

### ✅ Kelebihan
- **Sederhana & intuitif** — mudah dipahami dan diimplementasikan
- **Non-parametrik** — tidak ada asumsi distribusi data
- **Adaptif** — langsung menyesuaikan dengan data baru tanpa re-training
- **Multi-class** — secara natural mendukung lebih dari 2 kelas
- **Efektif pada data kecil** — performa baik jika data tidak terlalu besar

### ❌ Kekurangan
- **Lambat saat prediksi** — harus menghitung jarak ke semua data training (O(n·d))
- **Sensitif terhadap skala fitur** — wajib melakukan normalisasi/standardisasi
- **Sensitif terhadap outlier** — satu tetangga yang salah bisa mempengaruhi prediksi
- **Butuh memori besar** — menyimpan semua data training
- **Curse of dimensionality** — performa menurun drastis pada data berdimensi tinggi
- **Fitur tidak relevan mengganggu** — tidak ada pembobotan fitur otomatis

---

## Implementasi Python

### Menggunakan scikit-learn

```python
from sklearn.neighbors import KNeighborsClassifier
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import classification_report, accuracy_score
from sklearn.datasets import load_iris
import numpy as np

# Load dataset
data = load_iris()
X, y = data.data, data.target

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# ⚠️ PENTING: Normalisasi data sebelum KNN!
scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)
X_test  = scaler.transform(X_test)

# Inisialisasi model KNN
knn = KNeighborsClassifier(
    n_neighbors=5,        # nilai K
    metric='euclidean',   # metrik jarak
    weights='uniform'     # 'uniform' atau 'distance'
)

# Training (menyimpan data)
knn.fit(X_train, y_train)

# Prediksi
y_pred = knn.predict(X_test)

# Evaluasi
print("Accuracy:", accuracy_score(y_test, y_pred))
print("\nClassification Report:")
print(classification_report(y_test, y_pred, target_names=data.target_names))
```

---

### Mencari K Optimal

```python
from sklearn.neighbors import KNeighborsClassifier
from sklearn.model_selection import cross_val_score
import matplotlib.pyplot as plt
import numpy as np

k_range = range(1, 31)
train_scores = []
cv_scores = []

for k in k_range:
    knn = KNeighborsClassifier(n_neighbors=k)
    
    # Cross-validation score
    cv = cross_val_score(knn, X_train, y_train, cv=5, scoring='accuracy')
    cv_scores.append(cv.mean())

best_k = k_range[np.argmax(cv_scores)]
print(f"K terbaik: {best_k}")
print(f"CV Accuracy terbaik: {max(cv_scores):.4f}")

# Plot
plt.figure(figsize=(10, 5))
plt.plot(k_range, cv_scores, marker='o', color='steelblue')
plt.axvline(x=best_k, color='red', linestyle='--', label=f'K optimal = {best_k}')
plt.xlabel("Nilai K")
plt.ylabel("Cross-Validation Accuracy")
plt.title("Pemilihan K Optimal pada KNN")
plt.legend()
plt.grid(True)
plt.show()
```

---

### Implementasi dari Nol (Scratch)

```python
import numpy as np
from collections import Counter

class KNNClassifier:
    def __init__(self, k=5, metric='euclidean'):
        self.k = k
        self.metric = metric

    def fit(self, X, y):
        # KNN tidak melakukan training eksplisit
        # hanya menyimpan data
        self.X_train = np.array(X)
        self.y_train = np.array(y)

    def _euclidean(self, p, q):
        return np.sqrt(np.sum((p - q) ** 2))

    def _manhattan(self, p, q):
        return np.sum(np.abs(p - q))

    def _distance(self, p, q):
        if self.metric == 'euclidean':
            return self._euclidean(p, q)
        elif self.metric == 'manhattan':
            return self._manhattan(p, q)
        else:
            raise ValueError(f"Metrik tidak dikenal: {self.metric}")

    def predict(self, X):
        X = np.array(X)
        return np.array([self._predict_single(x) for x in X])

    def _predict_single(self, x):
        # Hitung jarak ke semua data training
        distances = [self._distance(x, x_train) for x_train in self.X_train]

        # Ambil indeks K tetangga terdekat
        k_indices = np.argsort(distances)[:self.k]

        # Ambil label K tetangga terdekat
        k_labels = [self.y_train[i] for i in k_indices]

        # Voting mayoritas
        most_common = Counter(k_labels).most_common(1)
        return most_common[0][0]

    def score(self, X, y):
        y_pred = self.predict(X)
        return np.mean(y_pred == np.array(y))


# Contoh penggunaan
knn = KNNClassifier(k=5, metric='euclidean')
knn.fit(X_train, y_train)
print("Accuracy:", knn.score(X_test, y_test))
```

---

### KNN dengan Weighted Voting

```python
# Tetangga yang lebih dekat mendapat bobot lebih besar
knn_weighted = KNeighborsClassifier(
    n_neighbors=5,
    weights='distance'  # bobot = 1/jarak
)
knn_weighted.fit(X_train, y_train)
y_pred_w = knn_weighted.predict(X_test)
print("Weighted KNN Accuracy:", accuracy_score(y_test, y_pred_w))
```

---

## Evaluasi Model

```python
from sklearn.metrics import (
    accuracy_score, precision_score,
    recall_score, f1_score,
    confusion_matrix, ConfusionMatrixDisplay
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
disp = ConfusionMatrixDisplay(confusion_matrix=cm, display_labels=data.target_names)
disp.plot(cmap='Blues')
plt.title("Confusion Matrix - KNN")
plt.show()
```

### Penjelasan Metrik

| Metrik | Rumus | Keterangan |
|--------|-------|------------|
| **Accuracy** | (TP + TN) / Total | Proporsi prediksi yang benar |
| **Precision** | TP / (TP + FP) | Dari yang diprediksi positif, berapa yang benar? |
| **Recall** | TP / (TP + FN) | Dari yang positif sebenarnya, berapa yang terdeteksi? |
| **F1-Score** | 2 × (P × R) / (P + R) | Harmonic mean dari Precision dan Recall |

---

## Perbandingan KNN vs Naive Bayes

| Aspek | KNN | Naive Bayes |
|-------|:---:|:-----------:|
| Tipe | Lazy Learning | Eager Learning |
| Training | ❌ Tidak ada | ✅ Ada |
| Prediksi | 🐢 Lambat (O(n·d)) | ⚡ Cepat |
| Memori | 🔴 Besar | 🟢 Kecil |
| Asumsi | Tidak ada | Independensi fitur |
| Sensitif skala | ✅ Ya (wajib scaling) | ❌ Tidak |
| Data berdimensi tinggi | 🔴 Buruk | 🟢 Baik |
| Interpretabilitas | 🟡 Sedang | 🟢 Mudah |

---

## Tips Praktis

> ⚠️ **Selalu normalisasi data** sebelum menggunakan KNN. Fitur dengan skala besar akan mendominasi perhitungan jarak.

> 💡 **Gunakan K ganjil** untuk klasifikasi biner agar tidak terjadi seri.

> 🔍 **Gunakan Cross-Validation** (bukan hanya train-test split) untuk mencari K optimal yang lebih reliabel.

> 📉 **Reduksi dimensi** (PCA, LDA) bisa meningkatkan performa KNN secara signifikan pada data berdimensi tinggi.

---

## Referensi

- Cover, T. & Hart, P. (1967). *Nearest Neighbor Pattern Classification*. IEEE Transactions on Information Theory.
- Fix, E. & Hodges, J. (1951). *Discriminatory Analysis — Nonparametric Discrimination*. USAF School of Aviation Medicine.
- Scikit-learn Documentation: [KNeighborsClassifier](https://scikit-learn.org/stable/modules/generated/sklearn.neighbors.KNeighborsClassifier.html)

---

> 📌 **Catatan:** KNN sangat cocok sebagai **baseline model** untuk memahami struktur data sebelum mencoba model yang lebih kompleks. Pastikan selalu melakukan **feature scaling** dan **pemilihan K yang tepat** untuk hasil terbaik.
