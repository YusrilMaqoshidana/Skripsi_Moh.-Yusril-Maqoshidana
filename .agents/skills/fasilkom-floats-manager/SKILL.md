---
name: fasilkom-floats-manager
description: >-
  Use this skill when creating, formatting, placing, or validating tables, figures,
  equations, and algorithms in Fasilkom UNEJ LaTeX theses, ensuring open-table formatting,
  proper caption placement, and strict in-text cross-referencing.
---

# Fasilkom Tables, Figures, Equations & Algorithms Skill

Skill ini mengatur tata cara teknis penyusunan dan penempatan elemen apung (*floats*) sesuai **Juknis Skripsi Fasilkom UNEJ Versi 2.0 (2023)**.

## 1. Ringkasan Aturan Float

| Elemen | Posisi Caption | Ukuran Font | Format & Tanda Baca | Garis Pemisah | Rule ID |
|---|---|---|---|---|---|
| **Tabel** | Di **ATAS** tabel | 11pt (`\small`) | *Sentence case*, tanpa titik akhir | Tabel Terbuka (`booktabs`), **tanpa garis vertikal** | `RULE-FLT-01, 04, 05` |
| **Gambar** | Di **BAWAH** gambar | 11pt (`\small`) | *Sentence case*, tanpa titik akhir, sumber `(...)` | Proporsional, terpusat | `RULE-FLT-01, 07` |
| **Persamaan** | Di kanan `(Bab.No)` | 12pt (matematis) | Dinomori berurutan per bab | Terpusat horizontal | `RULE-FLT-03` |
| **Lampiran** | Sesuai jenis lampiran | 12pt / 11pt | Nomor 2 digit: `Bab.Urutan` (mis. Lampiran 3.1) | N/A | `RULE-FLT-08` |

## 2. Aturan Mutlak Rujukan Silang (*Cross-referencing*) (`RULE-FLT-02`)

1. Setiap tabel dan gambar **WAJIB dirujuk secara eksplisit** dalam narasi sebelum float muncul di halaman dokumen.
2. Penulisan rujukan wajib menggunakan huruf kapital di awal (*Title Case*):
   - Benar: `...sebagaimana disajikan pada Tabel~\ref{tab:evaluasi_model}.`
   - Benar: `Berdasarkan arsitektur pada Gambar~\ref{fig:arsitektur_sistem}, komponen...`
   - Salah: `...dapat dilihat pada tabel 4.1` atau `...gambar di bawah ini:`
3. **Larangan Posisi Mendahului:** Halaman yang memuat tabel atau gambar **tidak boleh mendahului** halaman kalimat rujukan pertamanya.

## 3. Template Standar Penulisan Tabel (Format Tabel Terbuka)

Gunakan paket `booktabs` dan hindari tanda garis vertikal (`|`):

```latex
\begin{table}[htbp]
    \centering
    \caption{Perbandingan performa model usulan terhadap baseline pada dataset WhatsApp}
    \label{tab:perbandingan_performa}
    \vspace{6pt} % Jarak 6pt ke garis atas tabel (RULE-FLT-04)
    \begin{tabular}{l c c c c}
        \toprule
        \textbf{Model Evaluasi} & \textbf{C-NPMI} & \textbf{Topic Diversity} & \textbf{Outlier Rate (\%)} & \textbf{Density} \\
        \midrule
        BERTopic Standar (HDBSCAN) & 0,0662 & 0,9120 & 42,42\% & 0,5611 \\
        BERTopic + IndoBERTweet    & 0,1124 & 0,9350 & 41,18\% & 0,6012 \\
        Usulan (BIRCH + BM25)      & \textbf{0,1567} & \textbf{0,9559} & \textbf{8,79\%}  & \textbf{0,6666} \\
        \bottomrule
    \end{tabular}
    \vspace{2pt}
    \par\raggedright\small
    (Sumber: Hasil olah data eksperimen, 2026) % Keterangan/sumber di bawah tabel (RULE-FLT-06)
\end{table}
```

*Catatan Isian Sel Tabel (`RULE-FLT-05`):*
- Angka disusun rata tengah atau sejajar desimal.
- Frasa teks rata kiri berhuruf kecil tanpa titik.
- Kalimat teks rata kiri berhuruf besar di awal (*sentence case*).
- Jika data padat, gunakan font `\small` (11pt) atau `\footnotesize` (10pt).

## 4. Template Standar Penulisan Gambar

```latex
\begin{figure}[htbp]
    \centering
    \includegraphics[width=0.85\textwidth]{images/arsitektur_sistem.png}
    \vspace{4pt}
    \caption{Diagram arsitektur sistem analisis topik berbasis web (Sumber: Modifikasi dari Arsitektur Client-Server, 2026)}
    \label{fig:arsitektur_sistem}
\end{figure}
```

*Catatan:*
- Jika gambar adalah **kreasi asli penulis sendiri**, tidak perlu mencantumkan keterangan `(Sumber: ...)`.
- Keterangan/penjelasan tambahan dapat ditulis sebelum judul gambar.

## 5. Template Persamaan Matematika

Persamaan matematika ditulis menggunakan environment `equation` dan berposisi tengah:

```latex
\begin{equation}
    \text{C-NPMI}(W) = \sum_{j=2}^N \sum_{i=1}^{j-1} \frac{\ln \frac{P(w_i, w_j) + \epsilon}{P(w_i)P(w_j)}}{-\ln (P(w_i, w_j) + \epsilon)}
    \label{eq:cnpmi}
\end{equation}
```
Rujuk dalam teks menggunakan `Persamaan~\eqref{eq:cnpmi}`.

## 6. Contoh Pelanggaran & Solusinya

### Pelanggaran 1: Menggunakan garis vertikal pada tabel
- **Salah:** `\begin{tabular}{|l|c|c|}` dengan `\hline \hline`
- **Solusi:** Hapus seluruh `|` dan ganti `\hline` dengan `\toprule`, `\midrule`, `\bottomrule` dari paket `booktabs`.

### Pelanggaran 2: Judul tabel ditaruh di bawah tabel
- **Salah:** `\caption{...}` diletakkan setelah `\end{tabular}`
- **Solusi:** Pindahkan `\caption{...}` ke atas sebelum `\begin{tabular}` (`RULE-FLT-04`).

### Pelanggaran 3: Menggunakan kata referensi relatif "gambar di bawah"
- **Salah:** "Alur data dapat dilihat pada bagan di bawah ini:"
- **Solusi:** Beri label `\label{fig:alur}` dan tulis: "Alur data disajikan pada Gambar~\ref{fig:alur}."

## 7. Prosedur Relokasi Float ke Lampiran (Pengendalian Kuota 40 Halaman)

Untuk membantu menjaga batas maksimal 20 halaman pada Bab 4 (dan 40 halaman total bagian utama sesuai `RULE-PAG-08`):

1. **Prinsip Utama:**
   - **JANGAN PERNAH MENGUBAH ATAU MENGHAPUS TEKS EKSISTING.** Teks narasi analisis, angka-angka metrik, dan pembahasan saintifik wajib dipertahankan utuh di bab utama.
   - Pemindahan tabel atau gambar ke Lampiran **HANYA DILAKUKAN SETELAH MENDAPAT PERSETUJUAN EKSPLISIT PENGGUNA**.
2. **Kandidat Relokasi:**
   - Tabel mentah hasil pengujian fungsional black-box puluhan skenario.
   - Tabel konfigurasi hiperparameter yang sangat panjang ($> 1$ halaman).
   - Diagram atau screenshot tambahan yang bersifat pelengkap non-inti.
3. **Mekanisme Pelaksanaan:**
   - Ajukan usulan kepada pengguna: sebutkan nomor tabel/gambar dan estimasi penghematan halaman.
   - Setelah pengguna menyetujui, pindahkan environment `table`/`figure` ke `backmatter/02-appendices.tex` dengan format penomoran Lampiran (`RULE-FLT-08`).
   - Perbarui rujukan dalam bab utama (misal: *"Data pengujian lengkap disajikan pada Lampiran~\ref{app:blackbox}"*).
