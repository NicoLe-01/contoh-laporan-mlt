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
<br>
<br>
![image](https://user-images.githubusercontent.com/64530694/188132929-de6c83ce-fc5d-4aab-9d2f-3ac736e6b6c3.png)
<br>
Lihat pembagian data pada kolom jenis kelamin
<br>
<br>
![image](https://user-images.githubusercontent.com/64530694/188133737-6cb0d02f-a517-408a-a24f-aa22cae37603.png)
<br>
Cek pembagian data pada kolom smoker.<br>
Dapat dilihat pembagian data sekitar 80% pasien merupakan perokok
<br>
<br>
![image](https://user-images.githubusercontent.com/64530694/188135169-2392a7d0-0c65-452e-8d26-22f0738e0641.png)
<br>
Cek pembagian pada kolom region
<br>
<br>
Cek pesebaran data<br>
![image](https://user-images.githubusercontent.com/64530694/188136036-6a7bab39-ffe7-49ca-8d33-4296d98f62af.png)
![image](https://user-images.githubusercontent.com/64530694/188136778-e835e54e-abcb-4aa6-b6d9-cb0adc625cdc.png)
![image](https://user-images.githubusercontent.com/64530694/188137120-c90ebe44-8277-48cf-9ca6-612a320cb2a2.png)
<br>
<br>
Cek korelasi numerik antar data<br>
![image](https://user-images.githubusercontent.com/64530694/188137505-18200ac5-845a-4784-8013-062538eafe91.png)
<br>
Dapat dilihat, nilai numerik memiliki korelasi yang cukup rendah antar fitur nya
<br>
<br>
Encoding Fitur kategori<br>
![image](https://user-images.githubusercontent.com/64530694/188140648-fa786315-69c9-4897-b664-a7d9ba71dd73.png)
<br>
<br>
Cek kembali korelasi antar fitur<br>
![image](https://user-images.githubusercontent.com/64530694/188175507-5049a3bd-3996-4d65-9742-4e0279ded9fe.png)<br>
Dapat dilihat bahwa biaya berobat/charges berpengaruh cukup kuat dengan perokok atau tidaknya seorang pasien
<br>
<br>
Pisahkan label<br>
![image](https://user-images.githubusercontent.com/64530694/188140823-611d435e-a259-4f81-b37e-53e0093b77a1.png)
<br>
<br>
Bagi data train dan data test<br>
![image](https://user-images.githubusercontent.com/64530694/188140890-466b4c2d-eeaf-4375-92fc-92facf7b8dc2.png)
<br>
<br>
Normalisasi data<br>
![image](https://user-images.githubusercontent.com/64530694/188141015-8da38ce0-ab1c-4952-a500-d0619ec310e2.png)
<br>

## Modeling
Untuk dataset ini, disini menggunakan Algoritma KNN dan Random Forest.<br>
Pada Algoritma KNN<br>
![image](https://user-images.githubusercontent.com/64530694/188141324-12a75352-8ac6-4788-83bb-c77d3ab8e6be.png)
<br>
Kelebihan dari KNN adalah : 
- Mudah diimplementasikan

Kekurangan dari KNN adalah :
- Kurang baik untuk data yang sangat besar


Pada Algoritma Random Forest
<br>
![image](https://user-images.githubusercontent.com/64530694/188141419-f45a63fd-9dcb-4bf4-bb68-b37b8ea1907f.png)
<br>
Kelebihan Random Forest :
- Dapat mengatasi data yang non linear


Kekurangan Random Forest :
- Training lebih lama dibanding dengan algoritma lainnya


Jika dihitung nilai MSE dari kedua model diatas maka didapatkan nilai dengan :
<br>
![image](https://user-images.githubusercontent.com/64530694/188176379-b2e18a02-4dfd-42b6-acc9-1a9b1f9c626f.png)
<br>
<br>
Dapat dilihat nilai MSE pada model Random Forest lebih rendah dibanding dengan model KNN.


## Evaluation
Metrik evaluasi yang digunakan adalah MSE dan juga R Square.
Dengan nilai MSE:
<br>
![image](https://user-images.githubusercontent.com/64530694/188177669-8d81fc6c-9d1e-427b-8a02-df5fff541bb6.png)
<br>
<br>
Dengan prediksi :
<br>
![image](https://user-images.githubusercontent.com/64530694/188177770-e8a6a65e-5270-4fc5-99e8-651d6122ab55.png)
<br>
<br>
Nilai R Square :
<br>
![image](https://user-images.githubusercontent.com/64530694/188177996-f1ed812e-ac09-4951-a25c-9ac5ab616d2c.png)
<br>
<br>
Cara kerja MSE:<br>
![image](https://user-images.githubusercontent.com/64530694/188179389-f12984ac-1c07-4f05-8c1b-8340f3adf7d7.png)
<br>
MSE bekerja dengan mencari perbedaan kuadrat rata-rata antara nilai sebenarnya dengan nilai yang diprediksi oleh model.
<br>
<br>
Cara kerja R Square:<br>
![image](https://user-images.githubusercontent.com/64530694/188178413-91a81c7b-86e8-4432-b5de-a157677cfc0e.png)
<br>
Dengan, 
MSE (model) : Mean Squared error dari prediksi
MSE (baseline) : Mean Squared error dari prediksi rata-rata

Jadi dapat disimpulkan bahwa model Random Forest Lebih efektif untuk dataset ini dengan Nilai yang berkorelasi tinggi adalah pasien perokok atau bukan.
