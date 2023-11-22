# madugital-tutorials-github
ini adalah contoh mini project Habis Kerja tentang Modelling Leads Scoring perusahaan Madugital 

---

# Proyek Skor Peluang Leads (Lead Scoring)

## Tujuan Bisnis
Tujuan dari proyek ini adalah untuk mengembangkan model machine learning yang dapat memberikan peluang atau skor kepada leads (calon pelanggan) berdasarkan kemungkinan mereka untuk membeli produk kita. Skor ini akan membantu tim pemasaran dan penjualan dalam mengidentifikasi dan memprioritaskan leads yang lebih cenderung untuk dikonversi menjadi pelanggan yang membayar.

## Pertanyaan Bisnis Utama
- Bagaimana kita dapat memprediksi peluang leads untuk menjadi pelanggan yang konversi?
- Bagaimana kita dapat mengelompokkan leads ke dalam kategori HOT, MEDIUM, dan COLD berdasarkan skor peluang mereka?
- Dengan menggunakan model prediktif ini, seberapa akurat kita dapat mengidentifikasi dan memprioritaskan leads?

## Kriteria Keberhasilan Proyek
- Model harus mampu memberikan skor peluang yang akurat dengan mengklasifikasikan leads ke dalam kategori HOT, MEDIUM, atau COLD.
- Kinerja model harus dinilai dengan metrik yang relevan seperti akurasi, precision, recall, dan F1-Score.
- Model harus menyediakan threshold yang dapat disesuaikan untuk kategorisasi sehingga dapat disesuaikan dengan strategi penjualan dan pemasaran perusahaan.

## Konteks Tambahan
Data yang telah diupload akan digunakan untuk melatih model machine learning. Kami akan menggunakan `predict_proba` untuk mengestimasi peluang dan kemudian menetapkan setiap lead ke salah satu dari tiga kategori berdasarkan threshold yang akan kita tentukan selama fase pemodelan. Pengelompokan ini akan memungkinkan tim penjualan untuk menyusun strategi yang lebih baik dan meningkatkan efisiensi dalam mengonversi prospek menjadi penjualan yang sukses.

## Data
Data untuk proyek ini tersedia dalam file `lead_scoring.csv`, dengan kamus data terkait yang disediakan dalam `Leads Data Dictionary.xlsx`.

---

Proyek ini akan mengikuti metodologi CRISP-DM, dengan fokus pada pengembangan model yang tidak hanya akurat dari sudut pandang statistik tetapi juga memberikan wawasan bisnis yang dapat ditindaklanjuti untuk meningkatkan konversi leads.

# Tahapan Proyek
1. **Pemahaman Bisnis (Business Understanding)**
2. **Pemahaman Data (Data Understanding)**
3. **Persiapan Data (Data Preparation)**
4. **Pemodelan Data (Data Modelling)**
5. **Evaluasi Data (Data Evaluation)**
6. **Deployment**

Setiap tahap akan didokumentasikan secara terperinci di dalam repositori ini.
