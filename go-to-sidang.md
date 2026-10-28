---
title: "Roadmap Menuju Sidang Skripsi - Moh. Yusril Maqoshidana"
author: "Moh. Yusril Maqoshidana"
nim: "222410102064"
program_studi: "Teknologi Informasi"
fakultas: "Fakultas Ilmu Komputer, Universitas Jember"
status: "Persiapan Sidang"
target_sidang: 2026-06-01
tags:
  - skripsi
  - sidang
  - fasilkom-unej
  - checklist
  - obsidian
---

# 🎓 Roadmap & Checklist Go to Sidang Skripsi

> [!abstract] **Informasi Ujian Skripsi**
> - **Nama Mahasiswa:** Moh. Yusril Maqoshidana
> - **NIM:** 222410102064
> - **Program Studi:** Teknologi Informasi, Fakultas Ilmu Komputer, Universitas Jember
> - **Judul Skripsi:** *Sistem Analisis Topik Grup WhatsApp Berbasis Web Menggunakan BERTopic dengan IndoBERTweet dan BIRCH Clustering*
> - **Dosen Pembimbing:** Dr. Brian Rizqi Paradisiaca Darnoto, S.Kom., M.Kom. (NIP. 199804272024061001)
> - **Dosen Penguji 1:** Khoirunnisa' Afandi, S.Kom., M.Kom. (NIP. 199412282024062001)
> - **Dosen Penguji 2:** Dony Bahtera Firmawan, S.Kom., M.Kom. (NIP. 199711202024061001)
> - **Target Tanggal Ujian:** 01 Juni 2026

---

## 📊 Quick Progress Tracker

```
[▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓░░░░░] 80% Ready to Defend
```
- [x] Naskah Skripsi Bab 1 s.d. Bab 5 Selesai
- [x] Sistem Aplikasi Web (FastAPI + Vue.js) Selesai & Teruji
- [ ] Uji Plagiasi Turnitin Resmi (< 30%)
- [ ] Pengesahan Lembar Persetujuan Sidang
- [ ] Slide Presentasi Sidang (10–15 Slide)
- [ ] Simulasi Q&A Sidang

---

## 📑 FASE 1: Syarat Berkas & Pendaftaran Sidang (Administratif)

> [!info] Mengacu pada Buku Juknis Skripsi Fasilkom UNEJ Versi 2.0 (2023) & SOP Akademik.

- [ ] **Kelayakan Beban Akademik (`RULE-ADM-01`):**
  - [ ] Telah menempuh $\ge 120$ SKS.
  - [ ] Persentase Pembobotan (PP) $\ge 90\%$.
  - [ ] IPK minimal 2.00 dan tidak ada nilai E.
- [ ] **Uji Kemiripan / Bebas Plagiasi Turnitin (`RULE-ADM-05`):**
  - [ ] Total *Similarity Index* Turnitin $\le 30\%$.
  - [ ] Kesamaan sumber tunggal (*single source*) $\le 10\%$.
  - [ ] Cetak dan minta tanda tangan Dosen Pembimbing pada lembar bukti cek plagiasi (`RULE-ADM-04`).
- [ ] **Persetujuan Dosen Pembimbing:**
  - [ ] Naskah final telah disetujui penuh oleh Dr. Brian Rizqi Paradisiaca Darnoto, S.Kom., M.Kom.
  - [ ] Menandatangani Lembar Persetujuan Sidang (*Halaman Persetujuan*).
  - [ ] Kartu kendali bimbingan terisi lengkap (minimal frekuensi bimbingan terpenuhi).
- [ ] **Pendaftaran Sidang di Portal Fasilkom / SISTER:**
  - [ ] Mengunggah berkas naskah skripsi PDF (`main.pdf`).
  - [ ] Mengunggah bukti uji Turnitin bertanda tangan.
  - [ ] Mengunggah bukti persetujuan pembimbing.
  - [ ] Memperoleh Surat Tugas / Undangan Sidang dari Bagian Akademik Fasilkom.
- [ ] **Distribusi Draf Naskah Sidang:**
  - [ ] Cetak draf naskah skripsi (jilid lakban hitam / softcover sesuai aturan prodi) sebanyak 3 eksemplar.
  - [ ] Menyerahkan draf naskah ke Dosen Pembimbing dan kedua Dosen Penguji minimal **H-3 atau H-7** sebelum pelaksanaan sidang.

---

## 🔍 FASE 2: Audit Kesiapan Dokumen LaTeX (`main.pdf`)

> [!tip] Pastikan naskah PDF telah bersih dari pelanggaran tata letak (*layout errors*).

### Bagian Awal (Frontmatter)
- [ ] **Cover (`00-cover.tex`):**
  - [ ] Logo UNEJ berwarna berdiameter 5.0 cm (`RULE-STR-02`).
  - [ ] Judul skripsi berformat ALL CAPS, 14pt, tebal, berupa frasa bukan kalimat.
  - [ ] Hierarki instrumen: Kementerian $\rightarrow$ Universitas Jember $\rightarrow$ Fakultas Ilmu Komputer $\rightarrow$ Program Studi Teknologi Informasi $\rightarrow$ 2026.
- [ ] **Halaman Persembahan (`01-dedication.tex`):** Bahasa formal, santun, nama pembimbing dan penguji tertulis benar dengan gelar.
- [ ] **Halaman Pernyataan Orisinalitas (`03-originality.tex`):** Telah ditempel materai fisik Rp10.000 dan ditandatangani basah.
- [ ] **Lembar Persetujuan (`04-approval.tex`):** Format tanda tangan pembimbing & penguji lengkap NIP.
- [ ] **Abstrak Indonesia (`05-abstract-id.tex`):** Tepat 1 paragraf, 200–300 kata (`RULE-STR-05`), spasi tunggal, memuat latar belakang, tujuan, metode, hasil metrik, dan kesimpulan sistem. Kata kunci 3–5 istilah.
- [ ] **Abstract English (`06-abstract-en.tex`):** Terjemahan formal, 1 paragraf, istilah asing konsisten.
- [ ] **Ringkasan (`07-summary.tex`):** Panjang 1,5–2 halaman (`RULE-STR-07`), narasi holistik 3 blok babak tanpa butir-butir rumusan masalah.
- [ ] **Daftar Isi, Tabel, & Gambar (`09-toc.tex`):** Jarak antar section rapi (5pt), titik-titik pemimpin (*dot leaders*) sejajar, nomor halaman romawi kecil (i, ii, iii...) di tengah bawah.

### Bagian Utama (Main Body)
- [ ] **Bab 1 Pendahuluan:** Maksimal 4 halaman (`RULE-KEC-02`), rumusan masalah terarah, batasan masalah tegas.
- [ ] **Bab 2 Tinjauan Pustaka:** Maksimal 8 halaman (`RULE-KEC-03`), tabel komparasi penelitian terdahulu menyertakan minimal 3 jurnal bereputasi/Sinta 1-2.
- [ ] **Bab 3 Metodologi Penelitian:** Maksimal 4 halaman (`RULE-KEC-04`), diagram alur penelitian (*flowchart*) jelas, spesifikasi dataset WhatsApp 51.583 pesan.
- [ ] **Bab 4 Hasil & Pembahasan:** Maksimal 20 halaman (`RULE-KEC-05`), tabel terbuka (*open-table* / booktabs), metrik kurva pembelajaran ($C_{\text{NPMI}}$, Diversity, Outlier Rate) dianalisis kritis (*What, Why, How*).
- [ ] **Bab 5 Kesimpulan & Saran:** Maksimal 1 halaman (`RULE-KEC-06`), menjawab rumusan masalah secara lugas tanpa menyalin teks pembahasan.
- [ ] **Daftar Pustaka (`main.bbl`):** Format APA Style 7th edition, minimal 50% terbitan 10 tahun terakhir, semua sitasi di teks tertaut di daftar pustaka.
- [ ] **Lampiran (`02-appendices.tex`):** Bukti surat izin penelitian, bukti persetujuan admin grup WhatsApp, tabel pengujian black-box (34 test cases), dan tangkapan layar antarmuka sistem.

---

## 🖥️ FASE 3: Slide Presentasi & Demonstrasi Sistem Web

> [!important] Waktu presentasi di Fasilkom umumnya **15 menit**, sisanya 45–60 menit dialokasikan untuk tanya-jawab dan demo program.

### Struktur Slide (Target 12–15 Slide Padat)
- [ ] **Slide 1: Judul & Identitas** (Nama, NIM, Pembimbing, Penguji, Program Studi).
- [ ] **Slide 2: Latar Belakang & Masalah** (Fenomena *information overload* WhatsApp grup, urgensi pemodelan topik).
- [ ] **Slide 3: Paradoks Outlier & Limitasi Model Eksisting** (HDBSCAN membuang 42%–56% pesan; model jurnal tanpa reduksi topik menghasilkan 70+ topik acak).
- [ ] **Slide 4: Solusi & Kebaruan Arsitektur yang Diusulkan** (Diagram pipeline: IndoBERTweet + UMAP + ImprovedBIRCH + BM25 + Auto Reduction).
- [ ] **Slide 5: Dataset & Alur Preprocessing** (91.868 pesan mentah $\rightarrow$ 51.583 pesan bersih via deduplikasi, demojize, normalisasi teks).
- [ ] **Slide 6: Algoritma Usulan ImprovedBIRCH** (Threshold dinamis $[0{,}20, 0{,}25]$, pemangkasan outlier $2\sigma$ jarak sentroid, pembersihan klaster kerdil $N<5$).
- [ ] **Slide 7: Skema Eksperimen Kurva Pembelajaran (Learning Curve)** (Partisi bertahap 20%, 40%, 60%, 80%, 100% data pada 4 model komparasi).
- [ ] **Slide 8: Hasil Evaluasi Metrik Kuantitatif** (Tabel komparasi 100% data: Outlier 6,83%, $C_{\text{NPMI}}$ +0,0495, Diversity 0,9653, 150 topik).
- [ ] **Slide 9: Analisis Grafik Learning Curve** (Grafik tren $C_{\text{NPMI}}$, Outlier Rate, dan Intra-topic Similarity sepanjang pertambahan data).
- [ ] **Slide 10: Arsitektur Sistem Web Terintegrasi** (Diagram Client-Server: FastAPI backend, Vue.js frontend, Server-Sent Events, Client-Side Anonymization).
- [ ] **Slide 11: Pengujian Sistem (Black-Box Testing)** (Ringkasan 34 skenario pengujian fungsional dengan tingkat validitas 100%).
- [ ] **Slide 12: Kesimpulan & Saran** (Jawaban atas rumusan masalah dan roadmap penelitian lanjutan).
- [ ] **Slide 13: Slide Penutup & Ucapan Terima Kasih**.

### Kesiapan Demo Aplikasi (*Live Demonstration*)
- [ ] **Persiapan Lingkungan Lokal:**
  - [ ] Backend FastAPI berjalan lancar di `http://localhost:8000` (atau port terkait).
  - [ ] Frontend Vue.js berjalan di `http://localhost:5173`.
  - [ ] Bobot model / checkpoint IndoBERTweet dan dependensi NLP telah ter-cache lokal (tidak perlu download saat sidang).
- [ ] **Data Uji Siap Pakai:**
  - [ ] Menyiapkan file berkas chat WhatsApp `.txt` contoh (format valid) di folder desktop.
  - [ ] Menyiapkan file `.zip` WhatsApp obrolan.
  - [ ] Menyiapkan file invalid/korup untuk menunjukkan penanganan *error boundary* sistem.
- [ ] **Skenario Alur Demo (Durasi 3–5 Menit):**
  - [ ] *Langkah 1:* Buka halaman beranda $\rightarrow$ klik "Mulai Analisis".
  - [ ] *Langkah 2:* Unggah berkas chat $\rightarrow$ tunjukkan proses *client-side anonymization* (nama pengirim dan nomor langsung tersamarkan di browser sebelum diunggah).
  - [ ] *Langkah 3:* Atur rentang tanggal $\rightarrow$ jalankan analisis.
  - [ ] *Langkah 4:* Tunjukkan pemantauan *real-time progress* streaming via Server-Sent Events (SSE).
  - [ ] *Langkah 5:* Buka dashboard hasil: grafik jam aktif, panel metrik kuantitatif ($C_{\text{NPMI}}$, Diversity, Outlier), dan daftar klaster topik.
  - [ ] *Langkah 6:* Klik salah satu kartu topik $\rightarrow$ buka halaman detail topik $\rightarrow$ buka dialog modal *traceability* penelusuran konteks pesan asli.
- [ ] **Mitigasi Darurat / Rencana Cadangan (Plan B):**
  - [ ] Menyiapkan rekaman video demo (*screen recording* berkualitas tinggi MP4) berdurasi 3 menit jika server/browser mendadak hang.
  - [ ] Menyiapkan *hotspot* seluler cadangan jika koneksi WiFi fakultas bermasalah.

---

## 🎯 FASE 4: Simulasi Pertanyaan Sidang & Kunci Jawaban Ilmiah

> [!tip] Dosen penguji Fasilkom akan menguji **alasan metodologis (*why*)**, **pemahaman algoritma (*how*)**, serta **validitas data**. Kuasai 5 pertanyaan kunci berikut:

### Pertanyaan 1: Mengapa menggunakan IndoBERTweet, bukan model multilingual atau IndoBERT standar?
- **Poin Jawaban:**
  1. IndoBERTweet dilatih secara spesifik pada lebih dari 400 juta twit bahasa Indonesia yang karakternya sama persis dengan percakapan WhatsApp: teks pendek, tata bahasa informal, sarat bahasa slang, dan *code-mixing*.
  2. Model multilingual (seperti *multilingual-BERT* atau *all-MiniLM-L6-v2*) tidak memiliki representasi kosakata lokal Indonesia informal yang kaya, sehingga representasi vektor semantik obrolan grup WhatsApp menjadi bias.

### Pertanyaan 2: Apa kelemahan HDBSCAN bawaan BERTopic dan mengapa memilih BIRCH?
- **Poin Jawaban:**
  1. HDBSCAN bekerja berdasarkan estimasi kerapatan kepadatan (*density-based*). Pada teks obrolan WhatsApp yang ragam kosakatanya tinggi dan pesan-pesannya pendek, jarak antardokumen renggang, sehingga HDBSCAN menganggap 42%–56% pesan sebagai *outlier* (dibuang).
  2. BIRCH adalah algoritma hierarkis berkinerja tinggi yang memetakan dokumen ke dalam *Clustering Feature Tree* (CF-Tree) secara bertahap. Melalui modifikasi *ImprovedBIRCH*, kita berhasil menekan outlier menjadi hanya 6,83% (mempertahankan 93,17% data obrolan) tanpa kehilangan resolusi topik.

### Pertanyaan 3: Apa novelty / kontribusi baru algoritma *ImprovedBirch* yang Anda bangun?
- **Poin Jawaban:**
  1. **Inisialisasi Ambang Dinamis:** Menentukan ambang batas radius mikrogugus $\theta \in [0{,}20, 0{,}25]$ untuk menghasilkan subklaster awal yang homogen.
  2. **Pemotongan Outlier $2\sigma$:** Memangkas dokumen yang jarak kosinusnya melebihi 2 standar deviasi dari sentroid klaster.
  3. **Pembersihan Klaster Kerdil:** Mengeliminasi klaster dengan ukuran anggota $N < 5$.
  4. **Reduksi Topik Bertingkat:** Dipadukan dengan *hierarchical topic reduction* otomatis untuk menggabungkan subklaster semantik serupa.

### Pertanyaan 4: Mengapa skor koherensi $C_{\text{NPMI}}$ model usulan bernilai +0,0495 padahal baseline bernilai negatif (-0,0210)?
- **Poin Jawaban:**
  1. Baseline standar menggunakan c-TF-IDF konvensional yang rentan terhadap kata-kata berulang pada dokumen pendek, sehingga kata kunci topik sering kali berupa kata umum yang tidak koheren.
  2. Model usulan menggunakan skema pembobotan BM25 dengan saturasi frekuensi istilah dan normalisasi panjang dokumen, diperkaya kamus penyaring 9 kategori stopwords percakapan WhatsApp. Hal ini memastikan kata kunci topik memiliki asosiasi semantik yang kuat (*co-occurrence high*) di seluruh korpus.

### Pertanyaan 5: Bagaimana sistem web Anda menjamin privasi data anggota grup WhatsApp?
- **Poin Jawaban:**
  1. Menggunakan arsitektur *Client-Side Anonymization*: Sebelum pesan diunggah ke server FastAPI, browser (Vue.js) memproses data mentah di sisi pengguna terlebih dahulu.
  2. Identitas nomor HP, nama pengirim, dan mention pengguna langsung di-hashing menggunakan SHA-256 dan digantikan oleh pseudonim anonim di memori peramban klien.

---

## 🎒 FASE 5: Perlengkapan Hari-H Sidang (D-Day Kit)

### Busana & Penampilan (Sesuai Tata Tertib Fasilkom)
- [ ] Kemeja putih lengan panjang polos (berkerah, rapi disetrika).
- [ ] Dasi hitam polos / resmi.
- [ ] Celana kain formal warna hitam (bukan jeans/chino).
- [ ] Sabuk kulit formal warna hitam.
- [ ] Kaos kaki hitam dan sepatu pantofel formal warna hitam bersemir.
- [ ] Jas Almamater Universitas Jember (kancing lengkap).
- [ ] Potongan rambut rapi, bersih, dan harum.

### Perangkat Keras & Teknis
- [ ] Laptop kerja utama + kabel *charger* (baterai terisi penuh 100%).
- [ ] Dongle / konverter display: HDMI ke VGA dan Type-C ke HDMI (sesuaikan dengan proyektor ruang sidang).
- [ ] Wireless presenter / laser pointer + baterai cadangan.
- [ ] Flashdisk berisi: file slide PDF, slide PPTX, naskah `main.pdf`, dan video rekaman demo.
- [ ] Mouse wireless + mousepad.

### Berkas Fisik di Meja Ujian
- [ ] 3 Eksemplar draf naskah skripsi fisik (1 untuk mahasiswa, 2 untuk cadangan jika dosen memerlukan).
- [ ] Buku catatan revisi / notes kecil + pulpen tinta hitam 2 buah.
- [ ] *Sticky notes* (post-it) berwarna untuk menandai halaman yang dikritisi dosen.
- [ ] Air mineral botol tertutup untuk mahasiswa.

---

## 📝 FASE 6: Pasca-Sidang & Penyelesaian Revisi

- [ ] **Mencatat Seluruh Butir Masukan:**
  - [ ] Mencatat nama dosen penanya dan nomor halaman spesifik naskah yang direvisi.
  - [ ] Meminta Form Berita Acara Ujian Skripsi & Form Lembar Revisi dari sekretaris sidang / panitia.
- [ ] **Konsultasi Pasca-Sidang:**
  - [ ] Menemui Dosen Pembimbing untuk menyusun skala prioritas perbaikan naskah skripsi.
  - [ ] Menemui Dosen Penguji 1 dan Dosen Penguji 2 sesuai jadwal yang disepakati.
  - [ ] Menyelesaikan revisi naskah LaTeX dalam batas waktu resmi (maksimal 30 hari kalender).
- [ ] **Pengesahan Akhir:**
  - [ ] Menandatangani Lembar Pengesahan Kelulusan Skripsi (Dekan, Pembimbing, Penguji).
  - [ ] Mengurus bebas tanggungan perpustakaan UNEJ dan ruang baca Fasilkom.
  - [ ] Unggah berkas skripsi final (*full text* & naskah publikasi) ke repositori institusi UNEJ.
  - [ ] Mendaftar Yudisium dan Wisuda Sarjana Komputer (S.Kom.)! 🎓

---

> [!quote] *"Bukan kecerdasan semata yang menentukan kelulusan, melainkan ketekunan, ketenangan, dan penguasaan penuh atas apa yang telah Anda kerjakan sendiri."*  
> **Semoga sukses sidang skripsinya, Moh. Yusril Maqoshidana, S.Kom.!**
