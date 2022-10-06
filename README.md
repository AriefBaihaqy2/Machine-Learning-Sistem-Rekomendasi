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
   Pada tahap ini akan menghitung derajat kesamaan (similarity degree) antar judul buku dengan teknik cosine similarity, selanjutnya melihat matriks kesamaan setiap buku dengan menampilkan judul buku dalam 10 sampel kolom (axis=1) dan 10 sampel baris (axis=0) yang dapat dilihat pada Gambar 1.
   
   ![image](https://user-images.githubusercontent.com/110958395/194273397-ba6be757-34ec-4e59-bdb6-701c4ccee4c0.png)
   
   Gambar 1. Matriks Cosine Similarity






















Dalam  mengembangkan model machine learning pada proyek ini digunakan 3 algoritma, yang kemudian akan dievaluasi performa dari masing-masing algoritma dan menentukan salah satu algoritma yang memiliki hasil terbaik dan dengan nilai error yang paling kecil. Ketiga algoritma yang akan digunakan, antara lain:

-	K-Nearest Neighbor (KNN)

    Pada algortima ini menggunakan kesamaan fitur untuk memprediksi nilai dari setiap data yang baru. KNN bekerja     dengan membandingkan jarak satu sampel ke sampel pelatihan lain dengan memilih sejumlah k tetangga terdekat. Dalam pemilihan k harus hati-hati karena apabila memilih k yang terlalu rendah, maka akan menghasilkan model yang overfit dan hasil dari prediksinya akan memiliki varians yang tinggi. Dan jika memilih k yang terlalu tinggi, maka akan menghasilkan model yang underfitt dan hasil dari prediksinya akan memiliki bias yang tinggi. Kelebihan dari algoritma KNN ini relatif sederhana dibandingkan dengan algoritma lain, mudah dipahami dan digunakan. Algoritma KNN memiliki kekurangan jika dihadapkan pada jumlah fitur atau dimensi besar yang biasa disebut curse of dimensionality. Dalam melakukan pemodelan pada proyek ini didapatkan hasil akurasi data latih sebesar 0.830. Adapun parameter dan nilai yang digunakan dalam melakukan pemodelan pada algoritma ini yaitu:
    
    - n_neighbors = 8
      
      Parameter n_neighbors digunakan untuk menentukan jumlah tetangga terdekat (dengan k adalah sebuah angka positif).

-	Random Forest 

    Algoritma Random Forest adalah salah satu algoritma supervised learning. Algoritma ini disusun dari banyak    algoritma pohon (decision tree) yang pembagian data dan fiturnya dipilih secara acak. Kelebihan dari algoritma Random Forest adalah algoritma ini sering digunakan karena cukup sederhana tetapi memiliki stabilitas yang mumpuni, dan algoritma ini termasuk kedalam kategori ensemble (group) learning yang merupakan model prediksi yang terdiri dari beberapa model dan bekerja secara bersama-sama, sehingga tingkat keberhasilan akan lebih tinggi dibanding model yang bekerja sendirian. Algoritma Random Forest ini memiliki kekurangan dalam menentukan nilai parameternya harus benar-benar tepat untuk data. Dalam melakukan pemodelan pada proyek ini didapatkan hasil akurasi data latih sebesar 0.992. Adapun parameter dan nilai yang digunakan dalam melakukan pemodelan pada algoritma ini yaitu:
    
    - n_estimators = 50 
      
      Parameter n_estimators digunakan untuk menentukan jumlah pohon di forest.
      
    - max_depth = 8
    
      Parameter max_depth digunakan untuk menentukan kedalaman atau panjang pohon. Merupakan ukuran seberapa banyak pohon dapat membelah (splitting) untuk membagi setiap node kedalam jumlah pengamatan yang diinginkan.
      
    - random_state = 33
    
      Parameter random_state digunakan untuk mengontrol random number generator yang digunakan.
      
    - n_jobs = -1 
      
      Parameter n_jobs digunakan untuk menentukan jumlah job (pekerjaan) yang digunakan secara paralel. Merupakan komponen untuk mengontrol thread atau proses yang berjalan secara paralel.

-	Boosting Algorithm

    Boosting juga merupakan metode ensemble learning, perbedaannya dengan model Random Forest adalah model dilatih secara berurutan atau dalam proses yang iteratif. Algoritma yang menggunaakn teknik boosting bertugas memperbaiki kesalahan dari model pertama yang telah dibuat. Kelebihan dari algoritma ini adalah algoritma ini berfungsi untuk meningkatkan performa atau akurasi prediksi dengan cara menggabungkan beberapa model sederhana dan dianggap lemah sehingga membentuk suatu model yang kuat. Dalam melakukan pemodelan pada proyek ini didapatkan hasil akurasi data latih sebesar 0.851. Adapun parameter dan nilai yang digunakan dalam melakukan pemodelan pada algoritma ini yaitu:
    
    - learning_rate = 0.05
      
      Bobot yang diterapkan pada setiap regressor di masing-masing proses iterasi boosting.
      
    - n_estimators = 150
      
      Parameter n_estimators digunakan untuk memperkuat kontribusi pada setiap regresor.
      
    - random_state = 55
      
      Parameter random_state digunakan untuk mengontrol random number generator yang digunakan.
      
Sehingga dalam pembuatan model machine learning pada proyek ini performa terbaik ditunjukkan oleh algoritma Random Forest yang memiliki hasil akurasi sebesar 0.992.


## Evaluation

Metrik yang akan digunakan pada prediksi ini adalah MSE atau Mean Squared Error yang menghitung jumlah selisih kuadrat rata-rata nilai sebenarnya dengan nilai prediksi. MSE didefinisikan dalam persamaan yang dapat dilihat pada Gambar 9:

![13  image](https://user-images.githubusercontent.com/110958395/192091611-00955e63-4b7f-404c-8196-becad93dc8f0.png)

Gambar 9. Persamaan MSE.

Berdasarkan Gambar 9. Keterangan yang ada dalam persamaan MSE yaitu:

N = jumlah dataset

yi = nilai sebenarnya

y_pred = nilai prediksi

- Tabel 5. Hasil evaluasi MSE pada data latih dan data test adalah sebagai berikut:
    
  |          | train        | test         |
  |----------|--------------|--------------| 
  | KNN      | 22882.422789 | 28096.473822 |
  | RF       | 677.232434   | 1202.718556  |
  | Boosting | 23968.08805	| 24587.114802 |

- Hasil evaluasi plot metrik MSE dengan bar chart dapat dilihat pada Gambar 10:

    ![15  image](https://user-images.githubusercontent.com/110958395/192092719-39d3707d-1026-460e-9218-b1d1fc477fec.png)
    
    Gambar 10. Plot metrik MSE.

    Berdasarkan Gambar 10. Terlihat bahwa algoritma model Random Forest (RF) memiliki hasil yang paling baik dibandingkan dengan algoritma model Boosting dan KNN. Hal ini ditunjukkan karena hasil pengujian model Random Forest memiliki nilai error terkecil dibandingkan dengan dua algoritma lainnya yang memiliki angka error yang besar diatas 20.000.

- Tabel 6. Membuat prediksi dari data uji untuk melakukan pengujian:

    |          | y_true	| prediksi_KNN | prediksi_RF | prediksi_Boosting |
    |----------|--------|--------------|-------------|-------------------| 
    | 3821      | 14000 | 14875.0      | 13911.1	   | 15402.5           |

    Terlihat pada Tabel 6, bahwa prediksi dengan algoritma Random Forest (RF) pada kolom "prediksi_RF" memberikan nilai yang paling mendekati dengan nilai pada kolom "y_true".
    
 ## Referensi
[1] Putri Choirunisa (2020). Implementasi Artificial Inteligence untuk Memprediksi Harga Penjualan Rumah Menggunakan Metode Random Forest dan Flask (Studi kasus: Rohini, India). https://dspace.uii.ac.id/handle/123456789/29813 
