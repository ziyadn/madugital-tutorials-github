# madugital-tutorials-github
ini adalah contoh mini project Habis Kerja : Data Scientist Course, tentang Modelling Leads Scoring perusahaan Madugital.

---

# Proyek Skor Peluang Leads (Lead Scoring)

Proyek ini akan mengikuti metodologi CRISP-DM, dengan fokus pada pengembangan model yang tidak hanya akurat dari sudut pandang statistik tetapi juga memberikan wawasan bisnis yang dapat ditindaklanjuti untuk meningkatkan konversi leads.

# Tahapan Proyek
1. [**Pemahaman Bisnis (Business Understanding)**](https://github.com/ziyadn/madugital-tutorials-github/blob/main/README.md#pemahaman-bisnis-business-understanding)
2. [**Pemahaman Data (Data Understanding)**](https://github.com/ziyadn/madugital-tutorials-github/blob/main/README.md#pemahaman-data-data-understanding)
3. [**Persiapan Data (Data Preparation)**](https://github.com/ziyadn/madugital-tutorials-github/blob/main/README.md#persiapan-data-data-preparation)
4. [**Pemodelan Data (Data Modelling)**](https://github.com/ziyadn/madugital-tutorials-github/blob/main/README.md#persiapan-data-data-preparation)
5. [**Evaluasi Data (Data Evaluation)**](https://github.com/ziyadn/madugital-tutorials-github/blob/main/README.md#evaluasi-data-data-evaluation)
6. [**Deployment**](https://github.com/ziyadn/madugital-tutorials-github/blob/main/README.md#deployment)

Setiap tahap akan didokumentasikan secara terperinci di dalam repositori ini.

## Pemahaman Bisnis (Business Understanding)
### Tujuan Bisnis
Tujuan dari proyek ini adalah untuk mengembangkan model machine learning yang dapat memberikan peluang atau skor kepada leads (calon pelanggan) berdasarkan kemungkinan mereka untuk membeli produk kita. Skor ini akan membantu tim pemasaran dan penjualan dalam mengidentifikasi dan memprioritaskan leads yang lebih cenderung untuk dikonversi menjadi pelanggan yang membayar.

### Pertanyaan Bisnis Utama
- Bagaimana kita dapat memprediksi peluang leads untuk menjadi pelanggan yang konversi?
- Bagaimana kita dapat mengelompokkan leads ke dalam kategori HOT, MEDIUM, dan COLD berdasarkan skor peluang mereka?
- Dengan menggunakan model prediktif ini, seberapa akurat kita dapat mengidentifikasi dan memprioritaskan leads?

### Kriteria Keberhasilan Proyek
- Model harus mampu memberikan skor peluang yang akurat dengan mengklasifikasikan leads ke dalam kategori HOT, MEDIUM, atau COLD.
- Kinerja model harus dinilai dengan metrik yang relevan seperti akurasi, precision, recall, dan F1-Score.
- Model harus menyediakan threshold yang dapat disesuaikan untuk kategorisasi sehingga dapat disesuaikan dengan strategi penjualan dan pemasaran perusahaan.

### Konteks Tambahan
Data yang telah diupload akan digunakan untuk melatih model machine learning. Kami akan menggunakan `predict_proba` untuk mengestimasi peluang dan kemudian menetapkan setiap lead ke salah satu dari tiga kategori berdasarkan threshold yang akan kita tentukan selama fase pemodelan. Pengelompokan ini akan memungkinkan tim penjualan untuk menyusun strategi yang lebih baik dan meningkatkan efisiensi dalam mengonversi prospek menjadi penjualan yang sukses.

### Data
Data untuk proyek ini tersedia dalam file `lead_scoring.csv`, dengan kamus data terkait yang disediakan dalam `Leads Data Dictionary.xlsx`.

---
## Pemahaman Data (Data Understanding)
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

## Persiapan Data (Data Preparation)
### 1. Data Cleaning and Preprocessing
1. Duplicate Removal: membuang records yang duplikasi untuk menjaga integritas data.
2. Binary Encoding: Kolom tertentu yang memiliki nilai 'Yes' atau 'No' akan dikonversikan ke binary format (1 untuk 'Yes', 0 untuk 'No'). Hal ini dilakukan pada kolom 'Do Not Email', 'Do Not Call', dan bergbagai macam kolom lain yang terkait dengan preferensi dan consent dari User

### 2. Handling Special Cases in Variables:
1. Merged 'Quick Add Form' dengan 'Lead Ads Form' pada kolom Lead Origin.
2. Mengelompokkan Kategori yang jarang muncul (kurang dari 1% dari populasi) menjadi kelompok 'Others' pada kolom: Lead Source, Tags, dan Last Notable Activity.
3. Null values pada TotalVisits dan Page Views Per Visit diisi dengan nilai 0.
4. Klasifikasi ulang kolom Last Activity menjadi 'Good', 'Bad', dan 'Neutral' categories (dengan Null dianggap sebagai 'Bad').
5. Informasi Country dikelompokkan menjadi 'Indonesia' dan 'Outside Indonesia'.
6. Nilai 'Select' dan Null values di kolom Specialization, How did you hear about Madugital, Lead Profile, dan City diganti dengan 'Not Specified'.
7. Null values di kolom What is your current occupation, What matters most to you in choosing a product, dan Lead Quality diisi dengan 'Not Specified'.
8. Missing values di kolom Asymmetrique Activity dan Profile dihandling dengan mengisi score menjadi 0 dan indexes menjadi '00.Zero'.

### 3. Data Transformation and Preprocessing Pipeline
1. **Preprocessing Pipeline**: Sebuah pipeline dibuat untuk numerical dan categorical features. Untuk numerical features, kami menerapkan constant imputation dan scaling. Sedangkan untuk categorical features, constant imputation dan one-hot encoding diterapkan.
2. **Data Splitting**: Datasets yang sudah dipersiapkan kemudian dipisahkan menjadi dua bagian yaitu training dan test sets, dengan 80% data digunakan untuk training dan 20% untuk testing. Kami melakukan preprocessing sebelum split train-test karena kami tidak melakukan inputasi statistika *(contohnya: mean, meadian, modus filling)*.

### 4. Post-Preprocessing Analysis
**Data Shape Post-Processing:** Setelah praproses data, kami mendapatkan 123 kolom yang siap digunakan untuk training.
