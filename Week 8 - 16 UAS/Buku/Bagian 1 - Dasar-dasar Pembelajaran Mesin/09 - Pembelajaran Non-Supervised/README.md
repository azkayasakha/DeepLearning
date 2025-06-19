---

# 📘 Chapter 9 – Unsupervised Learning Techniques

---

## 🎯 Tujuan Bab Ini:

* Memahami apa itu **unsupervised learning**.
* Menerapkan teknik clustering seperti **K-Means**, **DBSCAN**, dan **Gaussian Mixture Models (GMM)**.
* Menangani tugas-tugas tanpa label seperti segmentasi, reduksi noise, dan deteksi anomali.

---

## 🧠 1. Apa itu Unsupervised Learning?

> **Unsupervised learning** adalah pembelajaran dari data **tanpa label**.

Model tidak tahu targetnya apa, dan hanya mencari pola tersembunyi atau struktur alami dalam data.

---

## 🧭 2. Kegunaan Unsupervised Learning

* **Clustering**: Mengelompokkan data berdasarkan kemiripan (misalnya: pelanggan, gambar, dokumen)
* **Dimensionality Reduction**: seperti PCA, t-SNE
* **Anomaly Detection**: deteksi data tidak wajar
* **Generative Models**: seperti Autoencoders, GAN

---

## 📦 3. Clustering – K-Means

### 🔹 Intuisi:

* Tentukan **k** pusat cluster (centroid)
* Setiap data bergabung ke centroid terdekat
* Ulangi hingga konvergen

```python
from sklearn.cluster import KMeans
kmeans = KMeans(n_clusters=3)
kmeans.fit(X)
```

🧠 Hasil `kmeans.labels_` = label cluster untuk tiap data

### 🔧 Hyperparameter:

* `n_clusters`: jumlah cluster
* `init`: metode inisialisasi centroid
* `n_init`: jumlah percobaan inisialisasi

### 📐 Evaluasi:

* **Inertia**: total jarak dari tiap titik ke centroidnya (semakin kecil semakin baik)
* Gunakan **Elbow method** atau **Silhouette Score**

---

## 🌪️ 4. DBSCAN (Density-Based Spatial Clustering)

### 🔹 Intuisi:

* DBSCAN membentuk cluster berdasarkan **kepadatan lokal**.
* Tidak perlu menentukan jumlah cluster.
* Mendeteksi **noise/outlier** otomatis.

### 🔧 Parameter:

* `eps`: radius jarak maksimum antar titik
* `min_samples`: minimal jumlah titik dalam `eps` agar dianggap “dense”

```python
from sklearn.cluster import DBSCAN
dbscan = DBSCAN(eps=0.5, min_samples=5)
dbscan.fit(X)
```

Hasil `labels_` akan berisi -1 untuk noise.

---

## 🧪 5. Gaussian Mixture Models (GMM)

### 🔹 Intuisi:

* Anggap data dihasilkan oleh beberapa **distribusi Gaussian**.
* Model mencari distribusi (komponen) terbaik dengan **probabilitas**.

```python
from sklearn.mixture import GaussianMixture
gmm = GaussianMixture(n_components=3)
gmm.fit(X)
labels = gmm.predict(X)
```

GMM bisa menghasilkan **soft labels** (probabilitas tiap kelas), tidak hanya hard labels.

---

## 🧰 6. Evaluasi Clustering

Clustering sulit dievaluasi karena **tidak ada label ground-truth**. Tapi kita bisa gunakan:

| Metode               | Keterangan                           |
| -------------------- | ------------------------------------ |
| Inertia              | (K-Means) jumlah jarak ke centroid   |
| Silhouette Score     | Seberapa baik objek cocok ke cluster |
| Adjusted Rand Index  | Jika ada label referensi             |
| Davies-Bouldin Index | Evaluasi jarak antar cluster         |

---

## 📑 Ringkasan Inti Bab Ini

* **K-Means** cepat dan efisien, tapi butuh jumlah cluster yang ditentukan.
* **DBSCAN** cocok untuk data dengan bentuk tidak beraturan dan banyak noise.
* **GMM** fleksibel karena bisa memberi **probabilitas keanggotaan**.
* Clustering cocok untuk **eksplorasi data**, segmentasi, dan anomaly detection.

---