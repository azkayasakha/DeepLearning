---

# 📘 Chapter 15 – Processing Sequences Using RNNs and CNNs

---

## 🎯 Tujuan Bab Ini:

* Memahami cara kerja dan arsitektur **Recurrent Neural Networks (RNNs)** untuk data sekuensial
* Menggunakan RNN seperti **SimpleRNN, LSTM, GRU** dengan Keras
* Memproses teks atau time series
* Menggunakan CNN untuk sekuens juga (1D Conv)
* Menangani masalah **vanishing gradients** dan **long-term dependencies**

---

## 📚 1. Apa itu Data Sekuensial?

Data yang urutannya penting:

* Teks (kalimat → kata → karakter)
* Time series (suhu per jam, harga saham)
* Sinyal suara
* Genom, musik, dll.

---

## 🔁 2. Recurrent Neural Network (RNN)

### Prinsip:

* Input diterima **berurutan**, bukan sekaligus
* Output tergantung **input saat ini dan state sebelumnya**
* Mirip jaringan feedback

### Sederhana (SimpleRNN):

```python
rnn = keras.layers.SimpleRNN(units=20)
```

---

## 🧱 3. Arsitektur RNN Lain

| Tipe     | Kelebihan                                   |
| -------- | ------------------------------------------- |
| **LSTM** | Menyimpan info jangka panjang, lebih stabil |
| **GRU**  | Ringan, lebih cepat daripada LSTM           |

```python
keras.layers.LSTM(20)
keras.layers.GRU(20)
```

---

## 📏 4. Input untuk RNN

Input harus dalam bentuk **3D tensor**:

```
[batch_size, time_steps, features]
```

Contoh:

```python
X = tf.random.normal([32, 10, 1])  # 32 sample, 10 langkah, 1 fitur per langkah
```

---

## 🔁 5. Sequence to Sequence

Output bisa:

* **1 nilai akhir saja** → `return_sequences=False` (default)
* **Semua langkah** → `return_sequences=True`

```python
keras.layers.SimpleRNN(20, return_sequences=True)
```

---

## 🔄 6. Bidirectional RNN

Membaca sekuens **dari depan dan belakang**:

```python
keras.layers.Bidirectional(keras.layers.LSTM(20))
```

---

## 🧠 7. CNN untuk Sekuens

Alternatif RNN → CNN dengan 1D convolution:

```python
keras.layers.Conv1D(filters=32, kernel_size=3, activation="relu")
```

CNN 1D cocok untuk:

* Time series pendek
* Ekstraksi fitur lokal

---

## 🧪 8. Time Series Forecasting

Contoh prediksi nilai ke depan (misal suhu 1 jam ke depan):

* Input: 20 langkah sebelumnya
* Output: prediksi langkah ke-21

Model:

```python
model = keras.models.Sequential([
    keras.layers.SimpleRNN(20, return_sequences=True, input_shape=[None, 1]),
    keras.layers.SimpleRNN(20),
    keras.layers.Dense(1)
])
```

---

## 🧬 9. Embedding untuk Teks

Jika input berupa teks (kata/karakter):

```python
keras.layers.Embedding(input_dim=vocab_size, output_dim=embedding_dim)
```

---

## 🧑‍🏫 10. Contoh Aplikasi

* Sentiment analysis
* Language modeling
* Speech recognition
* Music generation
* Forecasting (weather, stock, dsb.)

---

## ⚠️ Tantangan RNN

* **Vanishing gradient** → hindari dengan LSTM/GRU
* Lambat → tiap langkah harus berurutan
* CNN dan Transformer sering jadi alternatif lebih cepat

---

## 📑 Ringkasan Inti Bab Ini:

* Gunakan RNN, LSTM, atau GRU untuk data sekuensial
* Gunakan `return_sequences=True` untuk hasil per langkah
* CNN 1D bisa dipakai juga untuk ekstraksi lokal
* Input RNN: `[batch_size, time_steps, features]`
* Bisa digabung dengan `Embedding` layer untuk NLP

---