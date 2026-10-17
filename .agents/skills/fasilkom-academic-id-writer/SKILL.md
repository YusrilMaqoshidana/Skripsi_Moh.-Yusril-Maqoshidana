---
name: fasilkom-academic-id-writer
description: >-
  Use this skill when editing, proofreading, translating, or refining academic Indonesian
  prose in thesis documents to adhere to EYD V, academic objectivity, italicization of foreign terms,
  and formal scientific tone without altering factual research outcomes.
---

# Fasilkom Academic Indonesian Writing Skill

Skill ini mengatur tata cara penyuntingan kebahasaan akademik naskah skripsi dalam Bahasa Indonesia formal sesuai **Pedoman Umum Ejaan Bahasa Indonesia yang Disempurnakan (EYD Edisi V)** dan kaidah penulisan ilmiah **Juknis Skripsi Fasilkom UNEJ Versi 2.0 (2023)**.

## 1. Kaidah Utama Kebahasaan

### 1.1 Penulisan Kata dan Istilah Asing (`RULE-LAN-02`)
Seluruh istilah atau frasa bahasa asing (khususnya Bahasa Inggris) yang belum diserap secara baku ke dalam KBBI **WAJIB dicetak miring (*italic*)** menggunakan perintah `\textit{...}`.
- Contoh Istilah Komputasi:
  - `\textit{machine learning}`, `\textit{clustering}`, `\textit{deep learning}`
  - `\textit{framework}`, `\textit{baseline}`, `\textit{embedding}`
  - `\textit{outlier}`, `\textit{preprocessing}`, `\textit{traceability}`
  - `\textit{noise}`, `\textit{code-mixing}`, `\textit{real-time}`
- Istilah Asing yang Sudah Diserap Baku (TIDAK dicetak miring):
  - komputer, internet, data, server, algoritma, klaster, modifikasi, analisis, sistem, fungsi, variabel.

### 1.2 Struktur Kalimat dan Sudut Pandang Objektif
- **Hindari Kata Ganti Orang Pertama:** Dilarang menggunakan "saya", "kami", "kita", atau repetisi berlebihan "penulis".
  - *Tidak Baku:* "Pada penelitian ini, kami menggunakan model IndoBERTweet untuk menghasilkan vektor."
  - *Baku:* "Penelitian ini menerapkan model IndoBERTweet untuk menghasilkan representasi vektor dokumen."
- **Predikat Pasif Formal:** Utamakan konstruksi pasif objektif untuk mendeskripsikan eksperimen:
  - "Data diuji...", "Model dievaluasi...", "Tahapan praproses dilakukan...".
- **Penalaran Kritis (*Critical Tone*):**
  - Gunakan kata transisi ilmiah: *Oleh karena itu*, *Meskipun demikian*, *Di samping itu*, *Konsekuensinya*, *Secara komparatif*.

## 2. Tabel Glosarium Istilah Komputasi Sering Muncul

| Istilah Asing | Padanan Baku Indonesia (Opsional) | Format Penulisan LaTeX yang Dianjurkan |
|---|---|---|
| *Feature extraction* | Ekstraksi fitur | `ekstraksi fitur` atau `\textit{feature extraction}` |
| *Preprocessing* | Praproses | `praproses data` atau `\textit{preprocessing}` |
| *Outlier* | Pencilan / data menyimpang | `pencilan` atau `\textit{outlier}` |
| *Clustering* | Pengklasteran | `pengklasteran` atau `\textit{clustering}` |
| *Learning curve* | Kurva pembelajaran | `kurva pembelajaran` atau `\textit{learning curve}` |
| *Ground truth* | Data kebenaran acuan | `\textit{ground truth}` |
| *Hyperparameter* | Hiperparameter | `hiperparameter` |
| *Word embedding* | Penanaman kata / representasi vektor | `representasi vektor kata` atau `\textit{word embedding}` |

## 3. Contoh Refactoring Kalimat

### Contoh 1: Menghilangkan Kata Informal & Memperbaiki Istilah Asing
- **Sebelum (Canggung/Non-standar):**
  > Saya mencoba mengcluster chat whatsapp yang banyak noise dan bahasa gaulnya dengan bertopic tapi hasilnya jelek karena banyak data kebuang jadi outlier.
- **Sesudah (Akademik & EYD V):**
  > Penerapan algoritma pengklasteran pada data obrolan WhatsApp yang memiliki derau (*noise*) tinggi dan variasi bahasa informal menggunakan model BERTopic standar menghasilkan performa suboptimal, di mana sejumlah besar dokumen tereliminasi sebagai pencilan (*outlier*).

### Contoh 2: Menegakkan Kaidah Argumen Kritis di Bab 4
- **Sebelum:**
  > Tabel 4.1 menunjukkan skor kami lebih bagus dibanding baseline. Skor CNPMI naik dari 0.06 ke 0.15. Ini membuktikan model kami berhasil.
- **Sesudah:**
  > Berdasarkan data evaluasi yang disajikan pada Tabel 4.1, model yang diusulkan menunjukkan peningkatan performa yang signifikan dibandingkan model \textit{baseline}. Metrik \textit{Topic Coherence} (C-NPMI) mengalami kenaikan dari 0,0662 menjadi 0,1567. Kenaikan tersebut mengindikasikan bahwa integrasi IndoBERTweet dan representasi BM25 efektif dalam menangkap konteks semantik percakapan lokal secara lebih koheren.

## 4. Batasan Integritas Konten
- **Preservasi Makna:** Jangan mengubah angka metrik, persamaan matematis, variabel algoritma, atau nama fungsi kode saat menyunting kalimat.
- **Transparansi Ketidaklengkapan:** Jika mahasiswa belum menyediakan data empiris atau temuan tertentu, gunakan penanda komentar yang jelas (`% TODO: Lengkapi hasil pengujian`) dan jangan mengarang temuan fiktif.
