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

## Deskripsi Statistik
---
![Statistik!](/assets/laporan1_statistik.png")

