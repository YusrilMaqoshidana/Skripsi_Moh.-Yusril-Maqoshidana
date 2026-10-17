# Limitations & Human Subjective Decisions: Fasilkom UNEJ LaTeX Thesis System

Dokumen ini mendokumentasikan batasan sistem, aspek yang tidak dapat diotomatisasi secara penuh, serta keputusan akademik yang wajib dikonfirmasi langsung oleh mahasiswa dan dosen pembimbing.

---

## 1. Aspek Administratif & Verifikasi Fisik (Non-Automatable)

1. **Keabsahan Lembar Pernyataan Orisinalitas bermaterai Rp10.000 (`RULE-ADM-04`):**
   - Skrip dan agent AI hanya dapat memvalidasi struktur kode LaTeX pada `frontmatter/03-originality.tex`.
   - Penempelan fisik materai tempel Rp10.000 (atau e-Meterai resmi Peruri) serta pembubuhan tanda tangan basah dengan tinta biru di atas materai **wajib dilakukan secara manual oleh mahasiswa** sebelum berkas diserahkan ke Bagian Akademik.
2. **Hasil Uji Plagiasi Resmi Turnitin (`RULE-ADM-05`):**
   - Sistem dapat memeriksa gaya bahasa dan parafrase naskah untuk menekan kesamaan leksikal, namun **tidak dapat menggantikan uji similarity pada akun Turnitin resmi Universitas Jember**.
   - Ambang batas toleransi (maksimal 30% total dan maksimal 10% per sumber) serta *expert judgement* pembimbing jika similarity melampaui batas memerlukan verifikasi lembar hasil cetak fisik Turnitin.
3. **Surat Tugas & Kalender Birokrasi (`RULE-ADM-01..03`):**
   - Penerbitan Surat Tugas Pembimbing, plotting pembahas di SITA ILKOM / SIAKAD, serta jadwal seminar proposal dan ujian skripsi dikelola sepenuhnya oleh Operator Akademik dan Komisi Bimbingan.

---

## 2. Penilaian Akademik Subjektif (Human Expert Judgment)

1. **Kedalaman Analisis Kritis Bab 4 (`RULE-KEC-05`):**
   - Sistem skills dapat memastikan keberadaan data terolah, tabel terbuka, dan struktur paragraf penjelasan (*What, Why, How*).
   - Namun, **kualitas saintifik argumentasi**, validitas logika inferensi, dan signifikansi temuan terhadap rumusan masalah merupakan domain murni penilaian Dosen Pembimbing dan Dewan Penguji saat ujian lisan.
2. **Aspek Keunikan Skripsi (`RULE-KEC-01`):**
   - Skrip dapat memverifikasi keberadaan tabel komparasi penelitian terdahulu di Bab 2.
   - Penilaian apakah perbedaan metode, objek penelitian, atau mekanisme pengujian memiliki bobot akademik yang memadai pada level sarjana (S1) diputuskan oleh Dosen Pembimbing melalui formulir persetujuan judul (Lampiran 1 & 6 Juknis).
3. **Komponen Penilaian Non-Naskah pada Ujian Skripsi:**
   - Tabel 5.2 dan 5.3 Juknis memuat kriteria seperti:
     * *Kemampuan presentasi dan penguasaan substansi penelitian* (Bobot 2–3).
     * *Kemampuan menjawab pertanyaan dewan penguji* (Bobot 2–3).
     * *Kesiapan produk sistem/perangkat lunak yang dihasilkan* (Bobot 1).
     * *Proses bimbingan dan etika mahasiswa* (Bobot 3).
   - Aspek-aspek di atas sepenuhnya berada di luar kendali dokumen LaTeX.

---

## 3. Keterbatasan Teknis Toolchain LaTeX

1. **Penegakan Kuota Maksimal 40 Halaman (`RULE-PAG-08`):**
   - Aturan 40 halaman pada bagian utama skripsi memang sangat sulit diterapkan secara kaku pada penelitian rekayasa komputasi dan pemodelan kecerdasan buatan tanpa memangkas kedalaman analisis ilmiah.
   - Kebijakan resmi sistem skills:
     * **Larangan Mutasi Teks:** Agent secara mutlak DILARANG memotong, menyingkat, atau menghapus teks naskah eksisting secara sepihak demi mengejar batas halaman.
     * **Mekanisme Warning Informatif:** Agent hanya menerbitkan peringatan deskriptif (*Warning*) jika bab melampaui kuota halaman.
     * **Deteksi Pembahasan Ganda (*Double Discussion*):** Agent memberikan peringatan jika terdapat paragraf yang pembahasannya redundan antar-bab (misal penjelasan teori di Bab 4 yang mengulang verbatim teori Bab 2, atau langkah teknis di Bab 4 yang mengulang Bab 3), serta menyarankan perampingan berbasis rujukan silang (`\ref{...}`) yang keputusannya diserahkan kepada pengguna.
     * **Relokasi Float Terbimbing Persetujuan Pengguna:** Agent memfasilitasi pemindahan tabel data masif, matriks pengujian black-box, atau tangkapan layar UI ke **Lampiran (Backmatter)** HANYA SETELAH memperoleh persetujuan eksplisit dari pengguna. Teks pembahasan di bab utama tetap dipertahankan dengan merujuk ke nomor Lampiran.
2. **Pemenggalan Kata Bahasa Indonesia (*Hyphenation*):**
   - Engine `pdflatex` menggunakan pola pemenggalan dari paket `babel[indonesian]`. Beberapa kata serapan asing atau gabungan kata teknis dapat memicu `Overfull \hbox` jika berada di akhir baris. Penanganan membutuhkan tanda pemenggalan lunak manual `\-` pada kata terkait.
3. **Pengelolaan Format APA 7th Edition pada BibTeX:**
   - Template repositori menggunakan kombinasi stabil `natbib` + `\bibliographystyle{apalike}`. Gaya ini mendekati standar APA, namun untuk kepatuhan ketat format sitasi APA 7th edisi terbaru yang mencakup metadata DOI lengkap dan et al. pada $\ge 3$ penulis, mahasiswa dianjurkan memeriksa ketepatan kompilasi berkas `.bbl` atau mempertimbangkan migrasi ke `biblatex-apa` jika diizinkan oleh dosen pembimbing.

---

## 4. Kebijakan Keselamatan & Integritas AI (Safety Policy)

- **Larangan Halusinasi Akademik:** Agent AI dilarang keras mengarang sitasi, menambahkan referensi fiktif yang tidak dapat diverifikasi, atau mengubah data angka hasil evaluasi empiris mahasiswa.
- **Ketiadaan Jaminan Kelulusan:** Sistem skills tidak boleh memberikan klaim kelulusan mutlak ("Dijamin lulus ujian skripsi dengan nilai A"). Semua keputusan kelulusan sepenuhnya merupakan wewenang sah Majelis Sidang Ujian Skripsi Fakultas Ilmu Komputer Universitas Jember.
