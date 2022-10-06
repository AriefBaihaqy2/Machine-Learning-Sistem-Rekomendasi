# Laporan Proyek Machine Learning - Imam Arief Al Baihaqy

## Project Overview

Sistem rekomendasi buku merupakan sistem yang merekomendasikan buku kepda pengguna. Sistem rekomendasi yang dibuat ini berdasarkan dengan preferensi kesukaan pengguna pada masa lalu dan rating dari buku yang ada.
Dengan adanya sistem rekomendasi ini akan bermanfaat untuk meningkatkan keuntungan dari pembelian barang yang berupa buku atau juga bisa diterapkan pada perpustakaan agar pengguna mendapatkan rekomendasi buku yang sesuai dengan minatnya sehingga dapat menentukan pilihan dan dapat meningkatkan minat baca pangguna. 
 
## Business Understanding

### Problem Statements

- Bagaimana cara merekomendasikan buku yang mirip dengan buku yang disukai pengguna di masa lalu?
- Bagaimana cara merekomendasikan buku yang mungkin disukai pengguna berdasarkan preferensi pengguna lain?

### Goals

- Menghasilkan sejumlah rekomendasi buku yang mirip dengan buku yang disukai pengguna di masa lalu dengan teknik algoritma *Content Based Filtering*.
- Menghasilkan sejumlah rekomendasi buku yang belum pernah dibaca sebelumnya dan mungkin disukai pengguna berdasarkan preferensi pengguna lain dengan teknik algoritma *Collaborative Filtering*.


### Solution statements

Solusi yang dibuat yaitu dengan menggunakan 2 algoritma sistem rekomendasi pada Machine Learning. Adapun kedua algoritma tersebut yaitu:

- Content Based Filtering 

  *Content Based Filtering* mempelajari profil minat pengguna baru berdasarkan data dari objek yang telah dinilai pengguna. Algoritma ini bekerja dengan menyarankan konten/item serupa yang pernah disukai di masa lalu atau sedang dilihat di masa kini kepada pengguna. Semakin banyak informasi yang diberikan pengguna, semakin baik akurasi sistem rekomendasi. Algortima ini akan digunakan untuk merekomendasikan buku yang akan dibaca berdasarkan buku lain yang pernah dibaca pengguna di masa lalu.
    
- Collaborative Filtering

  *Collaborative Filtering* bergantung pada pendapat komunitas pengguna. Algoritma ini tidak memerlukan atribut untuk setiap itemnya seperti pada sistem berbasis konten (*Content Based Filtering *). Algoritma ini digunakan untuk merekomendasikan buku kepada pengguna berdasarkan nilai rating buku tertinggi.


## Data Understanding

Dataset yang digunakan pada proyek ini adalah dataset *Book Recommendation Dataset* yang didapat dari situs [Kaggle](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset). Pada dataset ini terdapat 3 berkas beformat csv yaitu: Books, Ratings, dan Users. Dari ketiga berkas tersebut akan dibuat variabel untuk memuat berbagai fitur didalamnya.


## Exploratory Data Analysis - Univariate Analysis

Variabel-variabel pada *Book Recommendation Dataset* adalah sebagai berikut:

1. **Variabel Books**

   Merupakan informasi seputar buku yang didalamnya terdapat fitur: judul buku, penulis buku, tahun publikasi buku, dan penerbit.

   Tabel 1. Mengecek informasi pada variabel Books:

   | Column              | Non-Null Count  | Dtype  |
   |---------------------|-----------------|--------|
   | ISBN                | 271360 non-null | object |
   | Book-Title          | 271360 non-null | object |
   | Book-Author         | 271359 non-null | object |
   | Year-Of-Publication | 271360 non-null | object |
   | Publisher           | 271358 non-null | object |
   | Image-URL-S         | 271360 non-null | object |
   | Image-URL-M         | 271360 non-null | object |
   | Image-URL-L         | 271357 non-null | object |

   Berdasarkan Tabel 1, dapat diketahui bahwa variabel Books memiliki kurang lebih 271359 entri. Terdapat 8 kolom disini, yaitu:

   - ISBN (International Standard Book Number) adalah kode pengidentifikasian buku.
   - Book-Title merupakan judul buku.
   - Book-Author merupakan nama dari penulis buku.
   - Year-Of-Publication merupakan tahun publikasi buku.
   - Publisher merupakan pihak yang menerbitkan buku.
   - Image-URL-S merupakan tautan dalam skala kecil (small).
   - Image-URL-M merupakan tautan dalam skala sedang (medium).
   - Image-URL-L merupakan tautan dalam skala besar (large).

2. **Variabel Ratings**

   Berisi informasi penilaian terhadap buku. Penilaian (Book-Rating) bersifat eksplisit, dinyatakan dalam skala 1-10 (semakin tinggi nilai menunjukkan apresiasi yang lebih tinggi), atau implisit, yang dinyatakan dengan 0.

   Tabel 2. Mengecek informasi pada variabel Ratings:

   | Column      | Non-Null Count   | Dtype  |
   |-------------|------------------|--------|
   | User-ID     | 1149780 non-null | int64  |
   | ISBN        | 1149780 non-null | object |
   | Book-Rating | 1149780 non-null | int64  |

   Berdasarkan Tabel 2, dapat diketahui bahwa variabel Ratings memiliki banyak entri yaitu 1.149.780 entri. Trrdapat 3 kolom disini, yaitu:

   - User-ID merupakan identitas pengguna.
   - ISBN merupakan kode pengidentifikasian buku.
   - Book-Rating metupakan informasi penilaian buku .

   Tabel 3. Melihat distribusi rating pada variabel Ratings:

   |       | User-ID        | Book-Rating    |
   |-------|----------------|----------------|
   | count | 1149780.000000 | 1149780.000000 |
   | mean  | 140386.395126	 | 2.866950       |
   | std   | 80562.277719	  |  3.854184      |
   | min   | 2.000000	      | 0.000000       |
   | 25%   | 70345.000000   | 0.000000       |
   | 50%   | 141010.000000	 | 0.000000       |
   | 75%   | 211028.000000	 | 7.000000       |
   | max   | 278854.000000	 | 10.000000      |

   Berdasarkan Tabel 3, dapat diketahui bahwa nilai maksimum Book-Rating adalah 10 dan nilai minimumnya adalah 0.
   
3. **Variabel Users**
   
   Berisi informasi seputar data pengguna yang didalamnya terdapat fitur: ID user, lokasi, dan umur.
   
   Tabel 4. Mengecek informasi pada variabel Users:
   
   | Column   | Non-Null Count  | Dtype  |
   |----------|-----------------|--------|
   | User-ID  | 278858 non-null | int64  |
   | Location | 278858 non-null | object |
   | Age      | 168096 non-null | float  |
   
Variabel yang akan di eksplorasi pada proyek ini adalah variabel Books dan Ratings. Sedangkan, variabel Users hanya digunakan untuk melihat bagaimana profile penguna saja.


## Data Preprocessing
Dapat dilihat sebelumnya pada bagian Exploratory Data Analysis bahwa sangat banyak entri pada masing-masing variabel, contohnya pada Variabel Ratings memiliki hingga 1.149.780 entri, dengan banyaknya entri akan memakan banyak penggunaan backend RAM gratis pada google colab, sehingga entri pada masing-masing variabel akan dikurangi menjadi 50.000 entri saja. Kemudian melakukan proses penggabungan data berkas berdasarkan fitur-fitur yang memiliki keterkaitan. Langkah selanjutnya adalah menghapus fitur pada variabel Books yaitu: Image-URL-S, Image-URL-M, dan Image-URL-L. Karena ketiga fitur tersebut tidak akan digunakan dan tidak memiliki pengaruh terhadap perekomendasian buku.


## Data Preparation Model Content Based Filtering

1. Mengatasi Missing Value

   Tabel 5. Mengecek missing value setelah proses penggabungan

   | Column              |      |
   |---------------------|------|
   | User-ID             | 0    |
   | ISBN                | 0    |
   | Book-Rating         | 0    |
   | Book-Title          | 5287 |
   | Book-Author         | 5287 |
   | Year-Of-Publication | 5287 |
   | Publisher           | 5287 |

   Berdasarkan Tabel 5, dapat diketahui terdapat 5287 dari 20963 missing value pada kolom Book-Title (judul buku), Book-Author (penulis), Year-Of-Publication (tahun publikasi buku), dan Publisher (penerbit). Maka data yang memiliki missing value ini akan dihapus agar pembuatan model akan menjadi lebih baik dan dapat meningkatkan performa model.

2. Menghapus data duplikat
   Menghapus data duplikat perlu dilakukan karena hanya akan digunakan data unik untuk dimasukkan ke dalam proses pemodelan. Oleh karena itu, perlu menghapus data yang duplikat. Dalam hal ini, kolom ISBN yang duplikat akan dibuang.
    
3. Langkah selanjutnya adalah melakukan konversi data series menjadi list untuk kemudian membuat dictionary untuk menentukan pasangan key-value pada data yang telah dikonversi menjadi list sebelumnya.


## Model Development dengan Content Based Filtering

Adapun langkah-langkah yang digunakan dalam pengembangan model dengan Content Based Filtering yaitu:

1. **TF-IDF Vectorizer**

   Pada tahap ini, membangun sistem rekomendasi sederhana berdasarkan judul buku yang tersedia menggunakan TF-IDF Vectorizer, selanjutnya melakukan fit pada judul buku dan ditransfotmasikan kedalam bentuk matriks yang kemudian menghasilkan vektor tf-idf dalam bentuk matriks.
   
2. **Cosine Similarity**

   Pada tahap ini akan menghitung derajat kesamaan (similarity degree) antar judul buku dengan teknik cosine similarity, selanjutnya melihat matriks kesamaan setiap judul buku dengan menampilkan judul buku dalam 10 sampel kolom (axis=1) dan 10 sampel baris (axis=0) yang dapat dilihat pada Gambar 1.
   
   ![image](https://user-images.githubusercontent.com/110958395/194380685-ffb489f4-d9d0-40b4-86dd-1cff1e28f16f.png)
   
   Gambar 1. Matriks Cosine Similarity
   
   Berdasarkan Gambar 1, dapat diketahui angka yang memiliki nilai lebih dari 0 mengindikasikan kemiripan judul buku. Dalam hal ini judul buku pada kolom X (horizontal) memiliki kemiripan dengan judul buku pada baris Y (vertikal). Sebagai contoh, buku dengan judul Resurrection Men (Inspector Rebus S.) teridentifikasi mirip dengan buku berjudul Wednesday's Child: An Inspector Banks Mystery.

3. **Mendapatkan Rekomendasi**
   
   Pada tahap ini akan menghasilkan sejumlah buku yang akan direkomendasikan kepada pengguna dengan keluaran sistem rekomendasi buku berupa top-N recommendaation, oleh karena itu sistem akan memberikan sejumlah rekomendasi buku pada pengguna. Sebagai contoh, pengguna X pernah membaca buku yang berjudul Resurrection Men (Inspector Rebus S.). Kemudian, saat pengguna tersebut berencana untuk membaca buku lain, sistem akan merekomendasikan buku lain yang memiliki kemiripan dengan buku yang sebelumnya pernah dibaca oleh pengguna. Rekomendasi kedua buku ini berdasarkan kesamaan yang dihitung dengan cosine similarity pada tahap sebelumnya.
   
## Evaluasi Content Based Filtering

Adapun langkah yang digunakan untuk mendapatkan rekomendasi yaitu dengan menggunakan Top-N Recommendation untuk mengambil k dengan nilai similarity terbesar pada index matrix yang diberikan. Langkah pertama yaitu mengambil data dengan menggunakan argpartition untuk melakukan partisi secara tidak langsung sepanjang sumbu yang diberikan yang kemudian dataframe akan diubah menjadi numpy, dengan menggunakan argpartition di ambil sejumlah nilai k tertinggi dari similarity, dalam kasus ini digunakan dataframe cosine similarity, Kemudian, mengambil data dari bobot (tingkat kesamaan) tertinggi ke terendah, kemudian menghapus judul buku agar nantinya output data judul buku yang dicari tidak muncul pada daftar rekomendasi buku.

Pada kasus ini, dilakukan uji coba untuk mencari judul buku yang mirip dengan buku yang berjudul Waking Up Screaming: Haunting Tales of Terror.

![Screenshot 2022-10-07 003703](https://user-images.githubusercontent.com/110958395/194398408-11b7599c-ab18-418a-abfb-ef559e0a49a7.jpg)

Gambar 2. Hasil Rekomendasi Buku

Berdasarkan Gambar 2, dapat diketahui bahwa dari 10 buku yang direkomendasikan memiliki kemiripan dengan buku yang berjudul Waking Up Screaming: Haunting Tales of Terror. Dalam hal ini juga dapat diketahui dari 10 buku yang direkomendasikan, terdapat 8 buku yang relevan, jadi dapat disimpulkan precision pada sistem ini sebesar 80% yang mengacu pada rumus berikut:

![image](https://user-images.githubusercontent.com/110958395/194400379-df1a09ee-72d7-461b-a1aa-99440a3f1fd0.png)

Gambar 3. Rumus Recommender System Precision



## Model Development dengan Collaborative Filtering

Adapun langkah-langkah yang digunakan dalam pengembangan model dengan Collaborative Filtering yaitu:

1. **Data Preparation Model Collaborative Filtering**
   
   Tahap pertama dalam melakukan persiapan sebelum melakukan pemodelan adalah melakukan persiapan data Ratings untuk menyandikan (encode) fitur User-ID dan ISBN kedalam indeks integer, kemudian memetakan User-ID dan ISBN ke dataframe yang berkaitan, dan terakhir mengecek beberapa hal dalam data seperti jumlah user, jumlah buku, dan mengubah nilai rating menjadi float.

2. **Membagi Data untuk Training dan Validasi**
   
   Sebelum melakukan pelatihan model tahapan yang harus diselesaikan yaitu mengacak data Ratings terlebih dahulu agar pendistribusiannya menjadi random, kemudian dilanjutkan dengan memetakan (mapping) data user dan buku menjadi satu value terlebih dahulu, lalu membuat rating dalam skala 0 sampai 1 agar mudah dalam melakukan proses training, agar nantinya data akan siap untuk dimasukkan ke dalam model, dan terakhir melakukan split data untuk membagi data menjadi 80% data train dan 20% data validasi.

3. **Proses Training**
   
   Pada tahap ini, model menghitung skor kecocokan antara pengguna dan buku dengan teknik embedding menggunakan class RecommenderNet. Pertama, melakukan proses embedding terhadap data user dan buku. Selanjutnya, melakukan operasi perkalian dot product antara embedding user dan buku. Selain itu, juga menambahkan bias untuk setiap user dan buku. Skor kecocokan ditetapkan dalam skala [0,1] dengan fungsi aktivasi sigmoid. Selanjutnya, melakukan proses compile terhadap model. Model ini menggunakan Binary Crossentropy untuk menghitung loss function, Adam (Adaptive Moment Estimation) sebagai optimizer, dan root mean squared error (RMSE) sebagai metrics evaluation.


## Evaluasi Collaborative Filtering

Adapun metrik evaluasi yang digunakan pada model Collaborative Filtering adalah Root Mean Squared Error (RMSE). Metode pengukuran ini berfungsi sebagai perkiraan nilai yang diamati dengan mengukur perbedaan nilai prediksi model. Root Mean Squared Error adalah hasil dari akar kuadrat dari Mean Squared Error. Keakuratan metode estimasi kesalahan pengukuran diwakili oleh nilai RMSE yang kecil. Semakin kecil (mendekati 0) nilai RMSE maka hasil prediksi akan semakin akurat. Rumus metrik RMSE ditunjukkan pada gambar berikut:

![image](https://user-images.githubusercontent.com/110958395/194405920-410f2583-fadc-41cb-9429-f20bf2306a78.png)

Gambar 4. Rumus Metrik RMSE

Berdasarkan Gambar 4, keterangan yang ada pada persamaan RMSE yaitu:

n => Jumlah data

i => Urutan Data

ŷ => Nilai hasil prediksi

y => Nilai hasil observasi

Melihat visualisasi proses training plot metrik evaluasi RMSE dengan matplotlib.

![image](https://user-images.githubusercontent.com/110958395/194392406-db867519-a312-4242-ab83-9c9b4f2f505e.png)

Gambar 5. Visualisasi plot metrik evaluasi RMSE

Berdasarkan Gambar 5, dapat diketahui proses training model cukup smooth pada epochs sekitar 25. Dari proses ini, diperoleh nilai error akhir sebesar sekitar 0.12 dan error pada data validasi sebesar 0.23. Nilai tersebut cukup bagus untuk sebuah sistem rekomendasi.


## Mendapatkan Rekomendasi Buku

Untuk mendapatkan rekomendasi buku, pertama mengambil sampel user secara acak dan mendefinisikan variabel books_unreaded yang merupakan daftar buku yang belum pernah dibaca oleh pengguna, books_unreaded inilah yang akan menjadi buku yang direkomendasikan kepada pengguna. Sebelumnya, pengguna telah memberi rating pada beberapa buku yang telah mereka baca. Rating ini digunakan untuk membuat rekomendasi buku yang mungkin cocok untuk pengguna. Buku yang akan direkomendasikan tentulah buku yang belum pernah dibaca oleh pengguna.

![image](https://user-images.githubusercontent.com/110958395/194392908-f688e1c7-95a5-427c-a208-5a5a90e8c0b2.png)

Gambar 6. Hasil Top 10 Recommendation

Berdasarkan Gambar 6 merupakan rekomendasi untuk user dengan id 8872. Dari output tersebut, dapat melakukan perbandingan antara Books with high ratings from user dan Top 10 Books recommendation untuk user.

    
## Referensi

[1] Reyvan Maulid (2022). *Kriteria Jenis Teknik Analisis Data dalam Forecasting. Diambil dari: https://www.dqlab.id/kriteria-jenis-teknik-analisis-data-dalam-forecasting*. Diakses tanggal 06 Oktober 2022.

[1] Putri Choirunisa (2020). Implementasi Artificial Inteligence untuk Memprediksi Harga Penjualan Rumah Menggunakan Metode Random Forest dan Flask (Studi kasus: Rohini, India). https://dspace.uii.ac.id/handle/123456789/29813
