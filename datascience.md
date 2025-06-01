# Proyek Akhir: Menyelesaikan Permasalahan HR Perusahaan Jaya Jaya Maju

## Business Understanding

Jaya Jaya Maju merupakan perusahaan multinasional yang telah berdiri sejak tahun 2000 dengan lebih dari 1000 karyawan tersebar di seluruh penjuru negeri. Meskipun telah berkembang menjadi perusahaan besar, Jaya Jaya Maju masih menghadapi kesulitan dalam mengelola karyawan yang berdampak pada tingginya attrition rate hingga lebih dari 10%.

### Permasalahan Bisnis

Berdasarkan kondisi yang dihadapi oleh Jaya Jaya Maju, berikut adalah permasalahan bisnis yang akan diselesaikan:

1. **Tingginya Attrition Rate (>10%)**: Rasio karyawan yang keluar dari perusahaan melebihi standar industri, yang mengindikasikan adanya masalah dalam employee retention.

2. **Kurangnya Pemahaman Faktor Penyebab**: Departemen HR belum memiliki pemahaman yang mendalam tentang faktor-faktor spesifik yang menyebabkan karyawan memutuskan untuk keluar dari perusahaan.

3. **Tidak Adanya Sistem Prediksi Dini**: Perusahaan belum memiliki sistem yang dapat memprediksi karyawan mana yang berpotensi untuk resign, sehingga tidak dapat melakukan tindakan preventif.

4. **Kurangnya Tools Monitoring**: Departemen HR membutuhkan dashboard untuk memantau dan menganalisis berbagai metrik terkait employee retention secara real-time.

5. **Dampak Finansial dan Operasional**: Tingginya turnover rate berdampak pada meningkatnya biaya rekrutmen, pelatihan, dan hilangnya institutional knowledge.

### Cakupan Proyek

Proyek ini akan mencakup beberapa tahapan utama untuk menyelesaikan permasalahan attrition rate di Jaya Jaya Maju:

1. **Analisis Data Karyawan**
   - Exploratory Data Analysis (EDA) untuk memahami karakteristik dataset
   - Identifikasi pola dan tren dalam data employee attrition
   - Analisis korelasi antara berbagai faktor dengan keputusan karyawan untuk keluar

2. **Pengembangan Model Prediksi**
   - Implementasi algoritma machine learning untuk memprediksi employee attrition
   - Evaluasi dan optimasi model untuk mendapatkan performa terbaik
   - Identifikasi feature importance untuk memahami faktor-faktor kunci

3. **Pembuatan Business Dashboard**
   - Pengembangan dashboard interaktif menggunakan Metabase
   - Visualisasi key metrics dan insights untuk departemen HR
   - Implementasi monitoring real-time untuk employee retention

4. **Rekomendasi Strategis**
   - Analisis actionable insights berdasarkan hasil model dan dashboard
   - Penyusunan strategi untuk mengurangi attrition rate
   - Action items yang dapat diimplementasikan oleh departemen HR

### Persiapan

**Sumber data**: Dataset karyawan Jaya Jaya Maju yang berisi informasi demografis, karakteristik pekerjaan, kompensasi, dan status attrition karyawan.

**Setup environment**:
```bash
# Install required libraries
pip install pandas numpy matplotlib seaborn scikit-learn
pip install plotly dash streamlit
pip install jupyter notebook

# Setup Metabase dengan Docker
docker run -d -p 3000:3000 --name metabase metabase/metabase

# Alternative setup untuk dashboard
pip install metabase-api
```

**Tools dan Technologies**:
- **Python**: Pandas, NumPy, Scikit-learn untuk data analysis dan machine learning
- **Visualization**: Matplotlib, Seaborn, Plotly untuk data visualization
- **Dashboard**: Metabase untuk business intelligence dashboard
- **Environment**: Jupyter Notebook untuk development dan documentation

## Business Dashboard

Business dashboard telah dibuat menggunakan Metabase untuk membantu departemen HR dalam monitoring dan analisis faktor-faktor yang mempengaruhi attrition rate. Dashboard ini menyediakan visualisasi interaktif yang memungkinkan stakeholder untuk:

**Fitur Utama Dashboard:**

1. **Overview Metrics**
   - Current attrition rate dan trend bulanan
   - Jumlah total karyawan dan distribusi per departemen
   - Perbandingan attrition rate antar departemen

2. **Demographic Analysis**
   - Distribusi attrition berdasarkan usia, jenis kelamin, dan status pernikahan
   - Analisis attrition berdasarkan tingkat pendidikan
   - Visualisasi geographic distribution karyawan

3. **Job-Related Factors**
   - Attrition rate berdasarkan job role dan job level
   - Analisis kepuasan kerja dan work-life balance
   - Distribusi jam kerja dan overtime

4. **Compensation Analysis**
   - Korelasi antara salary dan attrition rate
   - Analisis salary increment dan promotion frequency
   - Perbandingan kompensasi antar departemen

**Akses Dashboard:**
- **URL**: `http://localhost:3000` (running di local environment)
- **Username**: `root@mail.com`
- **Password**: `root123`

*Dashboard dapat diakses setelah menjalankan container Metabase dan melakukan setup database connection dengan dataset Jaya Jaya Maju.*

## Conclusion

Berdasarkan analisis data dan pengembangan model machine learning untuk kasus attrition rate di Jaya Jaya Maju, dapat disimpulkan beberapa hal penting:

**Key Findings:**

1. **Faktor Utama Attrition**: Analisis menunjukkan bahwa faktor-faktor seperti job satisfaction, work-life balance, compensation, dan career development opportunities menjadi prediktor utama employee attrition.

2. **Model Prediksi**: Model machine learning yang dikembangkan mampu memprediksi karyawan yang berpotensi resign dengan akurasi tinggi, memungkinkan departemen HR untuk melakukan intervensi preventif.

3. **Pola Attrition**: Terdapat pola spesifik dalam attrition berdasarkan demografis, job role, dan karakteristik pekerjaan yang dapat digunakan untuk strategi retention yang lebih targeted.

4. **Dashboard Monitoring**: Business dashboard yang telah dibuat memberikan visibility real-time terhadap key metrics dan memungkinkan monitoring proaktif terhadap faktor-faktor risiko attrition.

**Impact:**
Implementasi solusi ini diharapkan dapat membantu Jaya Jaya Maju mengurangi attrition rate dari >10% menjadi di bawah rata-rata industri (sekitar 6-8%), sehingga dapat menghemat biaya rekrutmen dan meningkatkan stabilitas operasional perusahaan.
