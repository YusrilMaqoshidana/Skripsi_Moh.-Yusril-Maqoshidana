---
name: fasilkom-compliance-audit
description: >-
  Use this skill to perform a comprehensive compliance audit of a Fasilkom UNEJ LaTeX
  thesis project against the 41 official Juknis Rule IDs, generate an audit report,
  and identify layout or academic structure violations.
---

# Fasilkom Thesis Compliance Audit Skill

Skill ini mengatur prosedur audit kepatuhan formal naskah skripsi LaTeX terhadap seluruh ketentuan resmi dalam **Juknis Skripsi Fasilkom UNEJ Versi 2.0 (2023)** dan **Keputusan Rektor UNEJ Nomor 5157/UN25/EP/2023**.

## 1. Prosedur Audit Komprehensif

Audit kepatuhan dijalankan dalam 3 fase:

```
[FASE 1: STATIC & LINT AUDIT]     --> Analisis kode TeX & .bib via skrip otomatis
[FASE 2: BUILD & LOG AUDIT]       --> Pemeriksaan log kompilasi & referensi silang
[FASE 3: PDF ARTIFACT INSPECTION] --> Pemeriksaan visual, font, & batas halaman PDF
```

### Langkah Eksekusi Audit Cepat:
Jalankan skrip validator bawaan sistem:
```bash
python3 .agents/scripts/validate_thesis.py
```
Skrip akan memindai seluruh berkas proyek (`main.tex`, `metadata.tex`, `config/`, `frontmatter/`, `chapters/`, `backmatter/`, `daftar_pustaka.bib`) dan menerbitkan laporan temuan lengkap dengan Rule ID.

## 2. Rubrik Checklist Audit Berdasarkan Rule ID

### A. Struktur & Kelengkapan Berkas
- [ ] `RULE-STR-01`: Seluruh 15 berkas frontmatter terpanggil dalam urutan hierarki yang benar.
- [ ] `RULE-STR-02`: Logo UNEJ berukuran diameter 5.0 cm (`width=5cm`).
- [ ] `RULE-STR-04`: Urutan institusi cover: Kementerian $\rightarrow$ Universitas $\rightarrow$ Fakultas $\rightarrow$ Prodi $\rightarrow$ Jember $\rightarrow$ Tahun.
- [ ] `RULE-STR-05`: Panjang Abstrak ID dan EN berada dalam rentang **200 s.d. 300 kata**.
- [ ] `RULE-STR-07`: Berkas Ringkasan (Summary) ada dan panjangnya **1–2 halaman**.
- [ ] `RULE-STR-08`: Terdapat 5 Bab utama lengkap dengan subbab wajib.

### B. Format Tata Letak & Tipografi
- [ ] `RULE-PAG-01`: Ukuran kertas A4 portrait.
- [ ] `RULE-PAG-02`: Margin tepat 4cm (Atas), 4cm (Kiri), 3cm (Bawah), 3cm (Kanan).
- [ ] `RULE-PAG-03`: Font Times New Roman 12pt (isi) dan 14pt tebal (bab).
- [ ] `RULE-PAG-04`: Spasi antar baris 1,5 spasi (`\setstretch{1.5}`).
- [ ] `RULE-PAG-05..07`: Nomor halaman Romawi kecil tengah bawah (frontmatter), Arab kanan atas (main body), dan tengah bawah pada halaman awal setiap bab.
- [ ] `RULE-PAG-08`: Total halaman bagian utama $\le 40$ halaman (Bab 1: 4, Bab 2: 8, Bab 3: 4, Bab 4: 20, Bab 5: 1).

### C. Ilustrasi & Elemen Apung (Floats)
- [ ] `RULE-FLT-01`: Semua tabel dan gambar terpusat horizontal (`\centering`).
- [ ] `RULE-FLT-02`: Semua tabel dan gambar dirujuk eksplisit dalam teks (*Title Case*: "Tabel X.Y", "Gambar X.Y") sebelum posisi float.
- [ ] `RULE-FLT-04`: Judul tabel di ATAS, *sentence case*, 11pt, tanpa titik akhir.
- [ ] `RULE-FLT-05`: Tabel Terbuka (`booktabs`), **tanpa garis vertikal (`|`)**.
- [ ] `RULE-FLT-07`: Judul gambar di BAWAH, *sentence case*, 11pt, tanpa titik akhir.

### D. Sitasi & Bibliografi
- [ ] `RULE-CIT-01`: Gaya sitasi APA (edisi 7), tidak ada sitasi numerik IEEE `[1]`.
- [ ] `RULE-CIT-03`: Total entri pustaka aktif $\ge 15$ referensi.
- [ ] `RULE-CIT-04`: Minimal 3 referensi utama dari jurnal internasional bereputasi atau SINTA 1 & 2.
- [ ] `RULE-CIT-05`: Minimal 50% referensi diterbitkan dalam kurun waktu 10 tahun terakhir.

### E. Judul & Kebahasaan
- [ ] `RULE-TIT-01`: Judul berupa frasa nominal dan tidak diawali kata kerja.
- [ ] `RULE-TIT-02`: Panjang judul $\le 15$ kata di luar kata sambung/depan.
- [ ] `RULE-LAN-02`: Istilah bahasa asing ditulis cetak miring (`\textit{...}`).

## 3. Protokol Penanganan Batasan 40 Halaman & Pembahasan Ganda (`RULE-PAG-08`)

Mengingat batas maksimal 40 halaman bagian utama (Bab 1: 4, Bab 2: 8, Bab 3: 4, Bab 4: 20, Bab 5: 1) sangat menantang untuk riset komputasi mendalam, sistem skills menetapkan protokol ketat:

### A. Larangan Keras Modifikasi Teks Sepihak (Zero Text Mutation)
- **JANGAN PERNAH MENGUBAH ATAU MENGHAPUS TEKS EKSISTING SECARA OTOMATIS!**
- Agent dilarang memotong kalimat, menghapus alinea, atau memadatkan teks narasi mahasiswa secara sepihak dengan dalih mengejar target halaman.

### B. Mekanisme Warning dan Deteksi Pembahasan Ganda (Double Discussion Warning)
Agent hanya memberikan **WARNING** deskriptif dan saran penajaman pada:
1. **Teks yang Berpotensi Dipangkas/Dipindahkan:**
   - Paragraf yang mengulang penjelasan landasan teori Bab 2 secara verbatim di Bab 4 (Hasil dan Pembahasan).
   - Paragraf yang mengulang rincian langkah teknis Bab 3 secara verbatim di Bab 4.
   - Penjelasan latar belakang yang melebar keluar dari batasan masalah di Bab 1.
2. **Format Peringatan Pembahasan Ganda:**
   > **[WARNING - DOUBLE DISCUSSION DETECTED]**
   > *Lokasi:* `chapters/04-results.tex` paragraf ke-3 (baris X-Y).
   > *Temuan:* Paragraf ini membahas ulang konsep dasar IndoBERTweet yang telah diuraikan pada Bab 2 (`chapters/02-literature.tex`).
   > *Saran Redaksional:* Paragraf dapat dipersingkat menjadi rujukan silang: *"Sebagaimana diuraikan pada Bab 2, model IndoBERTweet digunakan untuk..."* tanpa mengulang definisi formalnya. *(Pilihan revisi diserahkan sepenuhnya kepada persetujuan pengguna).*

### C. Alur Relokasi Tabel & Gambar ke Lampiran (Dengan Persetujuan Eksplisit Pengguna)
Untuk merampingkan jumlah halaman tanpa mengorbankan kelengkapan data:
1. **Identifikasi Float Kandidat:**
   - Tabel hasil pengujian berdimensi besar ($> 15$ baris atau multi-halaman).
   - Tabel matriks skenario pengujian black-box fungsional.
   - Tangkapan layar antarmuka pengguna (UI screenshots) non-esensial.
2. **Permintaan Persetujuan Pengguna (User Confirmation):**
   Agent **WAJIB meminta persetujuan pengguna** sebelum memindahkan berkas atau kode float apa pun:
   > *"Tabel 4.5 (Pengujian Kasus Uji Black-Box) membutuhkan 3 halaman di Bab 4. Apakah Anda menyetujui pemindahan tabel ini ke `backmatter/02-appendices.tex` sebagai Lampiran 4.1 agar halaman Bab 4 tetap ringkas? Teks narasi di Bab 4 akan dipertahankan dengan rujukan ke Lampiran."*
3. **Eksekusi Pasca-Persetujuan:**
   - Pindahkan blok float ke Lampiran.
   - Pertahankan kalimat rujukan di bab utama dengan memperbarui label: *"Rincian pengujian disajikan pada Lampiran~\ref{app:blackbox}."*

## 4. Format Pelaporan Temuan Audit

Laporan audit yang dihasilkan wajib mengikuti format standar:

```markdown
# Laporan Hasil Audit Kepatuhan Skripsi Fasilkom UNEJ

## Ringkasan Eksekutif
- Total Aturan Diuji: 41
- Status Kepatuhan: [LOLOS / MEMERLUKAN PERBAIKAN]
- Total Pelanggaran (ERROR): <N>
- Total Peringatan (WARNING): <N>

## Rincian Temuan Pelanggaran
### [ERROR] RULE-FLT-05: Format Tabel Terbuka Dilanggar
- Lokasi: `tables/tabel_evaluasi.tex` baris 12
- Bukti: Ditemukan garis vertikal `\begin{tabular}{|l|c|r|}`
- Rekomendasi: Hapus karakter `|` dan gunakan paket `booktabs` (`\toprule`, `\midrule`, `\bottomrule`).

### [WARNING] RULE-PAG-08: Pembahasan Melebihi Kuota Halaman
- Lokasi: `chapters/04-results.tex` (24 halaman)
- Bukti: Kuota maksimal Bab 4 adalah 20 halaman.
- Rekomendasi: Tawarkan opsi relokasi tabel hasil mentah ke Lampiran dengan persetujuan pengguna (tanpa menghapus teks narasi).
```

## 5. Batasan & Tanggung Jawab Manusia
- Pemeriksaan keaslian Turnitin dan tanda tangan fisik bermaterai memerlukan verifikasi fisik oleh mahasiswa dan pembimbing (`RULE-ADM-04`, `RULE-ADM-05`).
- Agent tidak boleh membuat klaim kelulusan mutlak ("Skripsi dijamin 100% lulus") karena penilaian akhir berada di tangan Dewan Penguji.
