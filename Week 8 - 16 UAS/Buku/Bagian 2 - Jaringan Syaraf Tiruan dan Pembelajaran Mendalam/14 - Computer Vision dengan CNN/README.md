---

# 📘 Chapter 14 – Deep Computer Vision Using Convolutional Neural Networks (CNNs)

---

## 🎯 Tujuan Bab Ini:

* Memahami arsitektur CNN dan kenapa mereka bagus untuk gambar
* Membangun CNN dengan Keras
* Menggunakan CNN untuk klasifikasi gambar (contoh: Fashion MNIST, CIFAR)
* Mengenal komponen CNN: **conv layer, pooling layer, padding, strides**
* Latih CNN modern: `Conv2D`, `MaxPooling2D`, `Dropout`, dll.

---

## 🧠 1. Mengapa CNN Efektif untuk Gambar?

### Masalah Dense Network:

* Layer dense butuh terlalu banyak parameter jika inputnya gambar (misal: 28×28 = 784 → ribuan weight)
* Tidak mempertahankan **struktur spasial** (misalnya piksel sebelah jadi tidak dianggap "berdekatan")

### Solusi: Convolution

* Hanya koneksi lokal (receptive field kecil)
* Parameter shared (**weight sharing**): satu filter (kernel) diterapkan ke seluruh gambar
* Efisien dan tetap mempertahankan informasi spasial

---

## 📐 2. Komponen Utama CNN

| Komponen         | Fungsi                                                            |
| ---------------- | ----------------------------------------------------------------- |
| **Conv2D**       | Menyaring fitur spasial dari input dengan kernel (filter)         |
| **ReLU**         | Fungsi aktivasi untuk menambahkan non-linearitas                  |
| **MaxPooling2D** | Mengurangi dimensi (spasial) sambil mempertahankan fitur penting  |
| **Dropout**      | Regularisasi, mencegah overfitting dengan "mematikan" neuron acak |
| **Flatten**      | Mengubah matriks fitur ke vektor untuk fully-connected layer      |
| **Dense**        | Layer akhir untuk klasifikasi (biasanya softmax)                  |

---

## 🏗️ 3. Arsitektur CNN Sederhana

```text
Input (28x28x1)
↓
Conv2D (32 filters 3x3) + ReLU
↓
MaxPooling2D (2x2)
↓
Conv2D (64 filters 3x3) + ReLU
↓
MaxPooling2D (2x2)
↓
Flatten
↓
Dense (128) + ReLU
↓
Dense (10) + Softmax
```

---

## 🧪 4. Dataset Fashion MNIST atau CIFAR-10

* **Fashion MNIST**: pakaian (grayscale, 28×28)
* **CIFAR-10**: objek (RGB, 32×32, 3 channel)

---

## 🧬 5. Padding dan Stride

| Parameter        | Fungsi                                                        |
| ---------------- | ------------------------------------------------------------- |
| `padding="same"` | Output tetap berukuran sama seperti input                     |
| `strides=2`      | Melompati piksel → mempercepat, mengurangi resolusi (spasial) |

---

## 🧮 6. Arsitektur Klasik CNN

* **LeNet-5**: CNN awal untuk digit MNIST
* **AlexNet**: revolusi CNN modern di 2012
* **VGG**, **ResNet**, **Inception**: arsitektur dalam dunia nyata (bab selanjutnya)

---

## 🧠 7. Transfer Learning (dibahas lebih lanjut di bab 15)

---

## 🧪 8. Tips Praktis CNN

* Gunakan batch normalization di antara conv layer
* Gunakan `Dropout()` untuk regularisasi
* Latih dengan `Adam` atau `RMSprop`
* CNN cocok untuk data grid-like (gambar, video, suara 1D)

---

## 📑 Ringkasan Inti Bab Ini:

* CNN lebih efisien dan efektif untuk pengolahan gambar daripada fully-connected network
* Komponen penting: Conv → ReLU → Pool → Flatten → Dense
* CNN menangkap fitur spasial lokal dan hierarkis
* Padding, strides, dan pooling mempengaruhi output spasial
* CNN bisa dibangun bertingkat, lalu dilatih untuk klasifikasi

---