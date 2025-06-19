---

# 📘 Chapter 4 – **Training Models**

---

## 🎯 Tujuan Bab Ini:

* Memahami bagaimana model machine learning dilatih.
* Memahami **Linear Regression** dan **Gradient Descent** (termasuk varian-nya).
* Mengenal **underfitting, overfitting**, dan **regularization**.

---

## ⚙️ 1. Model Linier

### 📌 Tujuan:

Mencari garis (atau hyperplane) terbaik yang **memprediksi nilai target** secara linier dari fitur.

### 🧮 Rumus dasar regresi linier:

$$
\hat{y} = \theta_0 + \theta_1 x_1 + \dots + \theta_n x_n
$$

atau secara vektor:

$$
\hat{y} = X \cdot \theta
$$

Tujuan training: temukan parameter **θ (theta)** yang meminimalkan **loss** antara prediksi dan label asli.

---

## 📉 2. Fungsi Loss: MSE

Untuk regresi, kita ingin meminimalkan **Mean Squared Error (MSE)**:

$$
MSE(\theta) = \frac{1}{m} \sum_{i=1}^{m} (\hat{y}^{(i)} - y^{(i)})^2
$$

Di sinilah **optimisasi** dilakukan — kita ingin mencari parameter model yang membuat MSE sekecil mungkin.

---

## 🔻 3. Metode Optimisasi: Gradient Descent

Gradient Descent adalah algoritma iteratif yang **bergerak ke bawah pada permukaan loss** sampai menemukan minimum.

### Jenis Gradient Descent:

| Jenis             | Ciri-ciri                                  | Pro                                  |
| ----------------- | ------------------------------------------ | ------------------------------------ |
| **Batch GD**      | Gunakan seluruh data untuk tiap update     | Stabil, akurat                       |
| **Stochastic GD** | Gunakan 1 data point per update            | Cepat, bisa keluar dari local minima |
| **Mini-batch GD** | Gunakan subset kecil dari data tiap update | Kombinasi efisiensi & stabilitas     |

---

## 🧠 4. Analitik Solusi: Normal Equation

Untuk regresi linier sederhana (tanpa regularisasi), ada solusi langsung:

$$
\theta = (X^T X)^{-1} X^T y
$$

Tidak perlu iterasi. Tapi: **tidak efisien untuk data besar**.

---

## 🧱 5. Regularization (Pencegahan Overfitting)

**Regularisasi** menambahkan penalti terhadap kompleksitas model. Ini membantu mengurangi overfitting.

### Jenis Regularisasi:

| Jenis           | Penalti                            | Tujuan                                       |
| --------------- | ---------------------------------- | -------------------------------------------- |
| **Ridge (L2)**  | Penalti terhadap kuadrat parameter | Menjaga parameter kecil                      |
| **Lasso (L1)**  | Penalti terhadap nilai absolut     | Mendorong sparsity (banyak parameter jadi 0) |
| **Elastic Net** | Gabungan L1 dan L2                 | Kompromi antara Ridge & Lasso                |

---

## 📉 6. Learning Curves: Diagnosa Under/Overfitting

Kamu bisa plot **kurva loss** terhadap waktu/training size:

* Jika **training error tinggi**, kemungkinan underfitting.
* Jika **gap besar antara training dan validation error**, kemungkinan overfitting.
* Idealnya: error training dan validation **rendah dan berdekatan**.

---

## 🧪 7. Polynomial Regression

Regresi linier tidak bisa menangkap **pola non-linier**. Solusinya:

* Buat **fitur polinomial**: $x^2, x^3, \ldots$
* Gunakan pipeline untuk preprocessing

---

## 📑 Ringkasan Inti Bab Ini

* **Training model = mencari parameter terbaik** yang meminimalkan loss.
* Gradient Descent adalah pendekatan umum dan fleksibel untuk optimisasi.
* Overfitting bisa diatasi dengan **regularization**.
* Underfitting diatasi dengan model lebih kompleks atau fitur yang lebih informatif.
* Evaluasi proses training dengan **learning curves**.

---

Selanjutnya, kita akan implementasikan:

* Regresi linier dengan Normal Equation dan Gradient Descent,
* Ridge & Lasso,
* serta visualisasi learning curves.