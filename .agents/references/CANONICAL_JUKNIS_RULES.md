# Canonical Rules Reference: Juknis Skripsi Fasilkom UNEJ Versi 2.0 (2023)

Dokumen ini merupakan referensi kanonis resmi yang mengodifikasi seluruh aturan penulisan tugas akhir/skripsi di lingkungan Fakultas Ilmu Komputer (Fasilkom), Universitas Jember (UNEJ) berdasarkan:
1. **Buku Petunjuk Teknis Skripsi Fasilkom Versi 2.0 (Ditetapkan 6 November 2023)**.
2. **Keputusan Rektor UNEJ Nomor 5157/UN25/EP/2023 tentang Pedoman Penulisan Tugas Akhir Mahasiswa**.
3. **Keputusan Dekan Fasilkom Nomor 3439/UN25.1.15/SP/2023 tentang Buku Profil Penelitian Dosen Fasilkom**.

Dokumen ini menjadi *Single Source of Truth (SSOT)* bagi seluruh agent skills dalam ekosistem penulisan dan validasi skripsi berbasis LaTeX.

---

## 1. Kategori ADM: Ketentuan Administratif, Etika, dan Prosedur

### [RULE-ADM-01] Prasyarat Pengajuan Skripsi
- **Sumber:** Juknis Bab 6.3 (hlm. 96), Butir 1.
- **Isi Ketentuan:** Mahasiswa berhak menempuh skripsi apabila telah menempuh minimal 120 SKS, Prosentase Pembobotan (PP) $\ge 90\%$, dan Indeks Prestasi Kumulatif (IPK) $\ge 2.00$.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Persyaratan akademik mahasiswa sebelum memulai penulisan.
- **Implementasi LaTeX:** Metadata dokumen (`\studentID`, data akademik) diverifikasi terhadap status KRS/Transkrip.
- **Validasi:** Pemeriksaan berkas transkrip nilai oleh sistem audit administratif.
- **Risiko Pelanggaran:** Pengajuan judul dan bimbingan ditolak oleh Komisi Bimbingan.

### [RULE-ADM-02] Batas Waktu Pelaksanaan Seminar Proposal
- **Sumber:** Juknis Bab 6.1 (hlm. 95), Butir 4.
- **Isi Ketentuan:** Seminar proposal wajib dilaksanakan paling lama 3 bulan sejak diterbitkannya Surat Tugas Dosen Pembimbing. Jika melebihi batas waktu 3 bulan, mahasiswa wajib mengajukan ulang judul dan pembimbing melalui prosedur normal.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Pengelolaan waktu proposal skripsi.
- **Implementasi LaTeX:** Pencatatan tanggal penerbitan SK pembimbing pada log riwayat/metadata.
- **Validasi:** Komparasi tanggal SK dengan tanggal pelaksanaan sempro.
- **Risiko Pelanggaran:** Surat tugas kadaluarsa; reset pengajuan judul.

### [RULE-ADM-03] Batas Waktu Masa Pengerjaan Skripsi
- **Sumber:** Juknis Bab 6.1 (hlm. 95), Butir 5.
- **Isi Ketentuan:** Masa pengerjaan skripsi dilaksanakan paling lama 12 bulan sejak diterbitkannya Surat Tugas Dosen Pembimbing. Jika melebihi 12 bulan dan belum mendaftar ujian, mahasiswa harus mengajukan perpanjangan tertulis dengan persetujuan kedua pembimbing atau mengajukan ulang judul.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Siklus hidup pengerjaan skripsi.
- **Implementasi LaTeX:** Metadata tanggal pengesahan dan tanggal SK.
- **Validasi:** Validasi selisih tanggal SK terhadap jadwal ujian skripsi.
- **Risiko Pelanggaran:** Pembatalan bimbingan skripsi secara administratif.

### [RULE-ADM-04] Pernyataan Orisinalitas Bermaterai Rp10.000
- **Sumber:** Juknis Bab 3.2.1.5 (hlm. 80), Bab 6.5 (hlm. 99), Lampiran 7 (hlm. 109).
- **Isi Ketentuan:** Halaman pernyataan orisinalitas wajib bermaterai Rp10.000 dan ditandatangani basah dengan tinta biru oleh mahasiswa, menyatakan karya bebas plagiasi dan belum pernah diajukan untuk gelar akademik lain.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Bagian awal naskah skripsi (Frontmatter).
- **Implementasi LaTeX:** Lingkungan `frontmatterchapter{PERNYATAAN ORISINALITAS}` dengan placeholder ruang materai dan tanda tangan fisik.
- **Validasi:** Verifikasi visual pada dokumen cetak/scan final.
- **Risiko Pelanggaran:** Dokumen skripsi tidak sah secara hukum dan ditolak saat pendaftaran yudisium.

### [RULE-ADM-05] Batas Toleransi Similarity Cek Plagiasi
- **Sumber:** Juknis Bab 1.5.1 (hlm. 10–11), Lampiran 7 (hlm. 109).
- **Isi Ketentuan:** Naskah skripsi wajib menyertakan bukti uji plagiasi (Turnitin/sistem rekomendasi UNEJ) dengan tingkat kesamaan (similarity) maksimal 30% pada bagian utama, dan maksimal 10% untuk satu sumber tunggal (*single source*), tidak termasuk daftar pustaka. Jika melebihi batas toleransi, wajib melampirkan *expert judgement* dari Dosen Pembimbing.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Bagian Inti naskah (Bab 1 s.d. Bab 5).
- **Implementasi LaTeX:** Parafrase ilmiah berbantukan skill penulisan EYD untuk meminimalkan kemiripan leksikal verbatim.
- **Validasi:** Laporan hasil Turnitin resmi bertanda tangan pembimbing.
- **Risiko Pelanggaran:** Pembatalan pendaftaran ujian skripsi, sanksi skorsing atau pembatalan skripsi.

### [RULE-ADM-06] Standar Kriteria Kelulusan Ujian Skripsi
- **Sumber:** Juknis Bab 5.3 (hlm. 94), Bab 6.5 (hlm. 99–100).
- **Isi Ketentuan:** Mahasiswa dinyatakan lulus jika memperoleh nilai akhir minimal 60 (huruf mutu C) hingga 100 (huruf mutu A). Nilai < 60 wajib ujian ulang minimal 2 minggu kemudian. Perbaikan nilai diperbolehkan maksimal 2 kali ujian ulang dengan persetujuan kedua pembimbing.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Tahap evaluasi akhir.
- **Implementasi LaTeX:** N/A (Administratif ujian).
- **Validasi:** Berita Acara Ujian Skripsi.
- **Risiko Pelanggaran:** Tidak lulus yudisium.

---

## 2. Kategori TIT: Ketentuan Judul Skripsi

### [RULE-TIT-01] Bentuk Frasa dan Larangan Kata Kerja Pembuka
- **Sumber:** Juknis Bab 4.1.4.a (hlm. 85).
- **Isi Ketentuan:** Judul skripsi harus berbentuk frasa, tidak boleh berupa kalimat deklaratif/berpredikat lengkap, dan TIDAK BOLEH diawali dengan kata kerja (misal: dilarang diawali kata "Membangun", "Membuat", "Menganalisis", "Mengembangkan").
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Judul Skripsi (Cover, Judul, Lembar Pengesahan, Abstrak, Metadata).
- **Implementasi LaTeX:** Makro `\titleLine` dan `\titleUpperCase` didefinisikan dengan frasa nominal (contoh: "Sistem Analisis...", "Rancang Bangun...", "Klasifikasi...").
- **Validasi:** Regex / NLP POS-tagger: kata pertama tidak boleh bermorfologi kata kerja prefiks me-/ber- aktif transisi.
- **Risiko Pelanggaran:** Penolakan usulan judul pada seminar proposal atau revisi wajib saat ujian skripsi.

### [RULE-TIT-02] Batas Maksimal Panjang Judul (Disarankan $\le$ 15 Kata)
- **Sumber:** Juknis Bab 4.1.4.b (hlm. 85).
- **Isi Ketentuan:** Panjang judul sebaiknya tidak lebih dari 15 kata, di luar kata sambung (dan, atau, serta) dan kata depan (pada, di, ke, dari, dengan, untuk, dalam).
- **Status:** DIANJURKAN (Recommended).
- **Ruang Lingkup:** Judul utama skripsi.
- **Implementasi LaTeX:** Script audit menghitung jumlah token leksikal non-stopwords dalam `\titleLine`.
- **Validasi:** Automated word count excluding Indonesian stopword conjunctions and prepositions.
- **Risiko Pelanggaran:** Teguran redaksional oleh tim komisi bimbingan/penguji.

### [RULE-TIT-03] Pembagian Judul dan Anak Judul
- **Sumber:** Juknis Bab 4.1.4.c (hlm. 85).
- **Isi Ketentuan:** Judul yang panjang dapat dibagi menjadi judul utama dan anak judul (subjudul) yang dipisahkan oleh tanda titik dua (`:`) atau kurung (`(...)`) dengan ukuran font yang seragam.
- **Status:** OPSIONAL (Optional).
- **Ruang Lingkup:** Judul skripsi kompleks/interdisipliner.
- **Implementasi LaTeX:** Pemisahan struktur subjudul pada `\titleLine`.
- **Validasi:** Pemeriksaan tanda pemisah `: ` atau `( )`.
- **Risiko Pelanggaran:** Tidak ada (panduan fleksibilitas redaksi).

### [RULE-TIT-04] Format Tipografi Judul
- **Sumber:** Juknis Bab 4.1.4.d (hlm. 85).
- **Isi Ketentuan:** Judul ditulis dengan huruf KAPITAL (ALL CAPS), dicetak TEBAL (bold), ukuran font 14pt, spasi 1 (single space), dan TIDAK DIAKHIRI dengan tanda titik (`.`).
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Sampul luar dan halaman judul dalam.
- **Implementasi LaTeX:** `{\bfseries\fontsize{14pt}{16pt}\selectfont \titleUpperCase\par}` tanpa tanda titik penutup.
- **Validasi:** Linting string `\titleUpperCase` memastikan semua huruf kapital dan tidak ada karakter `.` di akhir string.
- **Risiko Pelanggaran:** Pelanggaran format cover resmi Fasilkom.

---

## 3. Kategori STR: Struktur Dokumen dan Urutan Halaman

### [RULE-STR-01] Urutan Baku Bagian Awal (Frontmatter)
- **Sumber:** Juknis Bab 3.2.1 (hlm. 78–81).
- **Isi Ketentuan:** Bagian awal laporan skripsi wajib memuat halaman-halaman dengan urutan hierarki sebagai berikut:
  1. Halaman Sampul Depan (Cover Luar)
  2. Halaman Judul (Sub Cover Dalam)
  3. Halaman Persembahan (Dedication)
  4. Halaman Moto
  5. Halaman Pernyataan Orisinalitas (bermaterai)
  6. Halaman Persetujuan / Pengesahan
  7. Abstrak (Bahasa Indonesia)
  8. Abstract (Bahasa Inggris)
  9. Summary / Ringkasan
  10. Prakata (Preface)
  11. Daftar Isi
  12. Daftar Tabel (jika ada tabel dalam dokumen)
  13. Daftar Gambar (jika ada gambar dalam dokumen)
  14. Daftar Lampiran (jika ada lampiran dalam dokumen)
  15. Daftar Notasi / Istilah / Singkatan (opsional jika diperlukan)
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Keseluruhan blok Frontmatter.
- **Implementasi LaTeX:** Urutan berkas `\input{frontmatter/...}` di dalam `main.tex`.
- **Validasi:** Verifikasi urutan eksekusi file dan kecocokan daftar entri TOC.
- **Risiko Pelanggaran:** Dokumen tidak sesuai standar sistematika penulisan Fasilkom.

### [RULE-STR-02] Ketentuan Logo Universitas Jember pada Sampul
- **Sumber:** Juknis Bab 3.2.1.1.a (hlm. 79).
- **Isi Ketentuan:** Logo Universitas Jember resmi berwarna dengan diameter presisi 5.0 cm diletakkan di bagian atas halaman sampul.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Halaman Sampul dan Halaman Judul.
- **Implementasi LaTeX:** `\includegraphics[width=5cm]{images/logo_unej.png}`.
- **Validasi:** Pemeriksaan parameter `width` pada pemanggilan logo di berkas cover.
- **Risiko Pelanggaran:** Proporsi cover tidak simetris atau melanggar visual identity UNEJ.

### [RULE-STR-03] Maksud Penelitian pada Sampul
- **Sumber:** Juknis Bab 3.2.1.1.d (hlm. 79).
- **Isi Ketentuan:** Pernyataan maksud penelitian berbunyi: "diajukan untuk memenuhi sebagian persyaratan memperoleh gelar Sarjana Komputer pada Program Studi [Nama Prodi]".
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Halaman Sampul & Judul.
- **Implementasi LaTeX:** Teks statis terstandarisasi dalam berkas `frontmatter/00-cover.tex`.
- **Validasi:** String matching terhadap klausul resmi.
- **Risiko Pelanggaran:** Kesalahan administrasi penyebutan gelar sarjana.

### [RULE-STR-04] Urutan Hierarki Identitas Institusi pada Sampul
- **Sumber:** Juknis Bab 3.2.1.1.f, g (hlm. 79).
- **Isi Ketentuan:** Hierarki nama institusi wajib berurutan dari unit tertinggi ke terendah:
  1. KEMENTERIAN PENDIDIKAN, KEBUDAYAAN, RISET, DAN TEKNOLOGI (atau kementerian pembina terkini)
  2. UNIVERSITAS JEMBER
  3. FAKULTAS ILMU KOMPUTER
  4. PROGRAM STUDI [INFORMATIKA / SISTEM INFORMASI / TEKNOLOGI INFORMASI]
  5. JEMBER
  6. [TAHUN YUDISIUM] (diletakkan tepat di bawah kata Jember)
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Bagian bawah halaman sampul.
- **Implementasi LaTeX:** Penataan teks terpusat (centering) pada `frontmatter/00-cover.tex`.
- **Validasi:** Urutan blok teks diperiksa terhadap urutan kementerian -> universitas -> fakultas -> prodi -> kota -> tahun.
- **Risiko Pelanggaran:** Ditolak oleh staf akademik perpustakaan saat penyerahan berkas akhir.

### [RULE-STR-05] Ketentuan Abstrak (Indonesia dan Inggris)
- **Sumber:** Juknis Bab 3.2.1.7 (hlm. 80).
- **Isi Ketentuan:** Panjang teks Abstrak/Abstract wajib antara 200 sampai dengan 300 kata. Isi mencakup secara terpadu: permasalahan, tujuan, metodologi penelitian, hasil, dan kesimpulan. Ditulis dalam satu paragraf atau bentuk ikhtisar terpadu. Jika skripsi berbahasa Indonesia, abstract bahasa Inggris wajib disertakan.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** `frontmatter/05-abstract-id.tex` dan `frontmatter/06-abstract-en.tex`.
- **Implementasi LaTeX:** Teks abstrak berbobot 200–300 kata, diakhiri `\keywords{...}` atau `\keywordsen{...}`.
- **Validasi:** Perhitungan jumlah kata otomatis: $200 \le \text{word\_count} \le 300$.
- **Risiko Pelanggaran:** Teguran reviewer atau koreksi abstrak saat sidang akhir.

### [RULE-STR-06] Kata Kunci (Keywords)
- **Sumber:** Juknis Bab 3.2.1.7 (hlm. 80), Bab 4.1.3 (hlm. 85).
- **Isi Ketentuan:** Memuat 3 hingga 7 istilah representatif yang mencerminkan topik, metode, dan domain penelitian. Istilah bahasa asing ditulis cetak miring (*italic*).
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Lembar Abstrak & Abstract.
- **Implementasi LaTeX:** `\noindent \textbf{Kata Kunci:} \textit{Kata1, Kata2, Kata3}`.
- **Validasi:** Pemeriksaan keberadaan label kata kunci dan jumlah terms.
- **Risiko Pelanggaran:** Penurunan keterindeksan karya ilmiah di repositori UNEJ.

### [RULE-STR-07] Ketentuan Dokumen Summary / Ringkasan
- **Sumber:** Juknis Bab 3.2.1.8 (hlm. 80).
- **Isi Ketentuan:** Memberikan narasi komprehensif poin-poin utama naskah skripsi (konteks, masalah, metodologi, hasil analisis kuantitatif/kualitatif, implikasi/kesimpulan) dengan panjang 1–2 halaman, tanpa duplikasi kalimat verbatim secara sembarangan.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** `frontmatter/07-summary.tex`.
- **Implementasi LaTeX:** `\frontmatterchapter{RINGKASAN}` dengan 4–6 paragraf naratif terstruktur.
- **Validasi:** Pengecekan keberadaan bab Ringkasan dan panjang halaman ($1 \le \text{halaman} \le 2$).
- **Risiko Pelanggaran:** Kekurangan komponen frontmatter wajib Fasilkom.

### [RULE-STR-08] Struktur Bab Bagian Utama (Main Body)
- **Sumber:** Juknis Bab 3.2.2 (hlm. 81–83).
- **Isi Ketentuan:** Naskah skripsi terdiri atas 5 bab berurutan:
  - BAB 1: PENDAHULUAN (Latar Belakang, Rumusan Masalah, Batasan Masalah, Tujuan Penelitian, Manfaat Penelitian)
  - BAB 2: TINJAUAN PUSTAKA (Penelitian Terdahulu, Landasan Teori)
  - BAB 3: METODOLOGI PENELITIAN (Lokasi & Waktu, Populasi/Sampel/Subjek, Data Penelitian, Prosedur Penelitian/Flowchart, Alat/Instrumen, Metode Analisis)
  - BAB 4: HASIL DAN PEMBAHASAN (Penyajian data terolah, tabel, gambar, analisis kritis apa/mengapa/bagaimana)
  - BAB 5: KESIMPULAN DAN SARAN (Kesimpulan terpisah menjawab rumusan masalah, Saran rekomendasi/penelitian lanjutan)
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** `chapters/01-introduction.tex` s.d. `chapters/05-conclusion.tex`.
- **Implementasi LaTeX:** Definisi `\chapter{...}` dan `\section{...}` yang tepat dan berurutan.
- **Validasi:** Parser LaTeX memverifikasi kehadiran seluruh bab 1 s.d. 5 dan subbab wajib.
- **Risiko Pelanggaran:** Naskah dianggap tidak memenuhi kaidah penulisan ilmiah standar UNEJ.

### [RULE-STR-09] Bagian Akhir (Backmatter)
- **Sumber:** Juknis Bab 3.2.3 (hlm. 83–84).
- **Isi Ketentuan:** Memuat Daftar Pustaka (APA style) dan Lampiran (data pelengkap, kuesioner, source code, data mentah, surat izin).
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** `backmatter/01-references.tex` dan `backmatter/02-appendices.tex`.
- **Implementasi LaTeX:** `\bibliography{...}` dan lingkungan `\appendix`.
- **Validasi:** Memastikan Daftar Pustaka tidak kosong dan lampiran bernomor sesuai ketentuan.
- **Risiko Pelanggaran:** Hilangnya bukti pendukung penelitian.

---

## 4. Kategori PAG: Format Halaman, Layout, dan Tipografi

### [RULE-PAG-01] Standar Kertas Layout
- **Sumber:** Juknis Bab 4.1.2 (hlm. 85).
- **Isi Ketentuan:** Dokumen diketik dengan ukuran kertas A4 (21,0 cm $\times$ 29,7 cm), orientasi portrait (kecuali halaman tabel/grafik luas yang memerlukan landscape tersendiri).
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Global layout.
- **Implementasi LaTeX:** `\documentclass[12pt, a4paper, oneside]{report}` dan paket `geometry`.
- **Validasi:** pdfinfo memverifikasi `Page size: 595.276 x 841.89 pts (A4)`.
- **Risiko Pelanggaran:** Ukuran cetak tidak sesuai kertas penjilidan skripsi.

### [RULE-PAG-02] Batas Margin Dokumen
- **Sumber:** Juknis Bab 4.1.2 (hlm. 85).
- **Isi Ketentuan:** Batas tepi pengetikan (margin):
  - Margin Atas: 4 cm
  - Margin Kiri: 4 cm (ruang penjilidan)
  - Margin Bawah: 3 cm
  - Margin Kanan: 3 cm
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Seluruh halaman naskah.
- **Implementasi LaTeX:** `\usepackage[top=4cm, left=4cm, bottom=3cm, right=3cm]{geometry}`.
- **Validasi:** Linting konfigurasi `geometry` di `config/packages.tex`.
- **Risiko Pelanggaran:** Teks terpotong saat proses jilid skripsi (*hardcover*).

### [RULE-PAG-03] Jenis dan Ukuran Huruf (Font)
- **Sumber:** Juknis Bab 4.1.2 (hlm. 85).
- **Isi Ketentuan:** Jenis huruf wajib **Times New Roman** (atau font serif klon standar TeX `times`/`mathptmx`), ukuran teks isi 12pt, judul bab 14pt tebal, caption tabel/gambar 11pt, isian tabel 8–12pt.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Seluruh teks dokumen.
- **Implementasi LaTeX:** Paket `\usepackage{times}` atau `\usepackage{newtxtext,newtxmath}`, `\fontsize{12pt}{1.5}`.
- **Validasi:** PDF font inspection memastikan font Times/Nimbus Roman tersemat.
- **Risiko Pelanggaran:** Ketidakseragaman estetika naskah.

### [RULE-PAG-04] Jarak Antar Baris (Spasi Teks)
- **Sumber:** Juknis Bab 4.1.2 (hlm. 85).
- **Isi Ketentuan:** Jarak antar baris teks isi naskah adalah 1,5 spasi. Spasi tunggal (1 spasi) berlaku untuk judul skripsi, kutipan langsung $>4$ baris, isian sel tabel, caption multi-baris, dan entri bibliografi.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Teks utama dan elemen khusus.
- **Implementasi LaTeX:** `\usepackage{setspace}` dengan `\setstretch{1.5}` secara global, serta `\begin{spacing}{1}` pada tabel/kutipan.
- **Validasi:** Verifikasi parameter `setstretch` atau `onehalfspacing`.
- **Risiko Pelanggaran:** Naskah terlihat terlalu padat atau terlalu renggang.

### [RULE-PAG-05] Penomoran Halaman Bagian Awal
- **Sumber:** Juknis Bab 4.1.5.a (hlm. 85).
- **Isi Ketentuan:** Halaman bagian awal menggunakan angka Romawi kecil (`i`, `ii`, `iii`, `iv`, dst.) diletakkan di bagian TENGAH BAWAH halaman. Halaman sampul dihitung sebagai halaman `i` tetapi nomornya tidak dicetak.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Frontmatter.
- **Implementasi LaTeX:** `\pagenumbering{roman}`, `\pagestyle{plain}` (di mana `plain` didefinisikan nomor di `\fancyfoot[C]`).
- **Validasi:** Analisis tata letak header/footer pada halaman awal file PDF.
- **Risiko Pelanggaran:** Kesalahan format navigasi halaman awal.

### [RULE-PAG-06] Penomoran Halaman Bagian Utama (Halaman Biasa)
- **Sumber:** Juknis Bab 4.1.5.b (hlm. 85).
- **Isi Ketentuan:** Halaman isi bagian utama menggunakan angka Arab (`1`, `2`, `3`, dst.) diletakkan di bagian KANAN ATAS halaman, termasuk pada halaman lampiran dan halaman landscape.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Main Body & Backmatter.
- **Implementasi LaTeX:** `\pagenumbering{arabic}`, `\pagestyle{fancy}`, dengan `\fancyhead[R]{\thepage}` dan `\fancyfoot{}` kosong.
- **Validasi:** Inspeksi visual/otomatis penempatan nomor halaman pada running headers PDF.
- **Risiko Pelanggaran:** Pelanggaran standar tata letak nomor halaman UNEJ.

### [RULE-PAG-07] Penomoran Halaman Pertama Setiap Bab
- **Sumber:** Juknis Bab 4.1.5.c (hlm. 85).
- **Isi Ketentuan:** Pada halaman pertama setiap bab (halaman judul bab), nomor halaman Arab diletakkan di bagian TENGAH BAWAH, bukan di kanan atas.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Halaman awal setiap `\chapter`.
- **Implementasi LaTeX:** LaTeX secara otomatis menggunakan pagestyle `plain` untuk halaman pembuka chapter. Diatur via `\fancypagestyle{plain}{\fancyhf{}\fancyfoot[C]{\thepage}}`.
- **Validasi:** Pengujian PDF pada halaman-halaman awal Bab 1 s.d. Bab 5.
- **Risiko Pelanggaran:** Nomor halaman menimpa header atau tidak seragam di lembar awal bab.

### [RULE-PAG-08] Batas Maksimal Halaman Skripsi (Maksimal 40 Halaman)
- **Sumber:** Juknis Bab 4.2, Tabel 4.1 (hlm. 88).
- **Isi Ketentuan:** Jumlah maksimal halaman per bagian skripsi dibatasi sebagai berikut:
  - Bab 1 Pendahuluan: maksimal 4 halaman
  - Bab 2 Tinjauan Pustaka: maksimal 8 halaman
  - Bab 3 Metodologi Penelitian: maksimal 4 halaman
  - Bab 4 Hasil dan Pembahasan: maksimal 20 halaman
  - Bab 5 Kesimpulan dan Saran: maksimal 1 halaman
  - Daftar Pustaka: maksimal 3 halaman
  - **Total Maksimal Halaman Bagian Utama: 40 halaman**.
- **Status:** WAJIB / PANDUAN BATASAN KETAT (Strict Guideline).
- **Ruang Lingkup:** Bagian Inti naskah (Main Body).
- **Implementasi LaTeX:** Kebijakan Operasional Baku (Zero Text Mutation & User Consent):
  1. Agent dilarang keras mengubah atau memotong teks narasi eksisting pengguna secara sepihak.
  2. Agent hanya mengeluarkan warning informatif jika bab melampaui alokasi kuota halaman.
  3. Agent mendeteksi paragraf dengan pembahasan ganda (double discussion) antar-bab dan memberikan saran penajaman berbasis rujukan silang (`\ref{...}`).
  4. Pemindahan tabel data mentah atau gambar besar ke Lampiran (Backmatter) hanya dilakukan setelah mendapatkan persetujuan eksplisit dari pengguna.
- **Validasi:** Perhitungan jumlah halaman per bab dari log build dan deteksi paragraf redundan.
- **Risiko Pelanggaran:** Penolakan naskah atau permintaan pemangkasan ketat oleh komisi bimbingan karena melebihi kuota 40 halaman SK Rektor.

---

## 5. Kategori SEC: Penomoran Bab, Subbab, dan Hierarki Bagian

### [RULE-SEC-01] Format Judul Bab
- **Sumber:** Juknis Bab 4.1.6.a (hlm. 85).
- **Isi Ketentuan:** Penomoran bab menggunakan angka Arab setelah kata "BAB" (misal: "BAB 1", "BAB 2", bukan angka Romawi seperti BAB I). Ditulis dengan huruf kapital, bold, 14pt, center.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Headings Chapter.
- **Implementasi LaTeX:** Konfigurasi `\titleformat{\chapter}` di `config/formatting.tex`:
  `{\MakeUppercase{\chaptertitlename} \thechapter.\hspace{0.5em}}`.
- **Validasi:** Regex memeriksa naskah `BAB \d+` tanpa angka Romawi.
- **Risiko Pelanggaran:** Format heading usang yang tidak mematuhi Versi 2.0.

### [RULE-SEC-02] Format Penomoran Subbab
- **Sumber:** Juknis Bab 4.1.6.b (hlm. 85).
- **Isi Ketentuan:** Penomoran subbab menggunakan angka Arab 2 digit dipisahkan tanda titik bertuliskan tebal (bold). Digit 1 adalah nomor bab, digit 2 nomor urut subbab. Angka terakhir TIDAK DIBERI tanda titik (contoh yang benar: **1.1**, **2.3**; bukan 1.1.).
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** `\section` headings.
- **Implementasi LaTeX:** `\thesection` default LaTeX menghasilkan format `1.1` tanpa titik akhir.
- **Validasi:** Memastikan string section label tidak diakhiri tanda titik.
- **Risiko Pelanggaran:** Kesalahan tanda baca pada hierarki judul.

### [RULE-SEC-03] Format Penomoran Sub-subbab
- **Sumber:** Juknis Bab 4.1.6.c (hlm. 85–86).
- **Isi Ketentuan:** Penomoran sub-subbab menggunakan angka Arab 3 digit dipisahkan tanda titik (contoh: **1.1.1**, **2.3.1**). Angka terakhir tidak diberi tanda titik.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** `\subsection` headings.
- **Implementasi LaTeX:** `\thesubsection` menghasilkan format `1.1.1`.
- **Validasi:** Label heading tidak mengandung trailing dot.
- **Risiko Pelanggaran:** Inkonsistensi penomoran hierarki dokumen.

### [RULE-SEC-04] Batasan Kedalaman Digit Angka (Maksimal 3 Digit)
- **Sumber:** Juknis Bab 4.1.6.d (hlm. 85–86).
- **Isi Ketentuan:** Penomoran menggunakan digit angka TIDAK BOLEH lebih dari 3 digit (dilarang menggunakan format 1.1.1.1). Jika diperlukan hierarki lebih rendah, wajib menggunakan urutan penomoran:
  1. Huruf kecil: `a.`, `b.`, `c.`, dst.
  2. Angka dengan kurung tutup: `1)`, `2)`, `3)`, dst.
  3. Huruf kecil dengan kurung tutup: `a)`, `b)`, `c)`, dst.
  4. Angka dengan kurung ganda: `(1)`, `(2)`, `(3)`, dst.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Sub-headings dan list item dalam paragraf.
- **Implementasi LaTeX:** `\setcounter{secnumdepth}{3}`. Penggunaan `\subsubsubsection{...}` yang memetakan ke `\alph{subsubsection}.` atau `enumitem`.
- **Validasi:** Linting TeX memastikan tidak ada `1.1.1.1` atau `\subparagraph` berangka 4 digit.
- **Risiko Pelanggaran:** Penolakan format naskah pada tahap evaluasi teknis.

---

## 6. Kategori FLT: Tabel, Gambar, Persamaan, dan Lampiran

### [RULE-FLT-01] Penempatan Horizontal Elemen Apung (Float)
- **Sumber:** Juknis Bab 4.1.7.a (hlm. 86).
- **Isi Ketentuan:** Seluruh tabel dan gambar wajib diletakkan pada posisi TENGAH (center) secara horizontal dan menempati paragraf tersendiri, terpisah jelas dari teks narasi di atas dan di bawahnya.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Floating environments `table` dan `figure`.
- **Implementasi LaTeX:** Menyertakan deklarasi `\centering` di awal setiap blok environment float.
- **Validasi:** Linter memverifikasi adanya `\centering` di dalam setiap `\begin{table}` dan `\begin{figure}`.
- **Risiko Pelanggaran:** Tata letak visual dokumen berantakan dan tidak rapi.

### [RULE-FLT-02] Kewajiban Rujukan Naskah Sebelum Kemunculan Float
- **Sumber:** Juknis Bab 4.1.7.b, c (hlm. 86).
- **Isi Ketentuan:**
  1. Setiap tabel dan gambar WAJIB dirujuk secara eksplisit dalam naskah narasi.
  2. Penulisan rujukan wajib menggunakan huruf kapital di awal (*Title Case*), contoh: "...dapat dilihat pada Tabel 2.3", "...sebagaimana disajikan pada Gambar 3.1".
  3. Halaman yang memuat tabel atau gambar TIDAK BOLEH mendahului halaman yang memuat kalimat rujukan pertamanya.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Cross-referencing dan layout typesetting.
- **Implementasi LaTeX:** Penempatan `\label{tab:...}` dan `\label{fig:...}` serta pemanggilan via `Tabel~\ref{tab:...}` atau `Gambar~\ref{fig:...}`. Menghindari penempatan float dengan parameter spekulatif `[t]` sebelum teks rujukan.
- **Validasi:** Automated check: (1) Semua `\label` float memiliki minimal 1 `\ref` di dalam teks. (2) String rujukan diawali "Tabel" / "Gambar" kapital. (3) Nomor halaman float $\ge$ nomor halaman rujukan pertama.
- **Risiko Pelanggaran:** Catatan revisi fatal dari dosen penguji (tabel liar tanpa rujukan konteks).

### [RULE-FLT-03] Format Penomoran Ilustrasi (Tabel dan Gambar)
- **Sumber:** Juknis Bab 4.1.6.e (hlm. 86).
- **Isi Ketentuan:** Penomoran ilustrasi menggunakan angka Arab 2 digit dipisahkan tanda titik, diletakkan setelah kata "Tabel" atau "Gambar". Digit pertama menunjukkan nomor bab letak ilustrasi, digit kedua nomor urut ilustrasi yang dimulai dari angka 1 pada setiap bab. Tanda baca titik TIDAK DIPERLUKAN setelah digit kedua (contoh: "Tabel 2.1", "Gambar 4.12").
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Captions tabel dan gambar.
- **Implementasi LaTeX:** Konfigurasi default document class `report` menghasilkan `\thetable` berupa `<chapter>.<table_index>` dan `\thefigure` berupa `<chapter>.<figure_index>`.
- **Validasi:** Pengecekan caption label generator TeX.
- **Risiko Pelanggaran:** Penomoran ilustrasi salah atau tidak terikat bab.

### [RULE-FLT-04] Ketentuan Judul Tabel (Caption di Atas)
- **Sumber:** Juknis Bab 4.1.7.d, e (hlm. 86–87).
- **Isi Ketentuan:** Judul tabel diletakkan di ATAS tabel. Menggunakan huruf sentence case (hanya huruf awal kalimat yang kapital), font 11pt, dan TIDAK DIAKHIRI tanda titik. Jika hanya satu baris diletakkan di tengah (center); jika lebih dari satu baris, penulisan judul menggunakan format menggantung (indent) rata kiri sejajar huruf pertama judul dengan spasi 1. Jarak antara judul tabel dan garis atas tabel adalah 6pt.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Seluruh tabel skripsi.
- **Implementasi LaTeX:**
  ```latex
  \captionsetup[table]{
    position=above,
    font={small}, % 11pt
    labelsep=period,
    justification=centering,
    skip=6pt
  }
  ```
- **Validasi:** Linter memverifikasi `\caption{...}` berada SEBELUM isi tabel tabular/booktabs dan tidak diakhiri `.`.
- **Risiko Pelanggaran:** Pelanggaran format baku penyajian tabel akademik.

### [RULE-FLT-05] Format Tabel Terbuka (Open Table)
- **Sumber:** Juknis Bab 4.1.7.e (hlm. 86–87).
- **Isi Ketentuan:** Tabel wajib disajikan dengan format tabel terbuka: memiliki garis pemisah horizontal pada heading atas (`\toprule`), batas bawah heading (`\midrule`), dan garis penutup horizontal bawah (`\bottomrule`). Garis pemisah horizontal lainnya dan **seluruh garis pemisah vertikal dilarang ditampilkan** kecuali sangat diperlukan untuk matriks data khusus. Isian sel tabel berjarak 1 spasi, font dapat diperkecil hingga 8pt jika tabel padat.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Environment `tabular`, `tabularx`, `longtable`.
- **Implementasi LaTeX:** Penggunaan paket `booktabs` (`\toprule`, `\midrule`, `\bottomrule`) tanpa karakter `|` pada argumen kolom tabel (`\begin{tabular}{l c r}`).
- **Validasi:** Regex mendeteksi apakah argumen tabular mengandung kolom vertikal `|` dan apakah memakai `\hline` konvensional.
- **Risiko Pelanggaran:** Tampilan tabel bergaya kuno "kotak tertutup" yang melanggar standar modern Fasilkom UNEJ.

### [RULE-FLT-06] Sumber dan Keterangan Tabel
- **Sumber:** Juknis Bab 4.1.7.e (hlm. 87).
- **Isi Ketentuan:** Keterangan tabel (jika ada) diletakkan di BAWAH tabel menggunakan font 11pt tanpa mencantumkan kata "Keterangan:". Sumber tabel (khusus jika data bersumber dari data sekunder/pihak lain) diletakkan setelah keterangan tabel dengan font 11pt (contoh: "Sumber: BPS (2023)").
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Tabel data sekunder.
- **Implementasi LaTeX:** Catatan kaki tabel menggunakan `\vspace{2pt}\par\raggedright\small (Sumber: ...)\par`.
- **Validasi:** Memastikan keterangan diletakkan di bawah tabel.
- **Risiko Pelanggaran:** Pelanggaran atribusi hak cipta dan tata letak data sekunder.

### [RULE-FLT-07] Ketentuan Judul Gambar (Caption di Bawah)
- **Sumber:** Juknis Bab 4.1.7.d, f (hlm. 86–87).
- **Isi Ketentuan:** Judul gambar diletakkan di BAWAH gambar. Menggunakan format sentence case, font 11pt, dan tidak diakhiri tanda titik. Keterangan/penjelasan gambar ditulis sebelum judul gambar, sedangkan sumber gambar ditulis setelah judul gambar di dalam tanda kurung, misal: "Gambar 2.1 Arsitektur sistem (Sumber: Somervile, 2011)". Jarak gambar ke judul adalah 1 spasi. Penyajian gambar hasil kreasi sendiri tidak perlu mencantumkan sumber.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Seluruh gambar, bagan, flowchart, dan screenshot skripsi.
- **Implementasi LaTeX:** `\caption{...}` ditempatkan SETELAH `\includegraphics{...}`.
- **Validasi:** Linter memverifikasi posisi `\caption` berada di bawah gambar.
- **Risiko Pelanggaran:** Penempatan judul gambar di atas gambar (salah peletakan).

### [RULE-FLT-08] Penomoran Lampiran Berbasis Bab
- **Sumber:** Juknis Bab 4.1.6.f (hlm. 86).
- **Isi Ketentuan:** Penomoran lampiran menggunakan angka Arab 2 digit. Digit pertama adalah nomor bab tempat lampiran tersebut diperlukan/dirujuk, digit kedua adalah nomor urut lampiran pada bab tersebut (contoh: Lampiran 3.1 adalah lampiran pertama yang dirujuk dari Bab 3).
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** `backmatter/02-appendices.tex`.
- **Implementasi LaTeX:** Makro penomoran lampiran kustom yang mengaitkan nomor lampiran ke bab asal rujukan.
- **Validasi:** Pemeriksaan nomor lampiran di daftar lampiran.
- **Risiko Pelanggaran:** Ketidakjelasan asal-usul lampiran dalam pembahasan naskah.

---

## 7. Kategori CIT: Sitasi, Pengutipan, dan Daftar Pustaka

### [RULE-CIT-01] Penggunaan Gaya Sitasi APA Style
- **Sumber:** Juknis Bab 3.2.3.1 (hlm. 83), Bab 4.1.7.g (hlm. 88), Bab 4.3 (hlm. 88–90).
- **Isi Ketentuan:** Sistem sitasi dan penulisan daftar pustaka wajib menggunakan **APA Styles** (American Psychological Association, edisi ke-7). Menggunakan sistem pengacuan *innote* berkurung (contoh: `(Budi, 2021)` atau `Budi (2021)`) atau *footnote*.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Pengutipan dalam teks dan Daftar Pustaka.
- **Implementasi LaTeX:** Paket `natbib` dengan `\bibliographystyle{apalike}` atau `biblatex` dengan `style=apa`. Pemanggilan sitasi dalam teks menggunakan `\citep{...}` (kurung) dan `\citet{...}` (naratif). DILARANG menggunakan gaya angka numerik `[1]`, `[2]` (IEEE) kecuali secara eksplisit ada izin khusus program studi.
- **Validasi:** Parser BibTeX dan file `.bbl` memverifikasi tidak adanya nomor kurung siku `[1]` pada hasil render naskah.
- **Risiko Pelanggaran:** Pelanggaran berat format sitasi Fasilkom UNEJ.

### [RULE-CIT-02] Penggunaan Reference Manager Resmi
- **Sumber:** Juknis Bab 4.1.7.g (hlm. 88).
- **Isi Ketentuan:** Pengelolaan referensi diwajibkan menggunakan aplikasi reference manager seperti Mendeley atau Zotero yang diekspor ke basis data bibliografi (`.bib`).
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Basis data bibliografi proyek skripsi.
- **Implementasi LaTeX:** Penggunaan berkas `daftar_pustaka.bib` yang valid dan bersih.
- **Validasi:** Sintaks `.bib` divalidasi dengan `bibtex` atau validator parser.
- **Risiko Pelanggaran:** Referensi tidak konsisten atau entri metadata rusak.

### [RULE-CIT-03] Jumlah Minimal Pustaka ($\ge$ 15 Pustaka)
- **Sumber:** Juknis Bab 5.1.8 (hlm. 92).
- **Isi Ketentuan:** Daftar pustaka wajib memuat **minimal 15 pustaka** yang relevan dengan topik skripsi.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Berkas `daftar_pustaka.bib`.
- **Implementasi LaTeX:** Script audit menghitung jumlah total kunci `@article`, `@book`, `@inproceedings` yang disitasi dalam naskah.
- **Validasi:** Penghitungan jumlah referensi aktif: $\text{count}(\text{citations}) \ge 15$.
- **Risiko Pelanggaran:** Pengurangan nilai kriteria seminar proposal (bobot 2) dan ujian skripsi.

### [RULE-CIT-04] Kewajiban Minimal 3 Referensi Utama Bereputasi
- **Sumber:** Juknis Bab 2.2.3.1 Butir 5 (hlm. 75), Bab 2.2.3.2 Butir 8 (hlm. 77), Bab 5.1 Butir 8 (hlm. 92).
- **Isi Ketentuan:** Minimal 3 (tiga) referensi utama wajib merujuk pada penelitian terdahulu yang terkait langsung dan dipublikasikan pada:
  1. Jurnal Internasional Terindeks Bereputasi (Scopus / WoS Q1-Q3), dan/atau
  2. Jurnal Nasional Terakreditasi SINTA 1 atau SINTA 2.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Bab 2 Tinjauan Pustaka (Penelitian Terdahulu) dan Daftar Pustaka.
- **Implementasi LaTeX:** Menandai atau menyertakan metadata jurnal bereputasi pada entri `.bib` dan tabel perbandingan penelitian terdahulu di Bab 2.
- **Validasi:** Verifikasi manual/terbantu script terhadap indeks publikasi 3 referensi inti.
- **Risiko Pelanggaran:** Proposal tidak memenuhi aspek kecukupan pustaka Fasilkom.

### [RULE-CIT-05] Kemutakhiran Pustaka (Minimal 50% 10 Tahun Terakhir)
- **Sumber:** Juknis Bab 2.2.3.1 (hlm. 75), Bab 2.2.3.2 (hlm. 77), Bab 4.1.7.g (hlm. 88), Bab 5.1 (hlm. 92).
- **Isi Ketentuan:** Minimal 50% dari total pustaka merupakan artikel ilmiah yang dipublikasikan pada jurnal dan/atau prosiding dalam rentang waktu **10 tahun terakhir** sejak tahun pengerjaan skripsi.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Daftar Pustaka.
- **Implementasi LaTeX:** Pengecekan field `year` pada seluruh entri `@article` dan `@inproceedings` di `daftar_pustaka.bib`.
- **Validasi:** $\frac{\sum \text{publikasi}_{\text{year} \ge (\text{tahun\_skripsi} - 10)}}{\text{total\_pustaka}} \ge 0.50$.
- **Risiko Pelanggaran:** Penurunan skor evaluasi kecukupan pustaka.

### [RULE-CIT-06] Format Kutipan Langsung Lebih Dari 4 Baris
- **Sumber:** Juknis Bab 4.3.1.1.a (hlm. 89).
- **Isi Ketentuan:** Kutipan langsung yang panjangnya melebihi 4 baris teks wajib:
  1. Ditulis tanpa tanda kutip (`"`).
  2. Diletakkan terpisah dari teks narasi (blok tersendiri).
  3. Dibuat menjorok ke dalam (indent) baik dari margin kiri maupun margin kanan.
  4. Diketik dengan jarak baris spasi tunggal (1 spasi).
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Kutipan langsung panjang.
- **Implementasi LaTeX:**
  ```latex
  \begin{quote}
  \begin{spacing}{1}
  Teks kutipan panjang yang menjorok dari kiri dan kanan... (Nama, 2023, hlm. 45).
  \end{spacing}
  \end{quote}
  ```
- **Validasi:** Linting TeX memeriksa penggunaan environment `quote` dengan spacing tunggal untuk teks kutipan panjang.
- **Risiko Pelanggaran:** Pelanggaran teknik pengutipan langsung akademik.

### [RULE-CIT-07] Format Kutipan Langsung Maksimal 4 Baris
- **Sumber:** Juknis Bab 4.3.1.1.b (hlm. 89).
- **Isi Ketentuan:** Kutipan langsung yang tidak lebih dari 4 baris ditulis terpadu menyatu di dalam kalimat naskah dengan diapit tanda kutip (`"..."`) dan mencantumkan sumber pengarang dan tahun di awal atau akhir kalimat.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Kutipan langsung pendek.
- **Implementasi LaTeX:** Penulisan `"teks kutipan"` atau `\textquotedblleft teks\textquotedblright` menyatu dalam paragraf normal.
- **Validasi:** Memastikan teks bertanda kutip pendek tidak dipisah menjadi blockquote.
- **Risiko Pelanggaran:** Redaksi janggal pada paragraf narasi.

### [RULE-CIT-08] Tata Letak dan Spasi Entri Daftar Pustaka
- **Sumber:** Juknis Bab 4.1.7.g (hlm. 88).
- **Isi Ketentuan:** Setiap entri pustaka diketik dengan spasi tunggal (1 spasi), sedangkan jarak antar entri pustaka berjarak 2 spasi (atau berselang 1 baris kosong). Daftar pustaka diurutkan secara alfabetis berdasarkan nama belakang pengarang utama; jika terdapat beberapa karya dari pengarang yang sama, diurutkan secara kronologis berdasarkan tahun penerbitan.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Halaman Daftar Pustaka.
- **Implementasi LaTeX:** Pengaturan parameter `\setlength{\bibsep}{6pt}` atau `\setlength{\bibsep}{\baselineskip}` pada paket `natbib`.
- **Validasi:** Pemeriksaan visual/spasi pada file PDF yang dihasilkan.
- **Risiko Pelanggaran:** Format daftar pustaka terlalu rapat atau tidak beraturan.

### [RULE-CIT-09] Penandaan Kesalahan Teks Asli dan Elipsis
- **Sumber:** Juknis Bab 4.3.1.1.c (hlm. 89–90).
- **Isi Ketentuan:** Jika pada teks asli yang dikutip terdapat kesalahan cetak/tata bahasa, penulis dilarang mengubah teks asli tetapi wajib menambahkan tanda `[sic!]` tepat setelah kata yang salah. Jika ada bagian kalimat asli yang sengaja dihilangkan karena kurang relevan, wajib ditandai dengan tanda elipsis (`...`).
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Kutipan langsung.
- **Implementasi LaTeX:** Penggunaan teks `[sic!]` dan `\dots` pada kutipan langsung.
- **Validasi:** Review kualitatif pengutipan naskah.
- **Risiko Pelanggaran:** Pengubahan teks asli tanpa hak integritas sumber.

---

## 8. Kategori LAN: Kaidah Kebahasaan dan Penulisan Ilmiah

### [RULE-LAN-01] Penerapan EYD Edisi V
- **Sumber:** Juknis Bab 4.1.1 (hlm. 85).
- **Isi Ketentuan:** Naskah skripsi wajib ditulis dengan Bahasa Indonesia yang baik, benar, formal, dan berpedoman pada **Ejaan Bahasa Indonesia yang Disempurnakan (EYD) Versi 5**. Menghindari kata-kata ragam lisan, prokem, atau tidak baku.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Seluruh teks narasi skripsi.
- **Implementasi LaTeX:** Pemeriksaan ejaan (spelling & grammar check), penghindaran kata ganti orang pertama informal (seperti "saya", "kami", "penulis" secara berlebihan diganti bentuk pasif formal).
- **Validasi:** Linting teks bahasa Indonesia berbasis kamus baku KBBI/EYD.
- **Risiko Pelanggaran:** Catatan revisi tata bahasa dari dosen penguji.

### [RULE-LAN-02] Penulisan Istilah dan Bahasa Asing (*Italic*)
- **Sumber:** Juknis Bab 4.1.3 (hlm. 85).
- **Isi Ketentuan:** Seluruh istilah atau kata dalam bahasa asing (bukan bahasa Indonesia) yang belum diserap ke dalam KBBI WAJIB ditulis dengan cetak miring (*italic*). Contoh: *\textit{machine learning}*, *\textit{framework}*, *\textit{outlier}*, *\textit{preprocessing}*.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Seluruh teks naskah.
- **Implementasi LaTeX:** Penggunaan perintah `\textit{...}` untuk setiap kata serapan asing teknis.
- **Validasi:** Script regex memeriksa kata-kata bahasa Inggris umum di bidang informatika yang tidak berada di dalam blok `\textit{}`.
- **Risiko Pelanggaran:** Teguran penulisan istilah tidak baku pada lembar revisi ujian.

---

## 9. Kategori KEC: Aspek Kecukupan dan Kedalaman Substansi Ilmiah

### [RULE-KEC-01] Aspek Keunikan Skripsi (Larangan Perulangan Mutlak)
- **Sumber:** Juknis Bab 2 (hlm. 73).
- **Isi Ketentuan:** Skripsi tidak dituntut menemukan kebaruan (*novelty*) mutlak setara tesis/disertasi, namun TIDAK BOLEH merupakan perulangan mutlak (*absolute duplication*) dari penelitian terdahulu. Skripsi wajib memenuhi minimal SATU dari 3 indikator keunikan:
  1. Metode penelitian berbeda dengan penelitian sebelumnya.
  2. Obyek penelitian berbeda dengan penelitian sebelumnya.
  3. Mekanisme pengujian berbeda dengan penelitian sebelumnya.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** Bab 1 Latar Belakang dan Bab 2 Penelitian Terdahulu.
- **Implementasi LaTeX:** Penyajian tabel komparasi penelitian terdahulu di Bab 2 yang secara eksplisit memetakan pembeda pada kolom: Peneliti/Tahun, Metode, Objek, Mekanisme Uji, dan Posisi/Kontribusi Skripsi.
- **Validasi:** Review substansi pada Bab 1.1 dan Bab 2.1.
- **Risiko Pelanggaran:** Penolakan proposal oleh Komisi Bimbingan karena plagiasi ide atau duplikasi riset.

### [RULE-KEC-02] Aspek Kecukupan Bab 1 (Pendahuluan)
- **Sumber:** Juknis Tabel 2.34 & 2.35 (hlm. 74–76), Bab 3.2.2.1 (hlm. 81).
- **Isi Ketentuan:**
  - *Latar Belakang:* Memuat isu/masalah nyata dari literatur atau fakta lapangan, alasan urgensi, bukan sekadar opini.
  - *Rumusan Masalah:* Berupa kalimat tanya (*research question*) yang padat, terukur, dan relevan ilmu komputer.
  - *Batasan Masalah:* Membatasi ruang lingkup (objek, dataset, fitur, lingkungan sistem).
  - *Tujuan:* Kalimat pernyataan yang menjawab rumusan masalah.
  - *Manfaat:* Faedah teoretis dan praktis.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** `chapters/01-introduction.tex`.
- **Implementasi LaTeX:** Subbab terstruktur sesuai sistematika resmi.
- **Validasi:** Kelengkapan 5 subbab utama Bab 1.
- **Risiko Pelanggaran:** Proposal dinilai tidak fokus atau tidak layak uji.

### [RULE-KEC-03] Aspek Kecukupan Bab 2 (Tinjauan Pustaka)
- **Sumber:** Juknis Tabel 2.34 & 2.35 (hlm. 74–76), Bab 3.2.2.2 (hlm. 81–82).
- **Isi Ketentuan:**
  - *Penelitian Terdahulu:* Menguraikan riset relevan dari jurnal bereputasi dan memetakan diferensiasi skripsi.
  - *Landasan Teori:* Menjabarkan konsep, proposisi, algoritma, rumus matematis yang menjadi dasar penentu kesahihan riset, bukan sekadar tutorial software.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** `chapters/02-literature.tex`.
- **Implementasi LaTeX:** Penjabaran matematis algoritma (misal rumus BIRCH, IndoBERTweet, metrik evaluasi).
- **Validasi:** Keberadaan sitasi jurnal rujukan pada setiap landasan teori.
- **Risiko Pelanggaran:** Skripsi dinilai lemah secara landasan saintifik.

### [RULE-KEC-04] Aspek Kecukupan Bab 3 (Metodologi Penelitian)
- **Sumber:** Juknis Tabel 2.34 & 2.35 (hlm. 75–76), Bab 3.2.2.3 (hlm. 82).
- **Isi Ketentuan:**
  - Tahapan penelitian sistematis disertai diagram alir penelitian (*flowchart*).
  - Metode, teknik, dan luaran yang dihasilkan pada SETIAP tahapan.
  - Deskripsi data lengkap (tipe, jumlah, sumber, cara akuisisi, waktu pengambilan data).
  - Alat, instrumen, dan metode analisis yang digunakan.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** `chapters/03-methodology.tex`.
- **Implementasi LaTeX:** Flowchart tahapan via Gambar, tabel spesifikasi data dan instrumen.
- **Validasi:** Verifikasi keberadaan flowchart metodologi dan uraian tahapan.
- **Risiko Pelanggaran:** Riset tidak dapat direplikasi (*not reproducible*).

### [RULE-KEC-05] Aspek Kecukupan Bab 4 (Hasil dan Pembahasan)
- **Sumber:** Juknis Tabel 2.35 (hlm. 77), Bab 3.2.2.4 (hlm. 82–83).
- **Isi Ketentuan:**
  - Menyajikan data terolah (bukan data mentah/raw dumps), dalam bentuk uraian tekstual dan visual (tabel, grafik, visualisasi).
  - Pembahasan wajib dilakukan secara **analisis kritis (*critical analysis*)** menjawab apa (*what*), mengapa (*why*), dan bagaimana (*how*) hasil diperoleh.
  - Hasil wajib dihubungkan kembali dengan literatur teori di Bab 2 dan menjawab rumusan masalah di Bab 1.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** `chapters/04-results.tex`.
- **Implementasi LaTeX:** Tabel evaluasi komparatif, visualisasi grafik, dan paragraf analisis mendalam.
- **Validasi:** Pemeriksaan keterkaitan pembahasan dengan hipotesis/rumusan masalah.
- **Risiko Pelanggaran:** Skripsi dinilai seperti laporan praktikum tanpa telaah ilmiah.

### [RULE-KEC-06] Aspek Kecukupan Bab 5 (Kesimpulan dan Saran)
- **Sumber:** Juknis Tabel 2.35 (hlm. 77), Bab 3.2.2.5 (hlm. 83).
- **Isi Ketentuan:**
  - Kesimpulan dan Saran WAJIB dinyatakan terpisah dalam dua subbab berbeda.
  - *Kesimpulan:* Berisi ringkasan padat jawaban tuntas atas rumusan masalah berdasarkan fakta hasil penelitian (bukan mengulang teori).
  - *Saran:* Berisi rekomendasi aplikatif dan usulan arah penelitian lanjutan berbasis keterbatasan riset.
- **Status:** WAJIB (Mandatory).
- **Ruang Lingkup:** `chapters/05-conclusion.tex`.
- **Implementasi LaTeX:** Pemisahan tegas `\section{Kesimpulan}` dan `\section{Saran}`.
- **Validasi:** Memastikan tidak ada penggabungan judul menjadi satu subbab "Kesimpulan dan Saran".
- **Risiko Pelanggaran:** Kesimpulan tidak menjawab pertanyaan penelitian.

---
*Dokumen ini diperbarui secara berkala dan diverifikasi terhadap teks resmi Juknis Fasilkom UNEJ Versi 2.0 (2023).*
