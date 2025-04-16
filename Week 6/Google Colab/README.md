# Dasar Matematika Model Deteksi Sarkasme

Berikut penjelasan sederhana tentang persamaan matematika penting yang digunakan dalam model deteksi sarkasme.

## 1. Word Embedding (Penyematan Kata)

Word embedding mengubah kata-kata menjadi vektor angka:

$$E(kata) = \vec{v}_{kata}$$

Dimana:
- Setiap kata dipetakan ke vektor berdimensi 128
- Vektor ini menyimpan makna semantik kata

## 2. Model Jaringan Saraf Berulang

### RNN Dasar
Pada waktu t, status tersembunyi dihitung sebagai:

$$h_t = \tanh(W_{xh}x_t + W_{hh}h_{t-1} + b_h)$$

Dimana:
- $x_t$ adalah input pada waktu t
- $h_{t-1}$ adalah status tersembunyi sebelumnya
- $W$ adalah matriks bobot
- $b_h$ adalah bias

### LSTM dan GRU
LSTM dan GRU adalah versi RNN yang lebih canggih dengan mekanisme gerbang khusus untuk mengatasi masalah gradien yang menghilang.

## 3. Klasifikasi Biner

Prediksi akhir:

$$\hat{y} = \sigma(W \cdot h_T + b)$$

Dimana:
- $\sigma$ adalah fungsi sigmoid: $\sigma(z) = \frac{1}{1 + e^{-z}}$
- Hasil mendekati 1 berarti sarkasme, mendekati 0 berarti tidak sarkasme

## 4. Fungsi Kerugian (Loss Function)

Binary Cross-Entropy Loss:

$$L = -[y \log(\hat{y}) + (1-y)\log(1-\hat{y})]$$

Dimana:
- $y$ adalah label sebenarnya (0 atau 1)
- $\hat{y}$ adalah probabilitas prediksi

## 5. Metrik Evaluasi

### Akurasi
$$\text{Akurasi} = \frac{TP + TN}{TP + TN + FP + FN}$$

### Presisi
$$\text{Presisi} = \frac{TP}{TP + FP}$$

### Recall
$$\text{Recall} = \frac{TP}{TP + FN}$$

### F1 Score
$$\text{F1} = 2 \cdot \frac{\text{Presisi} \cdot \text{Recall}}{\text{Presisi} + \text{Recall}}$$

### F1 Kuadrat
$$\text{F1}^2 = \left(\text{F1}\right)^2$$

### AUC
Area di bawah kurva ROC yang mengukur kemampuan model membedakan kelas positif dan negatif.

## 6. Optimisasi Model

### Gradient Descent
Memperbarui bobot untuk meminimalkan kesalahan:

$$w_{baru} = w_{lama} - \eta \cdot \nabla_w L$$

Dimana:
- $\eta$ adalah learning rate
- $\nabla_w L$ adalah gradien loss terhadap bobot

### Adam Optimizer
Versi gradient descent yang lebih canggih dengan:
- Momentum untuk percepatan konvergensi
- Learning rate adaptif untuk setiap parameter

## 7. Hyperparameter Tuning

Proses mencari kombinasi terbaik dari:
- Learning rate
- Ukuran batch
- Jumlah neuron tersembunyi
- Dropout rate
- Jenis model (RNN, LSTM, GRU)
- Dimensi embedding

Dengan Keras Tuner (Tensorflow), kita secara otomatis mencari kombinasi hyperparameter yang menghasilkan performa terbaik pada dataset validasi.