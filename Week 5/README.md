# Penjelasan Matematika untuk Model RNN, LSTM, dan GRU

Berikut adalah penjelasan matematika yang digunakan dalam tiga arsitektur model deep learning untuk analisis sentimen review toko baju:

## 1. RNN (Recurrent Neural Network)

RNN adalah jaringan neural yang memiliki loop internal, memungkinkan informasi bertahan dalam "memori" jaringan.

### Persamaan Dasar RNN:
- **Hidden state**: $h_t = \tanh(W_{xh} x_t + W_{hh} h_{t-1} + b_h)$
- **Output**: $y_t = W_{hy} h_t + b_y$

Dimana:
- $h_t$ adalah hidden state pada waktu t
- $x_t$ adalah input pada waktu t
- $W_{xh}$, $W_{hh}$, $W_{hy}$ adalah matriks bobot
- $b_h$, $b_y$ adalah vektor bias
- $\tanh$ adalah fungsi aktivasi

RNN bidirectional dalam kode menggunakan dua arah pemrosesan:
- Forward direction: $\overrightarrow{h_t} = \tanh(W_{x\overrightarrow{h}} x_t + W_{\overrightarrow{h}\overrightarrow{h}} \overrightarrow{h_{t-1}} + b_{\overrightarrow{h}})$
- Backward direction: $\overleftarrow{h_t} = \tanh(W_{x\overleftarrow{h}} x_t + W_{\overleftarrow{h}\overleftarrow{h}} \overleftarrow{h_{t+1}} + b_{\overleftarrow{h}})$

## 2. LSTM (Long Short-Term Memory)

LSTM mengatasi masalah vanishing gradient pada RNN standar dengan menambahkan mekanisme gerbang kontrol.

### Persamaan LSTM:
- **Forget gate**: $f_t = \sigma(W_f \cdot [h_{t-1}, x_t] + b_f)$
- **Input gate**: $i_t = \sigma(W_i \cdot [h_{t-1}, x_t] + b_i)$
- **Candidate cell state**: $\tilde{C}_t = \tanh(W_C \cdot [h_{t-1}, x_t] + b_C)$
- **Cell state update**: $C_t = f_t \odot C_{t-1} + i_t \odot \tilde{C}_t$
- **Output gate**: $o_t = \sigma(W_o \cdot [h_{t-1}, x_t] + b_o)$
- **Hidden state**: $h_t = o_t \odot \tanh(C_t)$

Dimana:
- $\sigma$ adalah fungsi sigmoid
- $\odot$ adalah perkalian elemen demi elemen (Hadamard product)
- $[h_{t-1}, x_t]$ adalah konkatenasi vektor

## 3. GRU (Gated Recurrent Unit)

GRU adalah simplifikasi dari LSTM yang menggabungkan forget gate dan input gate menjadi satu "update gate".

### Persamaan GRU:
- **Update gate**: $z_t = \sigma(W_z \cdot [h_{t-1}, x_t] + b_z)$
- **Reset gate**: $r_t = \sigma(W_r \cdot [h_{t-1}, x_t] + b_r)$
- **Candidate hidden state**: $\tilde{h}_t = \tanh(W \cdot [r_t \odot h_{t-1}, x_t] + b)$
- **Hidden state update**: $h_t = (1 - z_t) \odot h_{t-1} + z_t \odot \tilde{h}_t$

## Binary Cross-Entropy Loss

Untuk klasifikasi biner review (positif atau negatif), model menggunakan Binary Cross-Entropy Loss:

$$\mathcal{L} = -\frac{1}{N} \sum_{i=1}^{N} [y_i \log(\hat{y}_i) + (1 - y_i) \log(1 - \hat{y}_i)]$$

Dimana:
- $N$ adalah jumlah sampel
- $y_i$ adalah label sebenarnya (0 atau 1)
- $\hat{y}_i$ adalah probabilitas yang diprediksi

## Metrik Evaluasi

### Accuracy
$$\text{Accuracy} = \frac{\text{TP} + \text{TN}}{\text{TP} + \text{TN} + \text{FP} + \text{FN}}$$

### Precision
$$\text{Precision} = \frac{\text{TP}}{\text{TP} + \text{FP}}$$

### Recall
$$\text{Recall} = \frac{\text{TP}}{\text{TP} + \text{FN}}$$

### F1 Squared
$$\text{F1 Squared} = \left(\frac{2 \times \text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}\right)^2$$

### AUC-ROC
Area Under the Receiver Operating Characteristic Curve dihitung dari plot TPR (True Positive Rate) vs FPR (False Positive Rate) pada berbagai threshold.

Dimana:
- TP = True Positive
- TN = True Negative
- FP = False Positive
- FN = False Negative