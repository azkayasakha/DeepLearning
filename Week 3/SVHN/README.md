# Penjelasan Persamaan Matematika pada Model CNN dan MLP untuk Dataset SVHN

## 1. Persamaan Matematika pada Model MLP

### a. Forward Propagation pada Fully Connected Layer

Pada model MLP, setiap lapisan terdiri dari neuron yang terhubung dengan bobot tertentu. Persamaan umum untuk perhitungan pada setiap neuron adalah:

\[ z = W \cdot x + b \]

Di mana:
- \( z \) adalah output sebelum aktivasi
- \( W \) adalah matriks bobot
- \( x \) adalah input
- \( b \) adalah bias

Setelah mendapatkan nilai \( z \), diterapkan fungsi aktivasi **ReLU**:

\[ f(z) = \max(0, z) \]

Lapisan terakhir menggunakan fungsi **Softmax** untuk menghasilkan probabilitas kelas:

\[ \text{softmax}(z_i) = \frac{e^{z_i}}{\sum_{j} e^{z_j}} \]

### b. Loss Function: Sparse Categorical Crossentropy

Fungsi loss yang digunakan adalah **Sparse Categorical Crossentropy**, yang dirumuskan sebagai:

\[ L = -\frac{1}{N} \sum_{i=1}^{N} y_i \log(\hat{y}_i) \]

Di mana:
- \( N \) adalah jumlah sampel
- \( y_i \) adalah label asli
- \( \hat{y}_i \) adalah probabilitas prediksi model

### c. Backpropagation dan Optimizer Adam

Gradient descent digunakan untuk memperbarui bobot dengan rumus:

\[ W = W - \eta \frac{\partial L}{\partial W} \]

Di mana \( \eta \) adalah learning rate. Optimizer **Adam** memperbaiki pembaruan bobot dengan momentum dan RMSProp.

---

## 2. Persamaan Matematika pada Model CNN

### a. Convolution Operation

Lapisan konvolusi pada CNN menggunakan filter untuk mengekstrak fitur dari gambar. Operasi konvolusi didefinisikan sebagai:

\[ Z_{i,j,k} = \sum_{m,n} X_{i+m, j+n} \cdot W_{m,n,k} + b_k \]

Di mana:
- \( Z_{i,j,k} \) adalah output setelah konvolusi
- \( X_{i+m, j+n} \) adalah piksel input
- \( W_{m,n,k} \) adalah filter konvolusi
- \( b_k \) adalah bias

### b. Pooling Layer

Pooling layer digunakan untuk mengurangi dimensi. Operasi **Max Pooling**:

\[ P_{i,j} = \max(X_{i+m, j+n}) \]

Di mana \( P_{i,j} \) adalah output setelah pooling.

### c. Fully Connected Layer dan Softmax

Setelah fitur diekstrak, hasilnya dilewatkan ke fully connected layer seperti pada MLP:

\[ z = W \cdot x + b \]

Dan akhirnya, output dikonversi ke probabilitas dengan fungsi **Softmax**.

---

## 3. Evaluasi Model

Model dievaluasi menggunakan metrik berikut:

- **Akurasi**:
  \[ \text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN} \]

- **Presisi**:
  \[ \text{Precision} = \frac{TP}{TP + FP} \]

- **Recall**:
  \[ \text{Recall} = \frac{TP}{TP + FN} \]

- **F1-Score**:
  \[ F1 = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}} \]

---

## Kesimpulan

- MLP menggunakan **lapisan fully connected**, sementara CNN menambahkan **konvolusi** untuk ekstraksi fitur.
- Fungsi aktivasi **ReLU** digunakan untuk meningkatkan non-linearitas.
- **Softmax** digunakan pada layer output untuk klasifikasi multi-kelas.
- Model dioptimalkan menggunakan **Adam optimizer** dengan **Sparse Categorical Crossentropy**.

Model ini memungkinkan klasifikasi angka dari dataset SVHN dengan akurasi tinggi.

