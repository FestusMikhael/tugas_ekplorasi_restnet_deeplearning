Festus Mikhael / 122140087
Kenneth Austin / 122140043

# Laporan Benchmark: ResNet-34 vs Plain-34 (Residual Connection Analysis)

## 1. Konfigurasi Hyperparameter

Eksperimen ini menggunakan konfigurasi hyperparameter yang identik untuk memastikan perbandingan performa yang adil.

| Parameter | Nilai |
| :--- | :--- |
| **Dataset** | Dataset Makanan Indonesia (5 Kelas) |
| **Model** | Plain-34 dan ResNet-34 |
| **Epochs** | 10 |
| **Batch Size** | 16 |
| **Learning Rate (LR)** | 0.01 |
| **Optimizer** | SGD dengan Momentum (0.9) |
| **Scheduler** | StepLR (step=7, gamma=0.1) |

---

## 2. Tabel Perbandingan Metrik (Epoch 10)

| Metrik | Plain-34 (Baseline) | ResNet-34 | Selisih (Peningkatan) |
| :--- | :--- | :--- | :--- |
| **Training Accuracy** | 46.65% | **66.31%** | **+19.66%** |
| **Validation Accuracy** | 40.12% | **66.47%** | **+26.35%** |
| **Training Loss** | 1.253 | **0.920** | **-0.333** |
| **Validation Loss** | 1.212 | **0.841** | **-0.371** |

---

## 3. Grafik Kurva Training

![Grafik Perbandingan Akurasi]<img width="813" height="479" alt="image" src="https://github.com/user-attachments/assets/2331fa19-c6f9-4842-92a1-e9cfa04d0872" />
![Grafik Perbandingan Loss]<img width="812" height="486" alt="image" src="https://github.com/user-attachments/assets/6464908a-e4ad-4389-9f0b-021519486917" />

---

## 4. Analisis Performa dan Dampak Residual Connection

### Analisis Kritis

Implementasi **Residual Connection** yang mengubah Plain-34 menjadi ResNet-34 memberikan dampak performa yang sangat signifikan. ResNet-34 mencapai akurasi validasi puncak **66.47%** pada Epoch 10, yang merupakan peningkatan substansial sebesar **26.35%** dibandingkan dengan Plain-34 yang hanya mencapai 40.12% di *epoch* terakhirnya. Peningkatan ini didukung oleh *validation loss* ResNet-34 yang jauh lebih rendah dan lebih stabil (0.841 berbanding 1.212).

Data menunjukkan bahwa arsitektur **Plain-34 mengalami masalah *degradasi***. Meskipun *training loss* masih menunjukkan upaya penurunan, *validation accuracy* model justru mengalami stagnasi parah dan menunjukkan penurunan tiba-tiba di akhir pelatihan. Kesulitan ini adalah manifestasi dari masalah *vanishing gradient*, di mana gradien menjadi terlalu kecil untuk secara efektif mengoptimalkan lapisan-lapisan awal pada jaringan yang sangat dalam.

Sebaliknya, **ResNet-34 menunjukkan *convergence* yang kuat dan cepat**. Dengan adanya *skip connection* (jalur pintas), sinyal gradien dapat mengalir langsung ke lapisan sebelumnya, memungkinkan pelatihan yang efisien tanpa *degradasi* performa. Hasilnya, ResNet-34 tidak hanya mencapai performa yang jauh lebih tinggi, tetapi juga menunjukkan stabilitas yang lebih baik, terbukti dari selisih kecil antara akurasi training dan validasi. Secara keseluruhan, Residual Connection berhasil mengatasi hambatan pelatihan jaringan dalam, membuktikan esensinya dalam pengembangan *Deep Learning*.
