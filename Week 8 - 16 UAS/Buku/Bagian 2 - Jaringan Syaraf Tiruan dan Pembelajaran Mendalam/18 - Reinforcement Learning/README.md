---

# 📘 Chapter 18 – Reinforcement Learning

---

## 🎯 Tujuan Bab Ini:

* Memahami konsep dasar **Reinforcement Learning (RL)**
* Membedakan antara RL vs Supervised Learning
* Implementasi **Q-learning** dan **Deep Q-Network (DQN)**
* Menggunakan **OpenAI Gym** sebagai environment interaktif
* Membuat agen belajar melalui eksplorasi dan imbalan

---

## 🔁 1. Apa itu Reinforcement Learning?

> **RL** adalah pendekatan pembelajaran di mana **agen** belajar mengambil keputusan dengan **berinteraksi dengan lingkungan** untuk **memaksimalkan reward jangka panjang**.

---

## 🧩 2. Komponen dalam RL

| Komponen        | Deskripsi                                     |
| --------------- | --------------------------------------------- |
| **Agent**       | Entitas yang belajar dan bertindak            |
| **Environment** | Dunia tempat agent berinteraksi               |
| **State (s)**   | Situasi saat ini dalam environment            |
| **Action (a)**  | Tindakan yang diambil oleh agent              |
| **Reward (r)**  | Angka yang menunjukkan nilai tindakan         |
| **Policy (π)**  | Strategi pemilihan aksi berdasarkan state     |
| **Episode**     | Satu siklus percobaan (dari awal ke terminal) |

---

## 🧠 3. Goal RL

Agen belajar **policy optimal** untuk **memaksimalkan expected cumulative reward** (sering disebut sebagai **return** atau `G_t`).

---

## 📈 4. Value Function dan Q-Function

* **Value function (V)**: ekspektasi reward dari state tertentu
* **Q-function (Q)**: ekspektasi reward dari state + action tertentu

---

## 🎲 5. Eksplorasi vs Eksploitasi

* **Eksploitasi**: pilih aksi terbaik yang diketahui
* **Eksplorasi**: coba aksi baru untuk belajar
* Strategi umum: **ε-greedy** (kadang eksplorasi, kadang eksploitasi)

---

## 🧠 6. Q-Learning (Tabular)

> Algoritma RL klasik untuk **mengisi tabel Q(s, a)**:

### Update Rule:

```
Q(s,a) ← Q(s,a) + α [r + γ * max_a’ Q(s’,a’) - Q(s,a)]
```

* α = learning rate
* γ = discount factor
* s’ = state berikutnya

---

## 🧪 7. Contoh: FrozenLake-v0 (OpenAI Gym)

Environment sederhana: Agen bergerak di grid menuju tujuan sambil menghindari lubang es.

```python
import gym
env = gym.make("FrozenLake-v1", is_slippery=False)
obs = env.reset()
```

---

## 🤖 8. Deep Q-Network (DQN)

Ketika **jumlah state/action terlalu besar**, kita tidak bisa pakai tabel → pakai neural network!

```python
Q(s, a) ≈ f(s, a; θ)
```

### Komponen DQN:

* Neural network Q(s, a)
* Replay buffer: menyimpan pengalaman
* Target network: salinan stabil untuk perhitungan Q-target

---

## 🔁 9. Training Loop DQN (Inti)

1. Dapatkan state `s`
2. Pilih aksi `a` dengan ε-greedy
3. Lakukan aksi → dapat `r`, `s'`
4. Simpan (s, a, r, s’) ke replay buffer
5. Sampling minibatch
6. Hitung Q-target: `r + γ max Q(s’, a’)`
7. Update Q-network

---

## 🧠 10. Perbedaan RL dengan Supervised Learning

| Aspek    | Supervised Learning | Reinforcement Learning  |
| -------- | ------------------- | ----------------------- |
| Label    | Ada                 | Tidak langsung (reward) |
| Tujuan   | Prediksi akurat     | Maksimalkan reward      |
| Training | Sekali (static)     | Interaktif              |
| Data     | Diberikan           | Dihasilkan sendiri      |

---

## 🧠 Bonus: Policy Gradient & Actor–Critic

* **Policy gradient** langsung melatih `π(a|s)`
* **Actor–Critic**: dua model → actor (policy), critic (value function)

---

## 📑 Ringkasan Inti Bab Ini:

* RL = belajar dari interaksi dan reward
* Agen belajar **policy** untuk mencapai tujuan jangka panjang
* Q-Learning mengisi tabel Q(s,a)
* DQN menggunakan neural network untuk memperkirakan Q(s,a)
* Konsep penting: eksplorasi vs eksploitasi, reward, value, policy

---