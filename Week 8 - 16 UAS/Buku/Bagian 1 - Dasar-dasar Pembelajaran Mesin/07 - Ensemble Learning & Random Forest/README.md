---

# 📘 Chapter 7 – Ensemble Learning and Random Forests

---

## 🎯 Tujuan Bab Ini:

* Memahami **ensemble learning** — menggabungkan banyak model lemah menjadi model kuat.
* Mengenal berbagai teknik ensemble: **bagging**, **pasting**, **random forest**, **AdaBoost**, **Gradient Boosting**.
* Membangun model dengan **RandomForestClassifier** dan **GradientBoostingRegressor**.

---

## 👥 1. Apa itu Ensemble Learning?

**Ensemble Learning** adalah teknik menggabungkan prediksi dari beberapa model untuk menghasilkan prediksi yang lebih baik.

> “Wisdom of the crowd” — gabungan opini banyak orang bisa lebih akurat daripada opini individu.

---

## 🧱 2. Voting Classifier

Gabungkan beberapa model klasifikasi (misalnya SVM, Logistic Regression, Decision Tree):

* **Hard voting**: mayoritas suara menang
* **Soft voting**: gabungkan probabilitas prediksi, lalu ambil prediksi dengan probabilitas tertinggi

🧠 Soft voting biasanya **lebih akurat** jika model cukup baik dalam memperkirakan probabilitas.

---

## 📦 3. Bagging dan Pasting

Kedua teknik ini melatih banyak model pada subset data:

| Teknik      | Sampel                | Repetisi | Variance   | Bias |
| ----------- | --------------------- | -------- | ---------- | ---- |
| **Bagging** | Acak + boleh duplikat | Ya       | ↓ Variance | —    |
| **Pasting** | Acak + tanpa duplikat | Tidak    | ↓ Variance | —    |

* **Bagging = Bootstrap Aggregating**
* Hasil digabungkan lewat voting (klasifikasi) atau rata-rata (regresi)

📌 Gunakan `BaggingClassifier` / `BaggingRegressor` di Scikit-Learn.

---

## 🌲 4. Random Forest

**Random Forest** = banyak Decision Tree + bagging + subset fitur acak tiap split

Keunggulan:

* Kuat terhadap overfitting
* Bisa estimasi pentingnya fitur (`feature_importances_`)
* Scikit-Learn: `RandomForestClassifier` dan `RandomForestRegressor`

---

## 🔀 5. Out-of-Bag Evaluation (OOB)

Saat menggunakan **bagging**, beberapa sampel **tidak terpilih** dalam training → disebut **Out-of-Bag (OOB)**.

Scikit-Learn bisa secara otomatis melakukan validasi menggunakan data OOB (`oob_score=True`).

---

## 🪄 6. Feature Importance

Random Forest bisa menghitung seberapa penting suatu fitur terhadap prediksi.

* `feature_importances_` mengembalikan skor tiap fitur
* Fitur yang lebih penting → dipakai lebih sering di awal pohon

---

## 🚀 7. Boosting (Model Bertahap)

**Boosting** adalah teknik training model **berurutan**, di mana setiap model baru fokus memperbaiki kesalahan model sebelumnya.

Dua metode utama:

### 🔸 a. AdaBoost (Adaptive Boosting)

* Tiap model dapat bobot berdasarkan kesalahannya
* Scikit-Learn: `AdaBoostClassifier`, `AdaBoostRegressor`

### 🔹 b. Gradient Boosting

* Model baru dilatih pada **residual (sisa kesalahan)** dari model sebelumnya
* Lebih presisi tapi sensitif terhadap noise
* `GradientBoostingClassifier` / `GradientBoostingRegressor`

📦 Untuk data besar, gunakan **Histogram-Based Gradient Boosting (HistGradientBoosting)** → lebih efisien.

---

## 🧪 8. Tuning dan Stacking

* Boosting bisa **overfit**, perlu diatur `n_estimators`, `learning_rate`, dan `max_depth`.
* **Stacking**: model akhir (meta-learner) dilatih berdasarkan output model-model sebelumnya → powerful tapi kompleks.

---

## 📑 Ringkasan Inti Bab Ini

* Ensemble learning menggabungkan banyak model untuk hasil lebih akurat.
* Random Forest adalah salah satu metode ensemble paling praktis dan kuat.
* Boosting (AdaBoost & Gradient Boosting) membangun model secara berurutan untuk memperbaiki kesalahan.
* Random Forest menyediakan estimasi pentingnya fitur.
* `oob_score_` dapat digunakan sebagai alternatif cross-validation.

---