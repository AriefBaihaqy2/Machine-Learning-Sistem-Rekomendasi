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










Tabel 2. Mengecek deskripsi statistik data:

|       | BHK         | Rent         | Size        | Bathroom    |
|-------|-------------|--------------|-------------|-------------| 
| count | 4746.000000 | 4.746000e+03 | 4746.000000 | 4746.000000 |
| mean  | 2.083860    | 3.499345e+04 | 967.490729	 | 1.965866    |
| std   | 0.832256    | 7.810641e+04 | 634.202328	 | 0.884532    |
| min   | 1.000000    | 1.200000e+03 | 10.000000	 | 1.000000    |
| 25%   | 2.000000    | 1.000000e+04 | 550.000000  | 1.000000    |
| 50%   | 2.000000    | 1.600000e+04 | 850.000000	 | 2.000000    |
| 75%   | 3.000000    | 3.300000e+04 | 1200.000000 | 2.000000    |
| max   | 6.000000    | 3.500000e+06 | 8000.000000 | 10.000000   |

Berdasarkan Tabel 2, fungsi terdapat informasi statistik pada masing-masing kolom, antara lain:

- Count  adalah jumlah sampel pada data.
- Mean adalah nilai rata-rata.
- Std adalah standar deviasi.
- Min yaitu nilai minimum setiap kolom. 
- 25% adalah kuartil pertama. Kuartil adalah nilai yang menandai batas interval dalam empat bagian sebaran yang sama. 
- 50% adalah kuartil kedua, atau biasa juga disebut median (nilai tengah).
- 75% adalah kuartil ketiga.
- Max adalah nilai maksimum.

Dapat diketahui tidak ada nilai 0 pada nilai minimum, sehingga dapat dikatakan tidak ada missing value pada dataset.


## Exploratory Data Analysis - Menangani Outliers

Terdapat beberapa outliers pada dataset, seperti contoh pada fitur Size yang divisualisasikan dengan boxplot dapat dilihat pada Gambar 1.

![3  Screenshot 2022-09-23 214955](https://user-images.githubusercontent.com/110958395/191991680-9a345ce6-74c5-4ba2-919a-be7534959c75.jpg)

Gambar 1. Outliers fitur Size.

Pada Gambar 1. Dalam menangani outliers digunakan metode IQR dengan membuat batas bawah dan batas atas dengan persamaan:

Batas bawah = Q1 - 1.5 * IQR

Batas atas  = Q3 + 1.5 * IQR

Kemudian persamaan tersebut diterapkan untuk menangani outliers yang dapat dilihat pada Gambar 2:

![4  Screenshot 2022-09-23 215017](https://user-images.githubusercontent.com/110958395/191989306-b63dfcc3-fe95-430c-958a-4a0cedb726c8.jpg)

Gambar 2. Hasil penanganan outliers.


## Exploratory Data Analysis - Univariate Analysis

Tabel 3. Mengecek nilai sample pada fitur Area Type:

|             | BHK         | Rent         | Size        | Bathroom    |
|-------------|-------------|--------------|-------------|-------------|
| Area Type   |             |              |             |             |
| Built Area  | 2           | 2            | 2           | 2           |
| Carpet Area | 1799        | 1799         | 1799        | 1799        |
| Super Area  | 2330        | 2330         | 2330        | 2330        |

Dari Tabel 3, diketahui jumlah sample pada baris Built Area di fitur Area Type hanya memliki 2 sample, maka sample Built Area akan dihapus karena memiliki sample yang terlalu sedikit.

Tabel 4. Mengecek nilai unique length pada masing-masing fitur:

| Feature            | Unique Length |
|--------------------|---------------|
| Floor              | 332           |
| Area Type          | 2             |
| Area Locality      | 1971          |
| City               | 6             | 
| Furnishing Status  | 3             |
| Tenant Preferred   | 3             |

Berdasarkan Tabel 4, dapat dilihat bahwa fitur Floor dan Area Locality memiliki nilai unique yang terlalu banyak, maka kedua fitur ini akan dihapus karena nilai unique yang terlalu banyak jika dibandingkan dengan fitur yang lain.

### Categorical Features

**Fitur Area Type**

![7  Screenshot 2022-09-23 224118](https://user-images.githubusercontent.com/110958395/192000297-d088a9ca-67d8-495f-b2a9-78fd38c9470c.jpg)

Gambar 3. Fitur Area Type.

Berdasarkan Gambar 3. Terdapat 2 kategori pada fitur Area Type, secara berurutan dari yang paling banyak yaitu: Super Area, dan Carpet Area. Dari data persentase dapat disimpulkan bahwa lebih dari 50% sampel merupakan rumah tipe grade tinggi, yaitu Super Area.

**Fitur City**

![8  Screenshot 2022-09-23 224212](https://user-images.githubusercontent.com/110958395/192000311-5aa7de96-795b-4e73-abbe-10b93e6f01cf.jpg)

Gambar 4. Fitur City.

Berdasarkan Gambar 4. Urutan kategori letak rumah/apartemen/rumah susun di kota yang paling sedikit ke yang paling banyak adalah Kolkata, Delhi, Mumbai, Hyderabad, Chennai, dan Bangalore. Dari grafik diatas dapat disimpulkan bahwa sebagian besar letak rumah/apartemen/rumah susun dari yang paling banyak berada pada kota Bangalore, Chennai, dan Hyderadab.

**Fitur Furnishing Status**

![9  Screenshot 2022-09-23 224237](https://user-images.githubusercontent.com/110958395/192000341-5bbc9661-7d8a-4435-b713-bd618f14da48.jpg)

Gambar 5. Fitur Funishing Status.

Berdasarkan Gambar 5. Fitur Furnishing Status terdiri dari 3 kategori dari yang paling sedikit ke yang paling banyak, yaitu: Furnished (ada perabotan), Unfurnished (tidak ada perabotan), Semi-Furnished (sedikit perabotan). Dapat disimpulkan bahwa rumah/apartemen/rumah susun lebih banyak yang memiliki sedikit perabotan dan tidak ada perabotan.

### Numerical Features

Menampilkan histogram pada masing-masing numerical features dapat dilihat pada Gambar 6:

![10  Screenshot 2022-09-23 225735](https://user-images.githubusercontent.com/110958395/192003012-8d103698-591b-451b-bf6f-b22bc58d5d25.jpg)

Gambar 6. Univariate numerical features.

Berdasarkan Gambar 6. Dapat disimpulkan bahwa:

- Rumah/apartemen/rumah susun memiliki 1 hingga 3 kamar tidur, aula, dan dapur, namun sebagian besar memiliki 2 kamar tidur, aula, dan dapur.
- Rumah/apartemen/rumah susun memiliki ukuran dibawah 2100 (ft<sup>2</sup>), namun sebagian besar memiliki ukuran diantara 500 (ft<sup>2</sup>) hingga 1200 (ft<sup>2</sup>).
- Rumah/apartemen/rumah susun memiliki 1 hingga 3 kamar mandi, namun sebagian besar memiliki 2 kamar mandi.

## Exploratory Data Analysis - Multivariate Analysis

### Categorical Features

Mengecek rata-rata sewa rumah/apartemen/rumah susun terhadap masing-masing fitur untuk mengetahui pengaruh fitur kategori terhadap sewa rumah/apartemen/rumah susun:

![11  Screenshot 2022-09-23 232225](https://user-images.githubusercontent.com/110958395/192007445-9c15382e-64c1-4134-a212-55f985c39045.jpg)

Gambar 7. Multivariate categorical features.

Berdasarkan Gambar 7. Dapat disimpulkan bahwa:

- Pada fitur Area Type, rata-rata sewa berada antara 3000 hingga 3300. Tipe grade tertinggi yaitu Super Area memiliki sewa yang rendah jika dibandingkan dengan sewa tipe grade dibawahnya yaitu Carpet Area. Dalam hal ini fitur Area Type memiliki pengaruh yang kecil.
- Pada fitur City, rata-rata sewa berada antara 1100 hingga 3600. Kota Bangalore, Chennai, dan hyderabad memiliki sewa yang rendah jika dibandingkan dengan sewa kota Mumbai. Dalam hal ini fitur City memiliki pangaruh yang cukup besar.
- Pada fitur Furnishing Status, rata-rata sewa berada antara 1600 hingga 2300. rumah/apartemen.rumah susun Semi-Furnished dan Unfurnished memiliki sewa yang rendah jika dibandingkan dengan sewa rumah/apartemen/rumah susun yang Furnished. Dalam hal ini fitur Furnishing Status memiliki pengaruh yang cukup besar.
- Pada Fitur Tenant Preferred, rata-rata sewa berada antara 1700 hingga 2400. Dari grafik dapat dilihat bahawa Family yang menyarankan sewa memiliki sewa yang paling tinggi dibandingkan dengan yang lain. Dalam hal ini fitur Tenant Preferred memiliki pengaruh yang cukup lumayan besar.

### Numerical Features

Menampilkan kolerasi antar fitur numerical dapat dilihat pada Gambar 8:

![12  Screenshot 2022-09-23 235352](https://user-images.githubusercontent.com/110958395/192013443-da1ce461-edff-4fc8-86a3-1b7843117d67.jpg)

Gambar 8. Multivariate numerical features.

Berdasarkan Gambar 8. Koefisien korelasi berkisar antara -1 dan +1. Ia mengukur kekuatan hubungan antara dua variabel serta arahnya (positif atau negatif). Mengenai kekuatan hubungan antar variabel, semakin dekat nilainya ke 1 atau -1, korelasinya semakin kuat. Sedangkan, semakin dekat nilainya ke 0, korelasinya semakin lemah. Dapat dilihat kolerasi pada Fitur BHK dan Bathroom berkolerasi dengan fitur Size dengan cukup baik.

## Data Preparation

1. Encoding Fitur Kategori

    Proses encoding fitur categorical menggunakan teknik one-hot-encoding dalam penerapannya untuk mendapatkan fitur  baru yang sesuai sehingga dapat mewakili variabel categorical. Dalam hal ini terdapat fitur categorical yaitu: Area Type, City, Furnishing Status, dan Tenant Preferred yang kemudian akan diubah menjadi numerical features.

2. Reduksi Dimensi dengan PCA

    Teknik Principal Component Analysis (PCA) digunakan untuk mereduksi dimensi/mengurangi jumlah fitur dengan tetap  mempertahankan informasi pada data.

3. Train-Test-Split

    Melakukan pembagian dataset menjadi data latih (train) dan data uji (test) dengan mempertahankan sebagian data  yang ada untuk menguji seberapa baik generalisasi model terhadap data baru. Sebaiknya pembagian data dilakukan sebelum proses transformasi data, sehingga dapat mengurangi potensi kebocoran data (data leakage). Dalam hal ini jumlah data sebesar 4.129 akan dibagi menjadi 3.922 data latih dan 207 data uji.

4. Standarisasi

    Teknik StandardScaler dari library Scikitlearn digunakan dalam tahapan transformasi data numerical. Proses  standarisasi mengubah nilai rata-rata (mean) menjadi 0 dan nilai standar deviasi menjadi 1.

## Modeling

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
