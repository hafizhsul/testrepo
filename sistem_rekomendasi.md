# Laporan Proyek Machine Learning - Masdika Ilhan Mansiz

## Project Overview

Di era digital dengan lebih dari 500.000 judul film tersedia secara global (IMDb, 2023), konsumen menghadapi tantangan besar dalam menemukan konten yang sesuai. Sistem rekomendasi menjadi solusi kritis, dengan pasar global diproyeksikan tumbuh 35% CAGR hingga 2027 (MarketsandMarkets, 2023). Proyek ini mengembangkan sistem rekomendasi berbasis konten untuk platform streaming, memanfaatkan metadata film dari TMDB.

Analisis Industri:
- Pengguna menghabiskan rata-rata 18 menit untuk memilih film (Netflix Research)
- 75% penonton mengandalkan rekomendasi sistem (McKinsey Digital)
- Platform dengan sistem rekomendasi baik meningkatkan retention rate hingga 40%

Teknologi Inti:
- Content-Based Filtering
- Natural Language Processing (TF-IDF)
- Similarity Computing (Cosine Similarity)

Referensi:
- Netflix Technology Blog. (2022). How Netflix Recommends Movies [[1]](https://netflixtechblog.com/foundation-model-for-personalized-recommendation-1a0bd8e02d39)
- IEEE Transactions on Multimedia. (2021). Advanced Content-Based Recommender Systems [[2]](https://www.researchgate.net/publication/344454095_Recommender_Systems_Leveraging_Multimedia_Content)

## Business Understanding

### Problem Statements
- Overload informasi: Pengguna kesulitan menemukan film sesuai preferensi dari 4803 opsi
- Rekomendasi tidak personal: Platform sering menampilkan film populer tanpa mempertimbangkan kesukaan spesifik pengguna
- Ketergantungan pada rating: Sistem tradisional hanya mengandalkan rating tanpa mempertimbangkan kemiripan konten

### Goals
- Membangun sistem yang merekomendasikan film berdasarkan kemiripan genre, kata kunci, dan sinopsis
- Meningkatkan akurasi rekomendasi dengan pendekatan content-based filtering
- Memberikan setidaknya 5 rekomendasi relevan untuk setiap film input

### Solution statements
1. Content-Based Filtering
   - Kelebihan:
     - Tidak memerlukan data historik pengguna
     - Efektif untuk film baru
     - Interpretasi hasil mudah
   - Kekurangan:
     - Terbatas pada metadata yang ada
     - Kurang adaptif terhadap preferensi kompleks
       
2. Collaborative Filtering  
*Catatan: Dipertimbangkan untuk pengembangan selanjutnya*

## Data Understanding

Dataset: [TMDB 5000 Movie Dataset](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata?select=tmdb_5000_movies.csv)
Jumlah Data: 4803 film
Variabel Kunci:
- `title`: Judul film
- `genres`: Genre dalam format JSON
- `keywords`: Kata kunci deskriptif
- `overview`: Sinopsis film
- `vote_average`: Rating rata-rata

Exploratory Data Analysis:
1. Distribusi Rating:
   ```python
   sns.histplot(movies['vote_average'], bins=20)
   ```
   ![image](https://github.com/user-attachments/assets/b962e81a-33e2-4bf3-b549-c947d6e71139)
   
   *Mayoritas film memiliki rating 5-7 dengan distribusi normal*

2. Top Genre:
    ```python
   pd.Series(all_genres).value_counts()[:10].plot(kind='bar')
   ```
   ![image](https://github.com/user-attachments/assets/542b7c4e-138f-460e-a632-66ba8054588e)

   *Drama (20%), Comedy (15%), dan Thriller (12%) dominan*

## Data Preparation

Tahapan yang dilakukan:
1. Ekstraksi Fitur:
   ```python
   def extract_text_from_column(data, column):
    return data[column].apply(lambda x: ' '.join([i['name'] for i in ast.literal_eval(x)]))
   ```
   *Alasan: Mengubah struktur JSON menjadi teks terstruktur*
   
3. Penggabungan Fitur:
   ```python
   movies['combined_features'] = movies['genres_clean'] + ' ' + movies['keywords_clean'] + ' ' + movies['overview']
   ```
   *Alasan: Membuat representasi teks komprehensif untuk analisis*
   
5. Handling Missing Values:
   ```python
   movies['overview'].fillna('', inplace=True)
   ```
   *Alasan: Mencegah error pada TF-IDF*

## Modeling

Content-Based Filtering
1. TF-IDF Vectorization:
   ```python
   tfidf = TfidfVectorizer(stop_words='english', max_features=5000)
   tfidf_matrix = tfidf.fit_transform(movies['combined_features'])
   ```
   *Mengubah teks menjadi vektor numerik*
   
3. Cosine Similarity:
   ```python
   cosine_sim = cosine_similarity(tfidf_matrix)
   ```
   *Menghitung kemiripan antar film*

   

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
