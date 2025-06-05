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

1. **Persiapan Virtual Environment**:
   - Buat virtual environment baru:
     ```
     python -m venv venv
     ```
   - Aktifkan virtual environment:
     - Windows:
       ```
       venv\Scripts\activate
       ```
     - macOS/Linux:
       ```
       source venv/bin/activate
       ```

2. **Instalasi Dependencies**:
   - Install semua package yang dibutuhkan:
     ```
     pip install -r requirements.txt
     ```
   - Jika file requirements.txt belum tersedia, install package secara manual:
     ```
     pip install pandas numpy matplotlib seaborn plotly jupyter
     ```

3. **Menjalankan Jupyter Notebook**:
   - Buka notebook dengan perintah:
     ```
     jupyter notebook notebook.ipynb
     ```
   - Jalankan semua cell secara berurutan

4. **Menjalankan Metabase Dashboard**:
   - Pastikan Docker sudah terinstal
   - Jalankan perintah berikut:
     ```
     docker pull metabase/metabase:latest
     docker run -d -p 3000:3000 --name metabase metabase/metabase
     ```
   - Akses dashboard di `http://localhost:3000` dengan:
     - Username: `root@mail.com`
     - Password: `root123`

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

## Conclusion

Berdasarkan analisis data untuk kasus attrition rate di Perusahaan Jaya Jaya Maju, dapat disimpulkan beberapa hal penting:

**Karakteristik Karyawan yang Melakukan Attrition**:
1. **Demografis**:
   - Usia rata-rata lebih muda (28-33 tahun) dibanding yang bertahan (36-38 tahun)
   - Masa kerja lebih pendek (4-5 tahun) dibanding yang bertahan (7-8 tahun)

2. **Faktor Pekerjaan**:
   - Gaji bulanan lebih rendah (rata-rata 20-30% lebih rendah dari yang bertahan)
   - Lebih sering melakukan overtime (attrition rate 2-3x lebih tinggi pada karyawan overtime)
   - Tingkat kepuasan kerja lebih rendah (terutama level 1-2)

3. **Departemen**:
   - Departemen Sales memiliki attrition rate tertinggi (>15%)
   - Departemen Research & Development memiliki jumlah attrition terbanyak (karena jumlah karyawan lebih banyak)

**Rekomendasi Strategi Retention**:
1. Program pengembangan karir untuk karyawan muda (usia <30 tahun)
2. Review sistem kompensasi, terutama untuk karyawan dengan masa kerja 3-5 tahun
3. Intervensi khusus untuk departemen Sales dengan program mentoring
4. Monitoring khusus untuk karyawan yang sering overtime
5. Program peningkatan kepuasan kerja melalui survey berkala

**Impact**:
Implementasi solusi ini diharapkan dapat membantu Jaya Jaya Maju:
- Mengurangi attrition rate dari >10% menjadi di bawah rata-rata industri (6-8%)
- Meningkatkan produktivitas melalui stabilitas SDM
- Mengoptimalkan biaya rekrutmen dan training karyawan baru
