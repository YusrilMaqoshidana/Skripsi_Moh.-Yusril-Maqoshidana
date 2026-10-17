# Production-Ready LaTeX Skills System for Fasilkom UNEJ Thesis

Sistem Skills Agent AI berbasis LaTeX resmi untuk penyusunan, penyuntingan, kompilasi, dan audit kepatuhan skripsi di lingkungan Fakultas Ilmu Komputer (Fasilkom), Universitas Jember (UNEJ) berdasarkan **Buku Petunjuk Teknis Skripsi Versi 2.0 (2023)** dan **Keputusan Rektor UNEJ Nomor 5157/UN25/EP/2023**.

---

## 1. Ringkasan Sistem & Konfigurasi

- **Target Agent:** Antigravity AI Agent System (Google DeepMind Agentic Coding Framework)
- **Sumber Panduan Resmi:** `jurnal/Buku Juknis Skripsi Fasilkom Versi-2.0-2023.pdf`
- **Lokasi Skills:** `.agents/skills/`
- **Format Dokumen:** LaTeX (Modular Architecture)
- **Engine Kompilasi:** `pdflatex` + `bibtex` (atau `latexmk -pdf`)
- **Gaya Sitasi:** APA Styles (7th Edition) via `natbib` & `apalike`
- **Bahasa Naskah:** Bahasa Indonesia Baku (EYD Edisi V)

---

## 2. Struktur Direktori Deliverables

```text
.agents/
├── README.md                      # Panduan umum sistem skills & penggunaan
├── ANALYSIS_REPORT.md             # Laporan ekstraksi aturan, scope, & gap analysis
├── RULES_TRACEABILITY.md          # Matriks pelacakan 41 Rule ID resmi
├── SKILLS_ARCHITECTURE.md         # Diagram arsitektur modular & alur kerja agent
├── LIMITATIONS.md                 # Batasan teknis, non-automatable, & keputusan manusia
├── TEST_SUITE_REPORT.md           # Laporan hasil eksekusi 10 skenario pengujian
├── references/
│   └── CANONICAL_JUKNIS_RULES.md  # Single Source of Truth kodifikasi aturan Juknis
├── scripts/
│   └── validate_thesis.py         # Skrip audit otomatis naskah TeX & .bib
├── tests/
│   └── run_tests.py               # Test runner eksekutabel untuk TC-01 s.d. TC-10
└── skills/
    ├── fasilkom-thesis-core/        # Basis pengetahuan aturan, etika & topik riset
    ├── fasilkom-latex-engineering/  # Konfigurasi layout, geometry, margin, fonts
    ├── fasilkom-thesis-writing/     # Pemandu penulisan Bab 1-5 & frontmatter
    ├── fasilkom-academic-id-writer/ # Penegakan EYD V, formal tone, istilah asing miring
    ├── fasilkom-citation-bib/       # Aturan APA 7, 15+ pustaka, 50% 10 tahun terakhir
    ├── fasilkom-floats-manager/     # Tabel terbuka, gambar, persamaan & rujukan silang
    ├── fasilkom-compliance-audit/   # Rubrik audit naskah & deteksi pelanggaran
    └── fasilkom-latex-diagnostics/  # Alur kompilasi, log parser & resolusi error
```

---

## 3. Cara Aktivasi & Penggunaan Skills pada Antigravity

Antigravity secara otomatis memindai direktori `.agents/skills/` di root workspace proyek. Untuk menggunakan kapabilitas sistem:

### A. Penulisan Bab Baru
Minta agent untuk menyusun kerangka atau menulis subbab tertentu:
> *"Tuliskan kerangka subbab Bab 3 Metodologi Penelitian untuk penelitian klasifikasi topik WhatsApp sesuai Juknis Fasilkom."*
*(Agent otomatis mengaktifkan `fasilkom-thesis-writing` dan menerapkan `fasilkom-academic-id-writer`).*

### B. Pembuatan Tabel Sesuai Format Juknis
Minta agent untuk membuat tabel evaluasi eksperimen:
> *"Buatkan tabel komparasi hasil pengujian model dalam format tabel terbuka sesuai Juknis Fasilkom."*
*(Agent otomatis mengaktifkan `fasilkom-floats-manager` menggunakan paket `booktabs` tanpa garis vertikal).*

### C. Penambahan Sitasi & Pengelolaan Bibliografi
Minta agent untuk menambahkan entri pustaka baru:
> *"Tambahkan sitasi artikel BERTopic Grootendorst (2022) ke dalam daftar_pustaka.bib dan kutip di Bab 2."*
*(Agent otomatis mengaktifkan `fasilkom-citation-bib` dengan format `\citep` / `\citet`).*

---

## 4. Alat Validasi & Pengujian Otomatis

### A. Menjalankan Audit Kepatuhan Dokumen
Untuk memverifikasi kepatuhan seluruh naskah proyek skripsi saat ini:
```bash
python3 .agents/scripts/validate_thesis.py .
```
Output berupa ringkasan PASS/WARNING/FAIL dan laporan lengkap akan disimpan di `.agents/AUDIT_REPORT.md`.

### B. Menjalankan Test Suite (TC-01 s.d. TC-10)
Untuk menjalankan suite pengujian sistem skills di lingkungan sandbox terisolasi:
```bash
python3 .agents/tests/run_tests.py
```
Hasil pengujian akan tercatat pada `.agents/TEST_SUITE_REPORT.md`.

---

## 5. Indeks Dokumen Terkait

1. [ANALYSIS_REPORT.md](./ANALYSIS_REPORT.md) — Analisis detail Juknis 2.0 dan gap analysis.
2. [RULES_TRACEABILITY.md](./RULES_TRACEABILITY.md) — Matriks keterlacakan 41 Rule ID resmi.
3. [SKILLS_ARCHITECTURE.md](./SKILLS_ARCHITECTURE.md) — Arsitektur teknis dan dependency graph.
4. [LIMITATIONS.md](./LIMITATIONS.md) — Batasan otomatisasi dan keputusan subjektif manusia.
5. [TEST_SUITE_REPORT.md](./TEST_SUITE_REPORT.md) — Bukti verifikasi 10 kasus uji standar.
6. [CANONICAL_JUKNIS_RULES.md](./references/CANONICAL_JUKNIS_RULES.md) — Referensi kanonis seluruh aturan resmi.
