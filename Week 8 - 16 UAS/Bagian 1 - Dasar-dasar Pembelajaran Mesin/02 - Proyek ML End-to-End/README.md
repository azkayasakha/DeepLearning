---

# 📘 Chapter 2 – End-to-End Machine Learning Project

---

## 🎯 Tujuan Bab Ini:

* Menunjukkan proses lengkap membangun proyek Machine Learning dari awal hingga akhir.
* Menggunakan dataset **California Housing**.
* Fokus pada **praktik nyata**: pembersihan data, eksplorasi, persiapan data, pelatihan model, evaluasi, dan simpan model.

---

## 🗂️ 1. Mengerti Masalah dan Tujuan Bisnis

> Proyek ini mensimulasikan skenario di mana kamu bekerja untuk perusahaan real estate yang ingin membuat sistem prediksi harga rumah berdasarkan data sensus California.

🔎 **Pertanyaan bisnis:**
Bagaimana kita bisa memprediksi harga rumah median di suatu daerah berdasarkan informasi demografis dan geografis?

🎯 **Target ML:**
Prediksi numerik → berarti kita berhadapan dengan **regression problem**.

---

## 📊 2. Memperoleh Data

Dataset yang digunakan:

* **California Housing Dataset** (dari tahun 1990)
* Tersedia langsung di `sklearn.datasets.fetch_california_housing()`

Opsi lain:

* File CSV (bila di-download terpisah dari repositori buku)
* Atau lewat repositori GitHub Aurélien Géron

---

## 🔍 3. Jelajahi Data dan Pahami

Gunakan statistik deskriptif dan visualisasi untuk memahami data:

* Cek info dataset (jumlah baris, kolom, missing value)
* Cek distribusi fitur
* Gunakan histogram, scatter plot, dan correlation matrix

🎯 Tujuannya:

* Menemukan pola
* Mengetahui anomali
* Menentukan preprocessing yang dibutuhkan

---

## 🧹 4. Membagi Dataset (Training/Test Set)

Kenapa harus dibagi?

* Agar kita bisa mengevaluasi performa model pada **data yang belum pernah dilihat sebelumnya**.
* Biasanya digunakan pembagian **80% training – 20% test**.

💡 Teknik tambahan:

* **Stratified sampling**: memastikan distribusi subset data tetap representatif (misal: pendapatan menengah).

---

## 🧽 5. Pembersihan dan Persiapan Data

### Langkah umum:

* Menangani **missing value**
* Mengubah **kategori ke numerik**
* **Feature scaling** (normalisasi/standarisasi)
* **Feature engineering** (membuat fitur baru dari yang ada)

🔧 Tools yang digunakan:

* `SimpleImputer`, `OneHotEncoder`, `StandardScaler`, dan `Pipeline` dari `scikit-learn`

---

## 🏗️ 6. Pilih Model dan Latih

* Mulai dari model sederhana: **Linear Regression**
* Coba model lebih kompleks: **Decision Tree**, **Random Forest**
* Gunakan **cross-validation** untuk menghindari overfitting

---

## 📈 7. Evaluasi Model

* Untuk regresi: **RMSE**, **MAE**
* Gunakan **cross-validation** untuk mengevaluasi secara lebih akurat
* Bandingkan beberapa model berdasarkan performa

---

## 🔄 8. Tuning dan Fine-tuning Model

Gunakan:

* **Grid Search**: mencoba semua kombinasi parameter
* **Randomized Search**: sampling parameter secara acak
* Validasi akhir pada test set

---

## 💾 9. Simpan dan Deploy Model

* Simpan model terlatih dengan `joblib` atau `pickle`
* Bisa digunakan kembali tanpa melatih ulang
* Model bisa di-*deploy* ke aplikasi web, API, atau sistem lain

---

## 📑 Ringkasan Alur Proyek ML End-to-End:

1. **Definisikan masalah**
2. **Dapatkan data**
3. **Eksplorasi data awal**
4. **Buat set validasi**
5. **Siapkan data**
6. **Pilih dan latih model**
7. **Evaluasi model**
8. **Perbaiki dan tuning model**
9. **Uji model akhir**
10. **Simpan dan deploy model**

---

📌 Setelah ini, kita bisa lanjut ke **kode praktikalnya**, mengikuti struktur langkah di atas secara langsung.