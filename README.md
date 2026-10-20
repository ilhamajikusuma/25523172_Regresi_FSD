# 25523172_Regresi_FSD

# Tugas: Linear Regression dan Logistic Regression

## Anggota Kelompok

**Nama**: ILHAM AJI KUSUMA
**NIM**: 25523172

## Pembagian Kontribusi

**Ilham Aji Kusuma (25523172)**: Pengerjaan Bagian A (Linear Regression), Bagian B (Logistic Regression), penyusunan README, dan dokumentasi repositori.

## Sumber Dataset

**Bagian A: California Housing** (`data/california_housing_train.csv`)

- **Sumber**: Folder `sample_data` bawaan Google Colab (data asli dari sensus California 1990 / Pace & Barry, 1997, juga tersedia di [Scikit-Learn Datasets](https://scikit-learn.org/stable/datasets/real_world.html#california-housing-dataset)).
- **Deskripsi**: 17.000 baris dan 9 kolom. Setiap baris mewakili satu _block group_ sensus.
- **Target**: `median_house_value` (harga median rumah, USD, numerik kontinu).
- **Fitur akhir yang dipakai**: `median_income`, `housing_median_age`, `total_rooms`, `population`, `latitude`, `longitude`.

**Bagian B: Titanic** (`data/titanic.csv`)

- **Sumber**: Dimuat dari library Seaborn (`sns.load_dataset('titanic')`), dengan data asli dari [Seaborn Data Repository](https://github.com/mwaskom/seaborn-data).
- **Deskripsi**: 891 baris dan 15 kolom. Setiap baris mewakili satu penumpang kapal RMS Titanic.
- **Target**: `survived` (0 = tidak selamat, 1 = selamat).
- **Fitur akhir yang dipakai**: `pclass`, `age`, `parch`, `fare`, `sex_male`, `embarked_S`.

## Ringkasan Hasil

### Bagian A (Linear Regression)

| Metrik     | Data Latih  | Data Uji    |
| ---------- | ----------- | ----------- |
| MAE (USD)  | 47.921      | 47.147      |
| MSE        | 4,063 × 10⁹ | 3,999 × 10⁹ |
| RMSE (USD) | 63.740      | 63.241      |
| R²         | 0,579       | 0,573       |

- **Analisis Performa**: Metrik pada data latih dan data uji hampir sama, menunjukkan bahwa model tidak mengalami _overfitting_. Nilai R² sekitar 0,57 mengindikasikan kecenderungan _underfitting_ karena hubungan antara fitur dan harga rumah tidak sepenuhnya linear. Fitur yang paling berpengaruh adalah `latitude`, `longitude`, dan `median_income`. Baris dengan harga terpotong di 500.001 telah dihapus pada tahap preprocessing.

### Bagian B (Logistic Regression)

| Metrik    | Data Latih | Data Uji |
| --------- | ---------- | -------- |
| Accuracy  | 0,791      | 0,777    |
| Precision | 0,704      | 0,684    |
| Recall    | 0,784      | 0,783    |
| F1-score  | 0,742      | 0,730    |
| AUC       | -          | 0,834    |

- **Analisis Performa**: Confusion matrix pada data uji menghasilkan: TN = 85, FP = 25, FN = 15, TP = 54. Performa metrik latih dan uji yang mirip menandakan tidak adanya _overfitting_. Ketidakseimbangan kelas (rasio sekitar 62% : 38%) diatasi menggunakan parameter `class_weight='balanced'`, sehingga berhasil menjaga _recall_ kelas selamat tetap tinggi (0,783) dengan konsekuensi _precision_ yang sedikit lebih rendah (kesalahan terbanyak berupa _False Positive_). Fitur yang paling berpengaruh adalah jenis kelamin (`sex_male`) dan kelas tiket (`pclass`).
