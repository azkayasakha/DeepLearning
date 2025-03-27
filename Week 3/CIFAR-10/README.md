# Persamaan Matematika pada Model CNN dan MLP

## 1. Multilayer Perceptron (MLP)
MLP terdiri dari beberapa lapisan fully connected yang memproses input menjadi output dengan menerapkan transformasi linear dan fungsi aktivasi.

### a. Lapisan Fully Connected
Setiap neuron dalam lapisan fully connected memiliki bobot dan bias:

$$
    z = W x + b
$$

- \( W \) adalah matriks bobot
- \( x \) adalah input
- \( b \) adalah bias
- \( z \) adalah output sebelum aktivasi

### b. Aktivasi ReLU
Fungsi aktivasi ReLU digunakan untuk memperkenalkan non-linearitas:

$$
    f(z) = \max(0, z)
$$

### c. Aktivasi Softmax
Pada lapisan output, digunakan softmax untuk mengubah skor menjadi probabilitas:

$$
    \text{softmax}(z_i) = \frac{e^{z_i}}{\sum e^{z_j}}
$$

- \( z_i \) adalah skor dari kelas \( i \)
- \( \sum e^{z_j} \) adalah normalisasi terhadap semua kelas

## 2. Convolutional Neural Network (CNN)
CNN terdiri dari beberapa lapisan konvolusi dan pooling yang mengekstrak fitur dari gambar.

### a. Operasi Konvolusi
Lapisan konvolusi menggunakan filter (kernel) untuk mengekstrak fitur spasial:

$$
    Y(i, j) = \sum_{m} \sum_{n} X(i+m, j+n) \cdot K(m, n) + b
$$

- \( X \) adalah input gambar
- \( K \) adalah kernel (filter)
- \( b \) adalah bias
- \( Y(i, j) \) adalah hasil konvolusi pada koordinat \( (i, j) \)

### b. Operasi Pooling
Pooling mengurangi dimensi fitur dengan memilih nilai maksimum atau rata-rata dalam suatu jendela:
- **Max Pooling**:

$$
    Y(i, j) = \max (X_{i:i+k, j:j+k})
$$

- **Average Pooling**:

$$
    Y(i, j) = \frac{1}{k^2} \sum X_{i:i+k, j:j+k}
$$

### c. Lapisan Fully Connected dan Softmax
Setelah ekstraksi fitur, output dari CNN diproses dengan fully connected layer dan softmax, seperti pada MLP.

## 3. Loss Function
Kedua model menggunakan fungsi loss Cross-Entropy untuk klasifikasi:

$$
    L = - \sum y \log(\hat{y})
$$

- \( y \) adalah label sebenarnya
- \( \hat{y} \) adalah output prediksi dari model

## 4. Evaluasi Model
Model dievaluasi menggunakan metrik seperti:
- **Akurasi:** 

$$
    \frac{TP + TN}{TP + TN + FP + FN}
$$

- **Presisi:** 

$$
    \frac{TP}{TP + FP}
$$

- **Recall:** 

$$
    \frac{TP}{TP + FN}
$$

- **F1 Score:** 

$$
    2 \times \frac{\text{Presisi} \times \text{Recall}}{\text{Presisi} + \text{Recall}}
$$

- **AUC-ROC:** Mengukur kemampuan model dalam membedakan kelas positif dan negatif.