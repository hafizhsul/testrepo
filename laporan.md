# Laporan Proyek Machine Learning - Masdika Ilhan Mansiz

## Domain Proyek

Manajemen sumber daya manusia (Human Resources Management) merupakan salah satu aspek krusial dalam operasional perusahaan modern. Employee turnover atau churn karyawan menjadi tantangan signifikan bagi perusahaan karena dapat mengakibatkan kerugian finansial yang substansial, mulai dari biaya rekrutmen, pelatihan karyawan baru, hingga kehilangan produktivitas dan pengetahuan institusional [[1](https://www.researchgate.net/publication/236145687_Retaining_Talent_Replacing_Misconceptions_With_Evidence-Based_Strategies)].

Berdasarkan riset dari Society for Human Resource Management (SHRM), biaya penggantian satu karyawan dapat mencapai 50-200% dari gaji tahunan karyawan tersebut, tergantung pada level dan kompleksitas posisi. Dalam era digital saat ini, perusahaan mulai memanfaatkan teknologi machine learning untuk memprediksi kemungkinan karyawan akan keluar dari perusahaan, sehingga dapat mengambil tindakan preventif yang tepat [[2](https://www.scirp.org/journal/paperinformation?paperid=116209)].

**Mengapa dan bagaimana masalah tersebut harus diselesaikan:**
- **Urgency**: Tingkat turnover yang tinggi dapat mengganggu stabilitas operasional dan meningkatkan biaya operasional perusahaan
- **Impact**: Prediksi yang akurat dapat membantu HR department mengambil tindakan proaktif untuk mempertahankan karyawan berkualitas
- **Solution**: Machine learning dapat mengidentifikasi pola dan faktor-faktor yang mempengaruhi keputusan karyawan untuk keluar dari perusahaan

## Business Understanding

Employee churn merupakan tantangan strategis yang mengakibatkan kerugian finansial hingga 50-200% dari gaji tahunan per karyawan. Dalam konteks dataset IBM HR Analytics dengan tingkat churn 16.1% (237 dari 1,470 karyawan), predictive analytics dapat membantu perusahaan mengidentifikasi early warning signals dan mengimplementasikan targeted retention strategies. Model prediktif ini memungkinkan stakeholder seperti CHRO dan HR Business Partners untuk membuat keputusan strategis berbasis data, mengurangi turnover rate hingga 25-40%, dan menghasilkan ROI signifikan melalui penghematan biaya rekrutmen dan training [[3](https://www.shrm.org/about/press-room/shrm-releases-2022-employee-benefits-survey)].

### Problem Statements
- Perusahaan mengalami tingkat turnover karyawan yang tinggi dan tidak dapat memprediksi karyawan mana yang berisiko untuk keluar dari perusahaan
- Kurangnya insight tentang faktor-faktor yang paling berpengaruh terhadap keputusan karyawan untuk meninggalkan perusahaan
- Tidak adanya sistem early warning untuk mengidentifikasi karyawan yang berpotensi churn sehingga perusahaan tidak dapat mengambil tindakan preventif

### Goals
- Membangun model prediktif yang dapat mengidentifikasi karyawan dengan risiko tinggi untuk keluar dari perusahaan dengan akurasi minimal 80%
- Mengidentifikasi dan menganalisis faktor-faktor utama yang mempengaruhi employee churn melalui feature importance analysis
- Mengembangkan sistem prediksi yang dapat diimplementasikan untuk monitoring berkelanjutan dan early intervention

### Solution Statements
- **Solusi 1**: Mengimplementasikan tiga algoritma berbeda (Random Forest, Logistic Regression, dan Gradient Boosting) untuk perbandingan performa
  - Metrik evaluasi yang akan digunakan: Accuracy dan AUC-ROC
  - Expected outcome: Identifikasi model terbaik dengan akurasi > 80%

- **Solusi 2**: Melakukan analisis feature importance untuk mengidentifikasi faktor-faktor kunci yang mempengaruhi churn
  - Metrik evaluasi yang akan digunakan: Feature importance scores dan visualisasi
  - Expected outcome: Insight yang actionable untuk HR department

- **Solusi 3**: Melakukan hyperparameter tuning pada model terbaik untuk optimasi performa
  - Metrik evaluasi yang akan digunakan: Grid Search Cross Validation dengan scoring accuracy
  - Expected outcome: Peningkatan performa model melalui optimasi parameter

## Data Understanding

Dataset yang digunakan dalam proyek ini adalah IBM HR Analytics Employee Attrition & Performance Dataset yang tersedia di platform Kaggle. Dataset ini merupakan dataset simulasi yang dibuat oleh IBM data scientists untuk keperluan pembelajaran dan analisis HR analytics.

**Informasi Dataset:**
- **Sumber Data**: IBM HR Analytics Employee Attrition & Performance Dataset
- **Link Dataset**: https://www.kaggle.com/pavansubhasht/ibm-hr-analytics-attrition-dataset
- **Jumlah Data**: 1470 baris dan 35 kolom
- **Ukuran File**: Approximately 300 KB
- **Format**: CSV (Comma Separated Values)

**Deskripsi Variabel:**

Variabel-variabel pada IBM HR Analytics Dataset adalah sebagai berikut:
- **Age**: Usia karyawan (numerik, rentang 18-60 tahun)
- **Attrition**: Status churn karyawan (kategorikal, "Yes"/"No" - target variable)
- **BusinessTravel**: Frekuensi perjalanan bisnis (kategorikal, "Non-Travel"/"Travel_Rarely"/"Travel_Frequently")
- **DailyRate**: Tarif harian karyawan (numerik, dalam USD)
- **Department**: Departemen tempat karyawan bekerja (kategorikal, "Sales"/"Research & Development"/"Human Resources")
- **DistanceFromHome**: Jarak rumah ke kantor (numerik, dalam miles)
- **Education**: Level pendidikan (numerik, 1-5 scale)
- **EducationField**: Bidang pendidikan (kategorikal, "Life Sciences"/"Medical"/"Marketing"/dll)
- **EmployeeCount**: Jumlah karyawan (konstanta, value=1)
- **EmployeeNumber**: ID unik karyawan (numerik)
- **EnvironmentSatisfaction**: Tingkat kepuasan lingkungan kerja (numerik, 1-4 scale)
- **Gender**: Jenis kelamin (kategorikal, "Male"/"Female")
- **HourlyRate**: Tarif per jam (numerik, dalam USD)
- **JobInvolvement**: Tingkat keterlibatan dalam pekerjaan (numerik, 1-4 scale)
- **JobLevel**: Level jabatan (numerik, 1-5 scale)
- **JobRole**: Peran pekerjaan (kategorikal, "Sales Executive"/"Research Scientist"/dll)
- **JobSatisfaction**: Tingkat kepuasan kerja (numerik, 1-4 scale)
- **MaritalStatus**: Status pernikahan (kategorikal, "Single"/"Married"/"Divorced")
- **MonthlyIncome**: Pendapatan bulanan (numerik, dalam USD)
- **MonthlyRate**: Tarif bulanan (numerik, dalam USD)
- **NumCompaniesWorked**: Jumlah perusahaan tempat pernah bekerja (numerik)
- **Over18**: Indikator usia di atas 18 tahun (kategorikal, konstanta "Y")
- **OverTime**: Status lembur (kategorikal, "Yes"/"No")
- **PercentSalaryHike**: Persentase kenaikan gaji (numerik, dalam %)
- **PerformanceRating**: Rating performa (numerik, 1-4 scale)
- **RelationshipSatisfaction**: Tingkat kepuasan hubungan (numerik, 1-4 scale)
- **StandardHours**: Jam kerja standar (konstanta, value=80)
- **StockOptionLevel**: Level stock option (numerik, 0-3 scale)
- **TotalWorkingYears**: Total tahun pengalaman kerja (numerik)
- **TrainingTimesLastYear**: Jumlah training tahun lalu (numerik)
- **WorkLifeBalance**: Keseimbangan kerja-hidup (numerik, 1-4 scale)
- **YearsAtCompany**: Lama bekerja di perusahaan current (numerik)
- **YearsInCurrentRole**: Lama di posisi current (numerik)
- **YearsSinceLastPromotion**: Tahun sejak promosi terakhir (numerik)
- **YearsWithCurrManager**: Lama dengan manager current (numerik)

### Exploratory Data Analysis (EDA)

**Analisis Statistik Deskriptif:**
- Dataset terdiri dari 1470 karyawan dengan 237 karyawan (16.1%) yang mengalami churn
- Distribusi usia karyawan cenderung normal dengan rata-rata 37 tahun
- Mayoritas karyawan bekerja di departemen Research & Development (65%)
- Terdapat ketimpangan dalam distribusi target variable (imbalanced dataset)

**Visualisasi Data:**
Berdasarkan kode yang diimplementasikan, beberapa visualisasi penting yang dihasilkan:
- **Count Plot Attrition**: Menunjukkan distribusi kelas target yang tidak seimbang
  ![image](https://github.com/user-attachments/assets/818570ef-75f7-4793-a9f5-89a78edfebf8)
  
- **Correlation Heatmap**: Mengidentifikasi korelasi antar variabel numerik
  ![image](https://github.com/user-attachments/assets/aa20e3f0-d7eb-46c6-a54d-9cd63fabc138)

- **ROC Curves**: Membandingkan performa model yang berbeda
  ![image](https://github.com/user-attachments/assets/ca4d4101-dc61-4640-84f1-81a781d3b93d)

- **Feature Importance Plot**: Menampilkan 10 fitur paling berpengaruh
  ![image](https://github.com/user-attachments/assets/aa223a53-3d6b-430f-95d0-a6662f0d5b86)

- **Age Distribution**: Analisis distribusi usia berdasarkan status churn
  ![image](https://github.com/user-attachments/assets/7c2e7772-7d2d-463b-8e11-2cab1a96a88e)

- **Monthly Income by Job Role**: Analisis income berdasarkan peran dan status churn
  ![image](https://github.com/user-attachments/assets/eefe80a4-debf-4ba8-99c1-8ba7d8fdfc05)

## Data Preparation

Pada bagian ini menerapkan dan menyebutkan teknik data preparation yang dilakukan sesuai dengan implementasi dalam kode.

### Proses Data Preparation:

1. **Data Loading dan Initial Exploration**
   ```python
   df = pd.read_csv("WA_Fn-UseC_-HR-Employee-Attrition.csv")
   print(df.head())
   print(df.info())
   ```

2. **Target Variable Encoding**
   - **Target Encoding**: Mengkonversi target variable 'Attrition' dari "Yes"/"No" menjadi 1/0
   ```python
   df['Attrition'] = df['Attrition'].apply(lambda x: 1 if x == 'Yes' else 0)
   ```

3. **Feature Cleaning**
   - **Removal of Irrelevant Features**: Menghapus kolom yang tidak memberikan informasi prediktif
   ```python
   cols_to_drop = ['EmployeeNumber', 'EmployeeCount', 'Over18', 'StandardHours']
   df.drop(columns=cols_to_drop, inplace=True)
   ```

4. **Categorical Feature Encoding**
   - **Label Encoding**: Mengkonversi semua variabel kategorikal menjadi numerik
   ```python
   cat_cols = df.select_dtypes(include=['object']).columns
   le = LabelEncoder()
   for col in cat_cols:
       df[col] = le.fit_transform(df[col])
   ```

5. **Data Splitting**
   - **Train-Test Split**: 80% untuk training, 20% untuk testing
   ```python
   X = df.drop('Attrition', axis=1)
   y = df['Attrition']
   X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
   ```

6. **Feature Scaling**
   - **Standardization**: Menerapkan StandardScaler untuk menormalisasi fitur numerik
   ```python
   scaler = StandardScaler()
   X_train = scaler.fit_transform(X_train)
   X_test = scaler.transform(X_test)
   ```

### Alasan Data Preparation:

**Mengapa setiap tahapan data preparation diperlukan:**

- **Removal of Irrelevant Features**: Kolom seperti EmployeeNumber adalah identifier unik yang tidak memiliki nilai prediktif, sementara EmployeeCount, Over18, dan StandardHours adalah konstanta yang tidak memberikan variasi informasi

- **Categorical Encoding**: Machine learning algorithms memerlukan input numerik, sehingga variabel kategorikal perlu dikonversi. Label Encoder dipilih karena efisien untuk tree-based models yang akan digunakan

- **Feature Scaling**: StandardScaler diperlukan terutama untuk Logistic Regression yang sensitif terhadap skala fitur. Random Forest relatif robust terhadap skala, namun standardisasi memastikan konsistensi

- **Target Transformation**: Konversi target dari string ke binary (0/1) diperlukan untuk classification algorithms

## Modeling

Tahapan modeling melibatkan implementasi dan perbandingan tiga algoritma machine learning untuk menyelesaikan masalah prediksi churn karyawan.

### Algoritma yang Digunakan:

#### 1. Random Forest Classifier
**Definisi**: Random Forest adalah metode ensemble berbasis decision tree yang menggunakan teknik **bagging** untuk membentuk banyak tree keputusan dari subset data yang di-random. Hasil akhir dipilih berdasarkan voting mayoritas dari semua tree.

**Kelebihan:**
- Robust terhadap overfitting
- Dapat menangani fitur kategorikal dan numerik
- Memberikan feature importance yang interpretable
- Tidak sensitif terhadap outliers
- Dapat menangani missing values dengan baik

**Kekurangan:**
- Computational cost yang tinggi untuk dataset besar
- Kurang interpretable dibandingkan decision tree tunggal
- Dapat bias terhadap fitur dengan lebih banyak level

**Parameter yang Digunakan dan Penjelasannya:**
- `n_estimators=100`: Jumlah tree keputusan dalam ensemble. Dipilih 100 untuk menyeimbangkan akurasi dan komputasi.
- `random_state=42`: Seed untuk reproduktibilitas hasil.

**Implementasi:**
```python
rf_model = RandomForestClassifier(n_estimators=100, random_state=42)
```

#### 2. Logistic Regression
**Definisi**: Logistic Regression merupakan algoritma klasifikasi linier yang digunakan untuk memperkirakan probabilitas kejadian suatu kelas berdasarkan hubungan linier logit dari variabel input.

**Kelebihan:**
- Sederhana dan cepat dalam training
- Probabilistic output yang mudah diinterpretasi
- Tidak memerlukan tuning parameter yang kompleks
- Robust dan stable

**Kekurangan:**
- Asumsi linear relationship antara fitur dan log-odds
- Sensitif terhadap outliers
- Dapat struggle dengan fitur yang sangat berkorelasi

**Parameter Default yang Relevan:**
- `penalty='l2'`: Regularisasi L2 (Ridge) untuk mencegah overfitting.
- `C=1.0`: Kebalikan dari kekuatan regularisasi (nilai kecil = regularisasi kuat).
- `solver='lbfgs'`: Algoritma optimasi untuk masalah klasifikasi multikelas.
- `max_iter=100`: Maksimum iterasi untuk konvergensi.

**Implementation:**
```python
log_model = LogisticRegression()
log_model.fit(X_train, y_train)
```

#### 3. Gradient Boosting Classifier
**Definisi**: Gradient Boosting adalah metode ensemble yang membentuk tree keputusan secara bertahap, di mana setiap tree baru memperbaiki kesalahan dari tree sebelumnya. Model ini menggunakan prinsip boosting dengan loss function gradient.

**Kelebihan:**
- Often achieves high accuracy
- Dapat menangani berbagai tipe data
- Built-in regularization
- Sequential learning yang powerful

**Kekurangan:**
- Prone to overfitting jika tidak di-tune dengan baik
- Computational cost yang tinggi
- Lebih kompleks untuk di-interpret

**Parameter Default yang Relevan:**
- `n_estimators=100`: Jumlah tree boosting stages.
- `learning_rate=0.1`: Tingkat pembelajaran (shrinkage) untuk setiap tree.
- `max_depth=3`: Kedalaman maksimal setiap tree.
- `min_samples_split=2`: Mirip dengan Random Forest.

**Implementation:**
```python
gb_model = GradientBoostingClassifier()
gb_model.fit(X_train, y_train)
```

### Hyperparameter Tuning:
Hyperparameter tuning dengan Grid Search pada Random Forest dilakukan untuk mengoptimasi tiga parameter utama: `n_estimators`, `max_depth`, dan `min_samples_split`.

```python
param_grid = {
    'n_estimators': [100, 200],  # Jumlah tree yang diuji
    'max_depth': [None, 10, 20],  # Kedalaman tree: unlimited vs dibatasi
    'min_samples_split': [2, 5]   # Minimum sampel untuk split node
}
```
**Alasan Pemilihan:**
- `n_estimators`: Mengevaluasi trade-off antara performa dan waktu komputasi.
- `max_depth`: Mencegah overfitting dengan membatasi kedalaman.
- `min_samples_split`: Mengontrol granularitas pemisahan node.

### Feature Importance Analysis:

Berdasarkan Random Forest model, top 10 fitur yang paling berpengaruh terhadap churn dapat diidentifikasi melalui feature importance scores dan divisualisasikan untuk memberikan insight kepada HR department.

## Evaluation

Pada bagian evaluasi, digunakan beberapa metrik untuk mengukur performa model klasifikasi yang telah dibangun.

### Metrik Evaluasi yang Digunakan:

#### 1. Accuracy
**Formula**: Accuracy = (TP + TN) / (TP + TN + FP + FN)

**Penjelasan**: Mengukur proporsi prediksi yang benar dari total prediksi. Metrik ini cocok untuk dataset yang balanced, namun dapat misleading untuk imbalanced dataset.

#### 2. AUC-ROC (Area Under the ROC Curve)
**Penjelasan**: Mengukur kemampuan model untuk membedakan antara kelas positif dan negatif. Nilai mendekati 1 menunjukkan performa yang excellent.

### Hasil Evaluasi Model:

![image](https://github.com/user-attachments/assets/481bb078-e1a9-4a95-8a3d-4bd3ec7e5136)

![image](https://github.com/user-attachments/assets/364816f4-8f24-4550-bda9-e626d519ad81)

Berdasarkan implementasi kode dan hasil yang diperoleh:

#### Perbandingan Performa Model:
- **Random Forest**: 
  - Accuracy: 0.88
  - AUC-ROC: 0.74
- **Logistic Regression**: 
  - Accuracy: 0.89
  - AUC-ROC: 0.77
- **Gradient Boosting**: 
  - Accuracy: 0.89
  - AUC-ROC: 0.77

**Tabel perbandingan parameter dan dampaknya:**
| Model | Parameter Kunci | Dampak pada Performa |
| ------------- | ------------- | ------ |
| Random Forest	 | `n_estimators=100`, `max_depth=None` | Akurasi tinggi, sedikit overfit |
| Logistic Reg. | `C=1.0`, `penalty='l2'` | Stabil, interpretasi mudah |
| Gradient Boosting	| `learning_rate=0.1`, `max_depth=3` | Akurasi optimal dengan komputasi efisien |

Secara keseluruhan, **Logistic Regression** dan **Gradient Boosting** menunjukkan performa terbaik dengan akurasi dan AUC yang paling tinggi.

* Jika interpretasi menjadi faktor penting (misalnya untuk HR atau manajemen), maka **Logistic Regression** lebih direkomendasikan karena lebih mudah dijelaskan.
* Jika kompleksitas data tinggi dan interpretasi bukan prioritas utama, maka **Gradient Boosting** bisa menjadi pilihan unggul.

#### **Kembali ke Problem Statements Awal:**

1. **Problem 1:**
   
   "Perusahaan tidak dapat memprediksi karyawan berisiko churn."
   
   **Solusi dari Proyek:**
    - Dibangun tiga model prediktif (Random Forest, Logistic Regression, Gradient Boosting) dengan akurasi >88% dan AUC >0.77.
    - Model terbaik (Logistic Regression) dapat mengidentifikasi karyawan berisiko churn dengan recall 0.45 (klasifikasi positif) dan precision 0.82.
    - Contoh implementasi:
      ``` python
      # Prediksi karyawan berisiko churn
      high_risk_employees = X_test[y_prob_log > 0.7]  # Ambil sampel dengan probabilitas >70%
      ```
      
2. **Problem 2:**

   "Tidak ada insight faktor penyebab churn."

   **Solusi dari Proyek:**
   - Analisis feature importance mengungkap 5 faktor utama churn:
     1. Overtime
     2. MonthlyIncome
     3. Age
     4. JobSatisfaction
     5. YearsAtCompany
   - Visualisasi:
     
     ![image](https://github.com/user-attachments/assets/cd8e24eb-b38f-42b4-8099-41a5071a1418)

   - Rekomendasi bisnis:
     * Berikan insentif untuk karyawan yang sering lembur.
     * Tingkatkan kepuasan kerja di departemen dengan churn tinggi (Sales).
       
2. **Problem 3:**

   "Tidak ada sistem early warning."

   **Solusi dari Proyek:**
   - Dibangun pipeline prediktif yang siap di-deploy:
     ``` python
     import joblib
     joblib.dump(log_model, 'churn_predictor.pkl')  # Model siap produksi
     ```
   - Threshold disesuaikan untuk mengoptimalkan recall (mengurangi false negative):
     ``` python
     y_pred_optimized = (y_prob_log > 0.4).astype(int)  # Threshold 40%
     ```

#### **Jawaban terhadap Problem Statements**

| Problem Statement |	Solusi dari Proyek |	Bukti/Dokumentasi |
| --- | --- | ---|
| Tidak bisa prediksi churn |	Model dengan akurasi 89% dan AUC 0.77 |	Classification Report, ROC Curve |
| Tidak tahu faktor churn |	Identifikasi 5 fitur kunci |	Feature Importance Plot |
| Tidak ada sistem early warning |	Pipeline model siap deploy dengan threshold tuning |	Kode ekspor model & threshold adjustment |

#### **Kesimpulan Final:**
Project ini berhasil menjawab ketiga problem statement awal melalui: (1) pembangunan model prediktif dengan metrik melebihi target (akurasi >80%), (2) analisis faktor risiko churn yang actionable, dan (3) penyediaan infrastruktur prediksi yang siap diintegrasikan ke sistem HR perusahaan.

## Referensi:
1. Allen, D. G., Bryant, P. C., & Vardaman, J. M. "Retaining talent: Replacing misconceptions with evidence-based strategies." Academy of Management Perspectives, vol. 24, no. 2, pp. 48-64, 2010.
2. Saradhi, V. V., & Palshikar, G. K. "Employee churn prediction." Expert Systems with Applications, vol. 38, no. 3, pp. 1999-2006, 2011.
3. Society for Human Resource Management (SHRM). "2022 Employee Benefits: The Evolution of Benefits." SHRM Research, 2022.
4. IBM Watson Analytics. "HR Analytics Employee Attrition & Performance Dataset." Kaggle, 2017. [Online]. Available: https://www.kaggle.com/pavansubhasht/ibm-hr-analytics-attrition-dataset
