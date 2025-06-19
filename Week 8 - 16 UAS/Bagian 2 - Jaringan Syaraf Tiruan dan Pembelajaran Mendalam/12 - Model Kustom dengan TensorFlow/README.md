---

# 📘 Chapter 12 – Custom Models and Training with TensorFlow

---

## 🎯 Tujuan Bab Ini:

* Belajar membangun **model neural network secara fleksibel** dengan *Functional API* dan *Subclassing API*
* Membuat **loss function, metrics, dan training loop kustom**
* Memahami **GradientTape** untuk training manual

---

## 🧩 1. Functional API

> Digunakan saat model tidak hanya “linear” berurutan (sequential), misalnya: model dengan input/output bercabang, skip connection (residual), dsb.

### Contoh:

```python
from keras import layers, models, Input

input_ = Input(shape=(28, 28))
flatten = layers.Flatten()(input_)
hidden1 = layers.Dense(128, activation="relu")(flatten)
hidden2 = layers.Dense(64, activation="relu")(hidden1)
output = layers.Dense(10, activation="softmax")(hidden2)

model = models.Model(inputs=input_, outputs=output)
```

---

## 🏗️ 2. Subclassing API (OOP)

Subclass dari `keras.Model` dan buat arsitektur serta forward pass secara eksplisit melalui method `call()`.

### Contoh:

```python
from keras import Model, layers

class MyModel(Model):
    def __init__(self):
        super().__init__()
        self.flatten = layers.Flatten()
        self.dense1 = layers.Dense(128, activation="relu")
        self.dense2 = layers.Dense(10, activation="softmax")

    def call(self, inputs):
        x = self.flatten(inputs)
        x = self.dense1(x)
        return self.dense2(x)

model = MyModel()
```

---

## 🎯 3. Custom Loss Function

Contoh loss kustom (dengan penalti tambahan):

```python
from keras import backend as K

def my_custom_loss(y_true, y_pred):
    return K.mean(K.square(y_pred - y_true)) + 0.01 * K.sum(K.abs(y_pred))
```

---

## 📊 4. Custom Metrics

Contoh akurasi kustom:

```python
from keras.metrics import Metric

class BinaryTruePositives(Metric):
    def __init__(self, name="true_positives", **kwargs):
        super().__init__(name=name, **kwargs)
        self.true_positives = self.add_weight(name="tp", initializer="zeros")

    def update_state(self, y_true, y_pred, sample_weight=None):
        values = K.round(K.clip(y_true * y_pred, 0, 1))
        self.true_positives.assign_add(K.sum(values))

    def result(self):
        return self.true_positives

    def reset_states(self):
        self.true_positives.assign(0)
```

---

## 📉 5. Custom Training Loop (Manual)

Gunakan **`tf.GradientTape`** untuk mengontrol proses training.

### Contoh Sederhana:

```python
import tensorflow as tf

loss_fn = tf.keras.losses.SparseCategoricalCrossentropy()
optimizer = tf.keras.optimizers.Adam()

for epoch in range(5):
    for x_batch, y_batch in dataset:
        with tf.GradientTape() as tape:
            y_pred = model(x_batch, training=True)
            loss = loss_fn(y_batch, y_pred)
        gradients = tape.gradient(loss, model.trainable_variables)
        optimizer.apply_gradients(zip(gradients, model.trainable_variables))
```

---

## 🔄 6. Training Loop vs Model.fit()

| `model.fit()`               | `GradientTape`                        |
| --------------------------- | ------------------------------------- |
| Mudah & otomatis            | Penuh kontrol, cocok untuk eksperimen |
| Tidak fleksibel untuk riset | Cocok untuk RL, GAN, dan multitask    |

---

## ✅ 7. Kapan Gunakan?

* Gunakan **Sequential API** untuk model berlapis sederhana
* Gunakan **Functional API** untuk model bercabang, berulang, atau multiple input/output
* Gunakan **Subclassing API + GradientTape** untuk:

  * GAN
  * Autoencoder
  * Reinforcement Learning
  * Model riset yang sangat kustom

---

## 📑 Ringkasan Inti Bab Ini:

* TensorFlow mendukung 3 cara membangun model: `Sequential`, `Functional`, dan `Subclassing`.
* Untuk fleksibilitas maksimal, gunakan `Model` subclass + `GradientTape`.
* Cocok untuk riset, GAN, atau situasi yang butuh kontrol penuh.
* Bisa buat **loss**, **metrics**, dan **training** kustom sendiri.

---