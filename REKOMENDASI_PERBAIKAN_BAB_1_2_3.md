# Rekomendasi dan Daftar Perbaikan Dokumen Skripsi
**Analisis File:** `chapters/01-introduction.tex`, `chapters/02-literature.tex`, dan `chapters/03-methodology.tex`  
**Referensi Utama:** *Integrating IndoBERT and balanced iterative reducing and clustering using hierarchies of BERTopic in Indonesian short text* (Muhajir et al., IAES IJ-AI, 2025).  
**Konteks Aplikasi:** Pemodelan Topik Otomatis Percakapan Grup WhatsApp Aktif ($\ge 100$ pesan/hari) dengan BERTopic Termodifikasi (**IndoBERTweet + BIRCH + BM25**).

---

## 1. Ringkasan Eksekutif & Temuan Kritis Lintas Bab

Berdasarkan analisis komparatif antara paper acuan ([Muhajir et al., 2025](file:///home/usereal/Projects/Sistem%20Skripsi/Skripsi_Moh.-Yusril-Maqoshidana/jurnal/document.pdf)) dan naskah Bab 1, Bab 2, serta Bab 3, ditemukan beberapa poin krusial yang memerlukan perbaikan dan penyelarasan:

1. **Inkonsistensi Objek & Data Penelitian Antara Bab 1 dan Bab 3 (CRITICAL)**:
   - **Bab 1 (Baris 95)** menyatakan: *"Data yang digunakan merupakan riwayat percakapan grup Komunitas Buku pada periode 2023–2026 dengan jumlah pesan sebanyak 91,868."*
   - **Bab 3 (Baris 28–29)** menyatakan: *"Objek penelitian ini adalah data percakapan grup WhatsApp Angkatan STAN Tahun 2022... total 55.000 pesan teks dari 100 partisipan aktif."*
   - *Tindakan*: Harus diselaraskan nama grup, rentang tahun, jumlah pesan, dan karakteristiknya secara konsisten di seluruh dokumen.

2. **Pengabaian BM25 pada Rumusan Masalah dan Tujuan Penelitian (Bab 1)**:
   - Modifikasi BERTopic terdiri dari 3 pilar: **IndoBERTweet (Embedding)**, **BIRCH (Clustering)**, dan **BM25 (Topic Representation)**.
   - Namun, pada Rumusan Masalah 1 & 3 serta Tujuan Penelitian 1 & 3, hanya disebutkan *"IndoBERTweet dan BIRCH clustering"*, sementara **BM25 terlewat/tidak dicantumkan**.
   - *Tindakan*: Cantumkan BM25 secara eksplisit agar mencerminkan keseluruhan metode proposed yang diusulkan.

3. **Penegasan Urgensi Masalah pada Grup WhatsApp Sangat Aktif ($\ge 100$ Pesan/Hari)**:
   - Latar belakang saat ini baru menjelaskan pertumbuhan WhatsApp dan masalah teks pendek secara umum.
   - *Tindakan*: Perlu ditambahkan justifikasi numerik/spesifik mengenai fenomena *information overload* pada grup WhatsApp dengan intensitas tinggi ($\ge 100$ pesan/hari) yang menyulitkan anggota yang tertinggal percakapan (*catch-up problem*), sehingga membutuhkan ekstraksi topik otomatis.

4. **Adopsi Metodologi Pengujian Paper Acuan ke Bab 3**:
   - Paper acuan membuktikan keunggulan BIRCH + BM25 melalui pengujian partisi data progresif (20%, 40%, 60%, 80%, 100%) dan pengukuran rasio *outlier* yang turun drastis dari 23–24% (HDBSCAN) ke 1–5% (BIRCH).
   - *Tindakan*: Skema eksperimen subset data bertingkat dan metrik rasio *outlier* perlu dipertegas pada bagian evaluasi Bab 3.

---

## 2. Analisis & Rekomendasi File `chapters/01-introduction.tex` (Bab 1)

### A. Latar Belakang Masalah (`\section{Latar Belakang}`)
* **Baris 20–25 (Konteks Grup WhatsApp Aktif)**:
  - *Kekurangan*: Pembahasan masih bersifat umum ("seiring meningkatnya volume pesan").
  - *Perbaikan*: Tambahkan penjelasan konkret mengenai dinamika grup dengan volume tinggi ($\ge 100$ pesan/hari), di mana diskusi sering kali terdiri dari berbagai sub-topik yang tumpang tindih (*interleaved conversation*). Jelaskan bahwa anggota grup yang tidak memantau grup selama beberapa jam akan menghadapi tumpukan ratusan pesan (*information overload*) dan kesulitan mengekstraksi poin utama pembicaraan secara cepat.
* **Baris 36–41 (Metode Proposed: IndoBERTweet + BIRCH + BM25)**:
  - *Kekurangan*: Penjelasan latar belakang sudah baik mengutip `\cite{iaes2025indobert}`, tetapi relasi antara nama model "IndoBERT" pada paper acuan dan "IndoBERTweet" pada skripsi perlu dipertegas.
  - *Perbaikan*: Jelaskan bahwa skripsi ini mengadopsi kerangka kerja modifikasi dari Muhajir et al. (2025), dengan peningkatan pada lapisan *embedding* menggunakan **IndoBERTweet** (Koto et al., 2021) karena dilatih secara khusus pada data media sosial Indonesia yang sarat dengan bahasa gaul/slang, singkatan, dan *code-mixing*, yang sangat cocok dengan karakteristik pesan obrolan WhatsApp.
* **Baris 42–47 (Research Gap)**:
  - *Kekurangan*: Poin gap sudah cukup terstruktur, namun gap nomor 1 dan 4 dapat diperkuat dengan menekankan integrasi sistem web yang mampu memproses ekspor obrolan secara otomatis untuk pengguna akhir.

### B. Rumusan Masalah (`\section{Rumusan Masalah}`)
* **Baris 57–61**:
  - *Kekurangan*: Rumusan butir 1, 2, dan 3 belum mencantumkan BM25.
  - *Rekomendasi Perbaikan Redaksi*:
    1. *“Bagaimana menerapkan framework BERTopic yang dimodifikasi dengan integrasi IndoBERTweet sebagai model embedding, BIRCH sebagai algoritma clustering, dan BM25 sebagai skema representasi topik pada data percakapan grup WhatsApp berbahasa Indonesia?”*
    2. *“Bagaimana performa dan kualitas topik yang dihasilkan oleh model usulan (IndoBERTweet + BIRCH + BM25) dibandingkan dengan model baseline BERTopic berdasarkan metrik Topic Coherence (NPMI), Topic Diversity, Embedding Density, Intra-topic Similarity, serta rasio pengurangan outlier?”*
    3. *“Bagaimana merancang dan mengimplementasikan sistem berbasis web untuk analisis topik otomatis percakapan grup WhatsApp menggunakan pipeline BERTopic termodifikasi tersebut?”*

### C. Tujuan Penelitian (`\section{Tujuan Penelitian}`)
* **Baris 68–72**:
  - *Kekurangan*: Belum menyertakan BM25 pada Tujuan butir 1 dan 3, serta belum eksplisit menyebutkan perbandingan dengan *baseline*.
  - *Rekomendasi Perbaikan Redaksi*:
    1. *“Menerapkan modifikasi framework BERTopic dengan mengintegrasikan IndoBERTweet untuk sentence embedding, BIRCH untuk clustering, dan BM25 untuk topic representation pada korpus percakapan grup WhatsApp berbahasa Indonesia.”*
    2. *“Mengevaluasi dan membandingkan performa model usulan terhadap baseline BERTopic berdasarkan metrik Topic Coherence (NPMI), Topic Diversity, Embedding Density, Intra-topic Similarity, dan proporsi outlier.”*
    3. *“Mengembangkan sistem aplikasi berbasis web interaktif yang memungkinkan pengguna menganalisis topik percakapan grup WhatsApp secara otomatis dari berkas ekspor chat.”*

### D. Batasan Penelitian (`\section{Batasan Penelitian}`)
* **Baris 95 (Poin 3 - Objek Data)**:
  - *Kekurangan*: Tertulis *"riwayat percakapan grup Komunitas Buku pada periode 2023–2026 dengan jumlah pesan sebanyak 91,868"*, bertentangan dengan Bab 3 (*STAN 2022, 55.000 pesan*).
  - *Perbaikan*: Tentukan satu dataset resmi yang digunakan dan sinkronkan angka serta nama grupnya.
* **Poin Tambahan Batasan Masalah**:
  - Tambahkan batasan bahwa sistem menganalisis percakapan berbasis teks obrolan grup aktif dengan rentang waktu atau volume pesan tertentu (misalnya batch harian/mingguan).

---

## 3. Analisis & Rekomendasi File `chapters/02-literature.tex` (Bab 2)

### A. Penelitian Terdahulu (`\section{Penelitian Terdahulu}`)
* **Baris 20–24**:
  - *Kekurangan*: Ulasan sintesis penelitian terdahulu perlu memperjelas posisi paper acuan utama (`iaes2025indobert` / Muhajir et al., 2025).
  - *Perbaikan*: Beri penekanan bahwa paper Muhajir et al. (2025) telah membuktikan bahwa penggantian HDBSCAN dengan BIRCH serta c-TF-IDF dengan BM25 berhasil memangkas *outlier* hingga 1–5% dan menjaga stabilitas metrik diversitas serta densitas pada data monolog (Twitter, Review, YouTube). Skripsi ini mengambil lompatan lebih jauh (*state of the art extension*) dengan menerapkannya pada data percakapan WhatsApp yang bersifat interaktif (*multi-turn*), memiliki *speaker turns*, dan tingkat *noise* lebih tinggi.

### B. Landasan Teori WhatsApp (`\subsection{Aplikasi WhatsApp}`)
* **Baris 29–35**:
  - *Kekurangan*: Belum menguraikan karakteristik komputasional dari obrolan grup WhatsApp aktif.
  - *Perbaikan*: Tambahkan sub-pembahasan mengenai karakteristik obrolan grup:
    1. *High Message Velocity*: Aliran pesan tinggi ($\ge 100$ pesan/hari).
    2. *Asynchronous Multi-Speaker*: Banyak pengguna berbicara dalam satu linimasa waktu tanpa urutan kaku.
    3. *Contextual Sparsity & High Noise*: Pesan terpecah menjadi beberapa gelembung chat pendek (*fragmented texts*), banyak slang, salah ketik (*typo*), singkatan, dan *code-mixing*.

### C. Landasan Teori BERTopic & Modifikasi (`\subsection{BERTopic}`)
* **Baris 36–67**:
  - *Perbaikan*: Gambar 2.1 dan penjelasan alur 4 tahap sudah baik. Pastikan penamaan komponen konsisten:
    - Baseline: *Sentence Transformers / Multilingual BERT* $\rightarrow$ *UMAP* $\rightarrow$ *HDBSCAN* $\rightarrow$ *c-TF-IDF*.
    - Proposed: *IndoBERTweet* $\rightarrow$ *UMAP* $\rightarrow$ *BIRCH* $\rightarrow$ *BM25*.

### D. IndoBERTweet (`\subsection{IndoBERTweet}`)
* **Baris 69–81**:
  - *Perbaikan*: Tambahkan tabel/deskripsi singkat mengapa IndoBERTweet lebih unggul dibandingkan IndoBERT Base atau multilingual mBERT untuk korpus obrolan WhatsApp: adanya penambahan 14.584 token kosakata informal/slang Indonesia yang sangat dominan muncul di obrolan chat.

### E. BIRCH Clustering (`\subsection{BIRCH Clustering}`)
* **Baris 83–132**:
  - *Kelebihan*: Formulasi matematis CF-Tree ($CF=(N, LS, SS)$), centroid $\mu$, dan radius $R$ sudah sangat rapi dan tepat.
  - *Perbaikan*: Tambahkan paragraf penutup di subbab ini yang mengaitkan teori BIRCH dengan penanganan *outlier* pada BERTopic: jelaskan bahwa berbeda dengan HDBSCAN yang membuang titik berkepadatan rendah sebagai noise (yang pada chat pendek bisa mencapai 24%), mekanisme *hierarchical clustering feature* pada BIRCH memetakan titik data ke subklaster terdekat yang memenuhi ambang batas $T$, sehingga seluruh pesan obrolan grup dapat terutilisasi secara maksimal.

### F. Topic Representation dengan BM25 (`\subsection{Topic Representation Dengan BM25}`)
* **Baris 134–186**:
  - *Kelebihan*: Penjelasan Persamaan (2.6) dan (2.7) sudah sesuai dengan formulasi pada paper acuan `iaes2025indobert`.
  - *Perbaikan*: Jelaskan secara intuitif peran parameter $k_1$ (biasanya 1.2–2.0) sebagai pengendali saturasi frekuensi istilah dan $b$ (biasanya 0.75) sebagai pengendali normalisasi panjang pesan WhatsApp yang bervariasi (dari 1 kata hingga paragraf panjang).

### G. Metrik Evaluasi (`\subsection{Topic Coherence}` s.d. `\subsection{Intra-topic Similarity}`)
* **Baris 188–258**:
  - *Kelebihan*: Formula NPMI, Topic Diversity, Embedding Density, dan Intra-topic Similarity sudah lengkap.
  - *Perbaikan/Penambahan*: Tambahkan satu subbab pendek mengenai **Rasio Outlier (Outlier Proportion)**:
    $$\text{Outlier Ratio} = \frac{N_{\text{outlier}}}{N_{\text{total}}} \times 100\%$$
    Hal ini penting karena reduksi outlier adalah salah satu tolok ukur keberhasilan utama dari modifikasi BIRCH yang dipublikasikan pada paper acuan.

---

## 4. Analisis & Rekomendasi File `chapters/03-methodology.tex` (Bab 3)

### A. Objek Penelitian (`\section{Objek Penelitian}`)
* **Baris 25–32**:
  - *Sinkronisasi Data*: Pastikan dataset disinkronkan dengan Bab 1 (pilih salah satu: data STAN 2022 55.000 pesan atau Komunitas Buku 91.868 pesan).
  - *Detail Karakteristik*: Tambahkan statistik rata-rata pesan harian (misal: rata-rata $\ge 100$ pesan/hari pada jam-jam sibuk) untuk memperkuat justifikasi pemilihan grup tersebut sebagai subjek penelitian.

### B. Tahapan Praproses Data (`\subsection{Praproses Data}`)
* **Baris 64–81 (Urutan Pipeline)**:
  - *Perbaikan*: 9 tahapan yang ditulis sudah sangat rinci. Berikan penekanan khusus pada penanganan artifak WhatsApp seperti:
    - Penghapusan teks bawaan sistem WhatsApp: `"<Media omitted>"`, `"<Media tidak disertakan>"`, pesan enkripsi end-to-end, dan panggilan tak terjawab.
    - Penghapusan pesan yang sangat pendek setelah dibersihkan (misal: pesan yang hanya tersisa 0 atau 1 karakter) agar tidak merusak representasi *embedding*.
    - Penjelasan apakah pesan dianalisis per-baris obrolan (*single message*) atau diagregasikan per-jendela waktu/sesi obrolan.

### C. Pembuatan Model BERTopic Modifikasi (`\subsection{Pembuatan Model}`)
* **Baris 82–129**:
  - *Perbaikan*: Tabelkan ringkasan konfigurasi hyperparameter yang digunakan/diuji untuk tiap tahapan:
    1. **Embedding**: Model `indobenchmark/indobertweet-base-uncased`, pooling: mean pooling.
    2. **Dimensionality Reduction (UMAP)**: `n_neighbors=15`, `n_components=5`, `metric='cosine'`, `min_dist=0.0`.
    3. **Clustering (BIRCH)**: Eksplorasi nilai `threshold` ($T \in [0.1, 1.0]$), `branching_factor` ($B=50$), dan `n_clusters`.
    4. **Topic Representation (BM25)**: $k_1=1.5$, $b=0.75$.

### D. Evaluasi Model (`\subsection{Evaluasi Model}`)
* **Baris 130–153**:
  - *Perbaikan*: Tambahkan kembali desain pengujian berbasis **subset partisi data** (20%, 40%, 60%, 80%, 100%) sebagaimana dilakukan pada paper acuan `iaes2025indobert`. Hal ini penting untuk membuktikan:
    1. *Stabilitas Topik*: Apakah Topic Diversity dan Intra-topic Similarity tetap stabil ketika jumlah pesan obrolan meningkat dari 20% ke 100%?
    2. *Skalabilitas Outlier*: Membuktikan bahwa BIRCH mempertahankan persentase outlier yang sangat rendah pada berbagai skala data obrolan.
  - *Model Pembanding (Baselines)*: Definisikan model pembanding yang diuji:
    1. Baseline 1: Standard BERTopic (Sentence-BERT + UMAP + HDBSCAN + c-TF-IDF).
    2. Baseline 2: BERTopic + K-Means (IndoBERTweet + UMAP + K-Means + BM25).
    3. Proposed: BERTopic Modifikasi (IndoBERTweet + UMAP + BIRCH + BM25).

### E. Implementasi & Evaluasi Sistem Web (`\subsection{Implementasi Sistem}` & `\subsection{Evaluasi Sistem}`)
* **Baris 154–174**:
  - *Perbaikan*: Jelaskan fitur fungsional utama pada web:
    1. Modul Unggah & Parsing Chat (.txt/.zip WhatsApp).
    2. Modul Pemrosesan Asinkron (FastAPI Background Tasks + SSE progress bar).
    3. Modul Visualisasi Topik:
       - *Barchart* kata kunci representatif per topik berbasis skor BM25.
       - *Topic distribution over time* (distribusi kemunculan topik per hari/minggu untuk mendeteksi topik terhangat pada grup aktif).
       - *Message explorer* untuk membaca pesan-pesan asli yang tergolong ke dalam topik tertentu.

---

## 5. Matriks Rencana Aksi Perbaikan (Actionable Checklist)

| No | File Target | Bagian / Baris | Masalah Teridentifikasi | Tindakan Perbaikan | Prioritas |
|:---|:---|:---|:---|:---|:---|
| 1 | `chapters/01-introduction.tex` & `chapters/03-methodology.tex` | Bab 1 (L.95) & Bab 3 (L.28) | Inkonsistensi nama grup & jumlah pesan (STAN 55k vs Komunitas Buku 91k) | Pilih satu dataset riil dan seragamkan di kedua bab. | **Tinggi** |
| 2 | `chapters/01-introduction.tex` | Bab 1 (L.58, 69, 81) | BM25 terlewat dari Rumusan Masalah 1, Tujuan 1, dan Manfaat 1 | Tambahkan BM25 secara eksplisit pada Rumusan, Tujuan, dan Manfaat. | **Tinggi** |
| 3 | `chapters/01-introduction.tex` | Bab 1 (L.20–25) | Latar belakang belum menyoroti masalah spesifik grup aktif ($\ge 100$ pesan/hari) | Tambahkan konteks *information overload* dan kebutuhan *catch-up* pada obrolan aktif. | **Sedang** |
| 4 | `chapters/02-literature.tex` | Bab 2 (L.20–24) | Posisi paper acuan (Muhajir et al., 2025) perlu dipertegas | Jelaskan kontribusi paper acuan dan justifikasi adaptasinya ke ranah percakapan WhatsApp. | **Sedang** |
| 5 | `chapters/02-literature.tex` | Bab 2 (L.258) | Belum ada subbab definisi matematis metrik Rasio Outlier | Tambahkan subbab formula *Outlier Proportion* (%) sebagai metrik kunci reduksi noise BIRCH. | **Sedang** |
| 6 | `chapters/03-methodology.tex` | Bab 3 (L.130–153) | Skenario evaluasi belum mencantumkan pengujian subset data (20%--100%) dan baseline | Tambahkan skema pengujian partisi data (20%--100%) dan tabel perbandingan baseline model. | **Tinggi** |
| 7 | `chapters/03-methodology.tex` | Bab 3 (L.82–129) | Parameter UMAP, BIRCH, dan BM25 belum ditabelkan secara spesifik | Tambahkan tabel rincian nilai parameter (*hyperparameter setup*) untuk eksperimen model. | **Sedang** |
| 8 | `chapters/03-methodology.tex` | Bab 3 (L.154–166) | Deskripsi keluaran visual sistem web masih umum | Tambahkan detail visualisasi topik (kata kunci BM25, tren waktu, penelusuran pesan). | **Sedang** |

---
*Dokumen ini disusun untuk memandu revisi penulisan Bab 1, Bab 2, dan Bab 3 skripsi agar selaras dengan paper acuan utama ([Muhajir et al., 2025](file:///home/usereal/Projects/Sistem%20Skripsi/Skripsi_Moh.-Yusril-Maqoshidana/jurnal/document.pdf)) dan memenuhi kaidah akademik yang ketat.*
