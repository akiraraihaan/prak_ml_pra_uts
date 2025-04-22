# Dokumentasi Project Klasifikasi Gambar Anemia dengan Random Forest

## Ringkasan
Project ini bertujuan untuk mengembangkan model machine learning yang dapat mengklasifikasikan gambar mikroskopis menjadi dua kategori: anemia dan non-anemia. Model menggunakan algoritma Random Forest untuk klasifikasi dan mencapai akurasi sekitar 91% dalam memprediksi kondisi anemia berdasarkan gambar.

## Daftar Isi
1. [Pendahuluan](#pendahuluan)
2. [Dataset](#dataset)
3. [Eksplorasi Data (EDA)](#eksplorasi-data-eda)
4. [Preprocessing Data](#preprocessing-data)
5. [Pemodelan](#pemodelan)
6. [Evaluasi Model](#evaluasi-model)
7. [Cross-Validation](#cross-validation)
8. [Hasil dan Kesimpulan](#hasil-dan-kesimpulan)
9. [Tim Project](#tim-project)

## Pendahuluan
Anemia adalah kondisi kesehatan yang ditandai dengan kekurangan sel darah merah atau hemoglobin dalam darah. Diagnosis anemia sering melibatkan analisis visual gambar mikroskopis darah. Project ini mengembangkan sistem otomatis berbasis machine learning untuk mengklasifikasikan gambar mikroskopis darah, membantu proses diagnosis anemia dengan lebih cepat dan akurat.

## Dataset
Dataset terdiri dari:

- **Gambar Anemic**: 2.563 gambar
- **Gambar Non-anemic**: 1.714 gambar

Setiap gambar merupakan gambar mikroskopis sampel darah yang diamati untuk tujuan diagnosis anemia. Gambar-gambar ini memiliki ukuran yang bervariasi dan dikonversi ke grayscale untuk analisis.

## Eksplorasi Data (EDA)
Dalam fase eksplorasi data, kami melakukan analisis terhadap:

### Distribusi Ukuran Gambar
- Gambar dalam dataset memiliki ukuran yang sangat bervariasi
- Standardisasi ukuran diperlukan untuk membandingkan fitur antar gambar dengan konsisten

### Ketidakseimbangan Kelas
- Kelas anemic memiliki lebih banyak sampel (2.563) dibandingkan non-anemic (1.714)
- Rasio ketidakseimbangan ini dapat mempengaruhi performa model jika tidak ditangani

### Analisis Intensitas Pixel
- Distribusi rata-rata intensitas pixel antara kelas anemic dan non-anemic menunjukkan tumpang tindih
- Nilai intensitas rata-rata berkisar antara 30-60 untuk sebagian besar gambar
- Klasifikasi berdasarkan intensitas rata-rata saja tidak memadai

### Identifikasi Outlier
- Kelas anemic memiliki beberapa outlier dengan intensitas di atas 70
- Kelas non-anemic menunjukkan variasi yang lebih lebar dan outlier yang lebih ekstrem (mendekati nilai 90)

## Preprocessing Data
Tahapan preprocessing data meliputi:

### 1. Standardisasi Ukuran Gambar
- Semua gambar dikonversi ke grayscale dan diubah ukurannya menjadi 128×128 pixel
- Hasil konversi kemudian diratakan (flatten) menjadi vektor 1D

### 2. Pembagian Data Training dan Testing
- Data dibagi dengan rasio 80% untuk training dan 20% untuk testing
- Stratifikasi digunakan untuk mempertahankan proporsi kelas di kedua subset

### 3. Normalisasi
- Normalisasi dilakukan menggunakan MinMaxScaler untuk menskala nilai pixel ke rentang [0,1]
- Scaler hanya di-fit pada data training untuk menghindari data leakage

### 4. Penanganan Outlier
- Outlier diidentifikasi menggunakan z-score pada rata-rata intensitas pixel
- Data dengan z-score absolut > 3 dianggap sebagai outlier dan dihapus dari training set

### 5. Mengatasi Ketidakseimbangan Data
- Random oversampling diterapkan untuk menyeimbangkan jumlah sampel antar kelas
- Kelas minoritas (non-anemic) dioversampling hingga jumlahnya setara dengan kelas mayoritas (anemic)

## Pemodelan
Model yang digunakan adalah **Random Forest Classifier** dengan 100 decision tree.

Random Forest dipilih karena:
- Mampu menangani data dengan dimensi tinggi
- Robust terhadap overfitting
- Efektif dalam mengklasifikasikan data gambar yang telah diubah ke dalam representasi vektor

## Evaluasi Model
Model dievaluasi menggunakan confusion matrix dan classification report:

### Hasil evaluasi:
- **Akurasi**: 91%
- **Precision**:
  - Kelas Non-Anemia: 92%
  - Kelas Anemia: 90%
- **Recall**:
  - Kelas Non-Anemia: 85%
  - Kelas Anemia: 95%
- **F1-Score**:
  - Kelas Non-Anemia: 88%
  - Kelas Anemia: 93%

### Confusion Matrix:
```
[[290  52]
 [ 25 485]]
```

## Cross-Validation
Untuk memvalidasi kehandalan model, kami melakukan 5-fold cross-validation:

Hasil cross-validation menunjukkan performa model yang konsisten di berbagai fold data.

## Hasil dan Kesimpulan

### Performa Klasifikasi yang Tinggi
- Model mencapai akurasi keseluruhan 91%, menunjukkan kemampuan yang baik dalam membedakan gambar anemia dan non-anemia.

### Deteksi Anemia yang Efektif
- Recall kelas anemia yang tinggi (95%) menunjukkan bahwa model sangat efektif dalam mendeteksi kasus anemia, meminimalkan risiko false negative.

### Kepercayaan Prediksi Non-Anemia
- Precision tinggi pada kelas non-anemia (92%) menunjukkan bahwa ketika model memprediksi non-anemia, kemungkinan besar prediksi tersebut benar.

### Keseimbangan Trade-off Precision dan Recall
- F1-score yang seimbang pada kedua kelas (88% dan 93%) menunjukkan model memiliki trade-off precision dan recall yang stabil.

### Efektivitas Oversampling
- Performa yang seimbang antar kelas menunjukkan bahwa strategi oversampling yang diterapkan berhasil mengurangi bias terhadap kelas mayoritas.

Model ini berpotensi menjadi alat bantu yang berharga dalam diagnosis awal anemia berdasarkan gambar mikroskopis darah, meskipun tentu saja keputusan medis final tetap harus dilakukan oleh dokter atau tenaga medis profesional.

## Tim Project
- **Raihan Akira Rahmaputra** (105222040)
- **Gema Fitri Ramadani** (105222009)