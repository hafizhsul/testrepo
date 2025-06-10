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

**Sumber data**:  
Dataset yang digunakan dalam proyek ini adalah [students' performance](https://github.com/dicodingacademy/dicoding_dataset/blob/main/students_performance/data.csv) yang berisi informasi tentang kinerja akademis siswa.

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
Jelaskan tentang business dashboard yang telah dibuat. Jika ada, sertakan juga link untuk mengakses dashboard tersebut.

## Menjalankan Sistem Machine Learning
Jelaskan cara menjalankan protoype sistem machine learning yang telah dibuat. Selain itu, sertakan juga link untuk mengakses prototype tersebut.

```

```

## Conclusion
Jelaskan konklusi dari proyek yang dikerjakan.

### Rekomendasi Action Items
Berikan beberapa rekomendasi action items yang harus dilakukan perusahaan guna menyelesaikan permasalahan atau mencapai target mereka.
- action item 1
- action item 2
