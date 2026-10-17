---
name: fasilkom-thesis-writing
description: >-
  Use this skill when drafting, outlining, or structuring thesis chapters (Bab 1 to 5),
  frontmatter (Cover, Abstract, Summary, Preface), backmatter, or validating academic
  completeness against official Fasilkom UNEJ guidelines.
---

# Fasilkom Thesis Structure & Chapter Writing Skill

Skill ini mengatur tata cara penyusunan kerangka dan penulisan naskah skripsi dari Bagian Awal (Frontmatter), Bagian Inti (Bab 1–5), hingga Bagian Akhir (Backmatter) sesuai **Juknis Skripsi Fasilkom UNEJ Versi 2.0 (2023)**.

## 1. Aturan Penulisan Judul Skripsi (`RULE-TIT-01..04`)

Saat menyusun atau merevisi judul skripsi:
1. **Frasa Nominal:** Wajib berbentuk frasa, bukan kalimat berpredikat lengkap.
2. **Larangan Kata Kerja:** DILARANG diawali kata kerja (misal: "Membangun...", "Menganalisis...", "Implementasi..." diperbolehkan jika berkedudukan nomina, namun lebih dianjurkan: "Sistem...", "Rancang Bangun...", "Klasifikasi...").
3. **Panjang Judul:** Sebaiknya $\le 15$ kata (di luar kata hubung dan depan).
4. **Format Tipografi:** Huruf KAPITAL, Bold, 14pt, 1 spasi, tanpa titik akhir.

Contoh Valid:
- `Sistem Analisis Topik Percakapan Komunitas Daring Menggunakan Modifikasi BERTopic` (11 kata non-stopwords — VALID)
Contoh Tidak Valid:
- `Menganalisis Performa Algoritma Machine Learning Pada Dataset Twitter.` (Diawali kata kerja dan diakhiri titik — TIDAK VALID).

## 2. Struktur Bagian Awal (Frontmatter)

Urutan halaman frontmatter wajib mematuhi `RULE-STR-01`:

1. `00-cover.tex`:
   - Logo UNEJ berwarna diameter 5.0 cm (`\includegraphics[width=5cm]{images/logo_unej.png}`).
   - Judul skripsi ALL CAPS 14pt tebal.
   - Maksud penelitian: *"Diajukan guna memenuhi sebagian persyaratan memperoleh gelar Sarjana Komputer pada Program Studi [Nama Prodi]"*.
   - Identitas institusi berurutan: KEMENTERIAN $\rightarrow$ UNIVERSITAS $\rightarrow$ FAKULTAS $\rightarrow$ PROGRAM STUDI $\rightarrow$ JEMBER $\rightarrow$ TAHUN.
2. `01-dedication.tex`: Persembahan dengan bahasa formal dan wajar.
3. `02-motto.tex`: Moto inspiratif dengan kutipan tokoh/sumber.
4. `03-originality.tex`: Pernyataan bermaterai Rp10.000 dengan tanda tangan fisik asli.
5. `04-approval.tex`: Lembar persetujuan Dosen Pembimbing dan Dosen Penguji.
6. `05-abstract-id.tex` & `06-abstract-en.tex`:
   - Panjang **200 sampai dengan 300 kata** (`RULE-STR-05`).
   - Memuat ikhtisar terpadu: permasalahan, tujuan, metode penelitian, hasil pengujian empiris, dan kesimpulan.
   - Kata kunci: 3–7 kata, istilah asing dicetak miring (`RULE-STR-06`).
7. `07-summary.tex`: Dokumen Ringkasan sepanjang **1–2 halaman** dengan narasi holistik yang komprehensif tanpa duplikasi verbatim dari abstrak (`RULE-STR-07`).
8. `08-preface.tex`: Prakata dan ucapan terima kasih kepada pimpinan fakultas, pembimbing, penguji, dan keluarga.
9. `09-toc.tex`: `\tableofcontents`, `\listoftables`, `\listoffigures`.

## 3. Struktur Bagian Inti (Main Body)

Sesuai `RULE-STR-08` dan Aspek Kecukupan Skripsi (Tabel 2.35 Juknis):

### BAB 1: PENDAHULUAN (`RULE-KEC-02`, Maksimal 4 Halaman)
- **1.1 Latar Belakang:** Fakta empiris lapangan atau telaah pustaka yang mendasari urgensi masalah; menunjukkan mengapa masalah penting dan kontribusi riset.
- **1.2 Rumusan Masalah:** Pertanyaan penelitian (*research questions*) yang padat, terarah, dan terukur.
- **1.3 Batasan Masalah:** Ruang lingkup batasan (karakteristik dataset, platform, batasan fungsional).
- **1.4 Tujuan Penelitian:** Kalimat pernyataan yang sejalan dengan rumusan masalah.
- **1.5 Manfaat Penelitian:** Faedah teoretis dan aplikatif.

### BAB 2: TINJAUAN PUSTAKA (`RULE-KEC-03`, Maksimal 8 Halaman)
- **2.1 Penelitian Terdahulu:**
  - Minimal 3 jurnal internasional bereputasi / Sinta 1-2 (`RULE-CIT-04`).
  - Sajikan tabel komparasi: Peneliti/Tahun, Metode, Objek, Hasil, dan Pembeda Skripsi (`RULE-KEC-01`).
- **2.2 Landasan Teori:** Konsep, algoritma, rumus matematis penentu kesahihan penelitian.

### BAB 3: METODOLOGI PENELITIAN (`RULE-KEC-04`, Maksimal 4 Halaman)
- **3.1 Waktu dan Lokasi Penelitian:** Tempat dan jadwal pelaksanaan riset.
- **3.2 Data Penelitian:** Identitas data (jenis, sumber, volume/jumlah data, teknik akuisisi, waktu pengambilan).
- **3.3 Prosedur Penelitian:** Tahapan sistematis disertai **Flowchart Penelitian**; jelaskan metode, teknik, dan luaran tiap tahap.
- **3.4 Alat dan Instrumen:** Perangkat keras, lingkungan perangkat lunak, pustaka pemrograman.
- **3.5 Metode Analisis:** Metrik evaluasi performa atau teknik evaluasi sistem.

### BAB 4: HASIL DAN PEMBAHASAN (`RULE-KEC-05`, Maksimal 20 Halaman)
- **Penyajian Data Terolah:** Sajikan data hasil pemodelan/eksperimen dalam bentuk tabel dan grafik (bukan data mentah/raw data dump).
- **Analisis Kritis (*Critical Analysis*):** Wajib mengupas aspek:
  - *What:* Apa pola atau hasil performa yang terjadi?
  - *Why:* Mengapa hasil tersebut dapat terjadi? Apa peran komponen/algoritma yang diusulkan?
  - *How:* Bagaimana perbandingannya dengan baseline atau literatur terkait di Bab 2?
- **Jawaban Masalah:** Pembahasan harus membuktikan jawaban atas rumusan masalah di Bab 1.

### BAB 5: KESIMPULAN DAN SARAN (`RULE-KEC-06`, Maksimal 1 Halaman)
- **5.1 Kesimpulan:** Rangkuman padat jawaban atas pertanyaan penelitian (bukan ringkasan bab).
- **5.2 Saran:** Rekomendasi aplikatif dan arah perbaikan untuk penelitian lanjutan. Dilarang menggabungkan judul menjadi "Kesimpulan dan Saran".

## 4. Bagian Akhir (Backmatter)
- `backmatter/01-references.tex`: Daftar Pustaka gaya APA 7 (`RULE-CIT-01`).
- `backmatter/02-appendices.tex`: Lampiran dikelompokkan menurut jenis dan bernomor sesuai bab rujukan (`RULE-FLT-08`).

## 5. Protokol Warning Batasan Halaman & Pencegahan Pembahasan Ganda

Sesuai `RULE-PAG-08` (kuota 40 halaman bagian utama):

1. **JANGAN PERNAH MENGUBAH TEKS EKSISTING SECARA SEPIHAK:**
   - Agent dilarang memotong atau menghapus paragraf naskah yang sudah ditulis pengguna.
2. **Warning Pembahasan Ganda (*Double Discussion Warning*):**
   - Jika ditemukan paragraf di Bab 4 yang mengulang penjelasan landasan teori yang sudah dibahas di Bab 2, berikan peringatan:
     > **[WARNING] Potensi Pembahasan Ganda:** Paragraf pada Bab 4 (baris X-Y) mengulang penjelasan teori dari Bab 2. Disarankan diganti dengan kalimat rujukan silang singkat (`\ref{...}`) agar halaman lebih hemat, dengan persetujuan Anda.
   - Jika ditemukan rincian prosedur praproses di Bab 4 yang mengulang teks Bab 3 secara verbatim, beri tanda warning serupa.
3. **Penyelamatan Halaman Melalui Relokasi Float Terbimbing:**
   - Tawarkan opsi memindahkan tabel matriks pengujian atau screenshot antarmuka ke Lampiran atas persetujuan pengguna. Teks narasi bab utama tetap dipertahankan dengan merujuk ke nomor Lampiran.

## 6. Protokol Verifikasi Pustaka Nyata (Anti-Asumsi Grounding)

Sesuai `RULE-CIT-09`, saat menyusun atau merevisi narasi bab:
1. **Bab 2 (Tinjauan Pustaka & Teori):**
   - Sebelum mengutip formulasi matematis, arsitektur sistem, atau temuan studi terdahulu, asisten wajib membaca berkas `jurnal/<file>.md` yang relevan (lihat katalog di `fasilkom-citation-bib`).
   - Dilarang membuat ringkasan generik jika berkas teks aslinya tersedia secara lokal.
2. **Bab 3 (Metodologi):**
   - Rumus, parameter default algoritma, atau batasan sistem harus merujuk pada definisi resmi di berkas `jurnal/*.md`.
3. **Bab 4 (Hasil dan Pembahasan):**
   - Saat membandingkan hasil empiris dengan literatur (misal: Muhajir et al., 2025 di `jurnal/muhammad_muhajir.md`), angka komparasi, metodologi, dan keterbatasan model pembanding harus diambil secara faktual dari dokumen acuan, bukan asumsi.

