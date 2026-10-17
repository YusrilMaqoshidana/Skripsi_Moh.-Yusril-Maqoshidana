# Analysis Report: Official Thesis Guidelines Fasilkom UNEJ Versi 2.0 (2023)

Dokumen ini menyajikan hasil analisis mendalam terhadap dokumen resmi pedoman tugas akhir mahasiswa di lingkungan Fakultas Ilmu Komputer (Fasilkom), Universitas Jember (UNEJ) untuk pengembangan sistem skills agent AI berbasis LaTeX.

---

## 1. Metadata Dokumen Sumber dan Konfigurasi Lingkungan

- **Dokumen Sumber Utama:** `jurnal/Buku Juknis Skripsi Fasilkom Versi-2.0-2023.pdf` (109 Halaman, Ditetapkan 6 November 2023 oleh Dekan Fasilkom UNEJ Prof. Drs. Antonius Cahya Prihandoko, M.App.Sc., Ph.D.).
- **Dasar Hukum Pembina:** Keputusan Rektor Universitas Jember Nomor 5157/UN25/EP/2023 tentang Pedoman Penulisan Tugas Akhir Mahasiswa.
- **Referensi Pendukung:** Keputusan Dekan Fasilkom Nomor 3439/UN25.1.15/SP/2023 tentang Buku Profil Penelitian Dosen Fasilkom Tahun 2023–2024.
- **Target AI Agent:** Antigravity AI Agent System (Customization Specification 2.0).
- **Format Target:** Native LaTeX Thesis Ecosystem (Modular Report Class, Times Font, 1.5 Spacing, APA 7th Citation).
- **Compiler Target:** `pdflatex` + `bibtex` (didukung oleh `latexmk` v4.83, TeX Live 2024+ di lingkungan Linux x86_64).

---

## 2. Ruang Lingkup dan Karakteristik Dokumen

Dokumen Petunjuk Teknis Versi 2.0 ini menggantikan Petunjuk Teknis Versi 1.0 (4 April 2022) dan Keputusan Dekan Nomor 1842/UN25.1.15/SP/2022. Ruang lingkup naskah mencakup:

1. **Program Studi:**
   - S1 Program Studi Informatika.
   - S1 Program Studi Sistem Informasi.
   - S1 Program Studi Teknologi Informasi.
2. **6 Profil Bidang Minat Utama:**
   - Data Science & Business Intelligence.
   - Artificial Intelligence.
   - Multimedia & Computer Games.
   - Computer Network & Security.
   - Smart Information System.
   - Software Engineering.
3. **31 Topik Penelitian Spesifik:**
   - Mulai dari Data Mining, Text Mining, Computer Vision, NLP, Machine Learning, Robotics, UI/UX, Cloud Computing, hingga Software Testing dan Optimization in Software Engineering.
4. **Sistematika Lengkap:**
   - Format Proposal Skripsi (Bab 3.1) dan Laporan Skripsi Akhir (Bab 3.2).
   - Format Penulisan Tipografis dan Tata Letak (Bab 4).
   - Rubrik Evaluasi Seminar Proposal dan Ujian Skripsi (Bab 5).
   - Aturan Waktu, Prosedur Operasional Standar (POS), dan Alur Birokrasi SIAKAD/SITA ILKOM (Bab 6).

---

## 3. Temuan Kunci Analisis dan Ekstraksi Ketentuan

### 3.1. Ketentuan Tipografi dan Tata Letak Fisik (Layout)
- **Kertas dan Margin:** Kertas A4 (21,0 $\times$ 29,7 cm), margin Atas 4 cm, Kiri 4 cm, Bawah 3 cm, Kanan 3 cm.
- **Jenis Huruf dan Spasi:** Times New Roman 12pt untuk teks isi, dengan jarak baris 1,5 spasi. Judul Bab berukuran 14pt tebal (*bold*), huruf kapital (*ALL CAPS*), posisi tengah (*centered*).
- **Penomoran Halaman:**
  - Bagian awal (*frontmatter*): angka Romawi kecil (`i`, `ii`, `iii`, dst.) di tengah bawah.
  - Bagian inti (*main body*): angka Arab (`1`, `2`, `3`, dst.) di kanan atas.
  - Halaman awal setiap bab: nomor diletakkan di **tengah bawah**.
- **Hierarki Heading:**
  - Penomoran bab menggunakan angka Arab (contoh: `BAB 1`, `BAB 2`). Dilarang memakai angka Romawi seperti `BAB I`.
  - Subbab maksimal **3 digit angka** (`1.1`, `1.1.1`). Tidak boleh ada tanda titik setelah angka terakhir.
  - Tingkat keempat dan seterusnya wajib bertingkat: huruf kecil (`a.`), angka kurung tutup (`1)`), huruf kurung tutup (`a)`), dan angka kurung ganda (`(1)`). Dilarang membuat format 4 digit angka seperti `1.1.1.1`.

### 3.2. Ketentuan Ilustrasi (Tabel dan Gambar)
- **Posisi:** Wajib di tengah secara horizontal (*centered*), menempati paragraf tersendiri.
- **Rujukan Naskah:** Seluruh float wajib dirujuk secara eksplisit dalam teks narasi menggunakan *Title Case* (misal: "Tabel 2.3", "Gambar 3.1"). Halaman tempat tabel/gambar berada **tidak boleh mendahului** halaman kalimat rujukan pertamanya.
- **Caption Tabel:** Terletak di **ATAS** tabel, ukuran 11pt, format *sentence case*, tanpa titik akhir. Jarak ke garis atas tabel adalah 6pt.
- **Tabel Terbuka (*Open Table*):** Hanya menampilkan garis horizontal atas heading (`\toprule`), batas bawah heading (`\midrule`), dan penutup tabel (`\bottomrule`). Seluruh garis vertikal **dilarang ditampilkan** kecuali ada kebutuhan matriks khusus.
- **Caption Gambar:** Terletak di **BAWAH** gambar, ukuran 11pt, *sentence case*, tanpa titik akhir. Penjelasan sebelum judul, sumber setelah judul dalam tanda kurung `(...)`.

### 3.3. Ketentuan Sitasi dan Bibliografi
- **Gaya Sitasi:** Wajib **APA Styles** (7th edition). Sistem *innote* atau *footnote*. Dilarang menggunakan nomor numerik IEEE (`[1]`, `[2]`).
- **Ambang Batas Jumlah Pustaka:** Minimal **15 pustaka**.
- **Kualitas Reputasi Pustaka:** Minimal **3 referensi utama** berasal dari Jurnal Internasional Terindeks Bereputasi (Scopus/WoS Q1–Q3) atau Jurnal Nasional Terakreditasi SINTA 1 atau SINTA 2.
- **Kemutakhiran Pustaka:** Minimal **50% pustaka** diterbitkan dalam kurun waktu **10 tahun terakhir**.
- **Daftar Pustaka:** Spasi tunggal (1 spasi) di dalam setiap entri, berselang 2 spasi antarentri. Diurutkan menurut abjad nama belakang penulis dan urut tahun jika penulis sama.

### 3.4. Ketentuan Judul Skripsi
- Wajib berbentuk **frasa nominal**, bukan kalimat deklaratif, dan **tidak boleh diawali dengan kata kerja**.
- Disarankan tidak lebih dari **15 kata** (di luar kata sambung dan kata depan).
- Judul ditulis kapital penuh, tebal, 14pt, spasi 1, dan tidak diakhiri tanda titik.

### 3.5. Aspek Kecukupan dan Integritas Akademik
- **Etika & Plagiarisme:** Nilai kesamaan Turnitin maksimal 30% pada bagian utama dan maksimal 10% untuk satu sumber tunggal.
- **Keunikan Skripsi:** Bukan perulangan mutlak. Wajib memiliki pembeda minimal pada satu aspek: metode, objek penelitian, atau mekanisme pengujian.
- **Pemisahan Kesimpulan dan Saran:** Bab 5 memisahkan secara tegas antara kesimpulan (jawaban rumusan masalah) dan saran (rekomendasi terapan / penelitian lanjutan).

---

## 4. Gap Analysis & Identifikasi Ambiguitas

Berdasarkan inspeksi terhadap template LaTeX yang terdapat di repositori aktif (`/home/usereal/apps/completed/Skripsi_Moh.-Yusril-Maqoshidana`), ditemukan beberapa ketidaksesuaian (*gaps*) dan isu ambigu yang perlu ditangani:

### GAP 1: Ukuran Logo UNEJ pada Cover (RESOLVED & IMPLEMENTED)
- **Aturan Juknis:** Bab 3.2.1.1.a menetapkan logo berwarna UNEJ berdiameter presisi **5.0 cm** (`width=5cm`).
- **Implementasi Awal:** Berkas `frontmatter/00-cover.tex` sebelumnya berukuran `width=4cm`.
- **Status Resolusi:** Telah diperbarui menjadi `\includegraphics[width=5cm]{images/logo.png}` sesuai Juknis resmi, dan didukung penuh oleh skill `fasilkom-latex-engineering` serta validator otomatis.

### GAP 2: Urutan Hierarki Identitas Institusi pada Cover (RESOLVED & IMPLEMENTED)
- **Aturan Juknis:** Bab 3.2.1.1.f menetapkan urutan resmi: Kementerian $\rightarrow$ Universitas Jember $\rightarrow$ Fakultas Ilmu Komputer $\rightarrow$ Program Studi $\rightarrow$ Jember $\rightarrow$ Tahun.
- **Implementasi Awal:** Berkas cover menaruh Program Studi sebelum Fakultas dan Universitas.
- **Status Resolusi:** Telah diperbarui secara resmi di `frontmatter/00-cover.tex` dengan urutan Kementerian $\rightarrow$ `\university` $\rightarrow$ `\faculty` $\rightarrow$ `\studyProgram` $\rightarrow$ Jember $\rightarrow$ `\graduationYear`.

### GAP 3: Penanganan Batas Maksimal 40 Halaman & Pembahasan Ganda (IMPLEMENTED via Warning Policy)
- **Aturan Juknis:** Bab 4.2 Tabel 4.1 menetapkan batasan ketat: Pendahuluan (4 hlm), Tinjauan Pustaka (8 hlm), Metodologi (4 hlm), Hasil dan Pembahasan (20 hlm), Kesimpulan (1 hlm), Pustaka (3 hlm), total maksimal **40 halaman** untuk Bagian Utama.
- **Kondisi Nyata:** Skripsi informatika dan komputasi lanjut (seperti evaluasi BERTopic, IndoBERTweet, BIRCH pada puluhan ribu korpus data) membutuhkan ruang pelaporan empiris yang kaya. Memangkas teks secara sembarangan berisiko merusak substansi akademik.
- **Kebijakan Operasional Baku (Zero Text Mutation & User Consent):**
  1. **Larangan Mutasi Teks Sepihak:** Agent secara mutlak DILARANG mengubah atau menghapus teks naskah eksisting pengguna demi mengejar batas halaman.
  2. **Mekanisme Warning Informatif:** Agent hanya menerbitkan peringatan deskriptif (*Warning*) jika Bab melampaui alokasi kuota halaman.
  3. **Deteksi Pembahasan Ganda (*Double Discussion Detection*):** Agent menandai paragraf yang pembahasannya redundan (misal pembahasan teori di Bab 4 yang mengulang verbatim teori Bab 2, atau langkah teknis di Bab 4 yang mengulang Bab 3) serta menyarankan penajaman berbasis rujukan silang (`\ref{...}`).
  4. **Relokasi Float Terbimbing Persetujuan Pengguna:** Agent memfasilitasi pemindahan tabel data mentah masif, matriks pengujian black-box, atau tangkapan layar UI ke **Lampiran (Backmatter)** HANYA SETELAH memperoleh persetujuan eksplisit dari pengguna. Teks pembahasan di bab utama tetap dipertahankan dengan merujuk ke nomor Lampiran.

### GAP 4: Gaya Bibliografi APA 7th Edition pada BibTeX
- **Aturan Juknis:** Mewajibkan APA Style (edisi 7).
- **Implementasi Eksisting:** Menggunakan paket `natbib` dengan `\bibliographystyle{apalike}`.
- **Keputusan:** Format `apalike` pada `natbib` merupakan pendekatan standar TeX Live yang paling stabil untuk menghasilkan sitasi berkurung `(Author, Year)` dan daftar pustaka berformat nama-tahun tanpa menimbulkan konflik paket yang umum terjadi pada `biblatex-apa` (yang membutuhkan backend `biber`). Skill tetap mempertahankan kompatibilitas `natbib` + `apalike` sambil memvalidasi bahwa seluruh format entri mematuhi konvensi APA.

---

## 5. Keputusan Desain Rekayasa Sistem Skills (Architectural Decisions)

1. **Modularitas Berorientasi Tanggung Jawab:**
   Membagi kapabilitas menjadi 8 skills khusus:
   - `fasilkom-thesis-core`: Pengetahuan kanonis, prioritas aturan, ruang lingkup.
   - `fasilkom-latex-engineering`: Konfigurasi preamble, geometry, fonts, custom commands, layout.
   - `fasilkom-thesis-writing`: Kerangka penulisan Bab 1–5, frontmatter, aspek kecukupan proposal & skripsi.
   - `fasilkom-academic-id-writer`: Tata bahasa formal akademik, EYD V, frasa ilmiah, miring istilah asing.
   - `fasilkom-citation-bib`: Aturan APA 7, validasi minimal 15 pustaka, 3 jurnal bereputasi, 50% 10 tahun terakhir.
   - `fasilkom-floats-manager`: Format tabel terbuka (booktabs), judul di atas 11pt, judul gambar di bawah, rujukan silang wajib.
   - `fasilkom-compliance-audit`: Pemeriksaan menyeluruh kepatuhan format naskah terhadap Rule ID.
   - `fasilkom-latex-diagnostics`: Build workflow, deteksi error, warning, unresolved labels/cites.

2. **Pola Progressive Disclosure:**
   File `SKILL.md` utama pada setiap skill dibuat padat dan prosedural. Seluruh rincian tekstual Juknis yang panjang dipusatkan pada `.agents/references/CANONICAL_JUKNIS_RULES.md` dan direferensikan melalui tautan markdown lokal. Hal ini menghemat token context window agent sekaligus menjaga integritas informasi.

3. **Pemisahan Tegas Tata Letak vs Substansi Akademik:**
   AI dilarang keras mengubah angka hasil evaluasi, memalsukan sitasi, atau mengarang kontribusi ilmiah saat memformat naskah. AI bertindak sebagai auditor format dan editor kebahasaan yang menjaga keaslian substansi penelitian mahasiswa.

4. **Automated Tooling & Verification:**
   Menyediakan skrip Python eksekutabel `.agents/scripts/validate_thesis.py` yang dapat dijalankan di lingkungan terminal pengguna untuk memeriksa kepatuhan naskah secara objektif dan menghasilkan laporan berbasis Rule ID.
