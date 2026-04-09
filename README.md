# Mini_project_klasifikasi_portofolio
# Proyek Klasifikasi Kelulusan Mahasiswa

## 1. Pendahuluan
Mini proyek ini bertujuan untuk membangun model klasifikasi guna memprediksi kelulusan maMinihasiswa berdasarkan beberapa indikator akademik sederhana. Proyek ini mencakup seluruh alur kerja `end-to-end` dari pemuatan data hingga evaluasi model dan penyimpanan data bersih.

## 2. Dataset
Dataset yang digunakan (`mini_project_klasifikasi_kelulusan.csv`) berisi informasi mengenai:
- `id`: ID Mahasiswa
- `jam_belajar`: Durasi jam belajar per minggu
- `kehadiran`: Persentase kehadiran
- `nilai_tugas`: Nilai tugas
- `nilai_uts`: Nilai Ujian Tengah Semester
- `ikut_bimbingan`: Status keikutsertaan bimbingan (ya/tidak)
- `akses_internet`: Status akses internet (ya/tidak)
- `lulus`: Variabel target (0 = tidak lulus, 1 = lulus)

## 3. Tahapan Proyek

### 3.1. Pemuatan Data (`LOAD DATASET`)
Data awal dimuat dari file CSV dan ditampilkan beberapa baris pertama serta dimensinya.

### 3.2. Preprocessing Data (`PREPROCESSING`)
Tahapan ini melibatkan:
- **Penghapusan Duplikasi**: Baris duplikat dihapus untuk memastikan keunikan data.
- **Konversi Tipe Data**: Kolom numerik dikonversi ke tipe data yang sesuai; nilai non-numerik (jika ada) diubah menjadi NaN.
- **Penanganan Missing Values**: 
    - Kolom numerik (`jam_belajar`, `kehadiran`, `nilai_tugas`, `nilai_uts`) diisi dengan nilai median.
    - Kolom kategorikal (`ikut_bimbingan`, `akses_internet`) diisi dengan modus (nilai paling sering muncul).
- **Encoding Kategorikal**: Kolom kategorikal `ikut_bimbingan` dan `akses_internet` diubah menjadi representasi numerik (0 dan 1) untuk digunakan dalam model.

### 3.3. Pemisahan Fitur dan Target (`FITUR DAN TARGET`)
Variabel fitur (X) dan target (y) ditentukan. Fitur meliputi `jam_belajar`, `kehadiran`, `nilai_tugas`, `nilai_uts`, `ikut_bimbingan_encoded`, dan `akses_internet_encoded`. Target adalah kolom `lulus`.

### 3.4. Pemisahan Data (`SPLIT DATA`)
Data dibagi menjadi _training set_ (75%) dan _test set_ (25%) menggunakan `train_test_split` dengan `random_state=42` dan `stratify=y` untuk menjaga proporsi kelas target.

### 3.5. Scaling Data
Data fitur untuk model `Logistic Regression` diskalakan menggunakan `StandardScaler` untuk menormalkan rentang nilai fitur.

### 3.6. Pelatihan Model (`TRAINING BEBERAPA MODEL`)
Tiga model klasifikasi dilatih dan dievaluasi:
- **Logistic Regression**
- **Decision Tree Classifier** (dengan `max_depth=4`)
- **Random Forest Classifier**

Setiap model dilatih menggunakan data training dan dievaluasi menggunakan data test. Khusus untuk `Logistic Regression`, data yang diskalakan digunakan.

### 3.7. Perbandingan Hasil (`BANDINGKAN HASIL`)
Metrik evaluasi (accuracy, precision, recall, F1-score) dihitung untuk setiap model dan disimpan dalam DataFrame `hasil_df`. DataFrame ini kemudian diurutkan berdasarkan `f1_score` secara menurun.

### 3.8. Pemilihan Model Terbaik (`PILIH MODEL TERBAIK`)
Model dengan `F1-score` terbaik diidentifikasi sebagai model terbaik. Dalam kasus ini, semua model mencapai F1-score 1.0, menunjukkan performa yang sangat baik pada dataset ini.

### 3.9. Interpretasi Model (`INTERPRETASI`)
Diskusi singkat mengenai karakteristik masing-masing model:
- **Logistic Regression**: Mudah dijelaskan, cocok sebagai _baseline_.
- **Decision Tree**: Aturan keputusan eksplisit dan mudah dipahami.
- **Random Forest**: Seringkali lebih kuat untuk data tabular.

### 3.10. Penyimpanan Data Bersih (`SIMPAN DATA BERSIH`)
Dataframe yang telah di-*preprocessing* (`df`) disimpan ke file CSV baru dengan nama `bab26_klasifikasi_kelulusan_bersih.csv` di dalam folder `Outputs`.

## 4. Visualisasi Kinerja Model
Grafik batang (bar charts) dibuat untuk membandingkan `accuracy`, `precision`, `recall`, dan `f1-score` dari ketiga model. Visualisasi ini memudahkan pemahaman kinerja relatif antar model.

## 5. Kesimpulan
Mini proyek ini berhasil menunjukkan alur kerja klasifikasi `end-to-end`, mulai dari penanganan masalah data hingga evaluasi dan pemilihan model. Meskipun semua model menunjukkan performa sempurna pada dataset ini, proses yang benar dalam _preprocessing_ dan evaluasi adalah kunci dalam pengembangan model `Machine Learning` yang robust dan dapat diinterpretasikan.
