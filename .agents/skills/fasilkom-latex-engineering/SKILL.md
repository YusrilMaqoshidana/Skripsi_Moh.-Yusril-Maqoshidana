---
name: fasilkom-latex-engineering
description: >-
  Use this skill when designing, configuring, or refactoring the LaTeX architecture,
  preamble, package configuration, margins, page styles, typography, or custom macros
  for Fasilkom UNEJ thesis documents.
---

# Fasilkom LaTeX Engineering Skill

Skill ini memandu konfigurasi teknis tingkat kode LaTeX agar sesuai dengan **Juknis Skripsi Fasilkom UNEJ Versi 2.0 (2023)**.

## 1. Spesifikasi Teknis Wajib

| Parameter | Ketentuan Juknis | Kode LaTeX Standar | Rule ID |
|---|---|---|---|
| Document Class | Report, 12pt, A4, single-side | `\documentclass[12pt, a4paper, oneside]{report}` | `RULE-PAG-01` |
| Batas Margin | Atas 4cm, Kiri 4cm, Bawah 3cm, Kanan 3cm | `\usepackage[top=4cm, left=4cm, bottom=3cm, right=3cm]{geometry}` | `RULE-PAG-02` |
| Jenis Font | Times New Roman (12pt isi) | `\usepackage{times}` (atau `\usepackage{newtxtext,newtxmath}`) | `RULE-PAG-03` |
| Jarak Baris | 1,5 spasi (isi dokumen) | `\usepackage{setspace}\setstretch{1.5}` | `RULE-PAG-04` |
| Judul Bab | 14pt, Bold, ALL CAPS, Centered | `\titleformat{\chapter}[block]{\bfseries\fontsize{14pt}{16pt}\selectfont\centering}{...}` | `RULE-SEC-01` |
| Subbab & Anak Bab | Bold, 12pt, maksimal 3 digit | `\setcounter{secnumdepth}{3}\setcounter{tocdepth}{2}` | `RULE-SEC-02..04` |

## 2. Konfigurasi Penomoran Halaman (`RULE-PAG-05..07`)

Aturan tata letak penomoran halaman UNEJ memiliki tiga kondisi unik:
1. **Bagian Awal (Frontmatter):** Angka Romawi kecil (`i, ii, iii`) di TENGAH BAWAH.
2. **Bagian Utama (Main Body):** Angka Arab (`1, 2, 3`) di KANAN ATAS.
3. **Halaman Pertama Bab:** Angka Arab di TENGAH BAWAH (tanpa header).

### Implementasi `fancyhdr` (`config/page-style.tex`)
```latex
% Halaman pembuka bab & frontmatter: nomor di tengah bawah
\fancypagestyle{plain}{%
    \fancyhf{}%
    \fancyfoot[C]{\thepage}%
    \renewcommand{\headrulewidth}{0pt}%
    \renewcommand{\footrulewidth}{0pt}%
}

% Halaman reguler bagian utama: nomor di kanan atas
\fancypagestyle{fancy}{%
    \fancyhf{}%
    \fancyhead[R]{\thepage}%
    \fancyfoot{}%
    \renewcommand{\headrulewidth}{0pt}%
    \renewcommand{\footrulewidth}{0pt}%
}
```

### Pemanggilan di `main.tex`
```latex
% --- Bagian Awal ---
\pagenumbering{roman}
\pagestyle{plain}
\input{frontmatter/01-dedication.tex}
...

% --- Bagian Utama ---
\pagenumbering{arabic}
\setcounter{page}{1}
\pagestyle{fancy}
\input{chapters/01-introduction.tex}
```

## 3. Konfigurasi Hierarki Judul Bab & Subbab (`config/formatting.tex`)

```latex
% Format Bab: BAB 1 PENDAHULUAN (Bold, 14pt, ALL CAPS, Tengah)
\titleformat{\chapter}[block]
  {\bfseries\fontsize{14pt}{16pt}\selectfont\centering}
  {\MakeUppercase{\chaptertitlename} \thechapter.\hspace{0.5em}}
  {0pt}
  {\MakeUppercase}
\titlespacing*{\chapter}{0pt}{-20pt}{40pt}

% Format Subbab (Section): 1.1 Latar Belakang (Bold, 12pt, Rata Kiri)
\titleformat{\section}
  {\bfseries\normalsize}
  {\thesection}
  {0.5em}
  {}

% Format Sub-subbab (Subsection): 1.1.1 Identifikasi Masalah
\titleformat{\subsection}
  {\bfseries\normalsize}
  {\thesubsection}
  {0.5em}
  {}

% Format Sub-sub-subbab (Tingkat 4): a. Tahapan Preprocessing (Maks 3 Digit Terlampaui)
\renewcommand{\thesubsubsection}{\alph{subsubsection}.}
\titleformat{\subsubsection}[block]
  {\normalfont\normalsize}
  {\hspace*{0.5cm}\thesubsubsection}
  {0.5em}
  {}
```

## 4. Contoh Pelanggaran & Cara Memperbaikinya

### Pelanggaran 1: Menggunakan 4 digit angka (`1.1.1.1`)
- **Salah:** `\subsubsection{1.1.2.1 Parameter Optimasi}` (`RULE-SEC-04`)
- **Benar:** Gunakan huruf kecil berurutan `a. Parameter Optimasi` menggunakan `\subsubsubsection{Parameter Optimasi}` atau `\begin{enumerate}[label=\alph*.]`.

### Pelanggaran 2: Logo cover berukuran 4cm
- **Salah:** `\includegraphics[width=4cm]{images/logo.png}`
- **Benar:** `\includegraphics[width=5cm]{images/logo_unej.png}` (`RULE-STR-02`, diameter 5.0 cm).

### Pelanggaran 3: Menggunakan angka Romawi untuk Bab
- **Salah:** `\chapter{BAB I PENDAHULUAN}`
- **Benar:** `\chapter{PENDAHULUAN}` dengan konfigurasi `\MakeUppercase{\chaptertitlename} \thechapter.` menghasilkan otomatis `BAB 1 PENDAHULUAN`.

### Pelanggaran 4: Urutan hierarki institusi cover tidak sesuai Juknis
- **Salah:** Menempatkan nama program studi sebelum fakultas atau universitas.
- **Benar:** Kementerian $\rightarrow$ Universitas Jember $\rightarrow$ Fakultas Ilmu Komputer $\rightarrow$ Program Studi $\rightarrow$ Jember $\rightarrow$ Tahun (`RULE-STR-04`).

## 5. Validasi Teknis
- Jalankan pemeriksaan file log TeX: pastikan tidak ada `Overfull \hbox` parah ($>15$pt).
- Periksa ukuran output PDF dengan `pdfinfo main.pdf`: ukuran harus `595.276 x 841.89 pts (A4)`.
- Pastikan tidak mendefinisikan ulang perintah inti LaTeX tanpa `\renewcommand` atau alasan arsitektur yang valid.
