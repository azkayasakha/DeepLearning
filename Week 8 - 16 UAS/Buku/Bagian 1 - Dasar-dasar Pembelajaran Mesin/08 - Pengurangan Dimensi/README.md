---

# 📘 Chapter 8 – Dimensionality Reduction

---

## 🎯 Tujuan Bab Ini:

* Memahami **masalah dimensionalitas tinggi** (curse of dimensionality).
* Belajar mengurangi jumlah fitur (dimensi) tanpa kehilangan informasi penting.
* Memahami dan menerapkan **PCA**, **Kernel PCA**, dan **LLE**.

---

## 🌌 1. Curse of Dimensionality

> Saat dimensi (fitur) meningkat, data jadi **jarang dan sulit dianalisis** secara efektif.

### Dampaknya:

* Model jadi lambat dan overfit
* Visualisasi tidak berguna
* Perhitungan jarak jadi tidak berarti

---

## ✂️ 2. Dimensionality Reduction

Tujuannya:

* **Kurangi kompleksitas model**
* **Hapus noise**
* **Visualisasi lebih mudah** (misalnya ke 2D/3D)

### Dua pendekatan:

1. **Feature Selection** → pilih subset fitur
2. **Feature Extraction** → buat fitur baru dari gabungan fitur lama (contoh: PCA)

---

## 📉 3. Principal Component Analysis (PCA)

**PCA** adalah teknik linear yang memproyeksikan data ke arah yang **memaksimalkan variasi (variance)**.

### Intuisi:

* Cari **vektor ortogonal (principal components)** yang menangkap informasi paling banyak dari data.
* Komponen pertama = arah dengan varian terbesar.

### Properti PCA:

* Komponen saling ortogonal
* Proyeksi terbaik dalam MSE (minimalkan kesalahan rekonstruksi)
* PCA tidak memperhatikan label → **unsupervised**

---

## 🔧 4. Menggunakan PCA

* Bisa digunakan untuk **visualisasi 2D**
* Bisa juga digunakan sebelum training model agar **lebih cepat dan tidak overfit**

Scikit-Learn:

```python
from sklearn.decomposition import PCA
pca = PCA(n_components=2)
X2D = pca.fit_transform(X)
```

📌 Bisa juga menentukan `n_components` berdasarkan rasio variansi (misal: 95%).

---

## 🧮 5. Memilih Jumlah Komponen

Gunakan atribut `explained_variance_ratio_`:

```python
cumsum = np.cumsum(pca.explained_variance_ratio_)
d = np.argmax(cumsum >= 0.95) + 1  # Berapa komponen cukup untuk menjelaskan 95% variansi
```

---

## 🧲 6. Kernel PCA

**PCA standar hanya untuk data linear**. Untuk data non-linear → gunakan **Kernel PCA (kPCA)**.

* Gunakan **kernel trick** seperti pada SVM (RBF, polynomial)
* Mampu menangkap pola non-linear

```python
from sklearn.decomposition import KernelPCA
kpca = KernelPCA(kernel="rbf", gamma=0.04)
X_kpca = kpca.fit_transform(X)
```

---

## 🧩 7. Manifold Learning

Jika data terletak pada struktur non-linear (manifold), gunakan teknik seperti:

* **LLE (Locally Linear Embedding)** → mempertahankan hubungan lokal
* **t-SNE** → sangat baik untuk visualisasi 2D/3D tapi lambat

```python
from sklearn.manifold import LocallyLinearEmbedding
lle = LocallyLinearEmbedding(n_components=2, n_neighbors=10)
X_lle = lle.fit_transform(X)
```

---

## 🧠 8. Kapan Gunakan Dimensionality Reduction?

Gunakan saat:

* Data punya banyak fitur (>10–50)
* Model terlalu overfit
* Butuh visualisasi
* Ingin efisiensi komputasi

---

## 📑 Ringkasan Inti Bab Ini:

* Dimensionality Reduction penting untuk kecepatan, akurasi, dan interpretasi model.
* PCA memproyeksikan data ke arah dengan varian terbesar.
* Kernel PCA dan LLE memungkinkan reduksi non-linear.
* Selalu evaluasi apakah reduksi membantu atau justru membuang informasi penting.

---