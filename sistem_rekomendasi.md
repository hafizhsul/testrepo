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
Dataset yang digunakan adalah TMDB 5000 Movie Dataset yang berisi 4803 film. Dataset ini mencakup informasi seperti genre, kata kunci, sinopsis, dan rating film yang digunakan untuk rekomendasi. Dataset dapat diakses [di sini](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata?select=tmdb_5000_movies.csv).

**Deskripsi Dataset**
- Jumlah baris: 4803 film
- Jumlah kolom: 20 kolom

**Variabel Utama**

Berikut adalah deskripsi lengkap semua kolom dalam dataset:
- `budget`: Anggaran produksi film (dalam USD)
- `genres`: Daftar genre film dalam format JSON
- `homepage`: URL homepage resmi film
- `id`: ID unik film di TMDB
- `keywords`: Kata kunci terkait film dalam format JSON
- `original_language`: Bahasa asli film (kode 2 huruf)
- `original_title`: Judul film dalam bahasa asli
- `overview`: Sinopsis film
- `popularity`: Skor popularitas film di TMDB
- `production_companies`: Perusahaan produksi dalam format JSON
- `production_countries`: Negara produksi dalam format JSON
- `release_date`: Tanggal rilis film
- `revenue`: Pendapatan film (dalam USD)
- `runtime`: Durasi film dalam menit
- `spoken_languages`: Bahasa yang digunakan dalam film (format JSON)
- `status`: Status rilis (Released, Post Production, dll)
- `tagline`: Tagline/slogan film
- `title`: Judul film dalam bahasa Inggris
- `vote_average`: Rating rata-rata film (skala 0-10)
- `vote_count`: Jumlah vote yang diterima

**Kondisi Data**

Hasil pemeriksaan missing values:
```python
movies.isna().sum()
```
- `homepage`: 3091 missing values (64.4%)
- `tagline`: 844 missing values (17.6%)
- `overview`: 3 missing values (0.06%)
- `runtime`: 2 missing values (0.04%)
- `release_date`: 1 missing value (0.02%)

Kolom lain tidak memiliki missing values.

**Exploratory Data Analysis**:

Dalam tahap Exploratory Data Analysis (EDA), dilakukan analisis distribusi rating dan genre paling populer. Hal ini membantu memahami bagaimana film dinilai dan genre apa yang mendominasi dalam dataset.

1. Distribusi Rating:  
   Histogram digunakan untuk melihat distribusi rating film yang ada. Ini membantu untuk memahami bagaimana film dinilai oleh pengguna.
   ```python
   sns.histplot(movies['vote_average'], bins=20)
   ```
   ![image](https://github.com/user-attachments/assets/b962e81a-33e2-4bf3-b549-c947d6e71139)
   
   *Mayoritas film memiliki rating 5-7 dengan distribusi normal*

3. Top Genre:  
   Bar plot digunakan untuk menampilkan 10 genre film paling populer dalam dataset. Ini memberikan gambaran tentang genre yang dominan di dataset.
    ```python
   pd.Series(all_genres).value_counts()[:10].plot(kind='bar')
   ```
   ![image](https://github.com/user-attachments/assets/542b7c4e-138f-460e-a632-66ba8054588e)

   *Drama (20%), Comedy (15%), dan Thriller (12%) dominan*

## Data Preparation
Data preparation dilakukan untuk mengubah data mentah (seperti format JSON dan nilai kosong) menjadi format yang siap digunakan dalam pemodelan. Langkah ini penting untuk memastikan bahwa model dapat memproses data dengan baik dan memberikan hasil yang akurat.

Tahapan yang dilakukan:
1. Ekstraksi Fitur
   
   Fungsi `extract_text_from_column` digunakan untuk membersihkan kolom genre dan kata kunci yang berupa format JSON dan mengubahnya menjadi string yang lebih mudah diproses.
   ```python
   def extract_text_from_column(data, column):
    return data[column].apply(lambda x: ' '.join([i['name'] for i in ast.literal_eval(x)]))
   ```
   *Alasan: Mengubah struktur JSON menjadi teks terstruktur*
   
2. Penggabungan Fitur
   
   Kolom genre, kata kunci, dan sinopsis digabungkan untuk menghasilkan fitur gabungan yang akan digunakan dalam perhitungan kemiripan film.
   ```python
   movies['combined_features'] = (
    movies['genres_clean'] + ' ' + 
    movies['keywords_clean'] + ' ' + 
    movies['overview'].fillna('')
   )
   ```
   *Alasan: Membuat representasi teks komprehensif untuk analisis*
   - Kolom `overview` yang kosong diisi dengan string kosong
   - Tidak dilakukan penghapusan data karena semua film memiliki metadata penting (genre dan keywords)

4. TF-IDF Vectorization
   
   Teknik TF-IDF Vectorization digunakan untuk mengubah teks menjadi vektor numerik.
   ```python
   tfidf = TfidfVectorizer(stop_words='english', max_features=5000)
   tfidf_matrix = tfidf.fit_transform(movies['combined_features'])
   ```

## Modeling
**Content-Based Filtering**  
- **Cosine Similarity**:
  
  Cosine Similarity digunakan untuk mengukur kemiripan antara vektor film input dan vektor semua film lain.
   ```python
   cosine_sim = cosine_similarity(tfidf_matrix)
   ```
   *Menghitung kemiripan antar film berdasarkan vektor TF-IDF*

  Contoh Perhitungan:  
  Misal kita hitung similarity antara The Avengers (A) dan Iron Man 3 (B):
  ```
  A = [Action:0.7, Superhero:0.6, Marvel:0.5]  
  B = [Action:0.8, Superhero:0.5, Tech:0.3]  
  similarity = (0.7×0.8 + 0.6×0.5 + 0.5×0) / (√(0.7²+0.6²+0.5²) × √(0.8²+0.5²+0.3²)) ≈ 0.89
  ```
  Nilai `0.89` menunjukkan kemiripan sangat tinggi.

- **Top-N Recommendation**:
  
  Fungsi `get_recommendations` digunakan untuk memberikan rekomendasi film berdasarkan input judul film. Hasilnya adalah 5 film yang memiliki kemiripan tinggi dengan film yang dimasukkan.
  ```python
  def get_recommendations(title, n=5):
    try:
        idx = movies[movies['title'].str.lower() == title.lower()].index[0]
        sim_scores = list(enumerate(cosine_sim[idx]))
        sim_scores = sorted(sim_scores, key=lambda x: x[1], reverse=True)[1:n+1]
        movie_indices = [i[0] for i in sim_scores]
        return movies[['title', 'genres_clean', 'vote_average']].iloc[movie_indices]
    except:
        return "Film tidak ditemukan"
  ```
   
   **Contoh Output untuk "Batman"**
   
   | Title | Genres | Vote Average |
   |---|---|---|
   | Batman & Robin | Action Crime Fantasy | 4.2 |
   | The Dark Knight Rises | Action Crime Drama Thriller | 7.6 |
   | Batman Begins | Action Crime Drama | 7.5 |
   | Batman Returns | Action Fantasy | 6.6 |
   | The Dark Knight | Drama Action Crime Thriller | 8.2 |

## Evaluation
**Metrik**: Precision@K
Precision@K digunakan untuk mengukur jumlah rekomendasi relevan dibandingkan dengan total rekomendasi yang diberikan (misalnya 5).
Formula:
```
Precision@5 = (Jumlah rekomendasi relevan) / 5
```
Metrik ini penting untuk mengevaluasi seberapa relevan rekomendasi yang diberikan oleh sistem. Precision yang tinggi menunjukkan bahwa sistem dapat memberikan rekomendasi yang sesuai dengan preferensi pengguna.

Hasil:
1. Untuk film "Inception":
   - 4/5 rekomendasi memiliki genre Sci-Fi/Thriller
   - Precision@5 = 0.8

2. Untuk film "Toy Story":
   - 5/5 rekomendasi animasi keluarga
   - Precision@5 = 1.0

Berdasarkan evaluasi pada film "Inception", sistem menghasilkan Precision@5 sebesar 0.8, yang menunjukkan bahwa 4 dari 5 rekomendasi relevan dengan genre Sci-Fi/Thriller.

Visualisasi:
```python
sns.barplot(x='vote_average', y='title', data=recommendations)
```
![image](https://github.com/user-attachments/assets/ad4d0aa3-3838-455e-a87b-c35b5d401725)





