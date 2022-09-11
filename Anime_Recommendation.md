# Laporan Proyek Machine Learning - Nama Anda

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
Melihat kolom/fitur pada anime.csv


Melihat apakah terdapat nilai null pada dataset


hal ini dilakukan agar 


Hapus nilai null


Melihat pesebaran genre yang ada pada dataset.


pada bagian ini penulis membuat visualisasi untuk melihat pesebaran genre yang ada pada dataset, yaitu dengan menggunakan library wordCloud

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
