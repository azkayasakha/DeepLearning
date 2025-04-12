# Penjelasan Matematis Model RNN, LSTM, dan GRU

## 1. Simple RNN (Recurrent Neural Network)

RNN standar memodelkan sekuens dengan mempertahankan state hidden yang diperbarui pada setiap langkah waktu. Persamaan dasar RNN adalah:

$$h_t = \sigma(W_{xh} x_t + W_{hh} h_{t-1} + b_h)$$
$$y_t = \sigma(W_{hy} h_t + b_y)$$

Di mana:
- $h_t$ adalah hidden state pada waktu $t$
- $x_t$ adalah input pada waktu $t$
- $y_t$ adalah output pada waktu $t$
- $W_{xh}$ adalah bobot untuk input-ke-hidden
- $W_{hh}$ adalah bobot untuk hidden-ke-hidden (rekurensi)
- $W_{hy}$ adalah bobot untuk hidden-ke-output
- $b_h$ dan $b_y$ adalah bias
- $\sigma$ adalah fungsi aktivasi (biasanya tanh untuk hidden layer dan sigmoid untuk output binary classification)

**Keterbatasan**: RNN standar sulit untuk memodelkan dependensi jangka panjang karena masalah vanishing/exploding gradient.

## 2. LSTM (Long Short-Term Memory)

LSTM mengatasi keterbatasan RNN dengan memperkenalkan mekanisme gating yang memungkinkan untuk menyimpan dan mengakses informasi untuk periode waktu yang panjang. LSTM terdiri dari cell state dan tiga gerbang: forget gate, input gate, dan output gate.

Persamaan LSTM:

1. **Forget Gate** - menentukan informasi mana yang dibuang dari cell state:
   $$f_t = \sigma(W_f \cdot [h_{t-1}, x_t] + b_f)$$

2. **Input Gate** - menentukan nilai baru yang disimpan dalam cell state:
   $$i_t = \sigma(W_i \cdot [h_{t-1}, x_t] + b_i)$$
   $$\tilde{C}_t = \tanh(W_C \cdot [h_{t-1}, x_t] + b_C)$$

3. **Pembaruan Cell State**:
   $$C_t = f_t \odot C_{t-1} + i_t \odot \tilde{C}_t$$

4. **Output Gate** - menentukan bagian cell state mana yang akan menjadi output:
   $$o_t = \sigma(W_o \cdot [h_{t-1}, x_t] + b_o)$$
   $$h_t = o_t \odot \tanh(C_t)$$

Di mana:
- $\odot$ adalah perkalian elemen-wise (Hadamard product)
- $[h_{t-1}, x_t]$ adalah konkatenasi hidden state sebelumnya dan input saat ini
- $C_t$ adalah cell state pada waktu $t$
- $f_t, i_t, o_t$ adalah output dari forget gate, input gate, dan output gate
- $\tilde{C}_t$ adalah kandidat nilai baru untuk cell state

## 3. GRU (Gated Recurrent Unit)

GRU adalah simplifikasi dari LSTM yang menggabungkan forget dan input gate menjadi "update gate" tunggal dan menggabungkan cell state dan hidden state.

Persamaan GRU:

1. **Update Gate** - menentukan seberapa banyak hidden state sebelumnya yang dipertahankan:
   $$z_t = \sigma(W_z \cdot [h_{t-1}, x_t] + b_z)$$

2. **Reset Gate** - menentukan seberapa banyak informasi sebelumnya yang dilupakan:
   $$r_t = \sigma(W_r \cdot [h_{t-1}, x_t] + b_r)$$

3. **Kandidat Hidden State**:
   $$\tilde{h}_t = \tanh(W \cdot [r_t \odot h_{t-1}, x_t] + b)$$

4. **Pembaruan Hidden State Akhir**:
   $$h_t = (1 - z_t) \odot h_{t-1} + z_t \odot \tilde{h}_t$$

Di mana:
- $z_t$ adalah update gate
- $r_t$ adalah reset gate
- $\tilde{h}_t$ adalah kandidat hidden state baru

## Fungsi Aktivasi

Dalam implementasi klasifikasi sentimen, fungsi aktivasi yang digunakan adalah:

1. **Sigmoid** - untuk output layer:
   $$\sigma(x) = \frac{1}{1 + e^{-x}}$$
   Output: [0,1] - Mewakili probabilitas kelas positif

2. **Tanh** - sering digunakan dalam hidden state:
   $$\tanh(x) = \frac{e^x - e^{-x}}{e^x + e^{-x}}$$
   Output: [-1,1]

## Metrik Evaluasi

1. **Accuracy**:
   $$\text{Accuracy} = \frac{\text{TP} + \text{TN}}{\text{TP} + \text{TN} + \text{FP} + \text{FN}}$$

2. **Precision**:
   $$\text{Precision} = \frac{\text{TP}}{\text{TP} + \text{FP}}$$

3. **Recall**:
   $$\text{Recall} = \frac{\text{TP}}{\text{TP} + \text{FN}}$$

4. **F1 Score**:
   $$\text{F1} = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}$$

5. **AUC-ROC**:
   Area di bawah kurva ROC, yang menggambarkan trade-off antara True Positive Rate (TPR) dan False Positive Rate (FPR) pada berbagai threshold.
   $$\text{TPR} = \frac{\text{TP}}{\text{TP} + \text{FN}}$$
   $$\text{FPR} = \frac{\text{FP}}{\text{FP} + \text{TN}}$$

Di mana:
- TP = True Positive
- TN = True Negative
- FP = False Positive
- FN = False Negative