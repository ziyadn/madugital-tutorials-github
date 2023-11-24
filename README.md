# madugital-tutorials-github
ini adalah contoh mini project Habis Kerja : Data Scientist Course, tentang Modelling Leads Scoring perusahaan Madugital.

---

# Proyek Skor Peluang Leads (Lead Scoring)

Proyek ini akan mengikuti metodologi CRISP-DM, dengan fokus pada pengembangan model yang tidak hanya akurat dari sudut pandang statistik tetapi juga memberikan wawasan bisnis yang dapat ditindaklanjuti untuk meningkatkan konversi leads.

# Tahapan Proyek
1. [**Pemahaman Bisnis (Business Understanding)**](https://github.com/ziyadn/madugital-tutorials-github/blob/main/README.md#1-pemahaman-bisnis-business-understanding)
2. [**Pemahaman Data (Data Understanding)**](https://github.com/ziyadn/madugital-tutorials-github/blob/main/README.md#2-pemahaman-data-data-understanding)
3. [**Persiapan Data (Data Preparation)**](https://github.com/ziyadn/madugital-tutorials-github/blob/main/README.md#3-persiapan-data-data-preparation)
4. [**Pemodelan Data (Data Modelling)**](https://github.com/ziyadn/madugital-tutorials-github/blob/main/README.md#4-pemodelan-data-data-modelling)
5. [**Evaluasi Model (Model Evaluation)**](https://github.com/ziyadn/madugital-tutorials-github/blob/main/README.md#5-evaluasi-model-model-evaluation)
6. [**Deployment**](https://github.com/ziyadn/madugital-tutorials-github/blob/main/README.md#6-deployment)

Setiap tahap akan didokumentasikan secara terperinci di dalam repositori ini.

## 1. Pemahaman Bisnis (Business Understanding)
### 1.1. Tujuan Bisnis
Tujuan dari proyek ini adalah untuk mengembangkan model machine learning yang dapat memberikan peluang atau skor kepada leads (calon pelanggan) berdasarkan kemungkinan mereka untuk membeli produk kita. Skor ini akan membantu tim pemasaran dan penjualan dalam mengidentifikasi dan memprioritaskan leads yang lebih cenderung untuk dikonversi menjadi pelanggan yang membayar.

### 1.2. Pertanyaan Bisnis Utama
- Bagaimana kita dapat memprediksi peluang leads untuk menjadi pelanggan yang konversi?
- Bagaimana kita dapat mengelompokkan leads ke dalam kategori HOT, MEDIUM, dan COLD berdasarkan skor peluang mereka?
- Dengan menggunakan model prediktif ini, seberapa akurat kita dapat mengidentifikasi dan memprioritaskan leads?

### 1.3. Kriteria Keberhasilan Proyek
- Model harus mampu memberikan skor peluang yang akurat dengan mengklasifikasikan leads ke dalam kategori HOT, MEDIUM, atau COLD.
- Kinerja model harus dinilai dengan metrik yang relevan seperti akurasi, precision, recall, dan F1-Score.
- Model harus menyediakan threshold yang dapat disesuaikan untuk kategorisasi sehingga dapat disesuaikan dengan strategi penjualan dan pemasaran perusahaan.

### 1.4. Konteks Tambahan
Data yang telah diupload akan digunakan untuk melatih model machine learning. Kami akan menggunakan `predict_proba` untuk mengestimasi peluang dan kemudian menetapkan setiap lead ke salah satu dari tiga kategori berdasarkan threshold yang akan kita tentukan selama fase pemodelan. Pengelompokan ini akan memungkinkan tim penjualan untuk menyusun strategi yang lebih baik dan meningkatkan efisiensi dalam mengonversi prospek menjadi penjualan yang sukses.

### 1.5. Data
Data untuk proyek ini tersedia dalam file `lead_scoring.csv`, dengan kamus data terkait yang disediakan dalam `Leads Data Dictionary.xlsx`.

---
## 2. Pemahaman Data (Data Understanding)
Pada tahap ini, kami telah memuat data ke dalam lingkungan Python menggunakan pandas dan melakukan inspeksi awal. Berikut adalah temuan awal kami:

- Data terdiri dari 9240 baris dan 37 kolom.
- Setiap kolom mewakili informasi berikut:
  - **Prospect ID**: Identitas unik setiap calon pelanggan.
  - **Lead Number**: Nomor yang diberikan kepada setiap prospek yang diperoleh.
  - **Lead Origin**: Asal usul bagaimana prospek mendapatkan akses ke dalam sistem.
  - **Lead Source**: Sumber dari mana prospek diakuisisi.
  - **Do Not Email**: Tandai jika prospek tidak ingin dihubungi melalui email.
  - **Do Not Call**: Tandai jika prospek tidak ingin dihubungi melalui telepon.
  - **Converted**: Apakah prospek berhasil dikonversi menjadi pelanggan.
  - **TotalVisits**: Jumlah total kunjungan yang dilakukan oleh prospek ke website.
  - **Total Time Spent on Website**: Total waktu yang dihabiskan oleh prospek di website.
  - **Page Views Per Visit**: Rata-rata halaman yang dilihat per kunjungan.
  - **Last Activity**: Aktivitas terakhir yang dilakukan oleh pelanggan.
  - **Country**: Negara dari pelanggan.
  - **Specialization**: Domain industri tempat pelanggan bekerja.
  - **How did you hear about Madugital**: Sumber informasi dari mana pelanggan mengetahui tentang Madugital.
  - **What is your current occupation**: Menunjukkan apakah pelanggan adalah seorang pelajar, menganggur, atau bekerja.
  - **What matters most to you in choosing this product**: Apa yang paling dihargai pelanggan ketika memilih produk.
  - **Search**: Menunjukkan apakah pelanggan melihat iklan dalam hasil pencarian mesin pencari.
  - **Through Recommendations**: Menunjukkan apakah pelanggan datang melalui rekomendasi.
  - **Receive More Updates About Our Courses**: Menunjukkan jika pelanggan memilih untuk menerima pembaruan tentang kursus.
  - **Tags**: Tag yang diberikan kepada pelanggan yang menunjukkan status terkini dari lead.
  - **Lead Quality**: Menunjukkan kualitas dari lead berdasarkan data yang diperoleh.
  - **Update me on Supply Chain Content**: Menunjukkan apakah pelanggan ingin mendapatkan pembaruan tentang konten rantai pasokan.
  - **Lead Profile**: Profil lead yang ditetapkan untuk setiap pelanggan berdasarkan tingkat keterlibatan mereka.
  - **City**: Kota dari pelanggan.
  - **Asymmetrique Activity Index**: Indeks yang diberikan kepada setiap pelanggan berdasarkan aktivitas mereka.
  - **Asymmetrique Profile Index**: Indeks yang diberikan kepada setiap pelanggan berdasarkan profil mereka.
  - ... [dan seterusnya untuk kolom lainnya].
- Terdapat nilai yang hilang yang tersebar di beberapa kolom penting seperti `Country` (2461 nilai hilang), `Specialization` (1438), dan `City` (1420).
- Statistik deskriptif dasar menunjukkan bahwa:
  - Rata-rata (`mean`) waktu yang dihabiskan di website adalah sekitar 487.7 menit.
  - Rata-rata kunjungan (`TotalVisits`) adalah sekitar 3.4 kali.
  - Skor aktivitas (`Asymmetrique Activity Score`) dan skor profil (`Asymmetrique Profile Score`) memiliki rata-rata sekitar 14.3 dan 16.3 secara berturut-turut.

Temuan awal ini akan digunakan untuk menginformasikan strategi persiapan data dan pemodelan kami.

## 3. Persiapan Data (Data Preparation)
### 3.1. Data Cleaning and Preprocessing
1. Duplicate Removal: membuang records yang duplikasi untuk menjaga integritas data.
2. Binary Encoding: Kolom tertentu yang memiliki nilai 'Yes' atau 'No' akan dikonversikan ke binary format (1 untuk 'Yes', 0 untuk 'No'). Hal ini dilakukan pada kolom `Do Not Email`, `Do Not Call`, dan bergbagai macam kolom lain yang terkait dengan preferensi dan consent dari User.

### 3.2. Handling Special Cases in Variables:
1. Gabungkan 'Quick Add Form' dengan 'Lead Ads Form' pada kolom `Lead Origin`.
2. Mengelompokkan Kategori yang jarang muncul (kurang dari 1% dari populasi) menjadi kelompok 'Others' pada kolom: `Lead Source`, `Tags`, dan `Last Notable Activity`.
3. Null values pada `TotalVisits` dan `Page Views Per Visit` diisi dengan nilai 0.
4. Klasifikasi ulang kolom `Last Activity` menjadi 'Good', 'Bad', dan 'Neutral' categories (dengan Null dianggap sebagai 'Bad').
5. Informasi `Country` dikelompokkan menjadi 'Indonesia' dan 'Outside Indonesia'.
6. Nilai 'Select' dan Null values di kolom `Specialization`, `How did you hear about Madugital`, `Lead Profile`, dan `City` diganti dengan 'Not Specified'.
7. Null values di kolom `What is your current occupation`, `What matters most to you in choosing a product`, dan `Lead Quality` diisi dengan 'Not Specified'.
8. Missing values di kolom `Asymmetrique Activity` dan `Profile` dihandling dengan mengisi score menjadi 0 dan indexes menjadi '00.Zero'.

### 3.3. Data Transformation and Preprocessing Pipeline
1. **Preprocessing Pipeline**: Sebuah pipeline dibuat untuk numerical dan categorical features. Untuk numerical features, kami menerapkan constant imputation dan scaling. Sedangkan untuk categorical features, constant imputation dan one-hot encoding diterapkan.
2. **Data Splitting**: Datasets yang sudah dipersiapkan kemudian dipisahkan menjadi dua bagian yaitu training dan test sets, dengan 80% data digunakan untuk training dan 20% untuk testing. Kami melakukan preprocessing sebelum split train-test karena kami tidak melakukan inputasi statistika *(contohnya: mean, meadian, modus filling)*.

### 3.4. Post-Preprocessing Analysis
**Data Shape Post-Processing:** Setelah praproses data, kami mendapatkan 123 kolom yang siap digunakan untuk training.

## 4. Pemodelan Data (Data Modelling)

### 4.1. Target Column `Converted`
Kolom target yang digunakan adalah `Converted`, yang menandakan konversi pelanggan potensial.

### 4.2. Klasifikasi Model
Kami menggunakan tiga model klasifikasi:
- Logistic Regression
- Decision Tree
- Random Forest

### 4.3. F1 Score sebagai Evaluation Metrics
F1 Score dipilih sebagai metrik evaluasi utama karena memberikan keseimbangan antara Precision dan Recall, terutama penting dalam kasus kelas yang tidak seimbang.

F1 Score sangat penting dalam konteks bisnis, terutama dalam situasi seperti Lead Scoring, di mana tujuannya adalah untuk menilai dan memprioritaskan prospek atau lead berdasarkan kemungkinan mereka untuk berkonversi menjadi pelanggan.

Dalam Lead Scoring:

- **Precision** (Ketepatan) mewakili proporsi lead yang diidentifikasi oleh model sebagai 'berpotensi berkonversi' yang benar-benar berkonversi. Precision yang tinggi berarti bahwa sebagian besar lead yang model prediksi akan berkonversi benar-benar berkonversi, yang mengurangi waktu dan sumber daya yang dihabiskan untuk mengejar lead yang tidak berkualitas.

- **Recall** (Pelacakan) mengukur proporsi lead aktual yang berkonversi yang diidentifikasi oleh model. Recall yang tinggi berarti model berhasil mengidentifikasi sebagian besar lead yang berpotensi berkonversi, sehingga meminimalkan kehilangan peluang dengan mengabaikan prospek yang baik.

F1 Score memberikan keseimbangan antara precision dan recall. Ini penting karena:

1. **Mengoptimalkan Sumber Daya**: Meningkatkan efisiensi dalam alokasi sumber daya penjualan dan pemasaran. Dengan memfokuskan upaya pada lead yang paling mungkin berkonversi, perusahaan dapat menghemat waktu dan uang.

2. **Meningkatkan ROI**: Dengan memprioritaskan lead yang berkualitas, perusahaan dapat meningkatkan peluang konversi, yang pada gilirannya meningkatkan pengembalian investasi (ROI) dari kampanye pemasaran.

3. **Menghindari Kehilangan Peluang**: Sebuah model dengan F1 Score yang tinggi memastikan bahwa perusahaan tidak melewatkan lead yang berpotensi menguntungkan, sambil tetap meminimalkan gangguan yang disebabkan oleh lead yang tidak berkualitas.

Dalam konteks bisnis seperti Lead Scoring, F1 Score membantu menciptakan keseimbangan yang tepat antara mengidentifikasi sebanyak mungkin lead berkualitas tinggi dan memastikan bahwa lead yang ditindaklanjuti benar-benar memiliki peluang tinggi untuk berkonversi. Ini merupakan kunci untuk mengoptimalkan strategi pemasaran dan penjualan, memastikan bahwa upaya dan sumber daya diarahkan secara efektif untuk memaksimalkan hasil.

### 4.4. Classification Report
Laporan klasifikasi dihasilkan untuk setiap model untuk memberikan gambaran menyeluruh tentang performa model.

### 4.5. Random Search untuk Hyperparameter Tuning
Kami menggunakan `RandomizedSearchCV` untuk tuning hyperparameter pada model RandomForest.

### 4.6. Pemilihan Best Parameter dan Evaluasi Model
Setelah menemukan parameter terbaik menggunakan Random Search, kami mengevaluasi model dengan parameter tersebut.

### 4.7. Top 10 Importance Feature
Kami menentukan 10 fitur terpenting dalam model menggunakan `feature_importances_` dari RandomForest.

## 5. Evaluasi Model (Model Evaluation)

### 5.1. Hasil Evaluasi Model
- F1 Score for Logistic Regression	: 0.92
- F1 Score for Decision Tree		: 0.90
- F1 Score for Random Forest		: 0.93 (tertinggi)

### 5.2. Parameter Terbaik untuk RandomForest
Parameter terbaik yang ditemukan melalui RandomSearch untuk RandomForest adalah:  
`{'n_estimators': 300, 'min_samples_split': 6, 'min_samples_leaf': 1, 'max_features': 'auto', 'max_depth': 80, 'bootstrap': True}`

### 5.3. Hasil F1 Score dengan Parameter Terbaik
Hasil F1 Score setelah menggunakan best params adalah 0.93.

### 5.4. Sepuluh Fitur Terbaik dari Model
10 Fitur terbaik yang ditemukan dalam model RandomForest adalah:
1. Tags_Will revert after reading the email: 0.1907
2. Total Time Spent on Website: 0.0987
3. Last Notable Activity_SMS Sent: 0.0512
4. Tags_Ringing: 0.0493
5. Lead Profile_Potential Lead: 0.0317
6. Tags_Not Specified: 0.0292
7. Tags_Closed by Horizzon: 0.0290
8. Tags_Lost to EINS: 0.0276
9. Lead Quality_Might be: 0.0268
10. Lead Quality_High in Relevance: 0.0240

Dari 10 fitur terbaik yang diidentifikasi dalam model Lead Scoring, kita dapat menarik beberapa strategi bisnis yang dapat diterapkan untuk meningkatkan efektivitas penjualan dan pemasaran. Berikut adalah interpretasi strategis dari fitur-fitur tersebut:

1. Tags_Will revert after reading the email: Menunjukkan bahwa prospek yang menanggapi email dengan indikasi akan memberikan respons lebih lanjut memiliki peluang konversi yang tinggi. Strategi: Fokuskan upaya follow-up pada grup ini dan kembangkan konten email yang menarik dan informatif untuk mempertahankan minat mereka.
2. Total Time Spent on Website: Waktu yang lebih lama yang dihabiskan di situs web menunjukkan minat yang lebih tinggi. Strategi: Investasikan dalam optimasi situs web untuk meningkatkan keterlibatan dan pertimbangkan retargeting iklan untuk pengunjung yang menghabiskan waktu lama di situs.
3. Last Notable Activity_SMS Sent: SMS sebagai medium komunikasi terakhir menunjukkan efektivitas dalam mendorong konversi. Strategi: Integrasikan SMS ke dalam strategi komunikasi pemasaran dan personalisasikan pesan untuk meningkatkan engagement.
4. Tags_Ringing: Prospek yang teleponnya berdering tetapi tidak dijawab mungkin memerlukan pendekatan berbeda. Strategi: Ulangi upaya kontak dengan strategi alternatif seperti email atau pesan teks.
5. Lead Profile_Potential Lead: Mengidentifikasi lead sebagai 'potensial' berdasarkan profil mereka. Strategi: Kembangkan konten dan penawaran khusus yang ditargetkan untuk kelompok ini, dengan memanfaatkan data profil untuk personalisasi.
6. Tags_Not Specified: Kurangnya informasi spesifik tentang prospek. Strategi: Tingkatkan upaya pengumpulan data untuk lebih mengenal calon pelanggan ini dan mengkategorikan mereka secara lebih efektif.
7. Tags_Closed by Horizzon: Ini menunjukkan penutupan yang efektif oleh tim atau proses tertentu. Strategi: Analisis dan replikasi metode penutupan ini di seluruh tim.
8. Tags_Lost to EINS: Kehilangan lead ke kompetitor. Strategi: Pelajari alasan di balik kehilangan ini untuk meningkatkan penawaran dan strategi retensi.
9. Lead Quality_Might be: Lead yang dianggap mungkin berkualitas. Strategi: Prioritaskan dan kembangkan strategi komunikasi yang lebih personal untuk mengonversi grup ini.
10. Lead Quality_High in Relevance: Lead yang sangat relevan dengan produk atau layanan. Strategi: Fokuskan sumber daya untuk konversi cepat dari grup ini, mungkin melalui penawaran khusus atau komunikasi prioritas.

## 6. Deployment
