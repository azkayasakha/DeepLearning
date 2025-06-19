---

# 📘 Chapter 5 – Support Vector Machines (SVM)

---

## 🎯 Tujuan Bab Ini:

* Memahami konsep dan intuisi di balik **Support Vector Machine (SVM)**.
* Menggunakan SVM untuk **klasifikasi** dan **regresi**.
* Mengenal **linear SVM**, **kernel SVM**, dan **hyperparameter tuning**.

---

## 🧠 1. Intuisi Dasar SVM

### 🔻 Masalah:

Diberikan data dua kelas yang bisa dipisahkan secara linear, bagaimana memilih *garis pemisah terbaik*?

### 💡 Solusi SVM:

Alih-alih hanya memilih garis *yang memisahkan data*, SVM memilih **garis yang memaksimalkan margin** — yaitu jarak antara garis ke titik data terdekat dari kedua kelas.

🧱 **Support Vectors** = Titik data yang berada paling dekat ke hyperplane (mereka menentukan margin).

---

## ➕ 2. Soft Margin vs Hard Margin

* **Hard Margin**: tidak membolehkan kesalahan (overfitting saat data noisy).
* **Soft Margin**: membolehkan sedikit pelanggaran margin agar generalisasi lebih baik.

🔧 **Hyperparameter `C`**:

* Kecil → lebih longgar (soft margin tinggi) → bisa underfit
* Besar → lebih ketat (margin kecil) → bisa overfit

---

## 🌐 3. Kernel Trick: SVM untuk Non-Linear Data

Jika data tidak bisa dipisahkan linear, kita bisa **proyeksikan ke dimensi lebih tinggi**. SVM melakukannya tanpa menghitung transformasi secara eksplisit, menggunakan **kernel trick**.

### 🔧 Jenis Kernel:

* **Linear**: cocok untuk data separable
* **Polynomial**: cocok untuk data yang dipisahkan oleh kurva polinomial
* **RBF (Radial Basis Function)** / Gaussian: sangat umum, cocok untuk data kompleks

🔧 **Hyperparameter:**

* `C` (seperti sebelumnya)
* `gamma` (khusus RBF kernel):

  * Kecil → fungsi lebih lebar → generalisasi lebih luas
  * Besar → fungsi lebih sempit → fit ke data → bisa overfit

---

## 📈 4. SVM untuk Regresi (SVR)

* Sama seperti SVM klasifikasi, tapi fokus untuk **mendekati semua data dalam margin tertentu**.
* Hyperparameter `epsilon` menentukan seberapa jauh kesalahan masih ditoleransi tanpa penalti.

---

## 💡 5. Skalabilitas dan Performa

* SVM tidak cocok untuk dataset sangat besar (>10k–100k sampel) karena training lambat.
* Cocok untuk data yang **tidak terlalu besar tapi kompleks**.

---

## 📑 Ringkasan Inti Bab Ini

* **SVM bekerja dengan mencari margin maksimum** antara kelas.
* **C** mengontrol keseimbangan antara margin lebar dan kesalahan kecil.
* **Kernel trick** memungkinkan SVM bekerja pada data nonlinier tanpa eksplisit mengubah dimensi.
* **SVR** digunakan untuk regresi dengan prinsip margin juga.
* Perlu hati-hati saat mengatur **C dan gamma** — karena keduanya sangat memengaruhi performa dan overfitting.

---

📌 Selanjutnya, kita akan lihat **kode praktik penggunaan SVM** dengan:

* Linear SVM (SGD & SVC)
* Nonlinear SVM (RBF kernel)
* Visualisasi margin
* Tuning parameter `C` dan `gamma`