Repeater: Publikasi Teknik Informatika dan Jaringan
Volume 3, Nomor 2, April 2025
E-ISSN : 3046-7276, P-ISSN : 3046-7284; Hal. 45-54
DOI: https://doi.org/10.62951/repeater.v3i2.404
Available online at: https://journal.aptii.or.id/index.php/Repeater
Dinamika Sentimen Komunikasi Mahasiswa dan Dosen dengan
Pemanfaatan Analisis Pesan Whatsapp Akademis Menggunakan
Machine Learning
Abdi Prayogi1 , Novriyenny 2 , I Gusti Prahmana3
1-3 STMIK Kaputama, Indonesia
JL.Veteran, No.4A-9A, Binjai, Sumatera Utara, Indonesia
Email : prayogi@gmail.com1 , novri_yenny@yahoo.com2 , igustiprahmana27@gmail.com3
Abstract. Communication is the process of exchanging information, ideas, thoughts, and feelings between
individuals or groups through the use of words, signs, or actions. This process can take place verbally or non-
verbally and involves various media and channels, such as face-to-face conversations, writing, gestures, facial
expressions, and digital technology. This research was conducted at STMIK Kaputama Binjai, namely the
WhatsApp group between lecturers and students. This study uses the Support Vector Machine (SVM) method.
SVM is a type of supervised learning machine learning that requires sample data. Support Vector Machine (SVM)
is an algorithm developed by Boser, Guyon, and Vapnik in 1992. Support Vector Machine (SVM) has a concept
that is combined with previous computational theories. This method can transform training data into higher
dimensions using non-linear patterns. The results of the Support Vector Machine method classification with a
total of 16 positive sentiments, 40 neutral sentiments and 71 negative sentiments. Accuracy value 67%, margin
error 39%. Positive prediction precision 75%, neutral prediction precision 83% and negative prediction precision
88%..
Keywords: Sentiment Analysis, Support Vector Machine and STMIK Kaputama Binjai
Abstrak. Komunikasi adalah proses pertukaran informasi, ide, pikiran, dan perasaan antara individu atau
kelompok melalui penggunaan kata-kata, tanda-tanda, atau tindakan. Proses ini dapat berlangsung secara verbal
maupun non-verbal dan melibatkan berbagai media dan saluran, seperti percakapan tatap muka, tulisan, gestur,
ekspresi wajah, dan teknologi digital. Pemahaman tentang dinamika sentimen dalam komunikasi menjadi semakin
penting di era modern, di mana interaksi terjadi melalui berbagai medium, baik tatap muka maupun digital.
Penelitian ini dilakuan Pada STMIK Kaputama Binjai yaitu group WhatsApp antara dosen dan mahasiswa.
Penelitian ini menggunakan metode Support Vactor Machine (SVM). SVM adalah jenis machine learning
supervised learning yang membutuhkan sample data. Support Vector Machine (SVM) merupakan algoritma yang
dikembangkan oleh Boser, Guyon, dan Vapnik pada tahun 1992. Support Vector Machine (SVM) memiliki
konsep yang dikombinasi dari teori komputasi sebelumnya. Metode ini dapat mengubah data latih ke dimensi
yang lebih tinggi menggunakan pola non linear.Hasil clasifikasi metode Support Vector Machine dengan jumlah
16 sentimen positif, 40 sentimen netral dan 71 sentimen negatif. Nilai akurasi 67% , magin error 39%. Presisi
prediksi positif 75%, Presisi prediksi netral 83% dan Presisi prediksi negatif 88%.
Kata kunci: Analisis Sentimen, Support Vector Machine dan STMIK Kaputama Binjai
1. LATAR BELAKANG
Komunikasi adalah proses pertukaran informasi, ide, pikiran, dan perasaan antara
individu atau kelompok melalui penggunaan kata-kata, tanda-tanda, atau tindakan (Lubis,
2022). Proses ini dapat berlangsung secara verbal maupun non-verbal dan melibatkan berbagai
media dan saluran, seperti percakapan tatap muka, tulisan, gestur, ekspresi wajah, dan
teknologi digital. Dalam interaksi sehari-hari, komunikasi tidak hanya mengandung aspek
informatif, tetapi juga emosional yang disebut sebagai sentimen. Sentimen ini mencakup
Received: Februari 10, 2025; Revised: Februari 25, 2025; Accepted: Maret 21, 2025; Online Available: Maret
24, 2025

Dinamika Sentimen Komunikasi Mahasiswa dan Dosen dengan Pemanfaatan Analisis Pesan Whatsapp
Akademis Menggunakan Machine Learning
perasaan positif, negatif, atau netral yang dapat memengaruhi dan membentuk dinamika
percakapan. Pemahaman tentang dinamika sentimen dalam komunikasi menjadi semakin
penting di era modern, di mana interaksi terjadi melalui berbagai medium, baik tatap muka
maupun digital.
Dinamika sentimen dalam komunikasi berperan penting dalam berbagai aspek
kehidupan, termasuk dalam hubungan interpersonal, lingkungan kerja, pendidikan, dan
pelayanan publik. Sentimen yang disampaikan dalam komunikasi dapat memengaruhi
persepsi, sikap, dan reaksi individu. Misalnya, dalam lingkungan kerja, komunikasi yang
dipenuhi sentimen positif dapat meningkatkan motivasi dan kerjasama tim, sementara sentimen
negatif dapat menyebabkan konflik dan penurunan produktivitas (Saputri, 2023).
Interaksi antara mahasiswa dan dosen merupakan proses komunikasi yang terjadi sehari-
hari dalam lingkungan akademik. Komunikasi yang efektif antara kedua belah pihak tidak
hanya mendukung pencapaian tujuan pendidikan, tetapi juga membangun hubungan yang
positif dan konstruktif. Aplikasi pesan instan seperti WhatsApp telah menjadi salah satu alat
komunikasi utama antara mahasiswa dan dosen. WhatsApp menawarkan kemudahan dan
kecepatan dalam bertukar informasi, baik terkait materi perkuliahan, tugas, konsultasi, maupun
keperluan administrasi lainnya. Namun, penggunaan WhatsApp juga membawa tantangan
dalam hal dinamika sentimen yang muncul selama komunikasi berlangsung. Machine learning
(ML) menawarkan alat dan teknik yang kuat untuk menganalisis data teks secara otomatis dan
mengidentifikasi pola-pola sentimen dalam komunikasi.
Beberapa penelitian telah dilakukan untuk analisis sentimen pesan Watshapp, salah
satunya penelitian yang dilakukan oleh Agus Setiawan Putra (2023), dengan judul penelitian
“Analisis Sentimen Multilingual Menggunakan Pendekatan Machine Learning”. Pendekatan
ini melibatkan beberapa tahap, termasuk preprocessing teks, ekstraksi fitur, dan pelatihan
model. Hasilnya menunjukkan bahwa pendekatan ini efektif dalam menganalisis sentimen
dalam teks multilingual, dengan kemampuan untuk mengklasifikasikan sentimen dengan
tingkat keakuratan yang tinggi di berbagai bahasa. Penelitian lebih lanjut diperlukan untuk
meningkatkan kinerja model dan menyesuaikannya dengan variasi bahasa yang lebih luas
(Putra, 2023).
2. KAJIAN TEORITIS
Dalam adanya permasalahan yang dihadapi, maka perumusan masalah adalah sebagai
berikut :
46 REPEATER - VOLUME 3, NOMOR 2, APRIL 2025

e-ISSN : 3046-7276, P-ISSN : 3046-7284; Hal. 45-54
1. Bagaimana mengumpulkan dan mengolah data pesan WhatsApp antara mahasiswa dan
dosen dalam lingkungan STMIK Kaputama Binjai untuk analisis sentimen?
2. Bagaimana karakteristik komunikasi antara mahasiswa dan dosen dapat diidentifikasi
dan diekstraksi dari data pesan WhatsApp?
3. Bagaimana model Machine Learning dapat diterapkan untuk mengklasifikasikan
sentimen negatif, positif dan netral dalam pesan WhatsApp antara mahasiswa dan
dosen?
Adapun tujuan dari penelitian Skripsi ini adalah
1. Untuk mengumpulkan dan mengolah data pesan WhatsApp antara mahasiswa dan
dosen dalam lingkungan STMIK Kaputama Binjai untuk analisis sentimen.
2. Untuk mengetahui karakteristik komunikasi antara mahasiswa dan dosen dapat
diidentifikasi dan diekstraksi dari data pesan WhatsApp.
3. Untuk mengetahui model Machine Learning dapat diterapkan untuk
mengklasifikasikan sentimen negatif, positif dan netral dalam pesan WhatsApp antara
mahasiswa dan dosen.
3. METODE PENELITIAN
3.1 Analisis Sentimen
Analisis sentimen merupakan salah satu contoh dari bidang Natural Language
Processing (NLP) yang paling populer. Natural Language Processing (NLP) adalah bidang
ilmiah yang membahas tentang bagaimana caranya agar komputer bisa bekerja dan berpikit
seperti manusia. Natural Language Processing (NLP) merupakan bagian dari Artifical
Intellegence atau kecerdasan buatan. Dalam perkembangan data mining, Artifical Intellegence
(AI) merupakan salah satu dari empat cabang ilmu data mining, yaitu statistika, database, dan
pencarian informasi. Dalam penerapannya, Artifical Intellegence (AI) juga memerlukan
machine learning sebagai algoritma penyelesaian. Adanya machine learning digunakan untuk
menggantikan manusia dalam mengambil keputusan. Machine learning tidak mempunyai
perasaan seperti manusia sehingga keputusan yang diambil berdasarkan data yang sudah diolah
(Saputra, 2022).
Analisis sentimen merupakan proses komputasi menggunakan teknik analisis teks dalam
bentuk data tekstual dengan cara mengelola, memahami, dan menggelompokkan emosional
baik positif atau negatif. Analisis sentimen banyak digunakan karena meningkatknya
kebutuhan individu atau kelompok dalam mengetahui pendapat seseorang terhadap sesuatu.

Dinamika Sentimen Komunikasi Mahasiswa dan Dosen dengan Pemanfaatan Analisis Pesan Whatsapp
Akademis Menggunakan Machine Learning
Analisis sentimen juga dipengaruhi oleh data set yang digunakan akan mengalami penanganan
yang berbeda (Widayat, 2021).
3.2 WhatsApp
WhatsApp adalah aplikasi pesan instan yang memungkinkan pengguna untuk mengirim
teks, suara, gambar, video, dan dokumen melalui koneksi internet. Aplikasi ini sangat populer
karena mudah digunakan, mendukung obrolan individu maupun grup, serta dilengkapi dengan
fitur enkripsi end-to-end yang melindungi privasi komunikasi. WhatsApp juga mendukung
panggilan suara dan video, serta dapat diakses melalui ponsel dan komputer.
Dr. Vaibhav Bhamore (2018) Dalam analisisnya tentang WhatsApp dalam konteks
komunikasi bisnis menyatakan bahwa "WhatsApp adalah salah satu alat komunikasi paling
efisien untuk bisnis modern, memungkinkan perusahaan untuk berinteraksi dengan pelanggan
secara langsung dan real-time, serta mendukung inisiatif pemasaran digital melalui pesan yang
dipersonalisasi”.
3.3 Lingkungan Akademis
Lingkungan akademis adalah suatu lingkungan yang berkaitan dengan pendidikan,
penelitian, dan pengembangan ilmu pengetahuan di lembaga-lembaga pendidikan seperti
sekolah, perguruan tinggi, dan universitas. Dalam lingkungan ini, terdapat berbagai aktivitas
intelektual yang melibatkan siswa, mahasiswa, dosen, peneliti, dan staf pendidikan lainnya
yang berfokus pada pembelajaran, pengajaran, dan penelitian.
Secara lebih spesifik, lingkungan akademis mencakup kegiatan belajar-mengajar, di
mana pengajar seperti dosen atau guru memberikan materi dan bimbingan kepada siswa atau
mahasiswa. Selain itu, lingkungan ini juga melibatkan kegiatan penelitian yang dilakukan
untuk mengembangkan pengetahuan baru atau memperdalam pemahaman tentang suatu
subjek, yang biasanya dikerjakan oleh dosen, peneliti, dan mahasiswa pascasarjana. Kebijakan
akademik juga menjadi bagian penting, mencakup aturan dan pedoman yang mengatur proses
pendidikan dan penelitian, termasuk kurikulum, evaluasi, dan standar akademis. Di dalamnya
juga terjadi interaksi sosial dan intelektual, di mana anggota komunitas akademik seperti
mahasiswa dan dosen berdiskusi, berkolaborasi, dan bertukar ide melalui seminar, konferensi,
kelompok studi, maupun diskusi informal. Selain itu, lingkungan akademis dilengkapi dengan
berbagai fasilitas dan sumber daya seperti perpustakaan, laboratorium, ruang kelas, dan pusat
penelitian yang mendukung semua kegiatan akademik tersebut.
48 REPEATER - VOLUME 3, NOMOR 2, APRIL 2025

e-ISSN : 3046-7276, P-ISSN : 3046-7284; Hal. 45-54
3.4 Metode Support Vector Machine
Metode Support Vector Machine (SVM) termasuk jenis machine learning supervised
learning yang membutuhkan sample data. Support Vector Machine (SVM) merupakan
algoritma yang dikembangkan oleh Boser, Guyon, dan Vapnik pada tahun 1992. Support
Vector Machine (SVM) memiliki konsep yang dikombinasi dari teori komputasi sebelumnya.
Metode ini dapat mengubah data latih ke dimensi yang lebih tinggi menggunakan pola non
linear (Hilda Kusumahadi et al., 2019).
Metode ini juga sering digunakan dalam klasifikasi yang termasuk ke dalam supervised
learning dan mempunyai konsep matematis yang jelas. Jika dibandingkan dengan metode lain,
metode ini mempunyai tingkat akurasi yang lebih tinggi (Pratiwi et al., 2021). Support Vector
Machine (SVM) dapat bekerja pada data set yang mempunyai dimensi tinggi menggunakan
kernek trik (Pane et al., 2021). Pada pola hasil pelatihan, metode ini meliputi machine learning
berdasarkan Structural Risk Minimization (SRM). Pada metode ini dilakukan pencarian
hyperplan terbaik atau batas keputusan untuk memisahkan dua kelas pada input space. Dalam
hal ini berperan memisahkan antara tweet positif dari tweet negatif. Pencarian nilai hyperplane
dilakukan menggunakan vektor bantu dan nilai margin. Hyperplane adalah bidang pemisah
antara satu kelas dengan kelas lainnya. Margin adalah jarak antara support vector machine
dengan hyperplan. (Santoso, 2021).
4. HASIL DAN PEMBAHASAN
4.1 Processing
a. Filtering
Proses filtering menggunakan stop-list dengan daftar kata stopword. Jika dalam suatu
data terdapat stopword, maka secara otomatis kata-kata tersebut akan dihapus.
Berikut contoh proses filtering
Gambar III. 1 Contoh Hasil Algoritma Filtering

Dinamika Sentimen Komunikasi Mahasiswa dan Dosen dengan Pemanfaatan Analisis Pesan Whatsapp
Akademis Menggunakan Machine Learning
b. Case Folding
Case folding adalah proses pengolahan data dimana setiap huruf capital pada tiap
pesan diubah menjadi huruh tidak capital (huruf kecil). Hal ini juga bertujuan untuk
memberikan nilai yang sama pada perbandingan kata yang sama. Berikut contoh
proses Case Folding
Gambar III.2 Contoh Hasil Algoritma Case Folding
c. Stemming
Stemming adalah proses menghilangkan imbuhan pada kata pada setiap kalimat pada
pesan. Berikut contoh proses Stemming
Gambar III.3 Contoh Hasil Algoritma Stemming
d. Tokenezing
Word Tokenizing merupakan sebuah proses memisahkan kata per-kata pada setiap
kalimat pada setiap pesan menjadi sebuah himpunan kata. Hal ini berguna untuk
memudahkan dalam melakukan komparasi data karena data yang dikomparasikan
dalam kasus ini adalah kata per-kata pada setiap kalimat pada pesan. Berikut contoh
proses Word Tokenizin.
50 REPEATER - VOLUME 3, NOMOR 2, APRIL 2025

e-ISSN : 3046-7276, P-ISSN : 3046-7284; Hal. 45-54

Gambar III.4 Contoh Hasil Algoritma Tokenizing

4.2 Evaluasi Kinerja Sistem
Tabel III. 1 Tabel Kontingensi
|             |           |                      |                   | Kelas Hasil Prediksi  |                      |     |     |
| ----------- | --------- | -------------------- | ----------------- | --------------------- | -------------------- | --- | --- |
|             |           |                      | Prediksi Positif  |                       | Prediksi Negative    |     |     |
| Kelas Asli  | Positif   | True Positive (TP)   |                   |                       | True Positive (TP)   |     |     |
|             | Negative  | False Negative (FN)  |                   |                       | False Negative (FN)  |     |     |

4.3 Perhitungan Algoritam Support Vector Machine (SVM)
a.  Pembobotan
Pada proses pembobotan berdasarkan data dari hasil preprocessing terdapat pada
tabel III. 2, diaman kategori 1 menandakan pesan whatshapp positif dan kategori 0
menandakan pesan whatshapp negatif.
Tabel III. 2 Hasil Pembobotan
| Term          |     | pw      |         | df  n/df  | idf      | Pw-idf   |          |
| ------------- | --- | ------- | ------- | --------- | -------- | -------- | -------- |
|               |     | p1  p2  | p3  p4  |           |          | p1  p2   | p3  p4   |
| Terakhir      |     | 1  0    | 0  0    | 1         | 4  0,60  | 0,60  0  | 0  0     |
| Pengumpulan   |     | 1  0    | 0  0    | 1         | 4  0,60  | 0,60  0  | 0  0     |
| Tugas         |     | 1  0    | 0  0    | 1         | 4  0,60  | 0,60  0  | 0  0     |
| Hari          |     | 1  0    | 0  0    | 1         | 4  0,60  | 0,60  0  | 0  0     |
| kamis         |     | 1  0    | 0  0    | 1         | 4  0,60  | 0,60  0  | 0  0     |
| Untuk         |     | 0  1    | 0  0    | 1         | 4  0,60  | 0  0,60  | 0  0     |
| Kelompok      |     | 0  1    | 0  0    | 1         | 4  0,60  | 0  0,60  | 0  0     |
| Yang          |     | 0  1    | 0  0    | 1         | 4  0,60  | 0  0,60  | 0  0     |
| Belum         |     | 0  1    | 0  0    | 1         | 4  0,60  | 0  0,60  | 0  0     |
| Presentasi    |     | 0  1    | 0  0    | 1         | 4  0,60  | 0  0,60  | 0  0     |
| Agar          |     | 0  0    | 1  0    | 1         | 4  0,60  | 0  0     | 0,60  0  |
| Menyiapkan    |     | 0  0    | 1  0    | 1         | 4  0,60  | 0  0     | 0,60  0  |
| Bahannya      |     | 0  0    | 1  0    | 1         | 4  0,60  | 0  0     | 0,60  0  |
| Untuk         |     | 0  0    | 1  0    | 1         | 4  0,60  | 0  0     | 0,60  0  |
| Pertemuan     |     | 0  0    | 1  0    | 1         | 4  0,60  | 0  0     | 0,60  0  |
| Selanjutnta   |     | 0  0    | 1  0    | 1         | 4  0,60  | 0  0     | 0,60  0  |
| Tidak         |     | 0  0    | 0  1    | 1         | 4  0     | 0  0     | 0  0,60  |
| ada           |     | 0  0    | 0  1    | 1         | 4  0     | 0  0     | 0  0,60  |
| tugas         |     | 0  0    | 0  1    | 1         | 4  0     | 0  0     | 0  0,60  |

Dinamika Sentimen Komunikasi Mahasiswa dan Dosen dengan Pemanfaatan Analisis Pesan Whatsapp
Akademis Menggunakan Machine Learning
penilaian 0 0 0 1 1 4 0 0 0 0 0,60
kososng 0 0 0 1 1 4 0 0 0 0 0,60
b. Normalisasi
Contoh bobot normalisasi dari p pada hasil ilustrasi pembobotan term “terakhir”
1
pada pesan whatshapp pertama sebagai berikut;
5. KESIMPULAN DAN SARAN
Kesimpulan
Dari hasil analisa yang sudah dilakukan berdasarkan data chat WhatsAhap antara
mahasiswa dan dosen dengan metode Support Vector Machine (SVM), maka dapat diambil
kesimpulan sebagai berikut:
1. Hasil clasifikasi metode Support Vector Machine dengan jumlah 16 sentimen positif,
40 sentimen netral dan 71 sentimen negatif. Nilai akurasi 67% , margin error 39%.
Presisi prediksi positif 75%, Presisi prediksi netral 83% dan Presisi prediksi negatif
88%.
2. Berdasarkan hasil penelitian ini meliki nilai akurasi, presisi dan recall yang baik,
sehingga bisa digunakan dalam sebuah analisis sentimen.
3. Berdasarkan hasil sentimen dari Support Vector Machine (SVM), sentimen positif
berjumlah 16, netral 40 dan sentimen negatif berjumalh 71. Jadi, sentimen negatif lebih
banyak daripada sentimen positif yang artinya pengguna group WhatsApp mahasiswa
dan dosen memiliki opini negatif.
Saran
Dari hasil penelitian analisis sentimen chat WhatsAhap antara mahasiswa dan dosen ini
maka penulis memberikan saran antara lain :
52 REPEATER - VOLUME 3, NOMOR 2, APRIL 2025

e-ISSN : 3046-7276, P-ISSN : 3046-7284; Hal. 45-54
1. Dosen dan mahasiswa perlu meningkatkan kualitas komunikasi mereka di grup
WhatsApp, sehingga dapat mengurangi sentimen negatif dan meningkatkan sentimen
positif.
2. Pengembangan sistem analisis sentimen yang lebih akurat dan efektif dapat
membantu dalam memantau dan menganalisis sentimen di grup WhatsApp.
3. Dosen dan mahasiswa perlu meningkatkan kesadaran akan pentingnya komunikasi
yang efektif dalam mencapai tujuan akademik dan mengurangi sentimen negatif.
6. DAFTAR REFERENSI
Acep Saepulrohman, Sudin Saepudin dan Dudih Gustian, (2019), Analisis
Sentimen Kepuasan Pengguna Aplikasi WhatsApp Menggunakan
Algoritma Naïve Bayes Dan Support Vector Machine, Jurnal: Sistem
Informasi, Universitas Nusa Putra
Agus Setiawan Putra, (2023), Analisis Sentimen Multilingual Menggunakan
Pendekatan Machine Learning, Jurnal: Teknologi Pintar, Vol. 3, No. 11
Ahmad, A. (2020). Media Sosial dan Tantangan Masa Depan Generasi Milenial.
08(02), 134–148.
Arviana, G. N. (2021). Sentiment Analysis, Teknik untuk Pahami Maksud di Balik
Opini Pelanggan. 1 Februarui.
Debi Sintia Amalia dan Ahmad Ari Aldino, (2021), Teks Dan Analisis Sentimen
Pada Chat Grup Whatsapp Menggunakan Long Short Term Memory
(LSTM), Jurnal: Sistem Informasi, Universitas Teknologi Indonesia, Vol.
2, No. 4, E-ISSN: 2746-3699
Detti Purnamasari, Ananda Bayu Aji, Desy Wulandari, Fanka Ari Reza, Milda
Safrila, Nafa Yanda dan Ulfa Hidayanti, (2023), Pengantar Metode
Analisis Sentimen, Jawa Barat: Gunadarma
Herlinawati, N., Yuliani, Y., Faizah, S., Gata, W., & Samudi, S. (2020). Analisis
Sentimen Zoom Cloud Meetings di Play Store Menggunakan Naïve Bayes
dan Support Vector Machine. CESS (Journal of Computer Engineering,
System and Science), 5(2), 293. https://doi.org/10.24114/cess.v5i2.18186
Hilda Kusumahadi, S., Junaedi, H., & Santoso, J. (2019). Klasifikasi Helpdesk
Menggunakan Metode Support Vector Machine. Jurnal Informatika:
Jurnal Pengembangan IT, 4(1), 54–60. https : //doi.org /10.30591/
jpit.v4i1.1125
Indah Alda Sapitri, Yusra dan Muhammad Fikri, (2023), Pengklasifikasian
Sentimen Ulasan Aplikasi Whatsapp Pada Google Play Store
Menggunakan Support Vector Machine, Jurnal: Sains dan Teknologi,
Universitas Islam Negeri Sultan Syarif Kasim Riau, Vol. 6, No. 1, ISSN:
2621-1556
Irwansyah Saputra, D. A. K. (2022). Machine Learning untuk Pemula, Bandung:
Informatika

Dinamika Sentimen Komunikasi Mahasiswa dan Dosen dengan Pemanfaatan Analisis Pesan Whatsapp
Akademis Menggunakan Machine Learning
Lina Kartika Pratiwi, (2023), Peningkatan Akurasi Analisis Sentimen Dengan
Algoritma Machine Learning, Jurnal: Teknologi Pintar, Vol. 3, No. 11
Natasuwarna, A. P. (2020). Seleksi Fitur Support Vector Machine pada Analisis
Sentimen Keberlanjutan Pembelajaran Daring. Techno.Com, 19(4), 437–
448. https://doi.org/10.33633/tc.v19i4.4044
Nur Rofiq dan Sartika Lina Mulani Sitio, (2024), Pengenalan Dasar Analisis Data
Dengan Phyton di Google Colab, Purbalingga: CV. Eureka Media Aksara
Taufiqurrahman, F., Faraby, S. Al, & Purbolaksono, M. D. (2021). Klasifikasi
Teks Multi Label pada Hadis Terjemahan Bahasa Indonesia Menggunakan
Chi Square dan SVM. E-Proceeding of Engineering, 8(5), 10650–10659.
Widayat, W. (2021). Analisis Sentimen Movie Review menggunakan Word2Vec
dan metode LSTM Deep Learning. Jurnal Media Informatika Budidarma,
5(3), 1018. https://doi.org/10.30865/mib.v5i3.3111
54 REPEATER - VOLUME 3, NOMOR 2, APRIL 2025