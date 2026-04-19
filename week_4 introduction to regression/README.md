# Week 4 - Supervised Learning (Regression)

## Training Result Analysis

Pada analisis ini, dilakukan evaluasi model regresi menggunakan beberapa metrik statistik seperti **coefficient, standard error, dan t-statistic** untuk memahami pengaruh masing-masing fitur terhadap target (harga rumah).

---

## 🔍 Hasil Analisis

- **Avg. Area Number of Bedrooms**
  - Memiliki nilai **t-statistic paling kecil**
  - Kemungkinan **tidak terlalu signifikan** dalam mempengaruhi harga rumah

- **Avg. Area House Age** dan **Avg. Area Number of Rooms**
  - Memiliki **koefisien terbesar**
  - Memberikan **pengaruh paling besar terhadap harga rumah**

- **Avg. Area Income**
  - Memiliki **t-statistic tertinggi**
  - Bukan karena pengaruh besar, tetapi karena **standard error kecil** (lebih stabil)

---

##  Interpretasi

### 1. Coefficient (Koefisien)
- Menunjukkan **besar pengaruh fitur terhadap target**
- Nilai besar → dampak perubahan fitur lebih signifikan

### 2. t-statistic
- Menunjukkan **tingkat signifikansi fitur**
- Nilai tinggi → fitur lebih konsisten & dapat dipercaya dalam model

---

##  Kesimpulan Model

1. Model memiliki performa yang baik dengan:
   - **R² ≈ 0.92** → mampu menjelaskan 92% variasi data

2. Rata-rata kesalahan prediksi sekitar:
   - **± 8.17% dari harga rumah**

3. Perbandingan error:
   - **RMSE > MAE**
   - Menandakan adanya **beberapa outlier (error besar)** dalam prediksi

---

## Kesimpulan

Model regresi yang digunakan sudah cukup akurat dan stabil dalam memprediksi harga rumah.  
Sebagian besar fitur memberikan kontribusi signifikan, meskipun ada fitur yang kurang berpengaruh.  
Namun, masih terdapat beberapa prediksi dengan error besar yang perlu diperhatikan (outliers).
