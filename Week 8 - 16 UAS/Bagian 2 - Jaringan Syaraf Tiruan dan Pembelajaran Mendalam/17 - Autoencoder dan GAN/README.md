---

# 📘 Chapter 17 – Representation Learning and Generative Learning Using Autoencoders and GANs

---

## 🎯 Tujuan Bab Ini:

* Memahami **autoencoder**: model untuk kompresi & rekonstruksi data
* Latih model untuk belajar **representasi tersembunyi**
* Memahami **generative learning**: model belajar menghasilkan data baru
* Latih dan gunakan **Variational Autoencoders (VAE)** dan **Generative Adversarial Networks (GANs)**

---

## 🧠 1. Apa itu Representation Learning?

Model **belajar fitur sendiri** dari data tanpa label eksplisit.

Contoh:

* Autoencoder mempelajari representasi ringkas dari input
* GAN belajar membuat data baru yang mirip distribusi aslinya

---

## 🛠️ 2. Autoencoder: Encoder + Decoder

### Arsitektur Umum:

```
Input → Encoder → Latent Vector → Decoder → Output ≈ Input
```

* **Encoder**: Kompres input jadi representasi (latent space)
* **Decoder**: Rekonstruksi input dari latent space

### Jenis:

| Jenis Autoencoder | Fungsi Khusus                     |
| ----------------- | --------------------------------- |
| Undercomplete     | Dimensi kecil → kompresi          |
| Denoising         | Input rusak → belajar bersihkan   |
| Sparse            | Latent harus sparing (banyak nol) |
| Variational (VAE) | Probabilistik → generatif         |

---

## ⚙️ 3. Loss Function Autoencoder

Biasanya:

* **MSE** antara input dan output

```python
loss = keras.losses.mean_squared_error(inputs, outputs)
```

---

## 🔄 4. Denoising Autoencoder

* Tambahkan noise ke input → target tetap input asli
* Membantu model belajar representasi **robust**

---

## 🌀 5. Variational Autoencoder (VAE)

Berbeda dari autoencoder biasa:

* Alih-alih titik, encoder hasilkan **distribusi (mean dan var)**
* Sampling dari distribusi → generatif!

### Arsitektur:

```
Input → Encoder → (μ, σ) → Sampling → Decoder → Output
```

### Loss VAE = Rekonstruksi + Regularisasi (KL Divergence)

```text
Loss = MSE + KL(N(μ,σ²) || N(0,1))
```

---

## 🤖 6. Generative Adversarial Network (GAN)

Dua model saling melawan:

* **Generator**: membuat data palsu
* **Discriminator**: membedakan data nyata vs palsu

### Arsitektur GAN:

```
Noise → Generator → Fake data
Real/Fake data → Discriminator → Real or Fake
```

### Latih dengan cara:

* Generator ingin mengecoh discriminator
* Discriminator ingin menangkap fake

---

## 🧪 7. Loss GAN

* Discriminator:

  ```text
  Loss = -log(D(real)) - log(1 - D(fake))
  ```
* Generator:

  ```text
  Loss = -log(D(fake))
  ```

---

## 🎨 8. Aplikasi Autoencoder & GAN

| Model       | Aplikasi                                |
| ----------- | --------------------------------------- |
| Autoencoder | Kompresi, denoising, anomaly detection  |
| VAE         | Image generation, latent space sampling |
| GAN         | Image synthesis, data augmentation      |

---

## 📑 Ringkasan Inti Bab Ini:

* Autoencoder belajar representasi dari input tanpa supervisi
* VAE menambahkan probabilistik dan regularisasi → generatif
* GAN gunakan dua model bertanding untuk menghasilkan data mirip aslinya
* VAE dan GAN bisa digunakan untuk visualisasi, deteksi anomali, dan generasi data

---