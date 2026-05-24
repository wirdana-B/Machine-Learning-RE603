🌳 Decision Tree Classification
📌 Deskripsi

Decision Tree Classification adalah salah satu algoritma Machine Learning yang digunakan untuk mengklasifikasikan data berdasarkan aturan keputusan berbentuk pohon.

Algoritma ini bekerja dengan membagi data menjadi beberapa cabang berdasarkan fitur tertentu hingga menghasilkan keputusan akhir atau kelas target.

Contoh penggunaan:

Prediksi kelulusan mahasiswa
Deteksi spam email
Diagnosa penyakit
Prediksi kualitas produk
Klasifikasi pelanggan
🧠 Cara Kerja Decision Tree

Decision Tree bekerja seperti diagram pohon:

                [Umur > 18?]
                 /       \
               Ya         Tidak
              /             \
      [Punya SIM?]        Ditolak
          /    \
        Ya     Tidak
      Diterima Ditolak

Setiap node berisi:

Root Node → node utama
Decision Node → pengambilan keputusan
Leaf Node → hasil akhir klasifikasi
⚙️ Algoritma yang Digunakan

Beberapa metode splitting:

Gini Index
Entropy
Information Gain

Rumus entropy:

Entropy(S)=−∑
i=1
n
	​

p
i
	​

log
2
	​

(p
i
	​

)

📚 Library yang Digunakan

Project ini menggunakan:

Python
Pandas
NumPy
Matplotlib
Scikit-Learn

Install library:

pip install pandas numpy matplotlib scikit-learn
📂 Struktur Project
decision-tree-classification/
│
├── dataset.csv
├── decision_tree.ipynb
├── README.md
└── requirements.txt
🚀 Contoh Implementasi
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score

# Membaca dataset
df = pd.read_csv('dataset.csv')

# Feature dan target
X = df.iloc[:, :-1]
y = df.iloc[:, -1]

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Model Decision Tree
model = DecisionTreeClassifier()

# Training
model.fit(X_train, y_train)

# Prediksi
y_pred = model.predict(X_test)

# Evaluasi
accuracy = accuracy_score(y_test, y_pred)

print("Accuracy:", accuracy)
📊 Visualisasi Decision Tree
from sklearn import tree
import matplotlib.pyplot as plt

plt.figure(figsize=(15,10))
tree.plot_tree(model, filled=True)
plt.show()
✅ Kelebihan Decision Tree
Mudah dipahami
Visualisasi sederhana
Tidak membutuhkan scaling data
Cocok untuk data kategorikal maupun numerik
❌ Kekurangan Decision Tree
Mudah overfitting
Sensitif terhadap perubahan data kecil
Akurasi bisa lebih rendah dibanding ensemble model
📈 Evaluasi Model

Beberapa metode evaluasi:

Accuracy
Precision
Recall
F1-Score
Confusion Matrix

Contoh confusion matrix:

from sklearn.metrics import confusion_matrix

cm = confusion_matrix(y_test, y_pred)
print(cm)
🎯 Kesimpulan

Decision Tree Classification merupakan algoritma Machine Learning yang sederhana namun powerful untuk menyelesaikan masalah klasifikasi. Algoritma ini sangat cocok digunakan untuk pembelajaran dasar Machine Learning karena mudah divisualisasikan dan dipahami.
