---

# 📘 Chapter 3 – Classification

---

## 🎯 Tujuan Bab Ini:

* Memahami konsep klasifikasi dalam machine learning.
* Membangun model klasifikasi pertama menggunakan dataset **MNIST** (angka tulisan tangan 0–9).
* Mengenal berbagai metrik evaluasi klasifikasi seperti akurasi, precision, recall, F1 score, dan confusion matrix.

---

## 🔢 1. Pengertian Klasifikasi

**Classification** adalah jenis supervised learning yang bertujuan memetakan input ke **label diskrit** (kategori).

### Contoh:

* Apakah email ini spam atau bukan? → **binary classification**
* Angka apa yang ditulis tangan ini? → **multiclass classification**
* Kategori jenis kelamin, status pelanggan, dsb.

---

## 📚 2. Dataset: MNIST

Dataset MNIST berisi:

* 70.000 gambar angka tulisan tangan (28×28 piksel)
* 60.000 data training dan 10.000 data testing
* Label berupa angka 0–9

📝 Setiap gambar direpresentasikan sebagai vektor panjang 784 (28×28).

---

## 🏗️ 3. Model Pertama: Stochastic Gradient Descent (SGD)

SGDClassifier cocok untuk data berukuran besar seperti MNIST karena:

* Dapat belajar **secara online (incremental)**.
* Cepat dan efisien untuk klasifikasi linier.

---

## 📊 4. Evaluasi Model Klasifikasi

### ✅ **Akurasi**

* Proporsi prediksi yang benar.
* Tidak cocok untuk data tidak seimbang.

### 📉 **Confusion Matrix**

* Matriks 2D untuk menunjukkan prediksi vs label asli.

### 🎯 **Precision dan Recall**

* **Precision**: dari semua prediksi positif, berapa yang benar?
* **Recall**: dari semua data positif, berapa yang berhasil terdeteksi?

### ⚖️ **F1-Score**

* Harmonic mean dari precision dan recall.
* Cocok untuk dataset tidak seimbang.

---

## 🧠 5. Strategi Multiclass

Beberapa algoritma hanya mendukung **binary classification**, sehingga perlu teknik untuk menangani multiclass:

* **OvA (One-vs-All)**: Latih 10 binary classifier (0 vs all, 1 vs all, dst.)
* **OvO (One-vs-One)**: Latih satu classifier untuk setiap pasangan kelas (45 classifier untuk 10 kelas)

Scikit-Learn memilih strategi secara otomatis tergantung algoritma.

---

## 🧼 6. Skala Fitur (Feature Scaling)

Sangat penting sebelum menggunakan SGD, karena perbedaan skala antar fitur bisa mengacaukan proses optimisasi.

Biasanya digunakan `StandardScaler`.

---

## 🔎 7. Validasi Silang (Cross Validation)

Evaluasi model dengan lebih akurat dan menghindari **overfitting** ke data training.

Fungsi: `cross_val_score(model, X, y, cv=3)`

---

## 🧪 8. Predicting Probabilities

Untuk beberapa algoritma (seperti `SGDClassifier`, `LogisticRegression`), kita bisa prediksi **probabilitas** tiap kelas dengan `.decision_function()` atau `.predict_proba()`.

---

## 🧯 9. Error Analisis

Setelah evaluasi awal, kita lakukan:

* Analisis **confusion matrix**
* Lihat **contoh prediksi salah**
* Cari tahu **pola kesalahan** yang bisa diperbaiki

---

## 📑 Ringkasan Inti Bab Ini

* Klasifikasi adalah tentang memprediksi kategori dari input.
* Dataset MNIST digunakan untuk klasifikasi angka tulisan tangan.
* Evaluasi klasifikasi perlu lebih dari sekadar akurasi.
* Tools penting: confusion matrix, precision, recall, F1, cross-validation.
* Strategi multiclass penting untuk model yang hanya mendukung binary.
* Error analysis membantu memperbaiki dan memahami model.

---

🧭 Selanjutnya kita akan membuat **kode praktikal klasifikasi angka MNIST** dengan `SGDClassifier`, evaluasi, dan analisis errornya.