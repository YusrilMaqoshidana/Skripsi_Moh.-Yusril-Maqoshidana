# Refactoring Dokumentasi: Skripsi FASILKOM UNEJ (Modular & Clean Architecture)

## 📋 Ringkasan Refactoring

Template LaTeX skripsi FASILKOM UNEJ telah di-refactor menjadi **arsitektur modular yang clean, reuseable, dan mudah dipelihara**. Perubahan utama:

✅ **Sebelum**: Semua kode dalam satu file `main.tex` yang sangat panjang (~350 baris)  
✅ **Sesudah**: File-file terpisah yang terorganisir dengan jelas, total lintas lebih bersih & fokus

---

## 📁 Struktur Folder Baru

```
.
├── main.tex                      ← File UTAMA (entry point yang CLEAN)
├── metadata.tex                  ← Edit untuk mengubah: judul, nama, pembimbing, dll
│
├── config/                       ← KONFIGURASI GLOBAL
│   ├── packages.tex              ← Semua \usepackage (encoding, bahasa, font, dll)
│   ├── hyperref-config.tex       ← PDF metadata & hyperlink settings
│   ├── formatting.tex            ← Format chapter/section/subsection (styling)
│   ├── page-style.tex            ← Header/footer & penomoran halaman
│   └── custom-commands.tex       ← Custom LaTeX commands & environments
│
├── frontmatter/                  ← BAGIAN AWAL (Front Matter)
│   ├── 00-cover.tex              ← Halaman sampul
│   ├── 01-dedication.tex         ← Halaman persembahan
│   ├── 02-motto.tex              ← Halaman motto
│   ├── 03-originality.tex        ← Pernyataan orisinalitas (bermaterai Rp10K)
│   ├── 04-approval.tex           ← Halaman persetujuan & pengesahan
│   ├── 05-abstract-id.tex        ← Abstrak Indonesia (200-300 kata)
│   ├── 06-abstract-en.tex        ← Abstract Inggris (200-300 kata)
│   ├── 07-summary.tex            ← Ringkasan (1-2 halaman)
│   ├── 08-preface.tex            ← Prakata/ucapan terima kasih
│   └── 09-toc.tex                ← Daftar Isi, Tabel, Gambar (otomatis)
│
├── chapters/                     ← BAB-BAB UTAMA (Main Body)
│   ├── 01-introduction.tex       ← BAB 1: Pendahuluan
│   ├── 02-literature.tex         ← BAB 2: Tinjauan Pustaka
│   ├── 03-methodology.tex        ← BAB 3: Metodologi Penelitian
│   ├── 04-results.tex            ← BAB 4: Hasil & Pembahasan
│   └── 05-conclusion.tex         ← BAB 5: Kesimpulan & Saran
│
├── backmatter/                   ← BAGIAN AKHIR (Back Matter)
│   ├── 01-references.tex         ← Daftar Pustaka (Bibliography)
│   └── 02-appendices.tex         ← Lampiran (Data, Instrumen, Output, Kode)
│
├── README.md                     ← Dokumentasi proyek (file ini)
└── main_backup_original.tex      ← Backup file main.tex original (untuk referensi)
```

---

## 🚀 QUICK START - Cara Mulai

### 1. Edit Metadata Dokumen
Buka file **`metadata.tex`** dan ubah informasi berikut:

```latex
% Contoh perubahan di metadata.tex
\newcommand{\authorName}{Nama Lengkap Mahasiswa}
\newcommand{\studentID}{202X1XXXXXXXXX}
\newcommand{\titleLine}{JUDUL SKRIPSI SESUAI TOPIK ANDA}
\newcommand{\titleLineTwo}{BAGIAN KEDUA JUDUL JIKA ADA}
\newcommand{\advisorOne}{Dr. Nama Pembimbing I, S.Kom., M.Kom}
\newcommand{\advisorTwo}{Dr. Nama Pembimbing II, S.Kom., M.Kom}
```

### 2. Compile & Generate PDF
Gunakan salah satu metode:

#### **Metode A: Command Line (Recommended)**
```bash
# Compile otomatis (2-3 kali agar TOC akurat)
latexmk -pdf main.tex

# Atau manual:
pdflatex main.tex
pdflatex main.tex
pdflatex main.tex
```

#### **Metode B: VS Code + LaTeX Workshop Extension**
1. Install extension: **James Yu - "LaTeX Workshop"**
2. Buka `main.tex` → Tekan `Ctrl+Alt+B` (atau klik "Build LaTeX project")
3. PDF auto-generate di folder `build/` atau output

### 3. Edit Isi Setiap Bab
File setiap bab sudah berisi **template dengan dokumentasi lengkap**:

- **BAB 1**: Edit `chapters/01-introduction.tex`
- **BAB 2**: Edit `chapters/02-literature.tex`
- **BAB 3**: Edit `chapters/03-methodology.tex`
- **BAB 4**: Edit `chapters/04-results.tex`
- **BAB 5**: Edit `chapters/05-conclusion.tex`

Setiap file sudah memiliki **struktur & placeholder** yang jelas.

---

## 📝 Keunggulan Arsitektur Modular

### ✅ **1. CLEAN & MUDAH DIBACA**
- File utama (`main.tex`) hanya **50 baris** (sebelumnya 350+ baris)
- Struktur logis & mudah dipahami
- Navigasi antar file sangat mudah

### ✅ **2. REUSEABLE & MAINTAINABLE**
- Semua konfigurasi di satu tempat (`config/` folder)
- Perubahan global hanya perlu edit di satu file
- Template dapat digunakan kembali di proyek LaTeX lain

### ✅ **3. KOLABORASI MUDAH**
- Banyak co-authors bisa edit bab berbeda tanpa konflik
- Git merge lebih smooth (file kecil)
- Clear ownership: siapa edit bab apa

### ✅ **4. DOKUMENTASI LENGKAP**
- Setiap file memiliki komentar dokumentasi
- Panduan pengisian dalam setiap file
- Tips & best practices terintegrasi

### ✅ **5. DRY PRINCIPLE (Don't Repeat Yourself)**
- Custom commands di `config/custom-commands.tex`
- Konsistensi formatting dijamin
- Perubahan styling di satu tempat berlaku ke seluruh dokumen

---

## 🎯 Fitur-Fitur Penting

### **A. Custom Commands (untuk efisiensi & konsistensi)**

```latex
% Di config/custom-commands.tex sudah ada:

\frontmatterchapter{JUDUL}          ← Replace \chapter*{}
\keywords{Kata 1, Kata 2, Kata 3}   ← Formatting kata kunci konsisten
\quoteline{Quote}{Author}           ← Quote indah & centered
\signatureBlock{Nama}{Tgl}{Jabatan} ← Blok tanda tangan
```

### **B. Automatic Table of Contents**
```latex
% Daftar Isi, Tabel, Gambar auto-generate dari:
\chapter{...}              ← Chapter
\section{...}              ← Section
\caption{...}              ← Captions dalam figures/tables
```

### **C. Flexible Bibliography**

**Opsi 1: Manual Bibliography** (di `backmatter/01-references.tex`):
```latex
\documentclass[...]{report}
\usepackage{natbib}
% Ganti untuk menggunakan BibTeX
```

**Opsi 2: BibTeX + Mendeley** (RECOMMENDED):
1. Create `references.bib` file
2. Uncomment di `backmatter/01-references.tex`:
```latex
\bibliographystyle{apalike}
\bibliography{references}
```
3. Compile: `pdflatex → bibtex → pdflatex → pdflatex`

---

## 📚 Dokumentasi File-by-File

### **`metadata.tex`** - WAJIB EDIT
Berisi semua variable yang dapat diubah di satu tempat:
- Nama mahasiswa, NIM
- Judul skripsi (title line 1 & 2)
- Pembimbing I & II
- Penguji I & II
- Kata kunci
- Tanggal ujian

✅ **Keuntungan**: Perubahan metadata berlaku otomatis ke seluruh dokumen (cover, approval, abstract, dll)

### **`config/packages.tex`** - Semua Paket
Terdokumentasi dengan baik:
- Encoding & bahasa (utf8, T1, Indonesian)
- Font & layout (times, geometry, setspace)
- Visual customization (titlesec, fancyhdr, caption)
- Content packages (graphicx, booktabs, amsmath, hyperref, natbib)

### **`config/formatting.tex`** - Format Styling
Mengatur:
- Chapter: Centered, Bold, ALL CAPS, 14pt (sesuai juknis)
- Section/Subsection: Bold, Normal size, Bernomor
- Spacing sebelum/sesudah heading

### **`config/page-style.tex`** - Header/Footer & Page Numbering
Mengatur penomoran halaman sesuai juknis:
- Front Matter: Romawi kecil (i, ii, iii) di tengah bawah
- Main Body: Angka Arab (1, 2, 3) di kanan atas
- Halaman pertama bab: Nomor di tengah bawah

### **`config/custom-commands.tex`** - Utility Commands
Custom LaTeX macros untuk konsistensi:
- `\frontmatterchapter{...}` - Chapter tanpa nomor dengan auto-TOC
- `\keywords{...}` / `\keywordsen{...}` - Formatting keywords
- `\quoteline{...}{...}` - Quote centered dengan attribution
- `\signatureBlock{...}{...}{...}` - Template tanda tangan

---

## 💡 Tips Penggunaan

### **1. Jangan Edit `main.tex`**
File utama hanya untuk structure. Semua content di file-file terpisah.

### **2. Gunakan Label & Reference**
```latex
% Di bab Anda:
\section{Judul Section}
\label{sec:intro-background}

% Reference dari tempat lain:
Seperti terlihat pada Section \ref{sec:intro-background}...
```

✅ **Benefit**: Cross-reference otomatis & robust (no hardcoding page numbers)

### **3. Gunakan Citations yang Benar**
```latex
\citet{Author2020}   % = Author (2020) ... [author-in-text]
\citep{Author2020}   % = (Author, 2020) [parenthetical]
```

Perlu `references.bib` file.

### **4. Compile Berkala**
Jangan tunggu selesai semua untuk compile pertama kali.  
Compile saat ada perubahan besar untuk deteksi error awal.

### **5. Gunakan Comment untuk Testing**
```latex
% Comment out section saat testing BAB 4
% \input{chapters/04-results.tex}

% Atau gunakan \iffalse ... \fi untuk block
\iffalse
  \input{chapters/04-results.tex}
\fi
```

---

## 🔧 Troubleshooting

| Error | Solusi |
|-------|--------|
| `Undefined control sequence` | Pastikan semua `\usepackage` di `config/packages.tex` |
| `File not found` | Cek path di `\input{...}` relatif terhadap `main.tex` |
| `TOC not updating` | Compile 2-3 kali, LaTeX butuh multiple pass |
| `Overfull hbox` | Biasanya warning minor, abaikan jika text fit OK |
| Bibliography not showing | Pastikan `references.bib` ada & compile 2x sesudah `bibtex` |

---

## 📖 Referensi Format Juknis UNEJ

### **Spesifikasi Teknis**
| Aspek | Ketentuan |
|-------|-----------|
| Kertas | A4 (21 × 29,7 cm) |
| Margin | Top 4cm, Left 4cm, Bottom 3cm, Right 3cm |
| Font | Times New Roman, 12 pt (body), 14 pt (chapter title) |
| Spasi | 1.5 line spacing |
| Penomoran | Romawi (front matter) / Arab (main body) |

### **Struktur Dokumen (Juknis v2.0)**
1. **Front Matter** (Romawi): Sampul, Persembahan, Motto, Orisinalitas, Persetujuan, Abstrak, Ringkasan, Prakata, TOC
2. **Main Body** (Arab): BAB 1-5
3. **Back Matter**: Daftar Pustaka, Lampiran

---

## 🎓 Catatan Khusus untuk Mahasiswa UNEJ

### **Checklist Sebelum Pengumpulan:**

- [ ] Edit `metadata.tex` dengan data pribadi yang benar
- [ ] Isi kesemua bab (1-5) dengan konten penelitian Anda
- [ ] Abstrak Indo & English (200-300 kata) sudah diisi
- [ ] Ringkasan (1-2 halaman) sudah dibuat
- [ ] Daftar Pustaka minimal 50% dari 10 tahun terakhir
- [ ] Semua gambar/tabel sudah proper labeled & captioned
- [ ] Cross-references (labels) sudah benar
- [ ] Compile 3x terakhir kalinya untuk ensure TOC accurate
- [ ] PDF di-generate dan di-check (no errors/warnings serius)
- [ ] Halaman orisinalitas sudah **bermaterai Rp10.000** (print & bermaterai)
- [ ] Semua tanda tangan (pembimbing, penguji) **asli tinta biru** (bukan scan)

---

## 📞 Support & Kontribusi

- **Questions?** Konsultasi dengan pembimbing akademik Anda
- **LaTeX Help?** Tanya di komunitas: [TeX StackExchange](https://tex.stackexchange.com)
- **Improvements?** Ubah template sesuai kebutuhan Anda
- **Feedback?** Re-use template ini untuk smart management & maintainability

---

## 📄 lisensi & Disclaimer

Template ini dibuat untuk memudahkan mahasiswa FASILKOM UNEJ dalam menyusun skripsi sesuai juknis. Gunakan dengan bebas, modifikasi sesuai kebutuhan, dan bagikan dengan sesama mahasiswa.

**Last Updated**: Mei 2026  
**Juknis Version**: 2.0 (2023)  
**Keputusan Rektor**: UNEJ No. 5157/UN25/EP/2023

---

## 🙏 Terima Kasih

Terimakasih telah menggunakan template LaTeX yang telah di-refactor ini.  
Semoga memudahkan proses penulisan skripsi Anda!

**Good luck with your thesis!** 🎓✨
