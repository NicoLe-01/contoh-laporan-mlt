# Laporan Proyek Machine Learning - Nico Siahaan

## Project Overview
Proyek ini merupakan proyek Rekomendasi Anime. Latar belakang proyek ini adalah pengalaman penulis saat mencari anime yang sesuai dengan selera. Dimana penulis cukup kesulitan dalam mencari anime yang sesuai dengan genre yang disukai. Maka dari itu penulis memiliki ide untuk membuat sistem rekomendasi anime. Agar penulis atau orang lain dapat mencari anime yang sesuai dengan genre yang disukai. Dari sudut pandang penyedia anime/distributor anime juga memiliki manfaat seperti dapat meningkatkan jumlah pengunjung/click rate pada penyedia anime tersebut.
Hal ini juga pernah diteliti oleh Zartesya, M. A., & Komalasari, D. (2021), dengan judul [Penerapan Collaborative Filtering, PCA dan K-Means dalam Pembangunan Sistem Rekomendasi Ongoing dan Upcoming Film Animasi Jepang](https://conference.upnvj.ac.id/index.php/senamika/article/view/1343) yang mana Zartesya menggunakan metode Collaborative Filtering, PCA dan K-Means proyek tersebut.

## Business Understanding
Seperi yang dijelaskan pada bagian Project Overview. Bayangkan terdapat seorang yang baru menonton suatu judul anime, lalu dia tertarik untuk menonton anime yang sejenis dengan anime yang ditonton sebelumnya. Lalu dia mencoba mencari aplikasi yang penyedia jasa streaming anime. Nah, dengan adanya sistem rekomendasi anime ini, pengguna baru tersebut dapat melihat anime yang populer atau pengguna dapat membuat akun, lalu membuat daftar anime yang ditonton. 
Sehingga dari sudut pandang pengguna, pengguna merasa terbantu dengan rekomedasi yang diberikan sistem. Sedangkan dari sudut pandang penyedia, penyedia mendapat click rate/trafic yang meningkat.

### Problem Statements

Menjelaskan pernyataan masalah:
- Data apa yang terpenting dalam membuat sistem rekomendasi anime ?
- Bagaimana cara membuat sistem rekomendasi anime yang cocok untuk pengguna ?
- Metode apa yang paling efektif untuk sistem rekomendasi anime ?

### Goals
- Untuk mengetahui data yang terpenting dalam membuat sistem rekomendasi anime.
- Membuat model machine learning untuk sistem rekomendasi.
- Untuk mengetahui metode yang paling efektif dalam sistem rekomendasi anime.

### Solution statements
 - Metode machine learning yang dibuat akan menggunakan Content-Based Filtering dan Collaborative Filtering dengan pendekatan deep learning.


## Data Understanding
Dataset proyek ini merupakan dataset yang diambil dari [Kaggle](https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database)

Dataset ini berisi 2 file csv, Anime.csv dan Rating.csv. Pada Anime.csv berisi 12.294 judul anime. Sedangkan Rating.csv berisi 73,516 rating pengguna.
Dataset ini masih memiliki cukup banyak *missing value*

Variabel-variabel pada Anime.csv adalah sebagai berikut:
- anime_id  : nilai *unique* suatu dari judul anime
- name      : nama anime
- genre     : genre anime
- type      : jenis anime (movie, TV, OVA, lainnya)
- episodes  : jumlah episode
- rating    : rating rata-rata pengguna
- members   : komunitas pada suatu judul anime

Variabel-variabel pada Rating.csv adalah sebagai berikut:
- user_id   : nilai *unique* seorang pengguna
- anime_id  : anime yang di nilai/rating oleh pengguna
- rating    : rating yang diberikan pengguna. -1 artinya belum memberikan rating

Untuk visualisasi data pada dataset ini penulis menggunakan library wordCloud, yang digunakan untuk mengetahui genre apa yang paling banyak pada dataset anime.

## Data Preparation
### Content-Based Filtering

Melihat kolom/fitur pada anime.csv\
![image](https://user-images.githubusercontent.com/64530694/189573284-44c89594-a0fc-4f5a-9f77-6efde513b71a.png)
<br>


Melihat apakah terdapat nilai null pada dataset.\
![image](https://user-images.githubusercontent.com/64530694/189573457-9dbf6494-a964-42eb-9f14-4d6fadec8e4d.png)
<br>


Hapus nilai null.\
![image](https://user-images.githubusercontent.com/64530694/189573498-14737488-d87a-4391-aa66-2537af60e280.png)
<br>

Melihat pesebaran genre yang ada pada dataset.\
![image](https://user-images.githubusercontent.com/64530694/189573609-ddbf225a-1a1f-4d4c-8d86-43a333b2f8cb.png)
<br>

Dapat dilihat genre paling mendominasi adalah Comedy, Action, dan Adventure

pada bagian ini penulis membuat visualisasi untuk melihat pesebaran genre yang ada pada dataset, yaitu dengan menggunakan library wordCloud

### Collaborative Filtering
Cek data.\
![image](https://user-images.githubusercontent.com/64530694/189573782-b22a1a28-b2ed-4f83-9d75-b81a13ed8b44.png)
<br>

Hilangkan nilai -1 (null).\
![image](https://user-images.githubusercontent.com/64530694/189573817-2611c0ef-c6eb-4b66-bfc9-748e8d4c9c0c.png)
<br>

Ambil 1000 data rating.\
![image](https://user-images.githubusercontent.com/64530694/189573842-7c26c3ce-403b-4be5-8caf-1f7df740a119.png)
<br>

Ambil nilai unique.\
![image](https://user-images.githubusercontent.com/64530694/189573939-89dd382b-6daa-4e66-ae77-e402214c67f9.png)
<br>

Bagi data.\
![image](https://user-images.githubusercontent.com/64530694/189573998-32d312b0-7568-494d-8c38-fc072d098219.png)



## Modeling
### Content-Based Filtering
Untuk metode ini, penulis menggunakan TfidfVectorizer dan cosine similarity.\
![image](https://user-images.githubusercontent.com/64530694/189574085-5fc70174-8f6a-40b8-86ce-527fd9c27ffe.png)
<br>
![image](https://user-images.githubusercontent.com/64530694/189574169-b7d98200-0746-4e98-88ee-6394691c2444.png)
<br>
Dengan fungsi prediksi :\
![image](https://user-images.githubusercontent.com/64530694/189574248-59e40f7e-000f-4f32-a7a3-57a60e261b8a.png)
<br>

Kelebihan :
- Tidak memerlukan data riwayat penguna
- Proses yang cepat
- Implementasinya mudah

Kekurangan :
- Rekomendasi yang ditampikan cukup terbatas. Hanya menampilkan genre yang sesuai dengan pengguna
- Rekomendasi yang ditampilkan tidak menggunakan rating. Hanya mencocokan genre yang diminta.

### Collaborative Filtering
Untuk metode ini, penulis menggunakan pendekatan deep learning.\
![image](https://user-images.githubusercontent.com/64530694/189574416-1215e14d-33cd-4c67-b625-20d310e2e1a6.png)
<br>
Dengan fungsi prediksi :\
![image](https://user-images.githubusercontent.com/64530694/189574652-5c32f5f1-06a4-4233-baa5-8bfec555013d.png)
<br>


Kelebihan : 
- Rekomendasi yang diberikan berdasarkan rating yang paling tinggi dan sesuai dengan genre.

Kekurangan :
- Proses traning yang cukup lama
- Implementasi cukup sulit

## Evaluation
### Conten-Based Filterring
Metrik evaluasi yang digunakan adalah menggunakan Precision dengan sedikit perubahan, yang formula nya :\
![image](https://user-images.githubusercontent.com/64530694/189574773-7869252c-7871-477e-93e2-c0f5fb06cc67.png)
<br>

Dengan prediksi :\
![image](https://user-images.githubusercontent.com/64530694/189574864-2a7640cd-5d95-4806-b4e5-676835e882c6.png)
<br>

jadi P   = (4 + 4 + (4 - 1) + 3 + 3) / 20 = 0.85
jadi presisi nya adalah 85%


### Collaborative Filtering
Metrik evaluasi yang digunakan adalah menggunakan Mean Squared Error, yang formulanya :\
![image](https://user-images.githubusercontent.com/64530694/189574922-e5cc96b1-30fe-4db7-b508-13aaf8c85c46.png)
<br>

Dengan :
- At = Nilai sebenarnya
- Ft = Nilai prediksi
- n = Banyaknya data

Yang prediksi nya adalah :\
![image](https://user-images.githubusercontent.com/64530694/189575053-9edf84aa-cc3b-42b8-b323-12457300580e.png)
<br>


## Kesimpulan 
Jadi kesimpulan yang didapat dari proyek ini adalah : 
- Data yang terpenting dalam membuat sistem rekomendasi anime adalah Genre dan Rating dari suatu anime.
- Dengan membuat sistem rekomendasi menggukanan machine learning, baik dengan Content-Based Filtering atau Collaborative Filtering.
- Kedua metode memiliki kelebihan dan kekurangan masing-masing. Seperti yang dijelaskan pada bagian Modelling, dengan pendekatan Content-Based Filtering bagus untuk pengguna baru yang belum memiliki riwayat menonton anime. Sedangkan Collaborative Filtering bagus untuk pengguna yang sudah memiliki riwayat menonton anime.
