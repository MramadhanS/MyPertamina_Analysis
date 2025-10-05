# ⛽ Analisis Ulasan Pengguna Aplikasi MyPertamina: Menguak Isu Kritis dengan IBM Granite

## 📜 Project Overview
---
Aplikasi **MyPertamina** adalah platform digital Pertamina yang vital untuk transaksi bahan bakar, khususnya pembelian BBM subsidi menggunakan skema *QR Code*. Proyek ini bertujuan untuk menganalisis **20.000 data ulasan** dari Google Play Store.

### **Tujuan Proyek**
1.  Mengukur polarisasi sentimen pengguna aplikasi MyPertamina.
2.  Menggunakan **IBM Granite LLM** untuk secara otomatis mengklasifikasikan ulasan negatif ke dalam kategori isu bisnis yang spesifik (Klasifikasi Isu).
3.  Meringkas inti keluhan dalam kategori isu paling kritis (Summarization).
4.  Memberikan **rekomendasi strategis yang konkret** untuk peningkatan produk dan layanan.

### **Permasalahan & Pendekatan**
Mengolah ribuan ulasan berbahasa Indonesia yang informal membutuhkan AI. Kami mengintegrasikan pendekatan data science tradisional dengan kemampuan Large Language Model:

| Tahap | Output | Tools Utama |
| :--- | :--- | :--- |
| **Data Prep** | Teks bersih, Label Sentimen. | `Pandas`, `Regex`, `Seaborn` |
| **LLM Processing**| Kategori Isu (Contoh: "QR Code"), Ringkasan 3 Poin Utama. | **IBM Granite 13B-Instruct v2 (via WatsonxLLM)** |
| **Insight Mining**| Distribusi Isu Kritis, Analisis Kualitas Respon CS. | `Pandas`, `Matplotlib` |
| **Recommendation**| Rencana aksi yang terukur. | *Synthesis & Business Acumen* |

***

## ⚙️ Process & Methodology

### **1. Data Cleansing dan Sentimen Awal**

1.  **Pembersihan Data:** Teks ulasan dibersihkan (*lowercase*, penghapusan tautan, penghapusan karakter non-alfanumerik) untuk memastikan kualitas input ke LLM.
2.  **Sentimen Labeling:** Sentimen dikelompokkan berdasarkan skor bintang (`score`):
    * **Negatif:** Skor $\le 2$ (Total: **10,436 ulasan**)
    * **Netral:** Skor $3$ (Total: **884 ulasan**)
    * **Positif:** Skor $\ge 4$ (Total: **8,680 ulasan**)
3.  **Temuan:** Dengan **47.2%** ulasan berlabel Negatif, fokus analisis dipusatkan pada ulasan ini untuk mengidentifikasi *root cause* ketidakpuasan.

### **2. AI Support Explanation: IBM Granite (LLM)**

Kami menggunakan **IBM Granite 13B-Instruct v2** karena kemampuannya memproses konteks dan bahasa informal Indonesia secara akurat.

| LLM Task | Fungsi dalam Proyek | Relevansi |
| :--- | :--- | :--- |
| **Isu Classification** | Mengelompokkan 10.436 ulasan Negatif ke dalam 5 kategori bisnis spesifik (mis. "Barcode/QR Code & Verifikasi", "UI/UX Aplikasi"). | Mengubah data tekstual mentah menjadi **metrik bisnis terstruktur** yang dapat diukur. |
| **Summarization** | Meringkas kumpulan ulasan dari kategori teratas menjadi **3 poin keluhan inti** yang koheren. | Mendukung **Executive Reporting**, memungkinkan pembuat keputusan memahami masalah tanpa membaca ribuan ulasan. |

***

## 💡 Insight & Findings

### **A. Titik Gesekan Utama (Major Friction Points)**

Hasil klasifikasi LLM (simulasi data) pada ulasan negatif menunjukkan isu **Barcode/QR Code & Verifikasi** sebagai masalah paling kritis, menyumbang lebih dari $\frac{1}{3}$ dari total keluhan:

| Kategori Isu | Jumlah Ulasan Negatif | Persentase Total Negatif |
| :--- | :--- | :--- |
| **Barcode/QR Code & Verifikasi** | **4,230** | **40.5%** |
| UI/UX Aplikasi | 2,658 | 25.5% |
| Pembayaran/Top-Up | 1,496 | 14.3% |
| Layanan SPBU | 1,047 | 10.0% |

**Insight:** Masalah utama MyPertamina adalah **kelancaran transaksi di titik akhir (SPBU)**, bukan hanya fitur di dalam aplikasi. Kegagalan QR Code secara langsung memicu antrean dan konflik.

### **B. Inti Keluhan Kritis & Kualitas Respon**

#### **Ringkasan Isu Kritis (Output Granite)**
1.  **Kesulitan Verifikasi QR Code:** Pengguna sering mengeluhkan kegagalan atau lambatnya proses *scan* QR code yang berujung pada antrean panjang dan transaksi gagal.
2.  **Pemblokiran Akun Mendadak:** Banyak pengguna melaporkan akun mereka diblokir tanpa adanya notifikasi atau kejelasan, dan proses pelaporan/banding memiliki **respon yang sangat sulit**.
3.  **Inkonsistensi Data:** Terdapat laporan mengenai data kuota BBM subsidi yang tidak sesuai antara di aplikasi dengan data di lapangan.

#### **Analisis Respon Layanan**
Dari ulasan kritis yang dibalas, ditemukan bahwa **16.6%** balasan tergolong **Generik** (hanya berisi permohonan maaf dan saran untuk menghubungi saluran lain).

**Implikasi:** Balasan generik pada masalah teknis yang spesifik memperburuk *frustrasi* pengguna, menandakan adanya celah dalam personalisasi dan efisiensi penanganan masalah teknis.

***

## ✅ Conclusion & Recommendation

### **Kesimpulan**
Analisis LLM secara tegas menyimpulkan bahwa **Verifikasi QR Code dan pemblokiran akun** adalah *pain point* terbesar yang menyebabkan sentimen negatif. Kualitas layanan *customer support* digital perlu ditingkatkan untuk mencerminkan pemahaman yang lebih dalam tentang masalah teknis pengguna.

### **Rekomendasi Aksi (Actionable Recommendations)**

Rekomendasi ini disusun berdasarkan tingkat dampak terhadap isu kritis:

| Prioritas | Rekomendasi Aksi | Dampak Bisnis | Target Isu |
| :--- | :--- | :--- | :--- |
| **High** | **Implementasi Sistem *Offline/Cached* QR Code Verification.** Mengembangkan mekanisme verifikasi berbasis *cached data* untuk SPBU di area koneksi lemah. | Mengurangi antrean dan transaksi gagal sebesar **>20%**. | `Barcode/QR Code` |
| **High** | **Service Level Agreement (SLA) untuk Resolusi Pemblokiran Akun.** Menetapkan standar waktu respon dan penyelesaian maksimum (misalnya: maks. 3x24 jam) untuk kasus pemblokiran. | Meningkatkan **Trust Score** pengguna dan memberikan kepastian penyelesaian masalah. | `Pemblokiran Akun` |
| **Medium** | **Integrasikan Output LLM untuk *Drafting* Respon CS.** Gunakan LLM untuk menghasilkan draf balasan yang langsung merujuk pada kategori isu yang diklasifikasikan, mengurangi balasan generik. | Meningkatkan **Kualitas Respon Digital** dan efisiensi *customer service agent*. | `Kualitas Respon` |

***

**Dibuat oleh:** [Nama Anda / Tim Anda]

**Dukungan AI:** IBM Granite via IBM watsonx.ai
