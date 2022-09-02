# Laporan Proyek Machine Learning - Nico Siahaan

## Domain Proyek

Proyek ini merupakan proyek Medical Analysis Cost. Proyek ini dibuat untuk memprediksi biaya pengobatan/charges yang diperlukan untuk berobat ke rumah sakit. Hal ini menjadi penting karena sebagian masyarakat takut akan berobat ke rumah sakit dikarenakan biayanya yang mahal [Survei: Takut dan Mahal Jadi Alasan Utama Orang Enggan ke Dokter](https://health.detik.com/berita-detikhealth/d-3205565/survei-takut-dan-mahal-jadi-alasan-utama-orang-enggan-ke-dokter). 
Hal ini juga pernah di teliti oleh PALMY RAWINDA MELIALA pada [Perbandingan Algoritma Machine Learning Untuk Survivabilitas Dan Biaya Pengobatan Pasien Kanker Paru-Paru Di Taiwan](https://dspace.uii.ac.id/handle/123456789/37617) yang mana mereka menggunakan metode decision tree dalam membuat proyek tersebut.
Maka dari itu proyek ini dibuat agar masyarakat tidak takut untuk berobat ke rumah sakit.

## Business Understanding

Coba bayangkan ada seorang laki-laki umur 30an yang sedang sakit. Dia mengeluh soal dadanya yang sering sesak setiap hari, dia terpikirkan untuk berobat ke rumah sakit. Akan tetapi mengingat bahwa biaya berobat rumah sakit cukup mahal, dia enggan mengunjungi rumah sakit. Sedangkan penyakitnya berlarut-larut semakin parah dan pada akhirnya akan ke rumah sakit dengan biaya perobatan yang lebih mahal sebelum penyakit tersebut parah. 
Maka dari itu dari pihak rumah sakit, membuat sistem/proyek untuk mengatasi hal tersebut, yang mana mereka membuat sistem untuk memprediksi biaya pengobatan rumah sakit. Yang mana hal tersebut dapat menguntungkan kedua pihak, dimana dari pasien dapat langsung mengetahui biaya dari pengobatannya sehingga mau untuk datang ke rumah sakit, dan dari pihak rumah sakit dapat mengatasi penyakit pasien sejak dini (sebelum penyakit parah).

### Problem Statements

Berdasarkan hal yang telah dijelaskan sebelumnya maka ditemukanlah masalah sebagai berikut :
- Dari berbagai fitur yang ada, apa yang paling mempengaruhi biaya pengobatan rumah sakit?
- Bagaimana cara perhitungan biaya pengobatan?

### Goals

Untuk menjawab permasalahan diatas, maka dibuatlah predictive model dengan tujuan sebagai berikut :
- Mengetahui fitur yang berkorelasi dengan biaya pengobatan
- Membuat model machine learning yang dapat memprediksi harga pengobatan dengan fitur yang ada

### Solution statements
- Untuk mencapai tujuan tersebut, maka akan dibuat model machine learning dengan penggunaan algoritma KKN dan Random Forest

## Data Understanding
Data yang digunakan pada proyek ini merupakan data yang didapat dari Kaggle yang mana datanya berasal dari US yang dapat diakses melalui [Kaggle](https://www.kaggle.com/datasets/mirichoi0218/insurance)

Selanjutnya uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

### Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- age : Umur dari pasien
- sex : Jenis kelamin pasien
- bmi : Body Mass Index (berat badan normal/sehat)
- children : Anak yang dicover(memiliki) asuransi
- smoker : Perokok atau bukan
- region : Asal negara bagian US
- charges : Biaya berobat

Dataset ini memiliki 1339 data, yang terbagi menjadi beberapa fitur, seperti fitur numerik : age, bmi, children, charges dan fitur non-numerik : sex, smoker, region.
Dataset yang didapat termasuk bersih, sehingga dataset tidak terlalu banyak memerlukan proses data cleaning.
Untuk visualisasi data, dapat menggunakan library seaborn dengan tambahan matplotlib. yang mana ditampilkan dengan diagram bar dan memakai plotscatter juga tabel korelasi yang akan dijelaskan bawah. 

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

Pertama baca dataset.<br>
![Import dataset](https://i.imgur.com/5f3Evuj.png)
<br>
<br>
![cek input dan fitur](https://i.imgur.com/nvyQRJx.png)<br>
Data memiliki 1339 input dengan 7 fitur
<br>
<br>
![Cek Dataset](https://i.imgur.com/NP5GdLU.png)<br>
cek data type setiap fitur
<br>
<br>
![image](https://user-images.githubusercontent.com/64530694/188114168-5930903c-2323-4a9a-b572-e94ab915ff0c.png)<br>
Cek apakah terdapat nilai null










**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model machine learning yang digunakan untuk menyelesaikan permasalahan. Anda perlu menjelaskan tahapan dan parameter yang digunakan pada proses pemodelan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan kelebihan dan kekurangan dari setiap algoritma yang digunakan.
- Jika menggunakan satu algoritma pada solution statement, lakukan proses improvement terhadap model dengan hyperparameter tuning. **Jelaskan proses improvement yang dilakukan**.
- Jika menggunakan dua atau lebih algoritma pada solution statement, maka pilih model terbaik sebagai solusi. **Jelaskan mengapa memilih model tersebut sebagai model terbaik**.

## Evaluation
Pada bagian ini anda perlu menyebutkan metrik evaluasi yang digunakan. Lalu anda perlu menjelaskan hasil proyek berdasarkan metrik evaluasi yang digunakan.

Sebagai contoh, Anda memiih kasus klasifikasi dan menggunakan metrik **akurasi, precision, recall, dan F1 score**. Jelaskan mengenai beberapa hal berikut:
- Penjelasan mengenai metrik yang digunakan
- Menjelaskan hasil proyek berdasarkan metrik evaluasi

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
