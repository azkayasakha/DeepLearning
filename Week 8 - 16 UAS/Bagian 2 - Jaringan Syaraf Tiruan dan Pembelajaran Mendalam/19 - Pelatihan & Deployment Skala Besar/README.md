---

# 📘 Chapter 19 – Training and Deploying TensorFlow Models at Scale

---

### 🎯 Tujuan Utama Bab Ini:

Menjelaskan bagaimana cara:

1. Melatih model TensorFlow secara efisien dalam skala besar (multi-GPU, multi-node).
2. Menyimpan dan men-deploy model ke lingkungan produksi.
3. Menggunakan TensorFlow Serving dan TFX untuk deployment profesional.

---

## 🧠 Materi Inti Bab 19

### 1. **Distribusi Pelatihan**

TensorFlow menyediakan berbagai strategi untuk melatih model pada beberapa CPU, GPU, atau bahkan banyak mesin (node).

#### a. `tf.distribute.Strategy`

Beberapa strategi yang sering digunakan:

* `MirroredStrategy`: untuk multi-GPU pada satu mesin.
* `MultiWorkerMirroredStrategy`: untuk pelatihan di beberapa mesin.
* `TPUStrategy`: untuk menggunakan TPU (di Google Cloud).
* `ParameterServerStrategy`: untuk skenario pelatihan skala besar yang lebih kompleks.

#### Contoh:

```python
strategy = tf.distribute.MirroredStrategy()
with strategy.scope():
    model = keras.Sequential([...])
    model.compile(...)
```

> Model dan optimizer harus didefinisikan di dalam `strategy.scope()` agar bisa berjalan paralel di beberapa GPU.

---

### 2. **Checkpoint dan Logging**

Untuk menyimpan progress model saat training:

* `ModelCheckpoint`: menyimpan bobot model setiap epoch atau ketika performa meningkat.
* `TensorBoard`: untuk visualisasi metrik training, grafik, dan lainnya.

#### Contoh:

```python
callbacks = [
    keras.callbacks.ModelCheckpoint("my_model.h5", save_best_only=True),
    keras.callbacks.TensorBoard(log_dir="./logs")
]
model.fit(..., callbacks=callbacks)
```

---

### 3. **Export Model dalam Format `SavedModel`**

TensorFlow menggunakan format `SavedModel` sebagai standar untuk menyimpan model siap-produksi.

```python
model.save("my_model")  # direktori "my_model" akan berisi SavedModel
```

> `SavedModel` berisi: grafik lengkap, bobot, dan signature untuk inferensi.

---

### 4. **Serving dengan TensorFlow Serving**

TensorFlow Serving memungkinkan model `SavedModel` di-*serve* melalui API REST atau gRPC.

#### Langkah Singkat:

1. Simpan model:

   ```bash
   model.save("/models/my_model/1")  # versi model = 1
   ```

2. Jalankan TensorFlow Serving dengan Docker:

   ```bash
   docker run -p 8501:8501 --name=tf_model_serving \
     -v "$(pwd)/models:/models" \
     -e MODEL_NAME=my_model \
     tensorflow/serving
   ```

3. Akses lewat REST API:

   ```bash
   curl -d '{"instances": [[1.0, 2.0, 3.0, 4.0]]}' \
     -H "Content-Type: application/json" \
     http://localhost:8501/v1/models/my_model:predict
   ```

---

### 5. **TFX: TensorFlow Extended**

TFX adalah pipeline produksi end-to-end untuk ML:

* **Components**:

  * `ExampleGen`: input data
  * `StatisticsGen`: eksplorasi data
  * `Trainer`: melatih model
  * `Evaluator`: mengevaluasi
  * `Pusher`: deploy ke produksi
* **Orchestration Tools**:

  * Apache Airflow
  * Kubeflow Pipelines
  * Vertex AI Pipelines (GCP)

> TFX cocok untuk sistem produksi yang kompleks, terutama di enterprise.

---

### 6. **Alternative Deployment**

* **TF Lite**: untuk perangkat mobile dan embedded.
* **TF.js**: untuk deployment di browser dengan JavaScript.
* **ONNX**: interoperabilitas dengan framework ML lainnya.

---

## ✅ Kesimpulan Bab 19

| Topik                    | Penjelasan Singkat                                           |
| ------------------------ | ------------------------------------------------------------ |
| `tf.distribute.Strategy` | Melatih model secara paralel di GPU/TPU/multi-node           |
| `SavedModel`             | Format standar TensorFlow untuk deployment                   |
| TensorFlow Serving       | Menyediakan REST/gRPC API untuk model yang dilatih           |
| TFX                      | Pipeline produksi lengkap untuk alur kerja ML                |
| TF Lite / JS / ONNX      | Alternatif deployment untuk edge, web, dan interoperabilitas |

---