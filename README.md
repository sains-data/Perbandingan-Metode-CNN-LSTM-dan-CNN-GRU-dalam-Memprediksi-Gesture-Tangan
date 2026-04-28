# Perbandingan Metode CNN-LSTM dan CNN-GRU dalam Memprediksi Gesture Tangan

Proyek ini membandingkan dua arsitektur deep learning untuk klasifikasi gesture tangan dari rangkaian frame video, yaitu CNN-LSTM dan CNN-GRU. Seluruh alur kerja disusun di notebook, mulai dari resampling data, preprocessing frame video, pelatihan model, evaluasi, hingga penyimpanan model akhir.

## Kelompok 22 Tugas Besar Deep Learning
- VENI ZAHARA KARTIKA_121450075
- YOSIA ADWILY NAINGGOLAN_121450063
- M. RIZKI ALFAINA_121140228
- TRI MURNIYANINGSIH_121450038
- IMA ALIFAH IZATI ZALFA_121450140
- ANITA RAHMA PRAMODA CAHYANI_121450154

## Deskripsi Proyek
Pengenalan gesture tangan merupakan bagian penting dari computer vision dan interaksi manusia-komputer. Pada proyek ini, gesture dipelajari dari dataset video dan diubah menjadi representasi frame agar model dapat menangkap pola spasial sekaligus temporal.

Tujuan utama proyek ini adalah:
- memproses data gesture menjadi format yang siap dilatih,
- membangun model CNN-LSTM dan CNN-GRU,
- membandingkan performa keduanya pada data validasi dan data uji,
- menghasilkan visualisasi evaluasi seperti confusion matrix dan kurva training.

## Dataset

### Sumber Dataset
- Dataset utama: https://www.kaggle.com/datasets/toxicmender/20bn-jester/data

Berdasarkan laporan pada folder `Laporan/`, Jester Dataset terdiri dari **148.092 video** dengan **27 label**. Pada penelitian ini label disederhanakan menjadi **5 label utama** untuk kebutuhan eksperimen dan keterbatasan komputasi.

### Struktur Data
Dataset yang digunakan berbasis video gesture dari Jester. Setiap sampel direpresentasikan sebagai folder video yang berisi frame-frame gambar, serta file CSV yang menyimpan pasangan `video_id` dan `label`.

### Pembagian Data
Di notebook, data dibagi menjadi:
- Train
- Validation
- Test

Pada eksperimen yang dilaporkan:
- **Train**: resampling menjadi **1.000 video per label** (total **5.000** video) dan setiap video diseragamkan menjadi **30 frame**.
- **Validation**: total **500** video-clips (setara **100 video per label**).
- **Test**: total **10** video (setara **2 video per label** pada 5 kelas).

### Label yang Digunakan
Notebook melakukan resampling pada lima kelas gesture berikut:
- Doing other things
- Pushing Two Fingers Away
- Drumming Fingers
- Sliding Two Fingers Down
- Pushing Hand Away

Label pada data train dan validation diterjemahkan ke bahasa Indonesia saat proses resampling.

### Preprocessing Dataset
Tahapan preprocessing yang dilakukan adalah:
1. Menyamakan jumlah frame setiap video menjadi 30 frame.
2. Jika frame kurang dari 30, frame terakhir digandakan.
3. Jika frame lebih dari 30, frame dipotong dari awal.
4. Setiap frame diubah ukurannya menjadi 64 x 64 piksel.
5. Frame diubah ke grayscale.
6. Data dinormalisasi menggunakan StandardScaler.

## Algoritma yang Digunakan

### CNN-LSTM
CNN-LSTM menggabungkan Convolutional Neural Network dan Long Short-Term Memory.

- CNN berfungsi mengekstraksi fitur spasial dari frame video.
- LSTM menangkap hubungan temporal antarframe secara berurutan.

Arsitektur pada notebook menggunakan:
- Conv3D
- MaxPool3D
- ConvLSTM2D
- Flatten
- Dense
- Softmax output

Model ini cocok untuk data video karena dapat mempelajari pola gerakan yang berubah sepanjang waktu.

### CNN-GRU
CNN-GRU juga menggabungkan CNN dengan unit recurrent, tetapi menggunakan GRU sebagai pengolah urutan.

- CNN mengekstraksi fitur visual dari frame.
- GRU mempelajari pola temporal dengan parameter yang lebih ringkas dibanding LSTM.

Arsitektur pada notebook menggunakan:
- Conv3D
- MaxPool3D
- Reshape
- GRU
- Dense
- Softmax output

Model ini umumnya lebih ringan dan lebih cepat dilatih dibanding LSTM, meskipun performa terbaik tetap bergantung pada karakteristik data.

### Perbandingan Konseptual
| Aspek | CNN-LSTM | CNN-GRU |
|---|---|---|
| Pengolah urutan | LSTM | GRU |
| Kompleksitas parameter | Lebih besar | Lebih ringkas |
| Potensi menangkap dependensi panjang | Sangat baik | Baik |
| Kecepatan komputasi | Cenderung lebih lambat | Cenderung lebih cepat |
| Cocok untuk | Analisis temporal yang lebih kaya | Model yang lebih efisien |

## Panduan Menjalankan Kode

### 1. Clone Repository
```bash
git clone <url-repository-anda>
cd <nama-folder-repository>
```

### 2. Siapkan Environment
Disarankan menggunakan Python 3.9 atau 3.10 dengan library berikut:
- numpy
- pandas
- matplotlib
- opencv-python
- scikit-learn
- tensorflow

Contoh instalasi:
```bash
pip install numpy pandas matplotlib opencv-python scikit-learn tensorflow
```

### 3. Siapkan Dataset
Notebook awalnya menggunakan path bergaya Kaggle. Jika dijalankan secara lokal, sesuaikan path berikut:
- folder train
- folder validation
- folder test
- file CSV label untuk masing-masing split

Pastikan struktur folder video dan file CSV tetap konsisten dengan yang dipakai notebook.

### 4. Jalankan Notebook
Buka notebook berikut:
- [Kelompok 22_CNN-LSTM & CNN-GRU_FIX.ipynb](Kelompok%2022_CNN-LSTM%20%26%20CNN-GRU_FIX.ipynb)

Jalankan sel secara berurutan mulai dari import library, resampling, preprocessing, training model, evaluasi, hingga penyimpanan model.

### 5. Output Model
Notebook akan menghasilkan file model terlatih:
- `model_cnnlstm.h5`
- `model_cnngru.h5`

## Hasil Output dan Visualisasi
Notebook menghasilkan beberapa output utama:

- Plot loss dan accuracy selama training untuk CNN-LSTM dan CNN-GRU.
- Confusion matrix pada data validasi.
- Classification report yang berisi precision, recall, dan f1-score.
- Evaluasi loss dan accuracy pada data train, validation, dan test.
- Prediksi label pada data test dalam bentuk DataFrame.

Visualisasi yang tersedia di notebook:
- grafik loss per epoch,
- grafik accuracy per epoch,
- confusion matrix validation,
- confusion matrix test.

## Hasil Eksperimen (Kuantitatif)

Bagian ini merangkum **angka hasil eksperimen** yang tercantum di dokumen laporan: [Full Paper_Kelompok 22_Perbandingan Metode CNN LSTM dan CNN GRU dalam Memprediksi Gesture Tangan.pdf](Laporan/Full%20Paper_Kelompok%2022_Perbandingan%20Metode%20CNN%20LSTM%20dan%20CNN%20GRU%20dalam%20Memprediksi%20Gesture%20Tangan.pdf).

### Setup Pelatihan (sesuai laporan)
- Optimizer: **Adam**
- Loss: **Sparse Categorical Cross Entropy**
- Maksimum epoch: **10**
- Batch size: **32**
- Early stopping: digunakan (pelatihan berhenti lebih cepat saat validasi tidak membaik)

### Ringkasan Akurasi (Train/Validation/Test)
Berikut ringkasan akurasi yang dilaporkan (Tabel 8 pada laporan):

| Split | CNN-LSTM (Accuracy) | CNN-GRU (Accuracy) |
|---|---:|---:|
| Train | 0.94 | 0.83 |
| Validation | 0.82 | 0.76 |
| Test | 0.60 | 0.70 |

### Dinamika Training (Loss & Accuracy per Epoch)
Rentang nilai yang diamati pada kurva training (berdasarkan pembahasan plot pada laporan):

- **CNN-LSTM**
    - Train loss: 1.6176 → 0.1152
    - Validation loss: 1.5931 → 0.8151
    - Train accuracy: 0.1985 → 0.9600
    - Validation accuracy: 0.2420 → 0.8020
    - Pelatihan berhenti pada **epoch ke-8** (early stopping)

- **CNN-GRU**
    - Train loss: 1.5642 → 0.3120
    - Validation loss: 1.0450 → 0.6852
    - Train accuracy: 0.2895 → 0.8881
    - Validation accuracy: 0.6220 → 0.8120
    - Pelatihan berhenti pada **epoch ke-4** (early stopping)

### Evaluasi per Kelas (Validation, n=500)

**CNN-LSTM (Tabel 2)**
| Label | Precision | Recall | F1-Score | Support |
|---|---:|---:|---:|---:|
| Menjauhkan Dua Jari | 0.69 | 0.83 | 0.75 | 100 |
| Melakukan hal lain | 0.84 | 0.78 | 0.81 | 100 |
| Mengetuk Jari | 0.89 | 0.93 | 0.91 | 100 |
| Menjauhkan Tangan | 0.88 | 0.78 | 0.83 | 100 |
| Menggeser Dua Jari Ke Bawah | 0.89 | 0.83 | 0.86 | 100 |
| **Accuracy** |  |  | **0.83** | **500** |
| Macro avg | 0.84 | 0.83 | 0.83 | 500 |
| Weighted avg | 0.84 | 0.83 | 0.83 | 500 |

**CNN-GRU (Tabel 5)**
| Label | Precision | Recall | F1-Score | Support |
|---|---:|---:|---:|---:|
| Menjauhkan Dua Jari | 0.58 | 0.76 | 0.66 | 100 |
| Melakukan hal lain | 0.83 | 0.71 | 0.76 | 100 |
| Mengetuk Jari | 0.98 | 0.81 | 0.89 | 100 |
| Menjauhkan Tangan | 0.76 | 0.76 | 0.76 | 100 |
| Menggeser Dua Jari Ke Bawah | 0.80 | 0.81 | 0.81 | 100 |
| **Accuracy** |  |  | **0.77** | **500** |
| Macro avg | 0.79 | 0.77 | 0.78 | 500 |
| Weighted avg | 0.79 | 0.77 | 0.78 | 500 |

### Evaluasi per Kelas (Test, n=10)
Catatan: data test pada laporan berukuran kecil (**10 video; 2 video per kelas**), sehingga interpretasi per-kelas perlu hati-hati.

**CNN-LSTM (Tabel 4)**
| Label | Precision | Recall | F1-Score | Support |
|---|---:|---:|---:|---:|
| Menjauhkan Dua Jari | 0.33 | 1.00 | 0.50 | 2 |
| Melakukan hal lain | 1.00 | 0.50 | 0.67 | 2 |
| Mengetuk Jari | 1.00 | 0.50 | 0.67 | 2 |
| Menjauhkan Tangan | 1.00 | 0.50 | 0.67 | 2 |
| Menggeser Dua Jari Ke Bawah | 1.00 | 0.50 | 0.67 | 2 |
| **Accuracy** |  |  | **0.60** | **10** |
| Macro avg | 0.50 | 0.60 | 0.63 | 10 |
| Weighted avg | 0.50 | 0.60 | 0.63 | 10 |

**CNN-GRU (Tabel 7)**
| Label | Precision | Recall | F1-Score | Support |
|---|---:|---:|---:|---:|
| Menjauhkan Dua Jari | 0.40 | 1.00 | 0.57 | 2 |
| Melakukan hal lain | 1.00 | 0.50 | 0.67 | 2 |
| Mengetuk Jari | 1.00 | 0.50 | 0.67 | 2 |
| Menjauhkan Tangan | 1.00 | 1.00 | 1.00 | 2 |
| Menggeser Dua Jari Ke Bawah | 1.00 | 0.50 | 0.67 | 2 |
| **Accuracy** |  |  | **0.70** | **10** |
| Macro avg | 0.88 | 0.70 | 0.71 | 10 |
| Weighted avg | 0.88 | 0.70 | 0.71 | 10 |

### Ringkasan Confusion Matrix (Validation)
Diagonal (prediksi benar) pada confusion matrix validation yang dijelaskan di laporan:

- **CNN-LSTM (n=500)**: 83 (Menjauhkan Dua Jari), 78 (Melakukan hal lain), 93 (Mengetuk Jari), 78 (Menjauhkan Tangan), 83 (Menggeser Dua Jari Ke Bawah).
- **CNN-GRU (n=500)**: 76 (Menjauhkan Dua Jari), 71 (Melakukan hal lain), 81 (Mengetuk Jari), 76 (Menjauhkan Tangan), 81 (Menggeser Dua Jari Ke Bawah).

## Komparasi Model
Perbandingan dilakukan menggunakan metrik yang sama (accuracy, precision, recall, F1-score, confusion matrix) pada split data yang sama.

Poin penting dari hasil kuantitatif:
- **Akurasi validation** lebih tinggi pada **CNN-LSTM (0.82)** dibanding **CNN-GRU (0.76)**.
- **Akurasi test** lebih tinggi pada **CNN-GRU (0.70)** dibanding **CNN-LSTM (0.60)**.
- Per-kelas pada validation, kelas dengan performa paling kuat adalah **Mengetuk Jari** (F1: 0.91 pada CNN-LSTM; 0.89 pada CNN-GRU) dan **Menggeser Dua Jari Ke Bawah** (F1: 0.86 pada CNN-LSTM; 0.81 pada CNN-GRU).
- Kelas yang paling menantang pada kedua model adalah **Menjauhkan Dua Jari** (F1: 0.75 pada CNN-LSTM; 0.66 pada CNN-GRU).

## Analisis
Secara metodologis, CNN-LSTM unggul dalam memodelkan dependensi temporal yang lebih panjang, sedangkan CNN-GRU lebih ringkas dan sering lebih stabil secara komputasi.

Berdasarkan hasil yang dilaporkan, terlihat indikasi **gap generalisasi** pada CNN-LSTM: akurasi train 0.94 dan validation 0.82, namun turun pada test menjadi 0.60. Sebaliknya, CNN-GRU memiliki akurasi train 0.83 dan validation 0.76, tetapi lebih baik pada test (0.70). Ini konsisten dengan pembahasan laporan yang menekankan CNN-GRU lebih baik dalam generalisasi pada data test pada kasus ini.

Dari sisi kesulitan kelas, kedua model paling sering mengalami masalah pada gesture **Menjauhkan Dua Jari**, ditunjukkan oleh F1-score terendah pada evaluasi validation (0.75 pada CNN-LSTM dan 0.66 pada CNN-GRU). Hal ini mengindikasikan adanya kemiripan pola visual/temporal gesture tersebut dengan kelas lain (ambiguity) sehingga lebih rentan tertukar.

## Kesimpulan
Proyek ini menunjukkan bahwa klasifikasi gesture tangan dapat dilakukan dengan pendekatan hybrid CNN dan recurrent network. Pada konfigurasi eksperimen yang dilaporkan:

- CNN-LSTM mencapai akurasi **0.82 (validation)** dan **0.60 (test)**.
- CNN-GRU mencapai akurasi **0.76 (validation)** dan **0.70 (test)**.

Jika kriteria utama adalah **performa pada data test (generalisasi)**, maka **CNN-GRU** menjadi pilihan yang lebih baik pada eksperimen ini. Jika fokusnya adalah **performa pada validasi**, maka **CNN-LSTM** lebih unggul.

## Referensi
- Jester Dataset: https://www.kaggle.com/datasets/toxicmender/20bn-jester/data
- TensorFlow: https://www.tensorflow.org/
- Scikit-learn: https://scikit-learn.org/
