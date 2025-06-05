# Proyek Akhir: Menyelesaikan Permasalahan HR Perusahaan Jaya Jaya Maju

## Business Understanding

Jaya Jaya Maju merupakan perusahaan multinasional yang telah berdiri sejak tahun 2000 dengan lebih dari 1000 karyawan tersebar di seluruh penjuru negeri. Meskipun telah berkembang menjadi perusahaan besar, Jaya Jaya Maju masih menghadapi kesulitan dalam mengelola karyawan yang berdampak pada tingginya attrition rate hingga lebih dari 10%.

### Permasalahan Bisnis

Berdasarkan kondisi yang dihadapi oleh Jaya Jaya Maju, berikut adalah permasalahan bisnis yang akan diselesaikan:

1. **Tingginya Attrition Rate (>10%)**: Rasio karyawan yang keluar dari perusahaan melebihi standar industri, yang mengindikasikan adanya masalah dalam employee retention.

2. **Kurangnya Pemahaman Faktor Penyebab**: Departemen HR belum memiliki pemahaman yang mendalam tentang faktor-faktor spesifik yang menyebabkan karyawan memutuskan untuk keluar dari perusahaan.

3. **Kurangnya Tools Monitoring**: Departemen HR membutuhkan dashboard untuk memantau dan menganalisis berbagai metrik terkait employee retention.

### Cakupan Proyek

Proyek ini akan mencakup beberapa tahapan utama untuk menyelesaikan permasalahan attrition rate di Jaya Jaya Maju:

1. **Analisis Data Karyawan**
   - Exploratory Data Analysis (EDA) untuk memahami karakteristik dataset
   - Identifikasi pola dan tren dalam data employee attrition
   - Analisis korelasi antara berbagai faktor dengan keputusan karyawan untuk keluar

2. **Pembuatan Business Dashboard**
   - Pengembangan dashboard interaktif menggunakan Metabase
   - Visualisasi key metrics dan insights untuk departemen HR
   - Implementasi monitoring untuk employee retention

### Persiapan

**Sumber data**: [Dataset Karyawan Jaya Jaya Maju](https://github.com/dicodingacademy/dicoding_dataset/blob/main/employee/employee_data.csv) yang berisi informasi demografis, karakteristik pekerjaan, kompensasi, dan status attrition karyawan.

**Setup environment**:
- Pastikan Docker sudah terinstal dan jalankan perintah berikut:
```
docker pull metabase/metabase:latest
```
- Kemudian jalankan perintah berikut:
```
docker run -d -p 3000:3000 --name metabase metabase/metabase
```
      
**Tools dan Technologies**:
- **Python**: Pandas dan NumPy
- **Visualization**: Matplotlib, Seaborn, Plotly untuk data visualization
- **Dashboard**: Metabase untuk business dashboard
- **Environment**: Jupyter Notebook untuk development dan documentation

## Business Dashboard

Business dashboard telah dibuat menggunakan Metabase untuk membantu departemen HR dalam monitoring dan analisis faktor-faktor yang mempengaruhi attrition rate. Dashboard ini menyediakan visualisasi interaktif yang memungkinkan stakeholder untuk:

**Fitur Utama Dashboard:**

1. **Overview Metrics**
   - Current attrition rate
   - Jumlah total karyawan dan distribusi per departemen
   - Perbandingan attrition rate antar departemen

2. **Demographic Analysis**
   - Distribusi attrition berdasarkan usia, dan masa kerja
   - Visualisasi geographic karyawan

3. **Job-Related Factors**
   - Analisis kepuasan kerja
   - Distribusi jam kerja dan overtime

**Akses Dashboard:**
- **URL**: `http://localhost:3000` (running di local environment)
- **Username**: `root@mail.com`
- **Password**: `root123`

## Conclusion

Berdasarkan analisis data untuk kasus attrition rate di Perusahaan Jaya Jaya Maju, dapat disimpulkan beberapa hal penting:

**Key Findings:**

1. **Faktor Utama Attrition**: Analisis menunjukkan bahwa faktor-faktor seperti job satisfaction, waktu overtime, dan usia menjadi prediktor utama employee attrition.

2. **Pola Attrition**: Terdapat pola spesifik dalam attrition berdasarkan demografis, dan karakteristik pekerjaan yang dapat digunakan untuk strategi retention.

3. **Dashboard Monitoring**: Business dashboard yang telah dibuat memberikan visibility terhadap key metrics dan memungkinkan monitoring terhadap faktor-faktor risiko attrition.

**Impact:**
Implementasi solusi ini diharapkan dapat membantu Jaya Jaya Maju mengurangi attrition rate dari >10% menjadi di bawah rata-rata industri (sekitar 6-8%), sehingga dapat meningkatkan stabilitas operasional perusahaan.
