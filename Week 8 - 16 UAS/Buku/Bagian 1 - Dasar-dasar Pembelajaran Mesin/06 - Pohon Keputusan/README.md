---

# 📘 Chapter 6 – Decision Trees

---

## 🎯 Tujuan Bab Ini:

* Memahami cara kerja **Decision Tree** untuk klasifikasi dan regresi.
* Mengenal istilah seperti **impurity**, **information gain**, dan **overfitting**.
* Menggunakan `DecisionTreeClassifier` dan `DecisionTreeRegressor` dari Scikit-Learn.

---

## 🌳 1. Apa itu Decision Tree?

**Decision Tree** adalah struktur pohon yang membuat keputusan berdasarkan **pembelahan fitur (splits)**.

Contoh:

```
Jika "umur < 30": 
    Jika "penghasilan < 50K": ... → Kelas A
    Jika "penghasilan >= 50K": ... → Kelas B
Jika "umur >= 30":
    ... dst
```

Setiap node **membelah data** menjadi subset berdasarkan kondisi logis.

---

## 🧠 2. Cara Tree Belajar

Decision Tree dilatih dengan **algoritma rekursif** yang memilih fitur dan threshold terbaik untuk membelah data.

🔍 **Tujuannya**: meminimalkan impurity (ketidakhomogenan label dalam satu node).

### Fungsi impurity:

* **Gini Impurity** (default Scikit-Learn)

$$
G_i = 1 - \sum_{k=1}^{n} p_k^2
$$

* **Entropy** (berbasis informasi)

$$
H = - \sum_{k=1}^{n} p_k \log_2(p_k)
$$

---

## 🔧 3. Hyperparameter Penting

| Parameter           | Fungsi                                                                  |
| ------------------- | ----------------------------------------------------------------------- |
| `max_depth`         | Maksimum kedalaman tree                                                 |
| `min_samples_split` | Minimum jumlah sampel untuk membelah node                               |
| `min_samples_leaf`  | Minimum sampel di setiap daun                                           |
| `max_leaf_nodes`    | Batas jumlah daun maksimal                                              |
| `max_features`      | Jumlah fitur acak yang dipilih saat membelah (berguna di Random Forest) |

📌 Pengaturan ini penting untuk **mengontrol overfitting**.

---

## 🔄 4. Decision Tree untuk Regresi

* Tree membelah data agar prediksi dalam tiap leaf **mendekati nilai rata-rata** target.
* Tidak menggunakan Gini/Entropy, tapi menggunakan **Mean Squared Error (MSE)** atau kriteria serupa.

---

## 🧱 5. Keuntungan & Kelemahan Decision Tree

### ✅ Kelebihan:

* Mudah dimengerti dan divisualisasikan
* Tidak butuh scaling
* Bisa menangani data kategorik dan numerik

### ❌ Kekurangan:

* Sangat rentan **overfitting**
* Sensitif terhadap data kecil & perubahan minor
* Kurang kuat untuk generalisasi dibanding ensemble methods

---

## 🧰 6. Visualisasi dan Interpretasi Tree

* Scikit-Learn menyediakan fungsi seperti `plot_tree()` dan `export_text()` untuk melihat struktur pohon.
* Setiap node bisa diartikan sebagai **aturan logis**.

---

## 🧪 7. Decision Trees di Ensemble Learning

Tree bisa digabung (bagian dari **Random Forest**, **Gradient Boosted Trees**, dll) untuk meningkatkan akurasi dan ketahanan terhadap overfitting.

→ Ini akan dibahas lebih dalam di **Bab 7 dan 8**.

---

## 📑 Ringkasan Inti Bab Ini:

* Decision Tree belajar dari data dengan membuat **pembelahan rekursif** berdasarkan impurity.
* Bisa digunakan untuk klasifikasi dan regresi.
* Sangat fleksibel, tetapi mudah **overfit** tanpa regularisasi.
* Visualisasi tree dapat membantu memahami model secara transparan.

---