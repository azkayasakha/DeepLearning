---

# 📘 Chapter 1 – **Pendahuluan Machine Learning**

---

## 🔍 Apa Itu Machine Learning?

**Machine Learning (ML)** adalah cabang dari kecerdasan buatan (AI) yang memungkinkan sistem belajar dari data tanpa diprogram secara eksplisit. Ini sangat berguna untuk tugas-tugas di mana membuat aturan logika eksplisit sangat sulit atau tidak mungkin.

### 📖 Definisi Resmi:

1. **Arthur Samuel (1959)**

> “Machine Learning adalah bidang studi yang memberi komputer kemampuan untuk belajar tanpa diprogram secara eksplisit.”

2. **Tom Mitchell (1997)**

> “Sebuah program komputer dikatakan belajar dari pengalaman E untuk tugas T dan ukuran performa P, jika performanya dalam T, diukur oleh P, meningkat seiring pengalaman E.”

---

## 💼 Contoh Penerapan Machine Learning:

* **Penyaring spam** pada email
* **Pengenalan wajah** pada foto
* **Rekomendasi produk** di e-commerce
* **Deteksi penipuan** kartu kredit
* **Asisten suara** seperti Google Assistant
* **Sistem navigasi mobil otonom**

---

## 🧠 Mengapa Gunakan Machine Learning?

Karena untuk beberapa tugas:

* Terlalu **kompleks untuk dikodekan** secara manual (misalnya: pengenalan gambar).
* Terlalu **berubah-ubah** aturannya (misalnya: deteksi penipuan).
* Dapat meningkatkan akurasi dari **sistem berbasis aturan** dengan belajar dari data nyata.

---

## 🧭 Tipe-tipe Machine Learning

### 1. **Supervised Learning**

Belajar dari data **berlabel**.
🔹 Input: fitur (X)
🔹 Output: target (y)

Contoh:

* Prediksi harga rumah (regresi)
* Klasifikasi email spam (klasifikasi)

---

### 2. **Unsupervised Learning**

Belajar dari data **tanpa label**.
Model mencari pola, struktur, atau hubungan dalam data.

Contoh:

* Klasterisasi pelanggan berdasarkan perilaku belanja
* Reduksi dimensi (PCA)

---

### 3. **Reinforcement Learning**

Agen belajar melalui **trial-and-error** dengan menerima **reward** atau **punishment**.
Digunakan dalam:

* Game (AlphaGo, Dota 2 AI)
* Robot navigasi

---

### 4. **Semi-Supervised Learning**

Menggunakan sebagian kecil data berlabel dan banyak data tidak berlabel. Berguna ketika label sulit didapat (misalnya: citra medis).

---

### 5. **Self-Supervised Learning**

Label dibuat otomatis dari data itu sendiri. Banyak digunakan dalam pelatihan awal model NLP dan computer vision.

---

## 🔁 Proses Umum dalam Proyek Machine Learning

1. **Mendefinisikan masalah**
   Apakah klasifikasi, regresi, klaster, dsb.

2. **Mengumpulkan data**
   Dari database, API, sensor, log aplikasi, dll.

3. **Eksplorasi dan pra-pemrosesan data**
   Visualisasi, pembersihan data, normalisasi, dll.

4. **Membangun model awal**
   Pilih model sederhana untuk baseline.

5. **Latih model**
   Dengan data training.

6. **Evaluasi model**
   Menggunakan data test dan metrik seperti akurasi, precision, recall, dsb.

7. **Tuning & Validasi**
   Gunakan teknik seperti cross-validation, grid search.

8. **Deploy model**
   Jalankan model ke produksi (web, aplikasi, embedded).

---

## ⚠️ Tantangan dalam Machine Learning

* **Overfitting**: Model terlalu cocok dengan data training, buruk pada data baru.
* **Underfitting**: Model terlalu sederhana, tidak menangkap pola data.
* **Data berkualitas rendah**: Sampah masuk = sampah keluar.
* **Feature Engineering**: Menentukan fitur mana yang relevan bisa sangat sulit.

---

## 🧩 Komponen Inti Machine Learning

* **Dataset**: Data input dan (jika supervised) label.
* **Fitur**: Atribut atau kolom penting dari data.
* **Model**: Fungsi matematika yang memetakan input ke output.
* **Algoritma**: Metode untuk melatih model (misalnya: SGD, Gradient Descent).

---

## 📑 Ringkasan Inti Bab Ini

* ML membuat komputer *belajar dari data*, bukan dari instruksi eksplisit.
* Jenis utama ML: **Supervised**, **Unsupervised**, dan **Reinforcement**.
* Proyek ML mengikuti langkah-langkah sistematis: dari definisi masalah hingga deployment.
* Tantangan umum: **overfitting**, **data jelek**, dan **pemilihan fitur**.
* ML adalah keterampilan yang berguna di berbagai bidang — mulai dari bisnis, teknologi, hingga ilmu sosial.

---

Setelah memahami teori ini, kita akan lanjut ke **contoh kode sederhana** menggunakan Python dan `scikit-learn`, untuk melihat bagaimana semua ini diterapkan dalam praktik.