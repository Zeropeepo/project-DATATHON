# Kontekstualisasi Risiko Kredit: Peningkatan Akurasi Model Prediktif UMKM Melalui Integrasi Data Makroekonomi Regional

Proyek ini merupakan solusi untuk kompetisi Datathon yang bertujuan untuk membangun model prediksi risiko kredit yang lebih adil, akurat, dan transparan bagi Usaha Mikro, Kecil, dan Menengah (UMKM) di Indonesia. Solusi ini mengatasi kelemahan model penilaian kredit konvensional dengan mengintegrasikan data makroekonomi regional sebagai proksi untuk merepresentasikan konteks ekonomi lokal.

---

## Daftar Isi
- [Latar Belakang Masalah](#1-latar-belakang-masalah)
- [Solusi yang Diusulkan](#2-solusi-yang-diusulkan)
- [Fitur Utama](#3-fitur-utama)
- [Struktur Proyek](#4-struktur-proyek)
- [Cara Menjalankan Proyek](#5-cara-menjalankan-proyek)
- [Hasil dan Analisis](#6-hasil-dan-analisis)
- [Kesimpulan dan Pengembangan Lanjutan](#7-kesimpulan-dan-pengembangan-lanjutan)

---

## 1. Latar Belakang Masalah
UMKM adalah pilar ekonomi Indonesia, namun akses mereka terhadap pembiayaan formal masih terbatas. Salah satu penyebab utamanya adalah model penilaian risiko kredit yang bersifat "satu ukuran untuk semua" (*one-size-fits-all*). Model seperti ini gagal memperhitungkan keragaman kondisi ekonomi antar wilayah di Indonesia, di mana faktor-faktor seperti Tingkat Pengangguran Terbuka (TPT), Produk Domestik Regional Bruto (PDRB), dan Non-Performing Loan (NPL) perbankan sangat bervariasi dan berpengaruh signifikan terhadap kelangsungan usaha UMKM.

Akibatnya, banyak UMKM potensial di daerah dengan tantangan ekonomi lebih tinggi dinilai memiliki risiko yang sama dengan UMKM di pusat ekonomi yang lebih stabil, menciptakan penilaian yang tidak adil dan menghambat inklusi keuangan.

## 2. Solusi yang Diusulkan
Untuk mengatasi masalah ini, kami mengusulkan **Metodologi Adaptasi Kontekstual Berbasis Data Proksi**. Kerangka kerja ini secara cerdas memperkaya dataset pinjaman dengan data makroekonomi regional dari sumber publik terpercaya (BPS dan OJK).

Metodologi ini terdiri dari empat tahap utama:
1.  **Pengumpulan Data Proksi**: Mengumpulkan data NPL, TPT, dan PDRB tingkat provinsi.
2.  **Feature Enrichment**: Menggabungkan data proksi tersebut ke dalam dataset pinjaman utama berdasarkan lokasi peminjam.
3.  **Pelatihan Model Kontekstual**: Melatih model klasifikasi (XGBoost) menggunakan dataset yang telah diperkaya untuk memprediksi status gagal bayar.
4.  **Implementasi Explainable AI (XAI)**: Menggunakan SHAP (SHapley Additive exPlanations) untuk menganalisis dan menjelaskan setiap keputusan kredit, sehingga prosesnya menjadi transparan.

## 3. Fitur Utama
- **Prediksi Risiko Adaptif**: Model mampu menyesuaikan prediksi risiko berdasarkan konteks ekonomi regional peminjam.
- **Transparansi Keputusan (XAI)**: Setiap keputusan (disetujui/ditolak) dapat dijelaskan, menunjukkan faktor-faktor utama yang mempengaruhinya, termasuk faktor ekonomi regional.
- **Wawasan Bisnis Regional**: Memberikan pemahaman mendalam tentang bagaimana kondisi ekonomi suatu daerah mempengaruhi profil risiko kredit secara keseluruhan.

## 4. Struktur Proyek
```
.
├── Dataset_Kredit_Diperkaya.csv      # Dataset utama yang sudah diperkaya dengan data proksi
├── KreditLensa_Dataset.csv           # Dataset asli dari kompetisi
├── best_model_pipeline.joblib        # Artefak pipeline model terbaik (XGBoost + TomekLinks)
├── best_explainer.joblib             # Artefak SHAP explainer yang sudah dilatih
├── loan_default_prediction.ipynb     # Notebook utama untuk pemrosesan data, pelatihan, dan evaluasi model
├── xai_analysis.ipynb                # Notebook untuk analisis dan visualisasi XAI pada studi kasus
├── requirements.txt                  # Daftar pustaka Python yang dibutuhkan
└── README.md                         # Dokumentasi proyek (file ini)
```

## 5. Cara Menjalankan Proyek
Untuk menjalankan dan mereproduksi hasil dari proyek ini, ikuti langkah-langkah berikut:

### Prasyarat
- Python 3.8 atau lebih tinggi
- Jupyter Notebook atau Jupyter Lab

### Instalasi
1.  **Clone Repositori**
    ```bash
    git clone https://github.com/Zeropeepo/project-DATATHON.git
    cd project-DATATHON
    ```

2.  **Buat Lingkungan Virtual (Direkomendasikan)**
    ```bash
    python -m venv venv
    source venv/bin/activate  # Di Windows, gunakan `venv\Scripts\activate`
    ```

3.  **Instal Pustaka yang Dibutuhkan**
    ```bash
    pip install -r requirements.txt
    ```

### Menjalankan Notebook
1.  **Mulai Jupyter**
    ```bash
    jupyter lab
    ```
2.  **Buka dan Jalankan Notebook Utama**
    - Buka `loan_default_prediction.ipynb`.
    - Jalankan semua sel secara berurutan untuk melakukan pra-pemrosesan data, melatih model, dan menyimpan artefak (`.joblib`).

3.  **Buka dan Jalankan Notebook Analisis XAI**
    - Buka `xai_analysis.ipynb`.
    - Jalankan semua sel untuk memuat model yang sudah jadi dan melihat bagaimana SHAP menjelaskan keputusan kredit untuk sampel data.

## 6. Hasil dan Analisis
- **Model Terbaik**: Hasil benchmark menunjukkan bahwa kombinasi **XGBoost** dengan teknik *undersampling* **TomekLinks** memberikan performa terbaik pada metrik AUPRC (Area Under the Precision-Recall Curve).
- **Pentingnya Konteks Regional**: Analisis menggunakan SHAP (di `xai_analysis.ipynb`) secara konsisten menunjukkan bahwa fitur-fitur makroekonomi yang ditambahkan (`DistribusiPDRBPersen`, `TPTTahunanPersen`, dll.) menjadi salah satu faktor paling berpengaruh dalam keputusan model. Ini membuktikan hipotesis awal bahwa konteks ekonomi regional adalah prediktor risiko yang signifikan.

## 7. Kesimpulan dan Pengembangan Lanjutan
Proyek ini berhasil mendemonstrasikan bahwa pendekatan adaptasi kontekstual dapat menciptakan model penilaian kredit yang lebih relevan dan transparan untuk UMKM di Indonesia.

**Saran Pengembangan:**
- **Data Alternatif**: Mengintegrasikan data alternatif yang lebih granular (misalnya, data transaksi digital) untuk pemahaman yang lebih mendalam.
- **Automasi Umpan Balik**: Membangun sistem yang secara otomatis memberikan umpan balik berbasis XAI kepada pemohon yang ditolak.
- **Penerapan Produksi**: Mengimplementasikan model sebagai *decision support tool* untuk membantu analis kredit di lembaga keuangan.
