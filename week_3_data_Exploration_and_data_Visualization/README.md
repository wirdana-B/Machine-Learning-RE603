# 🧹 Data Preprocessing Pipeline
> *"Data yang bersih adalah fondasi dari model yang cerdas."*

Pipeline lengkap untuk mempersiapkan data sebelum masuk ke tahap Machine Learning — mulai dari deteksi duplikat, penanganan outlier, imputasi missing value, encoding, hingga feature scaling.

---

## 📋 Daftar Isi

- [Handling Duplikat](#-handling-duplikat)
- [Outlier Handling](#-outlier-handling)
- [Splitting Data](#-splitting-data)
- [Missing Value Handling](#-missing-value-handling)
- [Encoding](#-encoding)
- [Feature Scaling](#-feature-scaling)

---

## 🔍 Handling Duplikat

Sebelum memproses data lebih lanjut, penting untuk memastikan tidak ada baris yang terduplikasi. Data duplikat dapat membuat model *overfitting* dan menghasilkan evaluasi yang tidak akurat.

```python
# Cek jumlah duplikat
df.duplicated().sum()

# Hapus duplikat
df.drop_duplicates(inplace=True)
```

> 💡 **Tips:** Bandingkan panjang data sebelum dan sesudah untuk memverifikasi hasilnya.

---

## 📊 Outlier Handling

**Outlier** adalah data yang nilainya sangat jauh menyimpang dari distribusi umum data — sehingga menimbulkan kecurigaan bahwa data tersebut berasal dari sumber yang berbeda.

### Dampak Outlier
| Dampak | Keterangan |
|--------|-----------|
| 📉 Distorsi Statistik | Memengaruhi nilai rata-rata dan varians |
| 🤖 Performa Model | Merusak performa beberapa algoritma ML |

### Metode Deteksi

Setiap kolom diviualisasikan menggunakan **3 plot sekaligus** untuk analisis menyeluruh:

| Visualisasi | Apa yang Dilihat |
|-------------|-----------------|
| 📊 **Histogram** | Distribusi data & skewness |
| 📈 **Q-Q Plot** | Titik yang keluar dari garis merah = outlier |
| 📦 **Box Plot** | Titik di luar whisker = outlier |

**Contoh temuan pada kolom `population` (California Housing Dataset):**
```
Histogram  → Skew kanan (ekor panjang di sisi kanan)
Q-Q Plot   → Titik biru keluar dari garis merah di ujung atas
Box Plot   → Banyak outlier di sisi atas, whisker atas sangat panjang
```

### Metode Penanganan

#### 1️⃣ IQR — Pendekatan Statistik
```python
Q1 = df['kolom'].quantile(0.25)
Q3 = df['kolom'].quantile(0.75)
IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR

df_clean = df[(df['kolom'] >= lower) & (df['kolom'] <= upper)]
```

#### 2️⃣ Nilai Sembarang — Pendekatan Bisnis
Gunakan domain knowledge untuk menentukan batas wajar sebuah nilai.
```python
# Contoh: populasi tidak mungkin lebih dari 50.000
df_clean = df[df['population'] <= 50000]
```

> ⚠️ **Penting:** Outlier handling **hanya dilakukan pada data train**, bukan data test!

---

## ✂️ Splitting Data

Data dibagi menjadi **train set** dan **test set** sebelum preprocessing lanjutan dilakukan.

```
Train : Test  →  80:20  |  75:25  |  70:30 (min)  |  85:15  |  90:10 (maks)
```

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
```

> 🧪 **Filosofi:** Data test adalah representasi **"data masa depan"** — jangan pernah melakukan fitting atau transformasi apapun berdasarkan data test!

---

## 🩹 Missing Value Handling

Aturan sederhana namun powerful untuk imputasi missing value:

| Tipe Data | Metode Imputasi | Alasan |
|-----------|----------------|--------|
| **Numerik** | **Median** | Robust terhadap outlier |
| **Kategorik / Object / String** | **Modus (Mode)** | Nilai yang paling sering muncul |

```python
from sklearn.impute import SimpleImputer

# Numerik → Median
num_imputer = SimpleImputer(strategy='median')

# Kategorik → Mode
cat_imputer = SimpleImputer(strategy='most_frequent')
```

**Studi Kasus — Kolom `Rating`:**
```
Sebelum : Nilai -1 tersebar di beberapa baris (penanda missing value)
Sesudah : Nilai -1 diganti median = 3.8
Efek    : Frekuensi nilai 3.8 meningkat drastis → distribusi lain tetap sama
```

> 💡 **Catatan:** Lakukan fit imputer **hanya** pada data train, lalu transform ke data test.

---

## 🏷️ Encoding

Mengubah data kategorik menjadi format numerik agar bisa diproses oleh algoritma ML.

### 1️⃣ One Hot Encoding
Cocok untuk fitur **nominal** (tidak ada urutan).
```python
from sklearn.preprocessing import OneHotEncoder
# atau
pd.get_dummies(df, columns=['kolom_kategorik'])
```
```
Contoh:  Kota = ['Jakarta', 'Bandung', 'Surabaya']
         → Jakarta_1, Bandung_0, Surabaya_0
```

### 2️⃣ Label Encoding
Cocok untuk fitur **ordinal** (ada urutan/ranking).
```python
from sklearn.preprocessing import LabelEncoder

le = LabelEncoder()
df['kolom'] = le.fit_transform(df['kolom'])
```
```
Contoh:  ['Low', 'Medium', 'High']  →  [0, 1, 2]
```

---

## ⚖️ Feature Scaling

Proses **mengubah skala nilai** tanpa mengubah makna data — memastikan semua fitur berada dalam rentang yang sebanding sehingga tidak ada fitur yang mendominasi model.

### Perbandingan Teknik

| Teknik | Formula | Rentang Output | Cocok Untuk |
|--------|---------|---------------|-------------|
| **StandardScaler** | `(x - μ) / σ` | Tidak terbatas (mean=0, std=1) | Data berdistribusi normal |
| **MinMaxScaler** | `(x - min) / (max - min)` | [0, 1] | Data dengan batas yang jelas |

### 1️⃣ StandardScaler
```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_train[['tenure', 'MonthlyCharges']] = scaler.fit_transform(
    X_train[['tenure', 'MonthlyCharges']]
)
X_test[['tenure', 'MonthlyCharges']] = scaler.transform(
    X_test[['tenure', 'MonthlyCharges']]
)
```

### 2️⃣ MinMaxScaler
```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
X_train[['tenure', 'MonthlyCharges']] = scaler.fit_transform(
    X_train[['tenure', 'MonthlyCharges']]
)
X_test[['tenure', 'MonthlyCharges']] = scaler.transform(
    X_test[['tenure', 'MonthlyCharges']]
)
```

> ⚠️ **Golden Rule:** Selalu `fit` pada **data train** saja, lalu `transform` pada keduanya. Jangan pernah `fit_transform` pada data test!

---

## 🔄 Alur Pipeline Lengkap

```
Raw Data
   │
   ▼
[1] Cek & Hapus Duplikat
   │
   ▼
[2] Split Data  →  Train (80%) | Test (20%)
   │
   ▼ (hanya pada Train)
[3] Outlier Handling (IQR / Business Rule)
   │
   ▼
[4] Missing Value Handling (Median / Mode)
   │
   ▼
[5] Encoding (One Hot / Label)
   │
   ▼
[6] Feature Scaling (Standard / MinMax)
   │
   ▼
Model Machine Learning 🚀
```




---

<p align="center">Made with ❤️ — Clean data, better models.</p>
