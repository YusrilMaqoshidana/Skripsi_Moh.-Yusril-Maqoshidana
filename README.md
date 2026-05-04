# Skripsi_Moh.-Yusril-Maqoshidana

Template LaTeX Skripsi Fakultas Ilmu Komputer (Fasilkom) Universitas Jember (UNEJ) sesuai **Buku Petunjuk Teknis Skripsi Versi 2.0 (2023)** dan Keputusan Rektor UNEJ Nomor 5157/UN25/EP/2023.

---

## Spesifikasi Teknis

| Parameter | Ketentuan |
|---|---|
| Kertas | A4 (21 × 29,7 cm) |
| Margin Atas | 4 cm |
| Margin Kiri | 4 cm |
| Margin Bawah | 3 cm |
| Margin Kanan | 3 cm |
| Jenis Huruf | Times New Roman |
| Ukuran Huruf Isi | 12 pt |
| Ukuran Huruf Judul Bab | 14 pt (Bold, Kapital) |
| Jarak Antar Baris | 1,5 spasi |

### Penomoran Halaman

- **Bagian Awal (Front Matter):** Angka Romawi kecil (i, ii, iii, …) di tengah bawah
- **Bagian Inti (Main Body):** Angka Arab (1, 2, 3, …) di kanan atas, kecuali halaman pertama setiap bab di tengah bawah

---

## Struktur Dokumen

### Bagian Awal (Front Matter)
1. Halaman Sampul & Halaman Judul
2. Halaman Persembahan
3. Halaman Motto
4. Pernyataan Orisinalitas (bermaterai Rp10.000)
5. Halaman Persetujuan (tanda tangan pembimbing & penguji)
6. Abstrak (Indonesia) & Abstract (Inggris) — 200–300 kata
7. Ringkasan (Summary)
8. Prakata
9. Daftar Isi, Daftar Tabel, Daftar Gambar

### Bagian Inti (Main Body)
| Bab | Judul | Konten |
|---|---|---|
| BAB 1 | PENDAHULUAN | Latar belakang, rumusan masalah, batasan, tujuan, manfaat |
| BAB 2 | TINJAUAN PUSTAKA | Penelitian terdahulu, landasan teori |
| BAB 3 | METODOLOGI PENELITIAN | Lokasi, data, prosedur, metode analisis |
| BAB 4 | HASIL DAN PEMBAHASAN | Data terolah, analisis kritis |
| BAB 5 | KESIMPULAN DAN SARAN | Jawaban rumusan masalah, rekomendasi |

### Bagian Akhir (Back Matter)
- Daftar Pustaka (APA Style, ≥ 50% dari 10 tahun terakhir)
- Lampiran

---

## Cara Menggunakan Template

### Prasyarat
Pastikan distribusi LaTeX sudah terinstal. Direkomendasikan:
- **TeX Live** (Linux/Windows) atau **MacTeX** (macOS)
- Atau gunakan editor online [Overleaf](https://www.overleaf.com)

Paket LaTeX yang diperlukan:
- `inputenc`, `fontenc`, `babel` (indonesian)
- `times`, `geometry`, `setspace`
- `titlesec`, `fancyhdr`, `caption`
- `graphicx`, `booktabs`, `amsmath`
- `hyperref`, `natbib`, `lipsum`

### Kompilasi

```bash
pdflatex main.tex
pdflatex main.tex   # Jalankan dua kali untuk referensi silang
```

### Langkah Kustomisasi

1. **Ganti judul skripsi** pada blok `\begin{titlepage}` di `main.tex`
2. **Isi nama dan NIM** mahasiswa pada bagian yang sama
3. **Masukkan logo UNEJ** dengan menghapus tanda komentar pada baris:
   ```latex
   % \includegraphics[width=5cm]{logo_unej.png}
   ```
   dan tempatkan file `logo_unej.png` di direktori yang sama
4. **Ganti teks placeholder** (`\lipsum[...]`) dengan konten nyata
5. **Kata kunci** diisi pada bagian Abstrak dan Abstract
6. **Referensi** dikelola menggunakan Mendeley atau Zotero dengan gaya sitasi APA

---

## Ketentuan Penting Juknis Versi 2.0

- Judul skripsi harus berupa **frasa**, bukan kalimat, dan tidak diawali kata kerja
- Panjang judul disarankan **≤ 15 kata** (di luar kata sambung dan kata depan)
- Minimal **3 referensi utama** dari jurnal internasional bereputasi atau SINTA 1/2
- Minimal **50%** referensi dari jurnal/prosiding terbitan **10 tahun terakhir**
- Batas kemiripan plagiasi: **maksimal 30%**
- Pengajuan judul: IPK **≥ 2.00** dan telah menempuh **≥ 120 SKS**

---

## Referensi

- Buku Petunjuk Teknis Skripsi Fasilkom UNEJ Versi 2.0 (6 November 2023)
- Keputusan Rektor UNEJ Nomor 5157/UN25/EP/2023 tentang Pedoman Penulisan Tugas Akhir Mahasiswa
