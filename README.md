# Analisis Sentimen & Aspek Ulasan Aplikasi inDrive Indonesia (2026)

Proyek ini bertujuan untuk menganalisis **9.927 ulasan pengguna aplikasi inDriver** di Google Play Store Indonesia sepanjang tahun 2026. Analisis dilakukan dengan pendekatan pemrograman Python menggunakan metode Lexicon-Based Sentiment Analysis (berbasis InSet Lexicon) dan Visualisasi Data untuk mengidentifikasi kepuasan pengguna, kendala teknis, performa rilis, dan respons layanan pelanggan.

---

## 📁 Struktur Direktori

Workspace ini telah diatur ke dalam folder yang terorganisir untuk memisahkan data, kode, visualisasi, dan dokumentasi:

```
Sentimen_analysis_sdpi/
├── data/                               # File dataset ulasan (CSV)
│   ├── reviews_playstore_indrive.csv
│   └── reviews_playstore_indrive_2026.csv
├── plots/                              # Grafik & visualisasi hasil analisis (PNG)
│   ├── cs_reply_rate.png               # Tingkat balasan CS per kelompok rating
│   ├── cs_response_time_distribution.png # Distribusi waktu respons CS
│   ├── rating_per_versi.png            # Rata-rata rating per versi aplikasi
│   ├── sentimen_per_aspek.png          # Analisis sentimen berbasis aspek (ABSA)
│   ├── tren_sentimen_bulanan.png       # Tren sentimen positif vs negatif bulanan
│   ├── volume_ulasan_bulanan.png       # Volume ulasan bulanan terbagi per sentimen
│   ├── wordcloud_systemic_issues.png   # WordCloud keluhan populer yang belum dibalas
│   └── wordcloud_version_5.164.0.png   # WordCloud ulasan negatif versi terburuk (5.164.0)
├── docs/                               # Jurnal & referensi dokumen PDF
│   └── Analisis Sentimen Ulasan Pengguna Aplikasi InDrive Menggunakan Metode VADER Berbasis Leksikon InSet.pdf
├── lexicons/                           # Kamus kata sentimen bahasa Indonesia
│   └── InSet Lexicon/
│       ├── negative.tsv
│       └── positive.tsv
├── scrap.ipynb                         # Notebook untuk scraping data ulasan Play Store
├── sentiment_analysis.ipynb            # Notebook utama analisis sentimen & aspek
└── README.md                           # Dokumentasi proyek (file ini)
```

---

## 📋 Rumusan Masalah (RM) & Temuan Utama

Proyek ini berhasil menjawab secara penuh enam rumusan masalah penelitian:

1. **RM-1: Keluhan Teknis Dominan per Versi Aplikasi**
   * **Versi 5.168.0** mencatat rating terburuk (rata-rata **2.00/5.00**).
   * Masalah teknis dominan adalah kegagalan penawaran harga (*"batas penawaran tercapai"*), orderan kadaluarsa, dan kegagalan respons tombol.
2. **RM-2: Korelasi Rating dengan Rilis Versi**
   * Rilis versi **5.164.0 (rating 3.06)** dan **5.168.0 (rating 2.00)** memicu penurunan rating rata-rata yang sangat signifikan akibat penghapusan fitur *Autobid*.
3. **RM-3: Aspek Layanan Bisnis yang Paling Sering Dikeluhkan/Dipuji**
   * **Aplikasi** (58.04% Negatif) dan **Driver** (55.29% Negatif) menjadi aspek yang paling banyak dikeluhkan pengguna (masalah *bug* sistem dan persaingan tidak jujur akibat penggunaan MOD APK).
   * **Keamanan** (72.04% Positif) dan **Harga** (50.20% Positif) menjadi aspek dengan tingkat kepuasan tertinggi.
4. **RM-4: Tren Sentimen Bulanan Sepanjang Tahun 2026**
   * Sentimen positif mendominasi awal tahun (>66%). Terjadi **lonjakan sentimen negatif yang tajam pada bulan April 2026 (34.29% Negatif)** dan **Mei 2026 (31.57% Negatif)** setelah pembaruan sistem lelang manual dirilis.
5. **RM-5: Responsivitas Customer Service (CS)**
   * CS sangat memprioritaskan ulasan buruk: **99.10% ulasan negatif dibalas** dengan median waktu respons yang cepat (**1,97 jam**). Sementara ulasan positif hanya dibalas sebanyak 13.80%.
6. **RM-6: Isu Sistemik dari Ulasan Berthumbs Up Tinggi**
   * Sebanyak **17.98% ulasan populer (top 5% likes) belum dibalas**.
   * Isu sistemik terbesar yang paling banyak disetujui pengguna namun belum terespons adalah tuntutan pengembalian fitur **Autobid/Terima Otomatis** demi keselamatan jalan raya, serta pemblokiran massal terhadap pengguna **MOD APK**.

---

## 🛠️ Instalasi & Kebutuhan Library

Untuk menjalankan notebook ini secara lokal, pastikan Anda menggunakan lingkungan Python 3 dan menginstal pustaka yang diperlukan:

```bash
pip install pandas numpy matplotlib seaborn nltk Sastrawi wordcloud scikit-learn
```

### ⚙️ Jalankan Notebook
1. Buka terminal di direktori proyek.
2. Jalankan server Jupyter:
   ```bash
   jupyter notebook
   ```
3. Buka dan jalankan sel di dalam file `sentiment_analysis.ipynb` dari atas ke bawah.

> 💡 **Info Optimasi**: Tahap stemming pada preprocessing teks menggunakan kelas `OptimizedPreprocessor` berbasis *unique word caching* untuk Sastrawi. Langkah ini berhasil menghemat waktu komputasi dari yang semula **~45 menit menjadi hanya 5 menit** untuk 9.927 baris data ulasan.
