---
name: fasilkom-latex-diagnostics
description: >-
  Use this skill to compile Fasilkom UNEJ LaTeX theses, parse compilation logs (.log and .blg),
  detect unresolved cross-references, missing citations, overfull boxes, syntax errors,
  and verify final PDF integrity.
---

# Fasilkom LaTeX Build & Diagnostics Skill

Skill ini memandu proses kompilasi dokumen skripsi, diagnosis kegagalan build, pembacaan berkas log, penanganan referensi silang yang belum terselesaikan, dan validasi integritas artefak PDF.

## 1. Toolchain Kompilasi Resmi

Berdasarkan template Fasilkom UNEJ dan dependensi paket (`natbib`, `hyperref`, `titlesec`, `fancyhdr`), alur kompilasi standar yang direkomendasikan adalah:

### Alur Standar `pdflatex` + `bibtex`:
```bash
pdflatex -interaction=nonstopmode main.tex
bibtex main
pdflatex -interaction=nonstopmode main.tex
pdflatex -interaction=nonstopmode main.tex
```

### Alternatif Otomatis via `latexmk`:
```bash
latexmk -pdf -interaction=nonstopmode main.tex
```

*Catatan:*
- Jangan menggunakan engine `xelatex` atau `lualatex` kecuali naskah secara khusus membutuhkan font sistem non-standar, karena template saat ini dioptimalkan untuk `pdflatex` + paket `times`.
- Selalu jalankan kompilasi minimal 3 lintasan (*passes*) agar seluruh label (`\label`), referensi (`\ref`, `\eqref`, `\cite`), Daftar Isi (`.toc`), Daftar Tabel (`.lot`), dan Daftar Gambar (`.lof`) tersinkronisasi sempurna.

## 2. Diagnosis Log Kompilasi Otomatis

Gunakan pola deteksi log berikut untuk mengidentifikasi akar masalah:

### A. Fatal Errors (`! Error`)
1. **`! Undefined control sequence`:**
   - *Penyebab:* Penggunaan perintah/makro LaTeX yang belum diimpor atau salah eja (typo).
   - *Solusi:* Periksa baris log terkait, pastikan paket terkait sudah diaktifkan di `config/packages.tex`.
2. **`! LaTeX Error: File 'xyz.sty' not found`:**
   - *Penyebab:* Paket TeX belum terinstal di sistem operasi.
   - *Solusi:* Pasang paket via package manager sistem (misal `tlmgr install xyz` atau package manager OS).
3. **`! Missing $ inserted` atau `! Display math should end with $$`:**
   - *Penyebab:* Karakter matematika khusus (seperti `_`, `^`, `%`, `&`, `#`) digunakan dalam teks biasa tanpa *escape* `\_` atau berada di luar lingkungan matematika `$ ... $`.
   - *Solusi:* Tambahkan tanda *escape* backslash `\` pada karakter spesial teks narasi.

### B. Referensi dan Sitasi Belum Terselesaikan
1. **`LaTeX Warning: Reference '...' on page X undefined`:**
   - *Penyebab:* Label rujukan silang belum terdefinisi atau naskah belum dikompilasi lintasan kedua.
   - *Solusi:* Cari apakah `\label{...}` ada di dokumen. Jika ada, jalankan ulang `pdflatex`. Jika tidak ada, buat label yang bersesuaian di tabel/gambar terkait.
2. **`LaTeX Warning: Citation '...' on page X undefined`:**
   - *Penyebab:* Kunci sitasi belum ada di `daftar_pustaka.bib`, atau proses `bibtex` belum dijalankan.
   - *Solusi:* Periksa file `main.blg`, pastikan entri BibTeX memiliki kunci yang tepat dan jalankan lintasan `bibtex main`.

### C. Overfull / Underfull Warnings
1. **`Overfull \hbox (... pt too wide) in paragraph at lines ...`:**
   - *Penyebab:* Kata panjang (misal istilah bahasa asing atau tautan URL panjang) tidak dapat dipenggal (*hyphenation*) sehingga melebar melebihi margin kanan 3cm.
   - *Solusi:*
     - Tambahkan titik pemenggalan lunak `\-` (misal `de\-pen\-den\-cy`).
     - Bungkus URL panjang dengan `\url{...}` atau aktifkan `\usepackage{xurl}`.
     - Bungkus paragraf dengan lingkungan `\begin{sloppypar} ... \end{sloppypar}` jika terjadi pada daftar referensi.

## 3. Verifikasi Artefak PDF Akhir

Setelah kompilasi selesai tanpa error fatal:
1. Periksa keberadaan berkas `main.pdf`.
2. Jalankan `pdfinfo main.pdf`:
   - Pastikan `Page size: 595.276 x 841.89 pts (A4)`.
   - Periksa total halaman (*Pages*).
3. Periksa file log untuk memastikan string berikut muncul di akhir:
   ```text
   Output written on main.pdf (... pages, ... bytes).
   ```
4. Pastikan tidak ada peringatan sisa:
   ```text
   LaTeX Warning: There were undefined references.
   ```

## 4. Perintah Cepat Pembersihan Cache (*Clean Build*)

Jika artefak build korup atau terjadi *incompatible auxiliary data*:
```bash
rm -f main.aux main.bbl main.blg main.log main.out main.toc main.lof main.lot main.fls main.fdb_latexmk
```
Lalu jalankan ulang seluruh siklus kompilasi dari awal.
