---

# 📘 Chapter 16 – Natural Language Processing with RNNs and Attention

---

## 🎯 Tujuan Bab Ini:

* Memproses teks untuk tugas NLP seperti klasifikasi, penerjemahan, dll.
* Menggunakan **embedding**, **tokenizer**, dan **padding**
* Melatih model RNN (LSTM/GRU) untuk teks
* Memahami konsep **attention mechanism**
* Mempersiapkan dasar untuk **Transformer** (bab 17)

---

## 🧾 1. Tahapan Umum dalam NLP

1. **Tokenisasi**: Ubah teks menjadi kata/karakter
2. **Encoding**: Ubah kata → angka (ID)
3. **Padding**: Seragamkan panjang sekuens
4. **Embedding**: Konversi integer → vektor
5. **Modeling**: RNN/LSTM/GRU/Attention
6. **Output**: Klasifikasi, sequence-to-sequence, dll.

---

## ✂️ 2. Tokenisasi dan Padding

Gunakan `Tokenizer` dari Keras:

```python
from keras.preprocessing.text import Tokenizer
from keras.preprocessing.sequence import pad_sequences

texts = ["I love NLP", "This is great", "Attention is powerful"]

tokenizer = Tokenizer(num_words=1000)
tokenizer.fit_on_texts(texts)

sequences = tokenizer.texts_to_sequences(texts)
padded_seqs = pad_sequences(sequences, padding='post')
```

---

## 🔢 3. Embedding Layer

Mapping integer → vektor real berdimensi tetap:

```python
keras.layers.Embedding(input_dim=1000, output_dim=16, input_length=10)
```

* `input_dim`: ukuran kosakata (jumlah kata unik + 1)
* `output_dim`: ukuran vektor per kata
* `input_length`: panjang sekuens (setelah padding)

---

## 🔁 4. NLP dengan RNN (Text Classification)

### Contoh arsitektur:

```python
model = keras.models.Sequential([
    keras.layers.Embedding(input_dim=10000, output_dim=16, input_length=100),
    keras.layers.LSTM(32),
    keras.layers.Dense(1, activation="sigmoid")  # binary classification
])
```

---

## 📚 5. Dataset IMDB untuk Sentimen

```python
from keras.datasets import imdb

(X_train, y_train), (X_test, y_test) = imdb.load_data(num_words=10000)

X_train = pad_sequences(X_train, maxlen=200)
X_test = pad_sequences(X_test, maxlen=200)
```

---

## 📡 6. Attention Mechanism (Konsep)

### Masalah RNN:

* Sulit menangkap informasi dari kata yang jauh
* Solusi: **attention** memilih bagian input yang "penting"

### Prinsip Attention:

* Setiap langkah output “memperhatikan” seluruh input
* Menimbang input dengan skor relevansi

---

## 🧠 7. Attention dalam Encoder–Decoder

* Encoder: memproses seluruh input
* Decoder: memproduksi output langkah demi langkah
* Attention: membantu decoder memilih konteks input yang penting di setiap langkah

---

## 📎 8. Ringkas Fungsi Attention

```python
attention_scores = tf.matmul(query, key, transpose_b=True)
attention_weights = tf.nn.softmax(attention_scores)
context_vector = tf.matmul(attention_weights, value)
```

---

## 🔍 9. Aplikasi NLP

* **Text classification** (sentimen, spam)
* **Sequence labeling** (NER, POS-tagging)
* **Machine translation**
* **Text summarization**
* **Question answering**

---

## 🧪 10. Kombinasi NLP Model

| Komponen        | Fungsi Utama                        |
| --------------- | ----------------------------------- |
| Embedding       | Konversi ID kata menjadi vektor     |
| RNN/LSTM/GRU    | Menangkap struktur sekuensial       |
| Attention Layer | Fokus ke bagian penting dari input  |
| Dense Layer     | Output (klasifikasi, regresi, dll.) |

---

## 📑 Ringkasan Inti Bab Ini:

* Gunakan **Tokenizer + Padding + Embedding** untuk praproses teks
* Model dasar NLP: **Embedding → LSTM/GRU → Dense**
* Attention membantu fokus ke bagian input yang paling relevan
* **IMDB dataset** jadi contoh untuk klasifikasi teks
* Konsep Attention sangat penting untuk memahami **Transformer**

---