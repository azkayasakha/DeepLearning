---

# 📘 Chapter 13 – Loading and Preprocessing Data with TensorFlow

---

## 🎯 Tujuan Bab Ini:

* Menggunakan API `tf.data` untuk membuat pipeline input yang efisien dan scalable
* Melakukan preprocessing data (normalize, augment, shuffle, cache, dsb.)
* Memahami alur data: **load → transform → batch → prefetch**

---

## 🔢 1. Dataset TensorFlow

Gunakan `tf.data.Dataset` untuk:

* **Efisiensi memori**: streaming data dari disk
* **Pipeline training**: cocok untuk dataset besar
* Mendukung transformasi data yang fleksibel dan paralel

---

## 📥 2. Membuat Dataset

### Dari numpy array:

```python
import tensorflow as tf

dataset = tf.data.Dataset.from_tensor_slices((X_train, y_train))
```

### Dari TFRecord (file binary TensorFlow):

Digunakan untuk skala besar, dibahas lanjut di bab 14.

---

## 🔄 3. Transformasi Dataset

| Operasi           | Fungsi                                             |
| ----------------- | -------------------------------------------------- |
| `shuffle(buffer)` | Acak elemen dengan buffer size tertentu            |
| `repeat(count)`   | Ulangi dataset `count` kali                        |
| `batch(size)`     | Bagi data menjadi batch                            |
| `map(fn)`         | Ubah/augment data dengan fungsi                    |
| `prefetch(n)`     | Ambil batch berikutnya sambil model masih training |
| `cache()`         | Simpan data di RAM untuk akses cepat (jika cukup)  |

---

## 🛠️ 4. Contoh Pipeline Lengkap

```python
def preprocess(X, y):
    X = tf.cast(X, tf.float32) / 255.0
    return X, y

train_dataset = tf.data.Dataset.from_tensor_slices((X_train, y_train))
train_dataset = (
    train_dataset
    .shuffle(10000)
    .map(preprocess)
    .batch(32)
    .prefetch(tf.data.AUTOTUNE)
)
```

* `.shuffle(10000)`: mengacak data
* `.map(preprocess)`: preprocessing (misalnya normalisasi)
* `.batch(32)`: kelompokkan data per 32
* `.prefetch()`: optimalkan pipeline agar GPU tidak idle

---

## 🖼️ 5. Data Augmentation

Data augmentation menambah variasi data untuk mencegah overfitting.

Contoh augmentasi:

```python
def augment(X, y):
    X = tf.image.random_flip_left_right(X)
    X = tf.image.random_brightness(X, max_delta=0.1)
    return X, y
```

Gabungkan dengan preprocessing:

```python
train_dataset = train_dataset.map(augment)
```

---

## 📦 6. Dataset Pipeline Validasi dan Tes

Untuk validasi dan tes, **jangan shuffle atau augment**, hanya normalisasi dan batch:

```python
valid_dataset = tf.data.Dataset.from_tensor_slices((X_valid, y_valid))
valid_dataset = (
    valid_dataset
    .map(preprocess)
    .batch(32)
    .prefetch(tf.data.AUTOTUNE)
)
```

---

## 🧠 7. Tips Optimasi `tf.data`

* Gunakan `.cache()` untuk dataset kecil
* Gunakan `.prefetch(tf.data.AUTOTUNE)` untuk performa maksimal
* Gunakan `.interleave()` saat membaca banyak file paralel
* Gunakan `.num_parallel_calls=tf.data.AUTOTUNE` pada `.map()` untuk percepat transformasi

---

## 📑 Ringkasan Inti Bab Ini:

* `tf.data` memudahkan loading, preprocessing, dan batching data secara efisien.
* Proses umum: **shuffle → map → batch → prefetch**
* **Data augmentation** penting untuk generalisasi, terutama pada gambar.
* **`AUTOTUNE`** memaksimalkan performa pipeline dengan paralelisme otomatis.
* Pipeline ini sangat efisien bahkan untuk data berukuran besar.

---