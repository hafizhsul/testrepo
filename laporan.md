# Proyek Akhir: Menyelesaikan Permasalahan Institusi Pendidikan Jaya Jaya Institut

## Business Understanding
Jaya Jaya Institut adalah institusi pendidikan perguruan tinggi yang telah berdiri sejak tahun 2000. Meskipun memiliki reputasi yang baik, institusi ini menghadapi masalah tingginya angka dropout siswa. Deteksi dini siswa berisiko dropout diperlukan untuk memberikan intervensi yang tepat.

### Permasalahan Bisnis
1. Tingginya angka dropout siswa yang berdampak pada reputasi institusi.
2. Kebutuhan untuk memonitor performa siswa secara real-time.
3. Kurangnya alat prediktif untuk mengidentifikasi siswa berisiko sejak dini.

### Cakupan Proyek
1. Menganalisis faktor penyebab terjadinya dropout pada siswa
2. Membangun model machine learning untuk memprediksi risiko dropout siswa.
3. Membuat dashboard visualisasi untuk memantau performa siswa dan faktor risiko.

### Persiapan

**Sumber data**: Dataset yang digunakan dalam proyek ini adalah [students' performance](https://github.com/dicodingacademy/dicoding_dataset/blob/main/students_performance/data.csv) yang berisi informasi tentang kinerja akademis siswa.

**Tools yang Digunakan**
1. **Machine Learning**: Scikit-learn (model klasifikasi).
2. **Dashboard**: Metabase (visualisasi interaktif).
3. **Deployment**: Streamlit Community Cloud.

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

## Business Dashboard
![Screenshot_20](https://github.com/user-attachments/assets/9df81b26-8757-40d8-a8f3-3ebe239599b8)

![Screenshot_21](https://github.com/user-attachments/assets/7b51d6be-fc3a-4b05-aacf-acf4303f6db8)

Dashboard dibuat menggunakan Metabase untuk memvisualisasikan:
1. **Distribusi Dropout per Jurusan**: Analisis tren dropout berdasarkan program studi (contoh: Manajemen, Teknologi).
2. **Faktor Risiko Utama**:
   - Status beasiswa (holder vs non-holder).
   - Kualifikasi pendidikan orang tua.
   - Status keuangan (tunggakan biaya).
3. **Dashboard Interaktif**: Filter data berdasarkan kriteria seperti usia, jurusan, dan status akademik.

Akses dashboard di `http://localhost:3000` dengan:
- Username: `root@mail.com`
- Password: `root123`

## Menjalankan Sistem Machine Learning

Prototype prediksi dropout diimplementasikan dengan **Streamlit**:

**Cara Menjalankan**:
1. **Lokal**:
   ```
   streamlit run app.py
   ```
3. **Cloud**: Akses via Link [Prototype](https://studentdropoutapp-7tgx6ok6vt647hkx9egmdd.streamlit.app/).

![Screenshot_15](https://github.com/user-attachments/assets/60a71064-94cd-4d44-a54f-b488483cee16)

![Screenshot_16](https://github.com/user-attachments/assets/4a9f4366-e176-4ff9-9af6-1cb9311502a0)

![Screenshot_17](https://github.com/user-attachments/assets/fa736cb2-5752-4787-90be-ffbfe870ec15)

**Fitur Prototype**
- **Input Data**:
  - Informasi pribadi (gender, usia).
  - Status akademik (beasiswa, tunggakan biaya).
  - Latar belakang keluarga (kualifikasi orang tua).
    
- **Hasil Prediksi**:
  - Probabilitas risiko dropout (76% Low Risk).
  - Rekomendasi intervensi ("Monitor perubahan performa").

## Conclusion
Proyek ini memberikan gambaran yang komprehensif tentang performa siswa di Jaya Jaya Institut dan masalah dropout yang dihadapi. Dengan total 4.424 siswa terdaftar, ditemukan bahwa 1.421 siswa telah mengalami dropout, yang menunjukkan angka dropout sebesar 32%.

**Analisis Utama**:
1. **Dropout Berdasarkan Usia**: Data menunjukkan bahwa jumlah dropout paling tinggi terjadi pada rentang usia muda, terutama di bawah 20 tahun. Ini mengisyaratkan perlunya perhatian tambahan pada siswa yang lebih muda, yang mungkin menghadapi lebih banyak tantangan dalam menyesuaikan diri dengan kehidupan kampus.
2. **Dropout Berdasarkan Jenis Kelamin**: Dari analisis, terdapat perbedaan signifikan antara dropout siswa laki-laki dan perempuan, dengan jumlah perempuan yang dropout lebih rendah daripada laki-laki. Hal ini memberikan insight bahwa ada kebutuhan untuk mengidentifikasi faktor-faktor yang menyebabkan perbedaan ini.
3. **Dropout Berdasarkan Kursus**: Kursus seperti Manajemen dan Keperawatan menunjukkan angka dropout yang tinggi. Oleh karena itu, perlu dilakukan evaluasi dan penyesuaian dalam kurikulum serta metodologi pengajaran untuk jurusan-jurusan ini.
4. **Analisis Berdasarkan Kualifikasi Orang Tua**: Terdapat hubungan antara kualifikasi pendidikan orang tua dan tingkat dropout siswa. Siswa dengan orang tua yang memiliki pendidikan yang lebih rendah cenderung memiliki risiko lebih tinggi untuk dropout. Ini menunjukkan perlunya program dukungan yang melibatkan keluarga dalam pendidikan anak-anak mereka.

### Rekomendasi Action Items
Berdasarkan analisis yang telah dilakukan selama proyek, berikut adalah beberapa rekomendasi action items yang dapat diterapkan oleh Jaya Jaya Institut untuk mengurangi angka dropout siswa:
1. **Implementasi Program Bimbingan Akademik**: Berikan bimbingan kepada siswa yang berisiko tinggi mengalami dropout berdasarkan hasil model prediksi. Sesi ini dapat berupa pendampingan akademik dan konsultasi psikologis.
2. **Meningkatkan Komunikasi dengan Orang Tua**: Membina hubungan yang lebih baik dengan orang tua siswa agar lebih terlibat dalam pendidikan anak-anak mereka. Hal ini dapat membantu memotivasi siswa dan mendukung mereka dalam menghadapi tantangan akademik.
3. **Menawarkan Program Kesejahteraan Siswa**: Implementasikan program yang di fokuskan pada kesejahteraan fisik dan mental siswa, termasuk workshop untuk mengembangkan keterampilan sosial dan manajemen waktu.
4. **Menyediakan Beasiswa dan Bantuan Keuangan**: Meningkatkan kesempatan untuk mendapatkan beasiswa bagi siswa berprestasi, serta memberikan bantuan keuangan kepada siswa yang menghadapi masalah membayar biaya pendidikan.
