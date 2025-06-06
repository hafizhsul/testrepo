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
- **Variabel Kunci**:
   - `title`: Judul film
   - `genres`: Genre dalam format JSON
   - `keywords`: Kata kunci deskriptif
   - `overview`: Sinopsis film
   - `vote_average`: Rating rata-rata

Exploratory Data Analysis:
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
1. Ekstraksi Fitur:
   Fungsi `extract_text_from_column` digunakan untuk membersihkan kolom genre dan kata kunci yang berupa format JSON dan mengubahnya menjadi string yang lebih mudah diproses.
   ```python
   def extract_text_from_column(data, column):
    return data[column].apply(lambda x: ' '.join([i['name'] for i in ast.literal_eval(x)]))
   ```
   *Alasan: Mengubah struktur JSON menjadi teks terstruktur*
   
3. Penggabungan Fitur:
   Kolom genre, kata kunci, dan sinopsis digabungkan untuk menghasilkan fitur gabungan yang akan digunakan dalam perhitungan kemiripan film.
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
- **Deskripsi Sistem Rekomendasi**:
Model rekomendasi dibangun menggunakan teknik TF-IDF Vectorization untuk mengubah teks menjadi vektor numerik. Kemudian, Cosine Similarity digunakan untuk menghitung tingkat kemiripan antara film berdasarkan fitur-fitur yang telah digabungkan.
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

- **Top-N Recommendation**:
Fungsi `get_recommendations` digunakan untuk memberikan rekomendasi film berdasarkan input judul film. Hasilnya adalah 5 film yang memiliki kemiripan tinggi dengan film yang dimasukkan.
   
**Output Contoh:**
| Film Input |	Rekomendasi 1 |	Rekomendasi 2 |
|---|---|---|
| The Avengers |	Iron Man 3 |	Captain America |

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





