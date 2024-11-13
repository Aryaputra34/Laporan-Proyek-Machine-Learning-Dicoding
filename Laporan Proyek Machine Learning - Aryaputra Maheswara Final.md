# Laporan Proyek Machine Learning - Aryaputra Maheswara
---
## Domain Proyek
---
Diabetes merupakan salah satu penyakit kronis yang menjadi tantangan besar dalam kesehatan global, dengan angka prevalensinya yang terus meningkat. Berdasarkan data dari Organisasi Kesehatan Dunia (WHO), lebih dari 400 juta orang di seluruh dunia hidup dengan diabetes, dan jumlah ini diperkirakan akan terus bertambah seiring dengan perubahan pola hidup dan semakin menua nya populasi [Diabetes Fact Sheet - WHO](https://www.who.int/news-room/fact-sheets/detail/diabetes) . Menurut International Diabetes Federation (IDF), Indonesia menduduki peringkat kelima negara dengan jumlah penderita diabetes terbanyak, dengan 19,5 juta orang yang mengidap diabetes pada tahun 2021. Angka ini diprediksi akan meningkat menjadi 28,6 juta pada tahun 2045. Masalah ini mendapatkan perhatian serius dari Kementerian Kesehatan, mengingat diabetes sering disebut sebagai "ibu dari segala penyakit", karena dapat memicu berbagai komplikasi serius lainnya [Saatnya Mengatur  Si Manis - Kemenkes](https://sehatnegeriku.kemkes.go.id/baca/blog/20240110/5344736/saatnya-mengatur-si-manis/).

Penyakit ini sering kali berkembang tanpa gejala yang jelas pada tahap awal, sehingga sering terdeteksi terlambat ketika komplikasi sudah mulai muncul. Oleh karena itu, penting untuk mendeteksi dini orang-orang yang berisiko mengembangkan diabetes, guna mencegah komplikasi yang lebih serius, seperti penyakit jantung, kerusakan ginjal, kebutaan, hingga amputasi ekstremitas. Dengan mengetahui risiko sejak dini, kita bisa mengambil langkah pencegahan, seperti perubahan gaya hidup, pengelolaan berat badan, serta pengaturan pola makan dan aktivitas fisik.

Dengan kemajuan teknologi, khususnya dalam bidang machine learning dan predictive analytics, kini ada peluang besar untuk meningkatkan akurasi dan efisiensi dalam mendeteksi risiko diabetes. Machine learning memungkinkan kita untuk menganalisis pola-pola dalam data medis yang kompleks, yang dapat digunakan untuk memprediksi kemungkinan seseorang mengidap diabetes berdasarkan berbagai faktor risiko, seperti usia, indeks massa tubuh (BMI), tingkat aktivitas fisik, tekanan darah, dan tingkat gula dalam darah.

## Business Understanding
---
## Problem Statement
---
- Berapa persentase responden yang mengidap penyakit diabetes ?
- Apakah jenis kelamin memiliki jumlah diabetes yang berbeda ?
- Apa faktor - faktor yang mempengaruhi diabetes ?
- Apa model terbaik yang dapat digunakan untuk memprediksi penyakit diabetes ?

## Goals
---
- Mengetahui total persentase responden yang mengidap penyakit diabetes
- Mencari perbandingan tingkat prevalensi diabetes dari jenis kelamin yang berbeda
- Mengetahui faktor - faktor yang mempengaruhi diabetes
- Menentukan model terbaik berdasarkan akurasi tertinggi untuk memprediksi penyakit diabetes pada resopenden

## Solution
---
- Melakukan proses Exploratory Data Analysis (EDA)
- Menggunakan 3 model machine learning, yaitu Logistic Regression, Decision Tree, dan Random Forest
- Menggunakan confusion matrix dan accuracy score

## Data Understanding
---
Pada proyek machine learning ini menggunakan data diabetes yang tersedia pada website kaggle [Diabetes prediction dataset](https://www.kaggle.com/datasets/iammustafatz/diabetes-prediction-dataset), dataset ini berisi data medis dan demografik dari pasien. 

Terdapat 9 variabel dalam dataset:
| Variabel | Keterangan |
|----------|------------|
| gender |  Jenis kelamin responden (Laki - laki dan perempuan)|
| age | Usia responden |
| hypertension | Apakah responden memiliki hipertensi |
| heart_disease | Apakah responden memiliki penyakit jantung |
| smoking_history | Apakah responden memiliki riwayat merokok |
| bmi | Index Massa Berat badan responden |
| HbA1c_level | Hemoglobin A1c adalah ukuran kadar gula darah rata-rata seseorang selama 2-3 bulan terakhi |
| blood_glucose_level | Jumlah glukosa dalam aliran darah pada waktu tertentu |
| diabetes | variabel target yang diprediksi, 1= memiliki diabetes, 0= tidak diabetes |

### Exploratory Data Analysis

---

#### Deskripsi Statistik

![Statistik](asset/laporan1_statistik.png)

Responden memiliki rentang
- Usia 0.08 - 80 tahun
- BMI 10 - 95
- HbA1c 3.5 - 9
- blood_glucose_level 80 - 300

#### Memeriksa Outlier

![Outlier](asset/laporan1_outlier.png)

Pada gambar diatas, terdapat outlier pada **bmi** (95), **HbA1c_level** (9), dan **blood_glucose_level** (300). Namun outlier **tidak dihapus** karena **seseorang mungkin memiliki kondisi** tersebut

#### Memeriksa nilai kolom gender

![Cek Gender](asset/cek_gender.png)

Terdapat gender yang bernilai other, melakukan drop pada gender yang memiliki value other karena merupakan missing value

#### Distribusi Variabel Numerik

![Distribusi Numerik](asset/distribusi_numerik.png)

Berdasarkan histogram diatas:
Age Distribution:
- Distribusi umur relatif seragam di sebagian besar rentang usia, dengan sedikit kenaikan di usia 50 hingga 60 tahun.
- Ada lonjakan pada usia yang lebih muda (mungkin di sekitar usia 0-5 tahun) dan di usia 80-an.
- Ini bisa menunjukkan bahwa dataset mencakup banyak individu muda dan lansia, mungkin karena faktor populasi tertentu dalam data.

BMI Distribution:

- Distribusi bmi sangat right-skewed atau menceng ke kanan.
- Sebagian besar nilai bmi terkonsentrasi antara 15 hingga 30, dengan puncak yang tajam di sekitar 20.
- Beberapa outlier tampak memiliki nilai bmi yang lebih tinggi di atas 40, namun jumlahnya sangat sedikit.
- Skewness ini menunjukkan bahwa sebagian besar individu dalam dataset memiliki bmi dalam rentang normal hingga sedikit kelebihan berat badan, sementara beberapa orang mungkin obesitas.

HbA1c Level Distribution:

- Distribusi HbA1c_level memiliki beberapa puncak, menunjukkan bahwa data mungkin bimodal atau memiliki beberapa kluster nilai.
- Puncak utama berada di sekitar level 5.5 hingga 6.5, yang menunjukkan nilai HbA1c yang mendekati batas diabetes atau pradiabetes.
- Ada beberapa nilai yang lebih tinggi (di atas 7), yang biasanya menunjukkan kondisi diabetes, tetapi jumlahnya relatif lebih kecil.

Blood Glucose Level Distribution:

- Distribusi blood_glucose_level juga memiliki beberapa puncak dengan rentang utama antara 80 hingga 200.
- Rentang umum dari 100-150 menunjukkan bahwa sebagian besar individu memiliki kadar glukosa yang relatif normal atau sedikit lebih tinggi.
- Beberapa outlier dengan nilai yang lebih tinggi dari 200 menunjukkan individu dengan kadar glukosa yang tinggi, yang dapat menunjukkan risiko diabetes atau masalah kesehatan lainnya.

#### Memeriksa Prevalensi Diabetes Berdasarkan Jenis Kelamin

![Prevalensi Diabetes](asset/diabetes_by_gender.png)

Perbandingan prevalensi diabetes pada setiap jenis kelamin
- Total prevalensi diabetes secara keseluruhan adalah sebesar 18% dari seluruh responden
- Perempuan memiliki prevalensi yang lebih tinggi dari laki - laki sebanyak 10% untuk perempuan dan 8% untuk laki - laki dari jumlah seluruh responden
- Dari seluruh responden yang mengidap penyakit diabetes, perempuan memiliki prevalensi sebanyak 52.4% dan laki - laki sebanyak 47.6%

#### Korelasi Diabetes Dengan Jumlah Kadar Gula Dalam Darah

![Korelasi Diabetes Dengan Kadar Gula Dalam Darah](asset/corr_diabetes_to_bgl.png)

Data diatas menunjukkan adanya perbedaan tingkat glukosa darah antara individu dengan dan tanpa diabetes, dengan individu yang memiliki diabetes cenderung memiliki tingkat glukosa darah yang lebih tinggi dan distribusi data yang lebih bervariasi.

#### Analisis Multivariate dengan menggunakan Heatmap, untuk melihat korelasi antara variabel

![Korelasi Antar Variabel Numerik](asset/korelasi_multivariate_numerik.png)

Diabetes pada responden memiliki:
- Korelasi positif yang cukup kuat dengan HbA1c_level dan kadar glukosa dalam darah
- Korelasi positif yang lemah terhadap usia, hipertensi, riwayat penyakit jantung, dan bmi

## Data Preparation

---

Data preparation adalah serangkaian langkah yang dilakukan untuk menyiapkan data agar dapat digunakan dalam pelatihan model machine learning. Proses ini sangat penting karena kualitas dan struktur data yang tepat dapat mempengaruhi kinerja model secara signifikan

Teknik yang digunakan :
- Data cleaning, untuk membersihkan data yang memiliki missing value
    - Data yang hilang atau kosong bisa menyebabkan model gagal mempelajari pola dengan benar. Mengatasi nilai yang hilang atau kosong sangat penting agar model tidak terdistorsi atau tidak dapat digunakan.
- Standarisasi, mengubah rentang data numerik agar memiliki skala yang sama
    - Fitur dengan skala yang sangat berbeda dapat mempengaruhi kinerja algoritma, terutama algoritma yang sensitif terhadap jarak, seperti KNN
- Encoding, Mengonversi data kategorikal menjadi format numerik 
    - Karena banyak algoritma machine learning hanya dapat bekerja dengan data numerik. Oleh karena itu, encoding fitur kategorikal (sepert gender) ke format numerik memungkinkan model untuk memproses dan memahami data tersebut.
- Pembagian data (Data Splitting), Membagi data menjadi data latih (train) dan data uji (test)
    - Dengan memisahkan data, kita dapat melatih model dengan data tertentu dan mengujinya pada data yang belum pernah dilihat sebelumnya, untuk mendapatkan gambaran yang lebih realistis tentang seberapa baik model akan bekerja dalam aplikasi nyata.
---

### Menangani Missing Value

Distribusi riwayat merokok responden

![Distribusi Riwayat Merokok](asset/smoking_history_distribution.png)

Dari gambar diatas, terdapat variabel bernama No info yang merupakan missing value, oleh karena itu maka responden dengan riwayat merokok no info dapat di hapus.

![Hapus No Info](asset/smoke_history_delete.png)

### Encoding

Melakukan encoding pada data kategorikal menjadi data numerik agar bisa diterima oleh model machine learning

smoking_history: 0=tidak merokok, 1=merokok
gender: 0=Perempuan, 1=Laki-laik

![Encoding](asset/encoding.png)

### Data Splitting

Melakukan data splitting dengan menggunakan Train-Test-Split

![Train Test Split](asset/diabetes_train_test_split.png)

Menggunakan rasio pembagian data latih uji sebesar 90:10 dikarenakan jumlah dataset yang cukup besar sebesar 63 ribu sampel

![Output Train Test Split](asset/output_train_test_split_diabetes.png)

### Standarisasi
Algoritma machine learning memiliki performa lebih baik dan konvergen lebih cepat ketika dimodelkan pada data dengan skala relatif sama atau mendekati distribusi normal. Proses scaling dan standarisasi membantu untuk membuat fitur data menjadi bentuk yang lebih mudah diolah oleh algoritma. 

StandardScaler melakukan proses standarisasi fitur dengan mengurangkan mean (nilai rata-rata) kemudian membaginya dengan standar deviasi untuk menggeser distribusi.

![Standarisasi Train set](asset/Standarisasi_train_diabetes.png)

Standarisasi dilakukan secara terpisah antar train set dan test set guna menghindari terjadinya kebocoran data (data leak)

![Standarisasi Train set](asset/Standarisasi_test_diabetes.png)

## Modelling

--- 

### Logistic Regression

Logistic regression adalah algoritma klasifikasi berbasis model linear yang memprediksi probabilitas kelas tertentu berdasarkan input fitur. Model ini bekerja dengan menghitung fungsi linear dari fitur, kemudian mengaplikasikan fungsi sigmoid (logistic function) untuk mengonversi hasilnya menjadi probabilitas antara 0 dan 1. Berdasarkan probabilitas tersebut, model kemudian memutuskan apakah input termasuk dalam kelas tertentu (biner) atau kelas yang lebih umum dalam versi multiklas.

Kelebihan
- Sederhana dan Mudah Ditafsirkan: Logistic regression adalah model yang linear, sehingga mudah dipahami dan ditafsirkan. Koefisien dari model ini memberikan wawasan tentang hubungan antara fitur dan probabilitas kelas.
- Efisien secara Komputasi: Logistic regression relatif cepat untuk dilatih, sehingga cocok untuk dataset besar.
- Penanganan yang Baik untuk Data Biner: Sangat efektif untuk masalah klasifikasi biner atau situasi di mana hubungan antara fitur dan output bersifat linear.
- Dukungan untuk Regulasi: Dengan menggunakan regulasi seperti L1 atau L2 (penalty elasticnet), model ini mampu mencegah overfitting dan meningkatkan generalisasi.

Kekurangan
- Kurang Efektif pada Data yang Kompleks dan Non-Linear: Logistic regression tidak cocok untuk data yang memiliki hubungan non-linear antara fitur dan label.
- Terlalu Sederhana untuk Masalah yang Kompleks: Dalam masalah klasifikasi yang kompleks atau multi-kelas, logistic regression mungkin gagal memberikan kinerja yang baik dibandingkan dengan model yang lebih kompleks.
- Sensitif terhadap Outlier: Model ini bisa dipengaruhi oleh outlier pada data, yang dapat menyebabkan hasil yang kurang optimal

Parameter
- solver: Ini adalah algoritma yang digunakan untuk optimasi model. Dalam contoh ini, kita menggunakan 'saga', yang mendukung penalti elasticnet dan dapat menangani dataset besar.
- penalty: Ini menunjukkan jenis regularisasi yang diterapkan untuk mencegah overfitting. 'elasticnet' adalah kombinasi dari regulasi L1 dan L2, yang mengendalikan kompleksitas model.
- l1_ratio: Ini adalah rasio antara L1 dan L2 dalam regularisasi elasticnet. Nilai ini berkisar antara 0 (hanya L2) dan 1 (hanya L1). Dengan menyesuaikan rasio ini, kita dapat mengatur keseimbangan antara kedua jenis regularisasi.
- C: Ini adalah parameter regularisasi yang menentukan seberapa besar penalti yang dikenakan pada koefisien. Nilai yang lebih kecil dari C berarti regularisasi yang lebih kuat, sehingga cenderung membuat model lebih sederhana.

---

### Random Forest
Random forest adalah algoritma berbasis ensemble yang terdiri dari banyak pohon keputusan (decision trees). Setiap pohon dilatih dengan sampel acak dari data dan fitur yang berbeda, menghasilkan model independen yang memprediksi secara terpisah. Hasil prediksi dari setiap pohon kemudian digabungkan dengan metode voting (untuk klasifikasi) atau rata-rata (untuk regresi) untuk mendapatkan prediksi akhir.

Kelebihan
- Kemampuan untuk Menangani Data yang Kompleks: Random forest terdiri dari banyak pohon keputusan (decision trees), sehingga memiliki kemampuan untuk menangkap pola yang kompleks dan interaksi antar fitur.
- Stabil dan Tidak Mudah Overfit: Penggunaan ensemble (kombinasi dari banyak pohon) membuat model lebih stabil dan cenderung tidak overfit, bahkan pada dataset yang besar dan kompleks.
- Dapat Menangani Fitur Tidak Linear: Random forest dapat menangani data yang tidak linear secara alami, sehingga lebih fleksibel dalam berbagai masalah klasifikasi.
- Menyediakan Importance Features: Algoritma ini dapat mengidentifikasi fitur mana yang paling penting, sehingga memudahkan interpretasi.

Kekurangan
- Membutuhkan Sumber Daya Komputasi yang Besar: Random forest membutuhkan lebih banyak waktu dan memori dibanding model linear, terutama pada dataset besar.
- Kurang Efisien untuk Dataset Sangat Besar: Untuk dataset yang sangat besar, model ini bisa lambat saat melakukan prediksi.
- Kurang Mudah untuk Ditafsirkan: Dengan banyaknya pohon yang digunakan, sulit untuk menafsirkan hubungan antara fitur dan output secara langsung.

Parameter
- n_estimators: Jumlah pohon keputusan (decision trees) dalam hutan. Semakin banyak pohon, umumnya semakin baik hasilnya, tetapi waktu komputasi juga akan meningkat.
- max_depth: Kedalaman maksimum dari setiap pohon. Nilai ini mengendalikan kompleksitas model; semakin besar nilai max_depth, semakin kompleks pohonnya, tetapi dapat menyebabkan overfitting.
- min_samples_split: Jumlah minimum sampel yang diperlukan untuk memisahkan sebuah node dalam pohon. Nilai yang lebih tinggi dapat membuat model lebih sederhana dan mencegah overfitting.
- bootstrap: Menentukan apakah pohon-pohon dalam hutan akan dilatih menggunakan sampel bootstrap (diambil secara acak dengan penggantian). Jika True, model mungkin lebih stabil karena variasi antar-pohon lebih besar.

---

### K-Nearest Neighbors

KNN adalah algoritma non-parametrik yang bekerja dengan mencari sejumlah tetangga terdekat (K) dari suatu titik data baru, kemudian menentukan kelas berdasarkan kelas mayoritas dari tetangga tersebut. Algoritma ini beroperasi dengan asumsi bahwa data dengan kelas yang sama akan lebih sering berada berdekatan.

Kelebihan
- Non-parametrik dan Fleksibel: KNN tidak membuat asumsi khusus tentang distribusi data, sehingga dapat bekerja baik pada data yang tidak memiliki pola linear.
- Mudah Dipahami dan Diterapkan: Algoritma ini sangat sederhana, hanya menghitung jarak antara titik data dan tetangganya, sehingga mudah dimengerti.
- Efektif untuk Dataset Kecil: KNN dapat memberikan performa yang baik pada dataset yang lebih kecil dan memiliki cluster yang terdefinisi dengan baik.

Kekurangan
- Lambat pada Dataset Besar: KNN membutuhkan waktu komputasi yang besar untuk mencari tetangga terdekat, terutama jika dataset sangat besar.
- Sensitif terhadap Skala Fitur: Karena bergantung pada perhitungan jarak, fitur dengan skala yang berbeda dapat mempengaruhi kinerja KNN. Oleh karena itu, normalisasi atau standarisasi fitur sering diperlukan.
- Rentan terhadap Outlier: KNN bisa sangat terpengaruh oleh outlier, karena tetangga terdekat dapat mencakup data yang tidak relevan atau noise.

Parameter
- n_neighbors: Jumlah tetangga terdekat yang akan dipertimbangkan dalam klasifikasi. Nilai yang lebih kecil cenderung membuat model lebih sensitif terhadap noise, sementara nilai yang lebih besar membuat model lebih stabil tetapi mungkin kurang presisi.
- weights: Menentukan bobot yang diberikan pada tetangga. 'uniform' berarti semua tetangga diberi bobot yang sama, sedangkan 'distance' memberikan bobot yang lebih besar pada tetangga yang lebih dekat.
- metric: Metode yang digunakan untuk mengukur jarak antara titik data. 'euclidean' adalah jarak biasa (garis lurus), sementara 'manhattan' mengukur jarak dalam grid (jarak absolut). Pilihan jarak yang tepat dapat memengaruhi kinerja model tergantung pada distribusi data.

---

### Hyperparameter Optimization

![Modelling](asset/modelling.png)

GridSearchCV adalah sebuah teknik dalam pemrograman machine learning yang digunakan untuk mencari parameter terbaik (hyperparameter) dari sebuah model secara sistematis. "Grid" mengacu pada pencarian dalam ruang parameter yang lebih besar, sementara "CV" merujuk pada cross-validation.

Parameter
- estimator: Parameter ini menunjukkan model yang akan dilakukan pencarian hyperparameter-nya.
- param_grid: Adalah dictionary yang berisi kombinasi hyperparameter yang ingin dicari
- cv: cross-validation, Cross-validation membantu dalam memvalidasi model agar performanya tidak terlalu bergantung pada pembagian data tertentu, mengurangi risiko overfitting.
- scoring: Menentukan metrik yang akan digunakan untuk mengevaluasi setiap kombinasi hyperparameter
    - AUC adalah metrik yang sering digunakan untuk mengukur performa model klasifikasi; semakin tinggi nilai AUC, semakin baik performa model dalam membedakan antara kelas positif dan negatif.
- n_jobs: Menentukan jumlah core CPU yang akan digunakan untuk menjalankan GridSearchCV, **-1** artinya semua core CPU akan digunakan

---

Kode dibawah berfungsi untuk melakukan training menggunakan beberapa model sesuai yang telah di deklarasikan pada variabel model dan menggunakan parameter - parameter yang telah di deklarasikan di param_grids

Dari GridSearchCV didapatkan model terbaik dan akan dilakukan prediksi. Dari hasil prediksi tersebut nilai akurasi dan F1 Score akan disimpan di dalam dictionary **model_performance**

![Algoritma Modelling](asset/algoritma_modelling.png)

### Evaluation

---

### Metrik yang digunakan

### Akurasi

Akurasi adalah metrik yang menunjukkan proporsi prediksi benar dari keseluruhan prediksi yang dibuat oleh model. Rumus akurasi adalah:

![Rumus Akurasi](asset/akurasi.png)

### F1 Score

F1 Score adalah metrik yang menggabungkan presisi (precision) dan recall, dan lebih tepat untuk data yang tidak seimbang. Rumus F1 Score adalah:

![F1 Score](asset/F1_score.png)

- Presisi menunjukkan proporsi prediksi positif yang benar-benar positif. Ini berguna saat kita ingin meminimalkan jumlah prediksi positif yang salah.
- Recall menunjukkan proporsi data aktual positif yang berhasil diprediksi dengan benar oleh model. Ini berguna saat penting untuk menangkap semua data positif.

![Hasil Evaluasi](asset/evaluasi.png)
![Hasil Evaluasi](asset/Grafik.png)

## Kesimpulan

1. Dari seluruh responden, 18% di antaranya mengidap penyakit diabetes, menunjukkan proporsi signifikan dari populasi yang terkena dampak.

2. Terdapat perbedaan tingkat prevalensi diabetes antara jenis kelamin, di mana perempuan memiliki prevalensi lebih tinggi (52,4%) dibandingkan laki-laki (47,6%).

3. Faktor-faktor yang mempengaruhi seseorang untuk mengidap diabetes meliputi level HbA1c, kadar glukosa dalam darah, indeks massa tubuh (BMI), usia, hipertensi, dan riwayat penyakit jantung. Faktor-faktor ini berkontribusi signifikan terhadap risiko diabetes.

4. Berdasarkan pengujian tiga model machine learning—Logistic Regression, Random Forest, dan K-Nearest Neighbors—untuk mendeteksi diabetes, model Random Forest menunjukkan akurasi tertinggi, menjadikannya model terbaik untuk memprediksi penyakit diabetes pada responden dalam dataset ini.




