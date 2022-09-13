# Laporan Proyek Machine Learning - Nico Siahaan

## Project Overview
Proyek ini merupakan proyek Rekomendasi Anime. Latar belakang proyek ini adalah pengalaman penulis saat mencari anime yang sesuai dengan selera. Dimana penulis cukup kesulitan dalam mencari anime yang sesuai dengan genre yang disukai. Maka dari itu penulis memiliki ide untuk membuat sistem rekomendasi anime. Agar penulis atau orang lain dapat mencari anime yang sesuai dengan genre yang disukai. Dari sudut pandang penyedia anime/distributor anime juga memiliki manfaat seperti dapat meningkatkan jumlah pengunjung/click rate pada penyedia anime tersebut.
Hal ini juga pernah diteliti oleh [Zartesya, M. A., & Komalasari, D. (2021)](https://conference.upnvj.ac.id/index.php/senamika/article/view/1343)[1], yang mana Zartesya menggunakan metode Collaborative Filtering, PCA dan K-Means proyek tersebut.
[SA Pratama - 2019](https://repository.upnvj.ac.id/2016/1/AWAL.pdf)[2], juga meneliti tentang hal ini, SA Pratama menggunakan metode Decision Tree pada proyeknya.

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
Tahapan : 
- Melihat kolom/fitur pada anime.csv\
- Melihat apakah terdapat nilai null pada dataset.
- Hapus nilai null.
- Melihat pesebaran genre yang ada pada dataset.

Pada bagian ini penulis membuat visualisasi untuk melihat pesebaran genre yang ada pada dataset, yaitu dengan menggunakan library wordCloud

### Collaborative Filtering
Tahapan : 
- Cek data
- Hilangkan nilai -1 (null).
- Ambil 1000 data rating.
- Ambil nilai unique.
- Bagi data.


## Modeling
### Content-Based Filtering
Untuk metode ini, penulis menggunakan TfidfVectorizer dan cosine similarity.\
Pertama import library
```
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity
```
```
tf = TfidfVectorizer() # inisiasi TfidfVectorizer
tf.fit(animes['genre']) # hitung idf
tf.get_feature_names()
```
Lalu transform ke bentuk matrix
```
tfidf_matrix = tf.fit_transform(animes['genre'])
```
Ubah vektor tf-idf
```
tfidf_matrix.todense()
```
Hitung cosine similarity
```
cosine_sim = cosine_similarity(tfidf_matrix)
```
Buat dataframe dengan baris dan kolom nama anime
```
cosine_sim_df = pd.DataFrame(cosine_sim, index=animes['name'], columns=animes['name'])
```
Buat fungsi rekomendasi
```
def anime_recommendation(nama_anime, similarity_data=cosine_sim_df, items=animes[['name', 'genre']], k=5):

# Parameter 
# nama_anime :  nama anime yang ingin dicari
# similarity_data : matriks kesamaan anime
# items : fitur kemiripan
# k : banyak rekomendasi yang diinginkan

  # ubah dataframe menjadi numpy
  # ambil data menggunakan argpartition
  index = similarity_data.loc[:, nama_anime].to_numpy().argpartition(
      range(-1, -k, -1)
  )
  
  # ambil similarity terbesar
  closest = similarity_data.columns[index[-1:-(k+2):-1]]
  
  # hilangkan anime yang sama, dengan judul anime yang diminta
  closest = closest.drop(nama_anime, errors='ignore')

  return pd.DataFrame(closest).merge(items).head(k)
```

Hasil Prediksi
```
anime_recommendation('Sword Art Online')
```
|               name               |                   genre                   |
|:--------------------------------:|:-----------------------------------------:|
| Sword Art Online II              | Action, Adventure, Fantasy, Game, Romance |
| Sword Art Online: Extra Edition  | Action, Adventure, Fantasy, Game, Romance |
| Sword Art Online II: Debriefing  | Action, Adventure, Fantasy, Game          |
| Bakugan Battle Brawlers          | Action, Fantasy, Game                     |
| Monster Strike: Mermaid Rhapsody | Action, Fantasy, Game                     |

Kelebihan :
- Tidak memerlukan data riwayat penguna
- Proses yang cepat
- Implementasinya mudah

Kekurangan :
- Rekomendasi yang ditampikan cukup terbatas. Hanya menampilkan genre yang sesuai dengan pengguna
- Rekomendasi yang ditampilkan tidak menggunakan rating. Hanya mencocokan genre yang diminta.

### Collaborative Filtering
Untuk metode ini, penulis menggunakan pendekatan deep learning.\

Import library
```
import tensorflow as tf
from tensorflow.keras import Model
from tensorflow.keras.layers import Input, Embedding, Reshape, Flatten, concatenate, Dense, Dropout
from tensorflow.keras.optimizers import Adam
from sklearn.model_selection import train_test_split
```

Buang kolom rating dan simpan ke variabel
```
X = ratings.drop(['rating'], axis=1)
```

Buat variabel untuk menyimpan label
```
y = ratings['rating'].astype(float)
```

Bagi data menjadi traning dan validation
```
X_train, X_val, y_train, y_val = train_test_split(X, y, test_size=0.2, random_state=22)
```

Buat model
```
def RecommenderAnime(n_users, n_movies, n_dim):
# Parameter 
# n_user = banyaknya jumlah dimensi untuk layer user
# n_moview = banyaknya jumlah dimensi untuk layer anime
# n_dim = output dimension

    # User
    user = Input(shape=(1,))
    U = Embedding(n_users, n_dim)(user)
    U = Dropout(0.2)(U)
    U = Flatten()(U)
    
    # Anime
    movie = Input(shape=(1,))
    M = Embedding(n_movies, n_dim)(movie)
    M = Dropout(0.2)(M)
    M = Flatten()(M)
    
    # Gabungkan disini
    merged_vector = concatenate([U, M])
    dense_1 = Dense(128, activation='relu')(merged_vector)
    dropout = Dropout(0.3)(dense_1)
    final = Dense(1)(dropout)
    
    model = Model(inputs=[user, movie], outputs=final)
    
    model.compile(optimizer=Adam(0.001),
                  loss='mean_squared_error')
    
    return model
```

Inisiasi model
```
model = RecommenderAnime(userid_unique, anime_unique, 100)
```

Traning model
```
history = model.fit(x=[X_train['user_id'], X_train['anime_id']],
                    y=y_train,
                    batch_size=8,
                    epochs=30,
                    verbose=1,
                    validation_data=([X_val['user_id'], X_val['anime_id']], y_val),
                    callbacks=[my_callbacks]
                    )
```

fungsi prediksi
```
def buat_prediksi(user_id, anime_id, model):
# Parameter 
# user_id : id user yang ingin diprediksi
# anime_id : id anime yang ingin diprediksi
# model : model yang sudah di traning

    return model.predict([np.array([user_id]), np.array([anime_id])])[0][0]
```

Fungsi untuk menampilkan rekomendasi
```
def prediksi_teratas(user_id, model, k):
  """
  Parameter user_id : input user ke n dari data set
  Parameter model : input model yang telah di traning
  Parameter k : input berapa banyak prediksi yang akan tampilkan
  """


  user_id = int(user_id) - 1    # ambil user id
  user_ratings = ratings[ratings['user_id'] == user_id] # lihat anime apa saja yg telah di review oleh pengguna
  anime_id_user_ratings = user_ratings.anime_id.values.tolist() # buatlist anime yang telah ditonton oleh pengguna
  anime_viewed = animes.loc[animes['anime_id'].isin(anime_id_user_ratings)].sort_values(by='anime_id')  # cari anime berdasarkan anime_id
  
  genre_viewed = defaultdict(int)  # buat dictionary

  for genres in anime_viewed['genre']:  # hitung genre yang muncul
    for genre in genres.split(','):
        genre_viewed[genre.strip()] += 1

  genre_viewed_by_user = list(sorted(genre_viewed, key=genre_viewed.get, reverse=True)) # urutkan genre yang muncul dari yang paling banyak
  top7_genre_by_user = genre_viewed_by_user[:7]  # ambil 7 genre tertinggi

  print("7 genre yang banyak ditonton oleh pengguna : \n")
  print(top7_genre_by_user, sep=", ")
  print("=======================" * 5)
  
  rekomendasi = ratings[~ratings['anime_id'].isin(user_ratings['anime_id'])][['anime_id']].drop_duplicates() # hilangkan anime yg telah di review dan masukkan ke dataframe rekomendasi
  rekomendasi['rating_predict'] = rekomendasi.apply(lambda x: buat_prediksi(user_id, x['anime_id'], model), axis=1) # prediksi semua baris data anime. yg hasilnya dimasukkan ke dataframe rekomendasi
  rekomendasi_fix = rekomendasi.sort_values(by='rating_predict', ascending=False).merge(animes[['anime_id', 'name', 'type', 'members', 'genre']],
                                                                                       on='anime_id').head(k) # urutkan dari rating 5 tertinggi 
  return rekomendasi_fix.sort_values('rating_predict', ascending=False)[['name', 'type', 'rating_predict', 'genre']]
```

Hasil prediksi
7 genre yang banyak ditonton oleh pengguna :\
'Comedy', 'Adventure', 'Sci-Fi', 'Action', 'Fantasy', 'Shounen', 'Drama'

|                    name                   |  type | rating_predict |                       genre                       |
|:-----------------------------------------:|:-----:|:--------------:|:-------------------------------------------------:|
| Doraemon Movie 16: Nobita no Sousei Nikki | Movie | 9.713937       | Adventure, Comedy, Fantasy, Kids, Sci-Fi, Shounen |
| Penguin Musume♥Heart                      | ONA   | 9.669694       | Comedy, Ecchi, School, Slice of Life              |
| Little Nemo                               | Movie | 9.631376       | Adventure, Fantasy                                |
| Batman: Gotham Knight                     | OVA   | 9.614861       | Action, Adventure, Martial Arts                   |
| Medarot Damashii                          | TV    | 9.591266       | Action, Adventure, Sci-Fi                         |

Kelebihan : 
- Rekomendasi yang diberikan berdasarkan rating yang paling tinggi dan sesuai dengan genre.

Kekurangan :
- Proses traning yang cukup lama
- Implementasi cukup sulit

## Evaluation
### Conten-Based Filterring
Metrik evaluasi yang digunakan adalah menggunakan Jaccard Similarity yang formula nya :\
![image](https://user-images.githubusercontent.com/64530694/189814134-c64b5304-178b-448e-b92c-9e092e073a03.png)

    
Dengan :
- A = Genre/nilai sebenarnya
- B = Genre/nilai prediksi

Dengan prediksi :\
|               name               |                   genre                   |
|:--------------------------------:|:-----------------------------------------:|
| Sword Art Online II              | Action, Adventure, Fantasy, Game, Romance |
| Sword Art Online: Extra Edition  | Action, Adventure, Fantasy, Game, Romance |
| Sword Art Online II: Debriefing  | Action, Adventure, Fantasy, Game          |
| Bakugan Battle Brawlers          | Action, Fantasy, Game                     |
| Monster Strike: Mermaid Rhapsody | Action, Fantasy, Game                     |

```
def jaccard_set(list_genre, list_genre_prediksi):
    intersection = len(list(set(list_genre).intersection(list_genre_prediksi)))
    union = (len(list_genre) + len(list_genre_prediksi)) - intersection
    return float(intersection) / union
```

```
def jaccard_value_total(genre_anime, genre_prediksi):
  total_jaccard_value = 0
  result = 0
  for i in range(len(genre_prediksi)):
    genre = genre_prediksi[i].split(',')
    jaccard_value = jaccard_set(genre_anime, genre)
    total_jaccard_value += jaccard_value
    result = total_jaccard_value / len(genre_prediksi)
  return result
```

```
jaccard_value_total(genre_anime, all_genre_prediksi)
> 0.8
```

Dapat dilihat score similarity sebesar 0.8, yang artinya sistem rekomendasi bekerja cukup baik.


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


## Kesimpulan 
Jadi kesimpulan yang didapat dari proyek ini adalah : 
- Data yang terpenting dalam membuat sistem rekomendasi anime adalah Genre dan Rating dari suatu anime.
- Dengan membuat sistem rekomendasi menggukanan machine learning, baik dengan Content-Based Filtering atau Collaborative Filtering.
- Kedua metode memiliki kelebihan dan kekurangan masing-masing. Seperti yang dijelaskan pada bagian Modelling, dengan pendekatan Content-Based Filtering bagus untuk pengguna baru yang belum memiliki riwayat menonton anime. Sedangkan Collaborative Filtering bagus untuk pengguna yang sudah memiliki riwayat menonton anime.


## Referensi
[1] Zartesya, M. A., & Komalasari, D. (2021). Penerapan Collaborative Filtering, PCA dan K-Means dalam Pembangunan Sistem Rekomendasi Ongoing dan Upcoming Film Animasi Jepang. Senamika, 2(1), 606-615.

[2] Pratama, S. A. (2019). PERANCANGAN SISTEM REKOMENDASI ANIME MENGGUNAKAN METODE DECISION TREE PADA INDUSTRI KREATIF (Doctoral dissertation, Universitas Pembangunan Nasional Veteran Jakarta).
