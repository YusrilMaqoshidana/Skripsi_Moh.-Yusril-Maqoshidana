# 📊 Panduan Lengkap Bahan Slide Presentasi Sidang Skripsi (PPT)

> **Informasi Presentasi:**
> - **Judul Skripsi:** *Sistem Analisis Topik Percakapan Grup WhatsApp Berbasis Web Menggunakan BERTopic dengan IndoBERTweet dan BIRCH Clustering*
> - **Penyaji:** Moh. Yusril Maqoshidana (NIM. 222410102064)
> - **Program Studi:** Teknologi Informasi, Fakultas Ilmu Komputer, Universitas Jember
> - **Dosen Pembimbing:** Dr. Brian Rizqi Paradisiaca Darnoto, S.Kom., M.Kom.
> - **Dosen Penguji 1:** Khoirunnisa' Afandi, S.Kom., M.Kom.
> - **Dosen Penguji 2:** Dony Bahtera Firmawan, S.Kom., M.Kom.
> - **Target Durasi Presentasi:** 15–20 Menit (15 Menit Presentasi Slide + 3–5 Menit Demo Web).

---

## Ringkasan Struktur 14 Slide Presentasi

| No. Slide | Topik Bahasan | Estimasi Durasi |
| :---: | :--- | :---: |
| **Slide 1** | Judul, Identitas, Pembimbing, dan Penguji | 1 Menit |
| **Slide 2** | Latar Belakang & Urgensi Penelitian (*Information Overload*) | 1,5 Menit |
| **Slide 3** | Rumusan Masalah & Keterbatasan Model Eksisting (*Outlier Paradox*) | 1,5 Menit |
| **Slide 4** | Solusi & Kebaruan Arsitektur yang Diusulkan (*Novelty*) | 1,5 Menit |
| **Slide 5** | Karakteristik Dataset & Pipeline Pra-Pemrosesan (10 Tahapan) | 1,5 Menit |
| **Slide 6** | Desain Algoritma Pengklasteran Usulan (*ImprovedBIRCH* + $2\sigma$) | 1,5 Menit |
| **Slide 7** | Skema Pengujian Eksperimental (*Learning Curve* 20% s.d. 100%) | 1 Menit |
| **Slide 8** | Hasil Evaluasi Kuantitatif Komparatif Korpus Penuh (Tabel 4.2) | 2 Menit |
| **Slide 9** | Analisis Grafik Stabilitas & Skalabilitas Kurva Pembelajaran | 1,5 Menit |
| **Slide 10** | Hasil Ekstraksi Topik & Representasi Kata Kunci Tematik | 1,5 Menit |
| **Slide 11** | Arsitektur Sistem Web Terintegrasi (*Client-Side Anonymization* & SSE) | 1,5 Menit |
| **Slide 12** | Pengujian Fungsional Sistem (*Black-Box Testing*) | 1 Menit |
| **Slide 13** | Kesimpulan & Saran Akademik | 1,5 Menit |
| **Slide 14** | Penutup & Transisi ke Live Demo Aplikasi | 0,5 Menit |

---

## Rincian Konten Per Slide (Point Slide, Rekomendasi Visual, & Speaker Notes)

---

### SLIDE 1: Judul & Identitas Penelitian
* **Durasi:** ~1 Menit
* **Fungsi:** Pembukaan formal, menyapa dewan penguji, dan memperkenalkan fokus skripsi.

#### 📌 Poin-Poin Ditampilkan di Slide:
* **Judul Skripsi:**  
  **SISTEM ANALISIS TOPIK PERCAKAPAN GRUP WHATSAPP BERBASIS WEB MENGGUNAKAN BERTopic DENGAN IndoBERTweet DAN BIRCH CLUSTERING**
* **Mahasiswa:** Moh. Yusril Maqoshidana (NIM. 222410102064)
* **Program Studi:** S1 Teknologi Informasi — Fakultas Ilmu Komputer, Universitas Jember
* **Dosen Pembimbing:** Dr. Brian Rizqi Paradisiaca Darnoto, S.Kom., M.Kom.
* **Dosen Penguji 1:** Khoirunnisa' Afandi, S.Kom., M.Kom.
* **Dosen Penguji 2:** Dony Bahtera Firmawan, S.Kom., M.Kom.
* **Tahun:** 2026

#### 🎨 Rekomendasi Elemen Visual:
* Logo resmi Universitas Jember di pojok atas.
* Latar belakang bersih, profesional, bernuansa akademis formal (navy/slate blue dan putih).

#### 🗣️ Catatan Bicara Mahasiswa (*Speaker Notes*):
> *"Selamat pagi/siang kepada Bapak Dr. Brian Rizqi Paradisiaca Darnoto selaku dosen pembimbing, Ibu Khoirunnisa' Afandi selaku penguji satu, dan Bapak Dony Bahtera Firmawan selaku penguji dua.*  
> *Terima kasih atas kesempatan yang diberikan kepada saya. Pada kesempatan hari ini, saya akan mempresentasikan hasil penelitian skripsi saya yang berjudul: **Sistem Analisis Topik Percakapan Grup WhatsApp Berbasis Web Menggunakan BERTopic dengan IndoBERTweet dan BIRCH Clustering**."*

---

### SLIDE 2: Latar Belakang & Urgensi Penelitian
* **Durasi:** ~1,5 Menit
* **Fungsi:** Menjelaskan fenomena riil dan mengapa masalah ini penting diteliti.

#### 📌 Poin-Poin Ditampilkan di Slide:
* **Ledakan Volume Pesan Komunitas WhatsApp:**
  * Grup obrolan aktif bertukar ribuan pesan setiap hari, memicu fenomena ***information overload***.
  * Anggota dan pengelola komunitas kesulitan menyaring pokok bahasan penting secara manual.
* **Karakteristik Teks Percakapan Informal:**
  * Teks sangat pendek (*short texts*), minim struktur sintaks baku.
  * Sarat singkatan (*slang*), pemanjangan kata (*elongation*), kata serapan, dan simbol emoji.
* **Kebutuhan Sistem Analitik Otomatis:**
  * Diperlukan pemodelan topik (*topic modeling*) yang mampu memetakan klaster topik secara otomatis, cepat, dan tetap menjaga privasi riwayat obrolan pengguna.

#### 🎨 Rekomendasi Elemen Visual:
* Ikon grafik obrolan WhatsApp + diagram ilustrasi alur dari ribuan pesan acak menuju klaster topik yang teratur.

#### 🗣️ Catatan Bicara Mahasiswa (*Speaker Notes*):
> *"Grup WhatsApp saat ini telah menjadi sarana komunikasi utama komunitas modern. Namun, tingginya intensitas percakapan kerap menimbulkan fenomena information overload. Anggota grup sering kali tertinggal konteks informasi penting di antara ribuan percakapan obrolan harian.*  
> *Teks percakapan WhatsApp memiliki sifat yang sangat unik: kalimatnya pendek, tidak formal, sarat singkatan, dan banyak campur kode. Pendekatan pembacaan riwayat obrolan secara manual sudah tidak efisien lagi, sehingga dibutuhkan sistem analitik cerdas berbasis pemodelan topik untuk mengekstraksi tema-tema utama secara terstruktur."*

---

### SLIDE 3: Paradoks Outlier & Limitasi Model Eksisting
* **Durasi:** ~1,5 Menit
* **Fungsi:** Mengungkap celah riset (*research gap*) dan kelemahan metode yang ada saat ini.

#### 📌 Poin-Poin Ditampilkan di Slide:
* **Limitasi BERTopic Standar (HDBSCAN):**
  * HDBSCAN bekerja berdasarkan estimasi kepadatan (*density-based*).
  * Pada teks pendek WhatsApp yang renggang, HDBSCAN membuang **40% hingga 57% pesan sebagai *outlier*** (hilang lebih dari separuh data percakapan).
* **Limitasi Model Jurnal Eksisting (Muhajir et al., 2025):**
  * Menggunakan BIRCH untuk menekan *outlier* hingga 4,6%, namun **tanpa penyaring wacana obrolan WhatsApp**.
  * Akibatnya: Keberagaman topik anjlok drastis (*Topic Diversity* hanya **0,5143**), kata-kata obrolan umum (*kak, bang, iya, nya*) menduplikasi hampir separuh kata kunci topik.
* **Pertanyaan Riset Utama:**
  * Bagaimana mempertahankan retensi data obrolan yang tinggi (> 90%) tanpa mengorbankan koherensi dan keberagaman kata kunci topik?

#### 🎨 Rekomendasi Elemen Visual:
* Diagram komparasi grafis: "Kelemahan HDBSCAN (Data Terbuang Banyak)" vs "Kelemahan Model Jurnal (Kata Kunci Duplikat)".

#### 🗣️ Catatan Bicara Mahasiswa (*Speaker Notes*):
> *"Ketika pemodelan topik mutakhir seperti BERTopic standar diterapkan pada teks obrolan WhatsApp, kita menemukan paradoks outlier yang nyata. Algoritma bawaan HDBSCAN membuang 40% hingga lebih dari 57% pesan sebagai pencilan karena pesan obrolan dianggap terlalu renggang. Ini artinya lebih dari separuh informasi anggota komunitas diabaikan begitu saja.*  
> *Di sisi lain, model replikasi jurnal terbaru karya Muhajir dkk. mencoba menggunakan algoritma BIRCH untuk menekan outlier, tetapi karena tidak memiliki penyaring wacana obrolan informal, sekitar separuh kata kuncinya menjadi duplikat antartopik dengan Topic Diversity anjlok di angka 0,5143.*  
> *Inilah celah penelitian yang saya selesaikan dalam skripsi ini."*

---

### SLIDE 4: Solusi & Kebaruan Arsitektur yang Diusulkan
* **Durasi:** ~1,5 Menit
* **Fungsi:** Menyajikan *novelty* dan arsitektur modular yang diajukan.

#### 📌 Poin-Poin Ditampilkan di Slide:
* **Arsitektur Modular *Proposed BERTopic*:**
  1. **IndoBERTweet Embedding (768 Dimensi):** Model bahasa khusus yang dilatih pada 400+ juta korpus media sosial bahasa Indonesia.
  2. **Reduksi Dimensi UMAP:** Memproyeksikan vektor ke manifold 5 dimensi dengan metrik *cosine*.
  3. **Pengklasteran Hierarkis BIRCH Mikro:** Inisialisasi ambang adaptif mikro $\theta \in [0{,}20, 0{,}25]$ berbasis konvergensi Ridler-Calvard.
  4. **Penyaring Pencilan Statis $2\sigma$ & Klaster Kerdil:** Memangkas pesan berjarak $> 2\sigma$ dari sentroid dan melebur klaster $N < 5$.
  5. **Representasi BM25 + Kamus 9 Kategori Stopwords Wacana:** Memurnikan kata kunci topik dari partikel obrolan non-konten.
  6. **Reduksi Topik Hierarkis Berpengaman:** Menggabungkan subklaster redundan secara otomatis (`nr_topics='auto'`).

#### 🎨 Rekomendasi Elemen Visual:
* Diagram alur arsitektur *pipeline* usulan (Gambar 3.2 di naskah skripsi: IndoBERTweet $\rightarrow$ UMAP $\rightarrow$ BIRCH $2\sigma$ $\rightarrow$ BM25 + Stopwords $\rightarrow$ Auto Reduction).

#### 🗣️ Catatan Bicara Mahasiswa (*Speaker Notes*):
> *"Untuk mengatasi paradoks tersebut, saya merancang modifikasi arsitektur BERTopic yang memadukan lima pilar utama: representasi IndoBERTweet 768 dimensi yang sangat peka terhadap ragam informal Indonesia; reduksi manifold UMAP; algoritma klasterisasi hierarkis BIRCH dengan ambang radius adaptif; pemangkasan pencilan berbasis deviasi standar 2-sigma; serta pembobotan BM25 yang diperkaya kamus penyaring sembilan kategori stopwords wacana WhatsApp.*  
> *Sinergi ini memastikan pesan percakapan dapat dirangkul secara maksimal sekaligus menjaga kemurnian kata kunci topik yang terbentuk."*

---

### SLIDE 5: Dataset & Pipeline Pra-Pemrosesan Korpus
* **Durasi:** ~1,5 Menit
* **Fungsi:** Memaparkan data empiris riil dan transparansi pembersihan data.

#### 📌 Poin-Poin Ditampilkan di Slide:
* **Spesifikasi Korpus WhatsApp:**
  * Sumber data: Grup WhatsApp Komunitas Buku (Juni 2023 – Juni 2026 / 1.113 hari).
  * Data Mentah: **91.868 pesan teks** (820.231 token) dari 1.307 partisipan.
* **Alur 10 Tahapan Pra-Pemrosesan Eksak:**
  * Eliminasi kontak `.vcf` (5 pesan), deduplikasi spam (18.240 pesan), notifikasi sistem (3 pesan).
  * Pembersihan URL (1.342 pesan), tag HTML/bracket (1.279 pesan), privasi email/telepon (769 pesan).
  * Transliterasi emoji / *demojize* (14.184 pesan $\rightarrow$ melestarikan semantik emosional).
  * Normalisasi elongasi (7.490 pesan) & pembakuan *slang* (32.255 pesan).
  * Filter pesan non-substantif $< 3$ kata (22.055 pesan).
* **Hasil Akhir Korpus Bersih:**
  * **51.583 dokumen bersih berkualitas tinggi** (retensi **87,49% token**, 717.642 kata).

#### 🎨 Rekomendasi Elemen Visual:
* Diagram batang atau infografis perbandingan data mentah (91.868) vs data bersih (51.583 pesan) beserta highlight retensi token 87,49%.

#### 🗣️ Catatan Bicara Mahasiswa (*Speaker Notes*):
> *"Data yang digunakan dalam penelitian ini merupakan korpus percakapan nyata dari grup WhatsApp Komunitas Buku sepanjang 3 tahun terakhir, dengan total 91.868 pesan mentah. Data ini telah mengantongi izin resmi fakultas dan persetujuan tertulis administrator grup.*  
> *Melalui sepuluh tahapan praproses terpadu—meliputi deduplikasi, sensor privasi nomor telepon, transliterasi emoji ke bentuk teks alfabetis, normalisasi kata slang, hingga eliminasi basa-basi satu kata—kita berhasil menyaring 40.285 pesan noise dan menyisakan 51.583 pesan bersih berbobot 717.642 token, dengan mempertahankan 87,49% substansi leksikal korpus."*

---

### SLIDE 6: Desain Algoritma Pengklasteran Usulan (ImprovedBIRCH)
* **Durasi:** ~1,5 Menit
* **Fungsi:** Menjelaskan formulasi teknis algoritma yang menjadi kontribusi utama skripsi.

#### 📌 Poin-Poin Ditampilkan di Slide:
* **Pohon Fitur Klaster (*Clustering Feature Tree* / CF-Tree):**
  * Parameter *branching factor* = 50, efisien memori $O(N)$ untuk data obrolan besar.
  * Inisialisasi ambang adaptif mikro $\theta \in [0{,}20, 0{,}25]$ via binerisasi Ridler-Calvard.
* **Mekanisme Pemotongan Outlier $2\sigma$ Jarak Kosinus:**
  $$d_{\cos}(x, c_k) = 1 - \frac{x \cdot c_k}{\lVert x \rVert \lVert c_k \rVert}, \qquad \tau_k = \mu_{d, k} + 2{,}0 \cdot \sigma_{d, k}$$
  * Titik dengan jarak $d_{\cos} > \tau_k$ dialokasikan sebagai pencilan (label $-1$).
* **Pembersihan Klaster Kerdil (*Micro-Cluster Cleaning*):**
  * Klaster dengan anggota $N < 5$ dokumen dilebur untuk menjamin kekompakan semantik.
* **Dampak Visual Proyeksi 2D UMAP:**
  * Mengeliminasi pembentukan *mega-cluster* semu HDBSCAN dan menata 135+ klaster mikro yang padat.

#### 🎨 Rekomendasi Elemen Visual:
* Gambar perbandingan 2D UMAP (Gambar 4.1 naskah skripsi: HDBSCAN yang berantakan vs Proposed Model yang terklaster rapi).

#### 🗣️ Catatan Bicara Mahasiswa (*Speaker Notes*):
> *"Kontribusi metodologis utama penelitian ini terletak pada modifikasi algoritma ImprovedBIRCH. Alih-alih mengandalkan kerapatan densitas seperti HDBSCAN yang kaku, BIRCH membangun Clustering Feature Tree yang adaptif. Kami menginisialisasi radius threshold mikro antara 0,20 hingga 0,25 dan menerapkan pemangkasan outlier terukur berbasis deviasi standar 2-sigma dari jarak kosinus ke sentroid klaster.*  
> *Seperti yang dapat dilihat pada visualisasi proyeksi UMAP 2D, jika HDBSCAN menghasilkan klaster raksasa homogen yang menelan data dengan outlier 16,2%, model usulan berhasil memetakan klaster-klaster mikro yang padat dan tegas dengan menekan outlier menjadi hanya 5,6%."*

---

### SLIDE 7: Skema Eksperimen Kurva Pembelajaran (Learning Curve)
* **Durasi:** ~1 Menit
* **Fungsi:** Menjelaskan desain pengujian empiris yang objektif dan adil.

#### 📌 Poin-Poin Ditampilkan di Slide:
* **Komparasi 4 Arsitektur Model:**
  1. *Baseline* Standar: MiniLM + HDBSCAN (*eom*) + c-TF-IDF.
  2. *Baseline Proposed*: MiniLM + HDBSCAN (*leaf*) + c-TF-IDF + Reduksi Auto.
  3. Model Modified: IndoBERTweet + BIRCH (*auto*) + BM25 (Muhajir et al., 2025).
  4. **Model Usulan:** IndoBERTweet + ImprovedBIRCH ($2\sigma$) + BM25 9 Kategori Wacana + Reduksi Auto.
* **Partisi Data Kronologis Kumulatif:**
  * 20% (10.316 dokumen) $\rightarrow$ 40% (20.633) $\rightarrow$ 60% (30.949) $\rightarrow$ 80% (41.266) $\rightarrow$ 100% (51.583 dokumen).
* **5 Metrik Evaluasi Kuantitatif:**
  * Dimensi Leksikal: *Topic Diversity* (TD) & *Topic Coherence* ($C_{\text{NPMI}}$).
  * Dimensi Geometris Ruang Vektor: *Embedding Density* (ED), *Intra-Topic Similarity* (ITS), & *Outlier Rate* (OR).

#### 🎨 Rekomendasi Elemen Visual:
* Bagan matriks komparasi 4 model dan ilustrasi piramida pembesaran data kurva pembelajaran (20% s.d. 100%).

#### 🗣️ Catatan Bicara Mahasiswa (*Speaker Notes*):
> *"Untuk memvalidasi keandalan model secara ilmiah, pengujian tidak hanya dilakukan pada korpus statis, melainkan melalui eksperimen kurva pembelajaran pada lima fraksi data kronologis: dari 20%, 40%, 60%, 80%, hingga 100% data penuh.*  
> *Keempat model diadu kinerjanya menggunakan lima metrik objektif yang mengevaluasi kualitas kata kunci dan kekohesifan dokumen di ruang vektor secara terukur."*

---

### SLIDE 8: Hasil Evaluasi Kuantitatif Korpus Penuh (100% Data)
* **Durasi:** ~2 Menit (SLIDE PALING KRUSIAL)
* **Fungsi:** Menyajikan bukti empiris keunggulan model usulan di depan penguji.

#### 📌 Poin-Poin Ditampilkan di Slide:
* **Tabel Hasil Evaluasi Komparatif (51.583 Dokumen):**

| Parameter \& Metrik | 1. Baseline Standar | 2. Baseline Proposed | 3. Model Modified (Jurnal) | **4. Model Usulan (Proposed)** |
| :--- | :---: | :---: | :---: | :---: |
| **Model Embedding** | all-MiniLM-L6-v2 | all-MiniLM-L6-v2 | IndoBERTweet | **IndoBERTweet** |
| **Algoritma Klastering** | HDBSCAN (*eom*) | HDBSCAN (*leaf*) | BIRCH (*auto*) | **BIRCH Usulan ($2\sigma$)** |
| **Representasi Kata** | c-TF-IDF | c-TF-IDF | BM25 | **BM25 + Stopwords Wacana** |
| **Reduksi Topik Auto** | Tidak | Ya | Tidak | **Ya** |
| **Jumlah Topik ($K$)** | 392 | 151 | 91 | **150** |
| **Outlier Rate ($OR \downarrow$)** | 40,44% | 57,36% | **4,63%** | **6,83% (Retensi 93,17%)** |
| **Topic Diversity ($TD \uparrow$)** | 0,9316 | 0,9623 | 0,5143 | **0,9653 (Tertinggi)** |
| **Koherensi ($C_{\text{NPMI}} \uparrow$)** | -0,0210 | +0,1534 | +0,0260 | **+0,0495 (Positif Solid)** |
| **Intra-Topic Sim ($ITS \uparrow$)** | 0,5778 | 0,4885 | 0,6445 | **0,6129** |
| **Embedding Density ($ED \uparrow$)** | 0,7089 | 0,5440 | 0,7464 | **0,5419** |

* **Temuan Evaluasi Kritis:**
  * *Baseline Proposed* memiliki koherensi +0,1534, tetapi **palsu/semu** karena membuang **57,36% data**.
  * Model Modified membuang sedikit data (4,63%), namun **Topic Diversity anjlok parah ke 0,5143** (banyak kata duplikat).
  * **Model Usulan mencapai titik Pareto-Optimal:** Keberagaman tertinggi (**0,9653**), koherensi semantik positif (**+0,0495**), dan mempertahankan **93,17% percakapan**.

#### 🎨 Rekomendasi Elemen Visual:
* Tabel di atas dengan *highlighting* kotak hijau tebal pada kolom **Model Usulan**, serta penanda panah merah pada kelemahan Baseline Proposed dan Model Modified.

#### 🗣️ Catatan Bicara Mahasiswa (*Speaker Notes*):
> *"Bapak Ibu dewan penguji, ini adalah tabel hasil evaluasi empiris inti pada korpus penuh 51.583 pesan.*  
> *Dapat kita cermati bersama bahwa Model Usulan berhasil mencatatkan Topic Diversity tertinggi sebesar 0,9653, unggul 87% dibandingkan Model Modified jurnal yang anjlok di angka 0,5143.*  
> *Memang, jika kita melihat metrik koherensi, Baseline Proposed mencatat skor +0,1534. Namun ini adalah koherensi semu, karena model tersebut membuang 57,36% data percakapan! Model hanya mengklasterkan 42% pesan yang sangat mirip dan mengabaikan sisanya.*  
> *Sebaliknya, Model Usulan mampu mempertahankan koherensi semantik positif +0,0495 secara adil pada 93,17% percakapan anggota grup, dengan outlier hanya 6,83%. Ini membuktikan bahwa arsitektur usulan merupakan solusi Pareto-Optimal paling seimbang."*

---

### SLIDE 9: Analisis Grafik Learning Curve & Skalabilitas Data
* **Durasi:** ~1,5 Menit
* **Fungsi:** Menunjukkan ketahanan dan konvergensi model terhadap pertambahan data.

#### 📌 Poin-Poin Ditampilkan di Slide:
* **Trajektori Konvergensi Model Usulan:**
  1. **Konvergensi Outlier Teratur:** Outlier menurun secara konsisten dari $15{,}08\% \rightarrow 11{,}05\% \rightarrow 8{,}10\% \rightarrow 7{,}39\% \rightarrow \mathbf{6{,}83\%}$.
  2. **Stabilitas Topic Diversity:** Selalu konsisten di atas $0{,}95$ di semua split data ($0{,}9604 \rightarrow 0{,}9653$), membuktikan ketahanan kamus stopwords wacana terhadap eskalasi volume pesan.
  3. **Akselerasi Koherensi $C_{\text{NPMI}}$:** Berakselerasi dari zona negatif pada data kecil ($-0{,}0242$ pada 20%) menuju zona positif solid ($+0{,}0495$ pada 100%), membuktikan model semakin pintar mengenali relasi semantik kata seiring bertambahnya data.
  4. **Kohesivitas Klaster Internal ($ITS$):** Stabil kokoh pada rentang $0{,}61$ s.d. $0{,}63$.

#### 🎨 Rekomendasi Elemen Visual:
* Gambar grafik Kurva Pembelajaran 4 panel (Gambar 4.3 naskah skripsi: grafik tren $C_{\text{NPMI}}$, Outlier Rate, Diversity, dan ITS).

#### 🗣️ Catatan Bicara Mahasiswa (*Speaker Notes*):
> *"Grafik kurva pembelajaran ini membuktikan perilaku skalabilitas model usulan sepanjang pertambahan data dari 20% ke 100%.*  
> *Tingkat outlier model usulan menunjukkan tren konvergensi yang sangat sehat, turun drastis dari 15% menuju 6,8% pada korpus penuh. Koherensi semantiknya berakselerasi menembus zona positif solid seiring bertambahnya bukti statistik pesan, sementara keberagaman leksikalnya tidak pernah turun di bawah 0,96.*  
> *Karakteristik ini membuktikan bahwa arsitektur usulan memiliki ketahanan tinggi untuk diimplementasikan pada grup obrolan yang terus bertambah volumenya setiap hari."*

---

### SLIDE 10: Hasil Ekstraksi Topik & Representasi Kata Kunci
* **Durasi:** ~1,5 Menit
* **Fungsi:** Menunjukkan bukti interpretatif bahwa topik yang dihasilkan benar-benar bermakna di dunia nyata.

#### 📌 Poin-Poin Ditampilkan di Slide:
* **Total Topik Terbentuk: 150 Klaster Tematik Terstruktur.**
* **Dualisme Klaster Tematik Komunitas Buku WhatsApp:**
  * **Pilar Wacana Literasi & Sastra Komunitas:**
    * *Topik 0 (Apresiasi Membaca):* buku, baca, novel, beli, gramedia.
    * *Topik 21 (Fiksi Populer):* tere, liye, novel, serial, bumi.
    * *Topik 28 (Kajian Sastra Klasik):* franz, kafka, metamorphosis, cerita, karya.
  * **Pilar Dinamika Interaksi Sosial WhatsApp:**
    * *Topik 11 (Kopdar & Pertemuan):* meet, kopi, yok, gas, kumpul.
    * *Topik 13 (Apresiasi Komunitas):* salut, keren, bangga, mantap, jaya.
    * *Topik 101 (Kegiatan Komunitas):* webinar, link, join, zoom, sesi.
* **Keunggulan Ekstraksi BM25:**
  * Bebas dari partikel obrolan umum (*kak, iya, nih, wkwk*), menghasilkan kata kunci yang spesifik dan interpretatif.

#### 🎨 Rekomendasi Elemen Visual:
* Diagram batang distribusi 5 kata kunci teratas berbobot BM25 (Gambar 4.2 naskah skripsi: `topic_keywords_distribution.png`).

#### 🗣️ Catatan Bicara Mahasiswa (*Speaker Notes*):
> *"Secara kualitatif, model usulan berhasil mengekstraksi 150 topik tematik yang sangat kaya dan terstruktur.*  
> *Dapat dilihat pada grafik distribusi kata kunci BM25, topik yang terbentuk merefleksikan dua kutub utama grup obrolan: pilar wacana literasi—seperti diskusi bedah novel Franz Kafka, karya Tere Liye, dan minat baca buku; serta pilar dinamika interaksi sosial—seperti agenda temu kopdar, webinar komunitas, dan ungkapan apresiasi anggota.*  
> *Berkat kamus penyaring wacana, tidak ada lagi kata kunci sampah seperti 'wkwk', 'kak', atau 'iya' yang mengotori topik."*

---

### SLIDE 11: Arsitektur Sistem Web Terintegrasi
* **Durasi:** ~1,5 Menit
* **Fungsi:** Menjelaskan hilirisasi model AI ke dalam aplikasi praktis yang aman dan fungsional.

#### 📌 Poin-Poin Ditampilkan di Slide:
* **Arsitektur *Client-Server* Modern:**
  * *Frontend:* Vue.js 3, TypeScript, Vite, TailwindCSS (Pola arsitektur MVI & Pinia Store).
  * *Backend:* FastAPI (Python asinkron, akselerasi GPU CUDA via PyTorch & Scikit-Learn).
* **Perlindungan Privasi Data (*Client-Side Anonymization*):**
  * Sesuai amanat **UU No. 27 Tahun 2022 tentang Perlindungan Data Pribadi (UU PDP)**.
  * Nama pengirim dan nomor kontak langsung di-hashing menggunakan algoritma kriptografi SHA-256 (`@user-xxxx`) di memori peramban klien sebelum data dikirim ke server.
* **Pemantauan Komputasi Waktu Nyata (*Real-Time Streaming*):**
  * Komunikasi *Server-Sent Events* (SSE) pada *endpoint* `GET /api/progress/{task_id}` untuk memancarkan progres praproses, *embedding*, dan klasterisasi ke antarmuka pengguna tanpa *polling*.
* **Penelusuran Konteks Pesan (*Traceability*):**
  * Pengguna dapat mengklik kartu topik dan memeriksa kutipan riwayat pesan percakapan aslinya.

#### 🎨 Rekomendasi Elemen Visual:
* Diagram arsitektur sistem web (arsitektur client-server: Browser Vue.js $\leftrightarrow$ REST API / SSE $\leftrightarrow$ FastAPI Engine).

#### 🗣️ Catatan Bicara Mahasiswa (*Speaker Notes*):
> *"Sebagai bentuk implementasi aplikatif, model ini dihilirisasi ke dalam prototipe aplikasi web bernama ChatAnalisis dengan arsitektur client-server berbasis FastAPI dan Vue.js 3.*  
> *Sistem mengedepankan aspek privasi data sesuai UU PDP Nomor 27 Tahun 2022: nomor telepon dan identitas anggota grup langsung disamarkan menggunakan enkripsi SHA-256 di browser pengguna sebelum diunggah ke server.*  
> *Proses komputasi berat dijalankan sebagai background task dan dipancarkan secara real-time ke antarmuka menggunakan Server-Sent Events, dilengkapi fitur penelusuran pesan asli untuk menjamin keterlacakan konteks topik."*

---

### SLIDE 12: Pengujian Fungsionalitas Sistem (Black-Box Testing)
* **Durasi:** ~1 Menit
* **Fungsi:** Menunjukkan keandalan teknis perangkat lunak.

#### 📌 Poin-Poin Ditampilkan di Slide:
* **Metodologi Pengujian:** *Black-Box Testing* Berbasis Skenario Ekivalensi Antarmuka (*Equivalence Partitioning*).
* **Cakupan Pengujian MVP (5 Modul Utama):**
  1. Modul Unggah & Ekstraksi Arsip Chat WhatsApp (`.txt` & `.zip`).
  2. Modul Pembersihan & Validasi Data Interaktif (Rentang Waktu & Filter).
  3. Modul Pemantauan Komputasi *Real-Time Progress* (SSE Streaming).
  4. Modul Visualisasi Hasil & Metrik Kuantitatif (Dashboard Interaktif).
  5. Modul Penelusuran Konteks Obrolan (*Message Traceability Modal*).
* **Hasil Pengujian:**
  * **14 Skenario Pengujian Fungsional Inti (34 Kasus Uji Detail):**
  * **Tingkat Keberhasilan: 100% Valid** (Seluruh luaran sistem sesuai dengan ekspektasi fungsional).

#### 🎨 Rekomendasi Elemen Visual:
* Tabel ringkasan hasil Black-Box Testing (Tabel 4.3 naskah skripsi) dengan badge centang hijau "100% Valid".

#### 🗣️ Catatan Bicara Mahasiswa (*Speaker Notes*):
> *"Pengujian fungsionalitas aplikasi web dilakukan melalui metode Black-Box Testing terhadap 14 skenario uji inti yang mencakup seluruh modul aplikasi: mulai dari pengunggahan berkas, validasi input korpus, streaming proses komputasi, visualisasi dashboard topik, hingga penelusuran pesan asli.*  
> *Seluruh kasus uji berhasil dieksekusi dengan tingkat keberhasilan 100% valid tanpa terjadi crash atau unhandled exceptions."*

---

### SLIDE 13: Kesimpulan & Saran Akademik
* **Durasi:** ~1,5 Menit
* **Fungsi:** Menjawab rumusan masalah secara lugas dan memberikan rekomendasi masa depan.

#### 📌 Poin-Poin Ditampilkan di Slide:
* **Kesimpulan:**
  1. Modifikasi arsitektur BERTopic (IndoBERTweet + ImprovedBIRCH $2\sigma$ + BM25 9 Kategori Wacana) berhasil mengekstraksi **150 topik tematik** terstruktur dari 51.583 pesan WhatsApp.
  2. Model usulan mencapai performa *Pareto-Optimal* paling unggul: mempertahankan retensi data **93,17% (outlier 6,83%)**, keberagaman leksikal tertinggi (**$TD = 0{,}9653$**), koherensi semantik positif (**$C_{\text{NPMI}} = +0{,}0495$**), serta kekohesifan klaster internal yang kokoh ($ITS = 0{,}6129$, $ED = 0{,}5419$).
  3. Sistem web analitik *ChatAnalisis* berhasil dibangun secara fungsional (100% valid) dengan perlindungan privasi SHA-256 dan pemantauan *real-time* berbasis SSE.
* **Saran Pengembangan:**
  1. Eksplorasi model bahasa fondasi mutakhir (*Large Language Models* / LLM dwibahasa) untuk menangkap campur kode (*code-mixing*) regional yang lebih kompleks.
  2. Integrasi pemodelan topik dengan analisis sentimen guna memetakan polaritas emosi komunitas pada setiap tema perbincangan.

#### 🎨 Rekomendasi Elemen Visual:
* Tiga kartu ringkasan kesimpulan dengan ikon centang + dua butir saran pengembangan masa depan.

#### 🗣️ Catatan Bicara Mahasiswa (*Speaker Notes*):
> *"Dari seluruh rangkaian penelitian dan pengujian yang telah dilaksanakan, dapat ditarik tiga kesimpulan utama:*  
> *Pertama, arsitektur pemodelan topik yang dibangun berhasil memetakan 150 topik tematik dari 51.583 pesan obrolan.*  
> *Kedua, model usulan terbukti secara empiris menyelesaikan paradoks outlier teks pendek dengan merangkul 93,17% pesan percakapan, mempertahankan keberagaman tertinggi 0,9653, dan koherensi positif solid.*  
> *Ketiga, prototipe sistem web analitik berhasil dibangun dan diuji 100% valid.*  
> *Untuk penelitian selanjutnya, saya menyarankan eksplorasi model LLM untuk menangani variasi bahasa daerah yang lebih ekstrem serta penggabungan pemodelan topik dengan analisis polaritas sentimen."*

---

### SLIDE 14: Penutup & Demo Sistem
* **Durasi:** ~0,5 Menit (Transisi ke Demo)
* **Fungsi:** Menutup presentasi lisan dan mengundang penguji untuk menyaksikan demo program.

#### 📌 Poin-Poin Ditampilkan di Slide:
* **Terima Kasih**
* *"Bukan kecerdasan semata yang menentukan kelulusan, melainkan ketekunan dan penguasaan penuh atas apa yang telah dikerjakan."*
* **Sesi Selanjutnya: Demonstrasi Sistem Web Interaktif (*Live Demo Application*)**
* *Tanya Jawab & Diskusi Terbuka Bersama Dewan Penguji.*

#### 🎨 Rekomendasi Elemen Visual:
* Tangkapan layar antarmuka beranda web *ChatAnalisis* (Gambar mockup modern).

#### 🗣️ Catatan Bicara Mahasiswa (*Speaker Notes*):
> *"Demikian presentasi laporan skripsi saya. Selanjutnya, izinkan saya mendemonstrasikan secara langsung cara kerja sistem web ChatAnalisis dalam memproses riwayat obrolan WhatsApp.*  
> *Terima kasih atas perhatian Bapak dan Ibu dewan penguji, waktu dan layar saya kembalikan."*

---

## 💡 Tips Tambahan Menghadapi Dosen Penguji Fasilkom UNEJ

1. **Penguasaan Angka Kunci Sidang (Hafalkan di Luar Kepala):**
   * Total pesan mentah: **91.868 pesan** (820.231 token).
   * Total pesan bersih: **51.583 pesan** (717.642 token, retensi token 87,49%).
   * Outlier model usulan: **6,83%** (retensi pesan **93,17%**).
   * Topic Diversity: **0,9653** (unggul telak dari model jurnal 0,5143).
   * Koherensi $C_{\text{NPMI}}$: **+0,0495** (positif solid; baseline -0,0210).
   * Jumlah topik: **150 topik**.

2. **Kunci Menjawab Pertanyaan Dosen Penguji Mengenai Koherensi:**
   * *Jika ditanya: "Mengapa Baseline Proposed memiliki koherensi +0,1534 yang lebih tinggi dari model Anda (+0,0495)?"*
   * *Jawab dengan tegas:*  
     *"Izin menjawab Bapak/Ibu. Koherensi +0,1534 pada Baseline Proposed merupakan koherensi semu (spurious coherence). Nilai tersebut didapat karena model membuang 57,36% data percakapan sebagai pencilan. Model hanya memilih sedikit pesan yang sangat mirip, sehingga kata-katanya tampak sangat koheren, namun model kehilangan lebih dari separuh isi percakapan grup. Sedangkan Model Usulan kami mempertahankan 93,17% data riwayat obrolan dengan koherensi positif solid +0,0495, yang merupakan titik kompromi paling optimal untuk kasus analisis komunitas."*
