---

# 📘 Chapter 10 – Introduction to Artificial Neural Networks with Keras

---

## 🎯 Tujuan Bab Ini:

* Memahami dasar **Artificial Neural Network (ANN)**
* Mengenal **Keras API** untuk membangun dan melatih ANN
* Membangun model deep learning pertama untuk klasifikasi gambar (Fashion MNIST)

---

## 🧠 1. Intuisi Artificial Neural Networks

* ANN terdiri dari **lapisan neuron (nodes)** yang terhubung ke lapisan sebelumnya.

* Setiap neuron melakukan:

  $$
  z = w_1x_1 + w_2x_2 + \dots + b \quad \text{(linear combination)}
  $$

  $$
  y = \phi(z) \quad \text{(non-linear activation)}
  $$

* Kombinasi banyak neuron dan lapisan menciptakan **representasi kompleks dari data**.

---

## 🧱 2. Struktur ANN

### 3 komponen utama:

1. **Input layer**
2. **Hidden layers**
3. **Output layer**

---

## ⚙️ 3. Activation Functions

* **ReLU (Rectified Linear Unit)**: umum di hidden layer
* **Sigmoid**: cocok untuk output biner
* **Softmax**: cocok untuk klasifikasi multi-kelas

---

## 🤖 4. Membangun Model dengan Keras

Keras menggunakan **Sequential API** untuk membuat model secara berurutan:

```python
from tensorflow import keras
from keras import layers

model = keras.models.Sequential([
    layers.Dense(300, activation="relu", input_shape=[784]),
    layers.Dense(100, activation="relu"),
    layers.Dense(10, activation="softmax")
])
```

---

## 🔧 5. Kompilasi Model

```python
model.compile(
    loss="sparse_categorical_crossentropy",  # untuk label integer
    optimizer="sgd",                         # Stochastic Gradient Descent
    metrics=["accuracy"]
)
```

---

## 🧪 6. Melatih Model

```python
history = model.fit(X_train, y_train, epochs=30,
                    validation_data=(X_valid, y_valid))
```

---

## 📈 7. Evaluasi dan Prediksi

```python
model.evaluate(X_test, y_test)  # Menghitung akurasi & loss
y_pred = model.predict(X_test)  # Prediksi probabilitas
```

---

## 👚 8. Studi Kasus: Fashion MNIST

Dataset yang digunakan:

* 70.000 gambar pakaian 28x28 piksel (60k train, 10k test)
* Setiap gambar diklasifikasikan ke salah satu dari 10 kategori (sepatu, baju, dll)

```python
from keras.datasets import fashion_mnist
(X_train_full, y_train_full), (X_test, y_test) = fashion_mnist.load_data()
```

* Lakukan normalisasi:

```python
X_train_full = X_train_full / 255.0
X_test = X_test / 255.0
```

* Bagi data validasi:

```python
X_valid, X_train = X_train_full[:5000], X_train_full[5000:]
y_valid, y_train = y_train_full[:5000], y_train_full[5000:]
```

---

## 🎨 9. Visualisasi Learning Curve

Setelah training:

```python
import pandas as pd
import matplotlib.pyplot as plt

pd.DataFrame(history.history).plot(figsize=(8, 5))
plt.grid(True)
plt.xlabel("Epochs")
plt.ylabel("Loss / Accuracy")
plt.show()
```

---

## 📑 Ringkasan Inti Bab Ini:

* ANN terdiri dari neuron yang menghitung output berdasarkan input dan bobot.
* Keras (`Sequential API`) membuat pembuatan model sangat mudah.
* Dataset Fashion MNIST digunakan sebagai latihan membangun model klasifikasi gambar.
* Aktivasi ReLU dan Softmax digunakan di hidden dan output layer.
* Proses utama: **build → compile → fit → evaluate → predict**

---