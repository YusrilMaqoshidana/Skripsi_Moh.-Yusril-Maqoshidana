---
name: fasilkom-citation-bib
description: >-
  Use this skill when managing BibTeX entries (.bib), formatting in-text citations (APA 7th edition),
  validating citation recency (50% 10-year rule), reputable journal thresholds (min 3 Scopus/SINTA 1-2),
  and auditing bibliography compliance for Fasilkom UNEJ theses.
---

# Fasilkom Citation & Bibliography Skill

Skill ini mengatur pengelolaan basis data referensi, teknik pengutipan dalam teks (*innote*), dan penyusunan Daftar Pustaka sesuai gaya **APA Styles (7th Edition)** dan **Juknis Skripsi Fasilkom UNEJ Versi 2.0 (2023)**.

## 1. Aturan Formal Sitasi dan Bibliografi

| Rule ID | Parameter | Ketentuan Resmi Juknis | Implementasi LaTeX |
|---|---|---|---|
| `RULE-CIT-01` | Gaya Sitasi | Wajib **APA Styles** (7th Edition) | `\bibliographystyle{apalike}` + `natbib` |
| `RULE-CIT-02` | Reference Manager | Dikelola via Zotero/Mendeley ke `.bib` | Berkas `daftar_pustaka.bib` |
| `RULE-CIT-03` | Batas Minimum Pustaka | Minimal **15 pustaka** | Validasi count kunci sitasi aktif $\ge 15$ |
| `RULE-CIT-04` | Referensi Utama | Minimal **3 referensi** Jurnal Bereputasi (Scopus / SINTA 1-2) | Metadata pada Bab 2 & entri `.bib` |
| `RULE-CIT-05` | Kemutakhiran Pustaka | Minimal **50% pustaka** dari **10 tahun terakhir** | Rasio tahun publikasi $\ge (\text{tahun} - 10)$ |
| `RULE-CIT-06` | Kutipan Langsung $>4$ baris | Menjorok kiri-kanan, spasi 1, tanpa tanda kutip | Environment `quote` + `\begin{spacing}{1}` |
| `RULE-CIT-07` | Kutipan Langsung $\le 4$ baris | Terpadu dalam teks diapit tanda kutip `"` | `"teks kutipan"` terpadu dalam kalimat |
| `RULE-CIT-08` | Spasi Daftar Pustaka | Spasi 1 dalam entri, berselang 2 spasi antarentri | `\setlength{\bibsep}{\baselineskip}` |
| `RULE-CIT-09` | Landasan Pustaka Nyata | DILARANG berasumsi/halusinasi isi referensi; wajib verifikasi berkas `jurnal/*.md` | Membaca dokumen lokal di `jurnal/<file>.md` |

## 2. Praktik Pengutipan Dalam Teks (In-text Citation)

Dengan menggunakan paket `natbib`, gunakan perintah berikut:

- **Pengutipan Berkurung (*Parenthetical Citation*):**
  - Perintah: `\citep{grootendorst2022bertopic}`
  - Output: `(Grootendorst, 2022)`
  - Contoh Kalimat: "Pemodelan topik modular memanfaatkan representasi c-TF-IDF \citep{grootendorst2022bertopic}."
- **Pengutipan Naratif (*Narrative Citation*):**
  - Perintah: `\citet{koto2021indobertweet}`
  - Output: `Koto dkk. (2021)` atau `Koto et al. (2021)`
  - Contoh Kalimat: "Menurut \citet{koto2021indobertweet}, korpus Twitter bahasa Indonesia memiliki karakteristik derau yang spesifik."
- **Kutipan Langsung dengan Halaman:**
  - Perintah: `\citep[hlm.~45]{sommerville2011software}`
  - Output: `(Sommerville, 2011, hlm. 45)`

*DILARANG menggunakan gaya sitasi angka numerik IEEE seperti `[1]`, `[2]`!*

## 3. Format Entri BibTeX yang Benar (`daftar_pustaka.bib`)

### Jurnal Ilmiah Bereputasi (@article)
```bibtex
@article{grootendorst2022bertopic,
  title   = {BERTopic: Neural topic modeling with a class-based TF-IDF procedure},
  author  = {Grootendorst, Maarten},
  journal = {arXiv preprint arXiv:2203.05794},
  year    = {2022},
  doi     = {10.48550/arXiv.2203.05794}
}
```

### Prosiding Seminar Internasional (@inproceedings)
```bibtex
@inproceedings{koto2021indobertweet,
  title     = {IndoBERTweet: A Pretrained Language Model for Indonesian Twitter with Effective Domain-Specific Vocabulary Initialization},
  author    = {Koto, Fajri and Rahimi, Afshin and Lau, Jey Han and Baldwin, Timothy},
  booktitle = {Proceedings of the 2021 Conference on Empirical Methods in Natural Language Processing (EMNLP)},
  pages     = {10660--10668},
  year      = {2021},
  doi       = {10.18653/v1/2021.emnlp-main.833}
}
```

### Buku Teks Ilmiah (@book)
```bibtex
@book{sommerville2011software,
  title     = {Software Engineering},
  author    = {Sommerville, Ian},
  edition   = {9th},
  publisher = {Addison-Wesley},
  address   = {Boston},
  year      = {2011}
}
```

## 4. Validasi Otomatis Kemutakhiran Pustaka

Gunakan skrip validasi `.agents/scripts/validate_thesis.py` untuk mengaudit:
1. Jumlah total pustaka yang disitasi ($\ge 15$).
2. Distribusi tahun terbit (minimal 50% berusia $\le 10$ tahun).
3. Entri yang tidak pernah disitasi dalam naskah (*unused bib entries*).
4. Sitasi naskah yang kuncinya hilang dari berkas `.bib` (*undefined citations*).

## 5. Basis Data Pengetahuan Pustaka Lokal (`jurnal/*.md`)

Untuk mematuhi `RULE-CIT-09`, setiap klaim, kutipan metodologis, perbandingan angka metrik, atau rumus yang diambil dari literatur wajib diverifikasi langsung dari berkas markdown lokal di folder `jurnal/`. Dilarang berspekulasi atau mengarang klaim yang tidak tercantum dalam berkas berikut:

| Kunci BibTeX (`daftar_pustaka.bib`) | Berkas Markdown Lokal (`jurnal/`) | Topik Inti / Relevansi Skripsi |
|---|---|---|
| `dieng2020topic` | `jurnal/adji_dieng.md` | Topic Modeling In Embedded Spaces (ETM) |
| `IJECE25896` | `jurnal/ahmad_alzubi1.md` | Automatic BIRCH thresholding, radius $R$, diameter $D$, centroid |
| `article` | `jurnal/ahmad_alzubi2.md` | Feature transformation & BIRCH dynamic thresholding |
| `antons2021computational` | `jurnal/antons_computational.md` | Computational literature review & topic modeling |
| `blei2003latent` | `jurnal/blei2003latent.md` | Latent Dirichlet Allocation (LDA) foundational paper |
| `debortoli2016comparing` | `jurnal/debortoli.md` | Comparing LDA vs latent semantic analysis in big data |
| `devlin2019bert` | `jurnal/devlin.md` | BERT: Pre-training of Deep Bidirectional Transformers |
| `eggers2018hybrid` | `jurnal/eggers.md` | Hybrid topic modeling approaches in business text |
| `Ramadhani_2020` | `jurnal/fanny_ramadhani.md` | Algoritma BIRCH clustering data, CF-Tree formula ($N, LS, SS$), dynamic threshold |
| `grootendorst2022bertopic` | `jurnal/grootendorst2022bertopic.md` | Arsitektur dasar BERTopic, c-TF-IDF, HDBSCAN integration |
| `koto2020indobert` | `jurnal/indobert_koto.md` | IndoBERT: Language model for Indonesian representation |
| `koto2021indobertweet` | `jurnal/koto2021indobertweet.md` | IndoBERTweet: Pretrained language model for Indonesian Twitter |
| `kumparan2021warganet` | `jurnal/kumparan2021warganet.md` | Fenomena percakapan warganet Indonesia |
| `manning2008information` | `jurnal/manning.md` | Introduction to Information Retrieval (Text processing) |
| `mcinnes2018umap` | `jurnal/mcinnes_umap.md` | UMAP: Dimension reduction algorithm |
| `iaes2025indobert` | `jurnal/muhammad_muhajir.md` | IndoBERT + BIRCH BERTopic (Baseline jurnal pembanding) |
| `mimno2011optimizing` | `jurnal/optimizing_semantic_coherence.md` | Semantic coherence for topic models (C_V, NPMI fundamentals) |
| `rahutomo2012semantic` | `jurnal/rahutomo.md` | Semantic cosine similarity measures on Indonesian text |
| `reimers2019sentencebert` | `jurnal/reimers.md` | Sentence-BERT (SBERT): Siamese sentence embeddings |
| `roder2015coherence` | `jurnal/roder_coherence.md` | Exploring the space of topic coherence measures |
| `silge2017text` | `jurnal/silge_text_mining.md` | Text Mining with R: A Tidy Approach |
| `sommerville2011software` | `jurnal/sommerville_software_engineering.md`| Software Engineering principles & methodologies |
| `suyanto2019datamining` | `jurnal/suyanto_data_mining.md` | Data Mining & clustering theory (Indonesian textbook) |
| `terrace2021twitter` | `jurnal/terrace_twitter_community.md` | Online community dynamics & social discourse analysis |
| `van2008visualizing` | `jurnal/van_der_maaten_tsne.md` | Visualizing data using t-SNE |
| `willett2021curse` | `jurnal/willett_curse_of_dimensionality.md` | High-dimensional geometry and curse of dimensionality |
| `xia2019short` | `jurnal/xia_short_text_topic.md` | Short text topic modeling challenges and solutions |
| `yang2020topic` | `jurnal/yang_topic_modeling_survey.md` | Survey on neural topic modeling techniques |
| `10.1145/235968.233324` | `jurnal/tian_zhang.md` | BIRCH: An efficient data clustering method for very large databases (SIGMOD 1996) |
| `10.1023/A:1009783824328` | `jurnal/tian_zhang_new.md` | BIRCH: A New Data Clustering Algorithm and Its Applications (DMKD 1997) |
| `11271424` | `jurnal/wannes_janssens.md` | A Comparative Analysis of Topic Reduction Techniques for BERTopic |
| `zhao2021topic` | `jurnal/zhao_topic_modeling_review.md` | Review of topic modeling in text mining and NLP |
