---

# 📘 Chapter 11 – Training Deep Neural Nets

---

## 🎯 Tujuan Bab Ini:

* Mengatasi kesulitan dalam melatih neural network dalam

  * **Inisialisasi bobot**
  * **Optimisasi**
  * **Regularisasi**
  * **Early stopping**
* Meningkatkan performa dan generalisasi model deep learning

---

## ⚠️ 1. Tantangan Melatih Neural Network

### a. **Vanishing & Exploding Gradients**

* Ketika gradien terlalu kecil/besar selama backpropagation
* Sering terjadi pada deep network
* Solusi:

  * Gunakan **ReLU**
  * **Batch Normalization**
  * **Weight Initialization** yang tepat

---

## 🔧 2. Inisialisasi Bobot

* Default di Keras: `glorot_uniform` (bagus untuk sigmoid/tanh)
* Untuk ReLU → gunakan **He initialization**:

```python
keras.layers.Dense(100, activation="relu", kernel_initializer="he_normal")
```

---

## 🚀 3. Optimizer Canggih

| Optimizer | Kelebihan                                    |
| --------- | -------------------------------------------- |
| SGD       | Stabil tapi lambat                           |
| Momentum  | Mempercepat SGD dengan "impuls"              |
| RMSProp   | Baik untuk data noisy                        |
| Adam      | Gabungan RMSProp + Momentum → **terpopuler** |

Contoh:

```python
model.compile(optimizer="adam", loss="sparse_categorical_crossentropy")
```

---

## 🔁 4. Early Stopping

Hentikan training jika tidak ada peningkatan dalam validation loss:

```python
early_stopping_cb = keras.callbacks.EarlyStopping(patience=10, restore_best_weights=True)
```

---

## 💾 5. Simpan Model Otomatis (Checkpoint)

```python
checkpoint_cb = keras.callbacks.ModelCheckpoint("my_model.keras", save_best_only=True)
```

---

## 🔀 6. Learning Rate Scheduling

Kurangi learning rate seiring waktu:

```python
lr_scheduler_cb = keras.callbacks.ReduceLROnPlateau(factor=0.5, patience=5)
```

Atau buat manual:

```python
def schedule(epoch):
    return 0.01 * 0.1**(epoch / 20)

lr_cb = keras.callbacks.LearningRateScheduler(schedule)
```

---

## 💨 7. Batch Normalization

Menstabilkan dan mempercepat training:

```python
model = keras.models.Sequential([
    keras.layers.Flatten(input_shape=[28, 28]),
    keras.layers.BatchNormalization(),
    keras.layers.Dense(100, activation="relu"),
    keras.layers.BatchNormalization(),
    keras.layers.Dense(10, activation="softmax")
])
```

---

## 📤 8. Dropout (Regularisasi)

Mematikan neuron secara acak saat training → mencegah overfitting:

```python
keras.layers.Dropout(rate=0.2)
```

* Aktif **saat training**, nonaktif saat evaluasi

---

## 🧪 9. Kombinasi Callback

Contoh:

```python
model.fit(X_train, y_train,
          validation_data=(X_valid, y_valid),
          epochs=100,
          callbacks=[checkpoint_cb, early_stopping_cb, lr_scheduler_cb])
```

---

## 📑 Ringkasan Inti Bab Ini

* Deep nets bisa sulit dilatih karena **gradien menghilang/eksplod**.
* Gunakan ReLU, He initialization, dan batch normalization.
* Gunakan **optimizer Adam**, dan kurangi learning rate saat perlu.
* **Dropout** dan **early stopping** penting untuk regularisasi.
* Simpan model terbaik secara otomatis dengan **checkpoint**.

---