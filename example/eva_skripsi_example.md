DIGITAL REPOSITORY UNIVERSITAS JEMBER
ANALISIS NIAT PENGGUNAAN BERKELANJUTAN AI DESIGN TOOLS
PADA APLIKASI FIGMA MAKE MELALUI INTEGRASI TAM-ECM
DENGAN FAKTOR EKSTERNAL UX
Diajukan guna memenuhi salah satu syarat memperoleh gelar Sarjana pada
program studi Sistem Informasi
SKRIPSI
Oleh:
Eva Oktaviana
NIM 222410101015
KEMENTERIAN PENDIDIKAN, KEBUDAYAAN, RISET, DAN
TEKNOLOGI
UNIVERSITAS JEMBER
FAKULTAS ILMU KOMPUTER
PROGRAM STUDI SISTEM INFORMASI
JEMBER
2026
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
PERSEMBAHAN
Penulisan skripsi ini saya persembahkan kepada:
1. Allah SWT. Atas segala Rahmat dan hidayah-Nya, sehingga penulis dapat
menyelesaikan skripsi dengan baik;
2. Bapak Moh. Yanto dan Ibu Siti Khotimah yang selalu mengusahakan hal-
hal terbaik, selalu melangitkan doa, dan mendukung penulis dalam berbagai
hal;
3. Bapak Fahrobby Adnan, S.Kom., M.MSI. selaku dosen pembimbing yang
senantiasa memberikan arahan dan motivasi sehingga penulis yakin dan
mampu menyelesaikan skripsi hingga akhir;
4. Ibu Karina Nine Amalia, S.Kom., M.Kom. dan Martiana Kholila Fadhil,
M.Kom selaku dosen penguji yang selalu memberikan saran dan masukan
dalam proses pengembangan skripsi;
5. Dosen-dosen Fakultas Ilmu Komputer, Universitas Jember yang
memberikan ilmu dan bimbingan;
6. Almamater Program Studi Sistem Informasi, Fakultas Ilmu Komputer,
Universitas Jember yang menjadi tempat penulis menuntut ilmu, tumbuh,
dan menempa diri;
7. Teman-teman tercinta yang selalu hadir memberikan do’a, semangat, dan
pengalaman berharga bagi penulis.
DIGITAL REPOSITORY UNIVERSITAS JEMBER
i

DIGITAL REPOSITORY UNIVERSITAS JEMBER
MOTTO
“In life, you either win or learn. When you lose, experience is the reward”
(Nelson Mandela)
ن َ ي نس حْ مُ لْٱ عَ مَ َل َللّ َّ ٱ نَّ إوَ ۚ اَنَلُبسُ مْ هُ َّنَيد هْ َنَل اَني ف ا وُدهَ ـٰجَ نَ ي ذ َّلٱوَ
“As for those who struggle in Our cause, We will surely guide them along Our
Way. And Allah is certainly with the good-doers”
(Al-‘Ankabut (29:69))
DIGITAL REPOSITORY UNIVERSITAS JEMBER
ii

DIGITAL REPOSITORY UNIVERSITAS JEMBER
PERNYATAAN ORISINALITAS
DIGITAL REPOSITORY UNIVERSITAS JEMBER
iii

DIGITAL REPOSITORY UNIVERSITAS JEMBER
HALAMAN PERSETUJUAN
DIGITAL REPOSITORY UNIVERSITAS JEMBER
iv

DIGITAL REPOSITORY UNIVERSITAS JEMBER
ABSTRACT
The rapid advancement of Artificial Intelligence (AI) technologies has significantly
transformed UI/UX design practices, particularly through the emergence of AI-
powered design tools such as Figma Make. Despite their growing adoption,
empirical studies examining the determinants of continuance intention toward AI
design tools remain limited, especially among Generation Z, a user group
characterized by rapid technology adoption and high experiential expectations. To
address this gap, this study integrates the Technology Acceptance Model (TAM) and
the Expectation Confirmation Model (ECM) with external User Experience (UX)
factors while incorporating key characteristics of AI design tools. The study aims
to provide a comprehensive understanding of the factors influencing users’
continuance intention to use AI design tools within the Figma Make application.
Data were collected from 124 active Figma Make users and analyzed using Partial
Least Squares Structural Equation Modelling (PLS-SEM) with SmartPLS. The
results show that Emotional Experience (EE) has a significant direct effect on
Continuance Intention (CI) (β = 0.268, p = 0.001), followed by Interactive
Experience (IE) (β = 0.193, p = 0.024), Perceived Intelligence (PI) (β = 0.215, p =
0.034), and Satisfaction (SAT) (β = 0.243, p = 0.019). Confirmation of Expectation
(CE) influences CI indirectly through Satisfaction, supporting the post-adoption
mechanism proposed by ECM. In addition, Perceived Intelligence significantly
affects Perceived Trust (PT), highlighting the importance of perceived AI capability
in building user trust. The structural model demonstrates marginal fit (SRMR =
0.123; R² = 0.474; GoF = 0.566), suggesting that future studies may improve model
robustness through larger sample sizes and a more parsimonious model structure.
Eleven indicators were also identified as priority areas for improvement. Overall,
this study enriches continuance intention research by extending TAM–ECM with
UX and AI-related factors while providing practical insights for improving AI
design tools and sustaining long-term user engagement.
Keyword: AI design tools; Technology Acceptance Model (TAM); Expectation
Confirmation Model (ECM); continuance intention; PLS-SEM
DIGITAL REPOSITORY UNIVERSITAS JEMBER
v

DIGITAL REPOSITORY UNIVERSITAS JEMBER
RINGKASAN
Analisis Niat Penggunaan Berkelanjutan AI Design Tools Pada Aplikasi Figma
Make Melalui Integrasi TAM-ECM Dengan Faktor Eksternal UX; Eva
Oktaviana; 222410101015; 2026; 91 Halaman, Program Studi Sistem Informasi
Fakultas Ilmu Komputer Universitas Jember
Perkembangan teknologi Artificial Intelligence (AI) mendorong
pemanfaatannya dalam berbagai bidang, salah satunya pada desain UI/UX melalui
aplikasi Figma Make. Kehadiran AI pada aplikasi ini menawarkan kemudahan dan
efisiensi dalam proses desain, namun keberlanjutan penggunaannya belum
sepenuhnya terjamin, khususnya pada Generasi Z sebagai kelompok yang cepat
mengadopsi teknologi tetapi juga memiliki ekspektasi tinggi terhadap kualitas
pengalaman pengguna. Hingga saat ini, kajian yang menganalisis faktor-faktor
yang memengaruhi niat penggunaan berkelanjutan AI design tools pada Figma
Make secara komprehensif masih terbatas, sehingga diperlukan penelitian yang
mengintegrasikan aspek penerimaan teknologi, konfirmasi harapan, pengalaman
pengguna, serta karakteristik AI.
Penelitian ini bertujuan untuk menganalisis faktor-faktor yang
memengaruhi niat penggunaan berkelanjutan AI design tools pada aplikasi Figma
Make serta memberikan rekomendasi prioritas perbaikan. Metode yang digunakan
adalah Technology Acceptance Model (TAM) dan Expectation Confirmation Model
(ECM) yang dikombinasikan dengan faktor eksternal User Experience (UX) serta
karakteristik AI design tools. Data dikumpulkan dari 124 responden yang
merupakan pengguna aktif Figma Make melalui penyebaran kuesioner. Instrumen
penelitian terdiri dari 37 indikator yang merepresentasikan 11 variabel. Analisis
data dilakukan menggunakan metode Partial Least Squares Structural Equation
Modeling (PLS-SEM) dengan aplikasi SmartPLS versi 4.0.0.9.
Berdasarkan 17 hipotesis yang diajukan, 10 diantaranya diterima dan 7
lainnya ditolak. Hasil penelitian menunjukkan bahwa beberapa variabel memiliki
pengaruh signifikan terhadap niat penggunaan berkelanjutan. Emotional
Experience (EE) terbukti berpengaruh positif dan signifikan secara langsung
DIGITAL REPOSITORY UNIVERSITAS JEMBER
vi

DIGITAL REPOSITORY UNIVERSITAS JEMBER
terhadap variabel Continuance Intention (CI), diikuti oleh Interactive Experience
(IE), Perceived Intelligence (PI), dan Satisfaction (SAT). Selain itu, variabel
Confirmation of Expectation (CE) memengaruhi Continuance Intention (CI) secara
tidak langsung melalui Satisfaction (SAT). Selanjutnya hasil hipotesis juga
dirumuskan dan dianalisis untuk mengidentifikasi prioritas perbaikan yang perlu
dilakukan oleh Figma Make. Temuan penelitian ini diharapkan dapat menjadi dasar
bagi pengembang dalam mengoptimalkan kinerja dan desain pada aplikasi agar
mampu meningkatkan kepuasan dan keberlanjutan penggunaan aplikasi.
DIGITAL REPOSITORY UNIVERSITAS JEMBER
vii

DIGITAL REPOSITORY UNIVERSITAS JEMBER
PRAKATA
Alhamdulillahirobbil’alamin, puji dan syukur penulis panjatkan ke hadirat
Allah SWT. atas segala rahmat, hidayah, dan karunia-Nya sehingga penulis dapat
menyelesaikan skripsi dengan judul “Analisis Niat Penggunaan Berkelanjutan AI
Design Tools Pada Aplikasi Figma Make Melalui Integrasi TAM-ECM Dengan
Faktor Eksternal UX.” dengan baik. Skripsi ini disusun sebagai salah satu syarat
untuk memperoleh gelar Sarjana pada Program Studi Sistem Informasi, Fakultas
Ilmu Komputer, Universitas Jember.
Penulis menyadari bahwa penyusunan skripsi ini tidak terlepas dari bantuan,
bimbingan, dan dukungan berbagai pihak. Oleh karena itu, pada kesempatan ini
penulis ingin menyampaikan ucapan terima kasih yang sebesar-besarnya kepada:
1. Allah SWT. atas limpahan rahmat dan hidayah-Nya sehingga penulis dapat
menyelesaikan proses studi dari awal hingga proses penyusunan skripsi ini
selesai dengan baik;
2. Prof. Drs. Antonius Cahya Prihandoko, M.App.Sc., Ph.D, selaku dekan
Fakultas Ilmu Komputer, Universitas Jember;
3. Bapak Fahrobby Adnan, S.Kom., M.MSI selaku dosen pembimbing yang
selalu sabar memberikan arahan, bimbingan, dan motivasi selama proses
penyusunan skripsi;
4. Ibu Karina Nine Amalia, S.Kom., M.Kom dan Ibu Martiana Kholila Fadhil,
M.Kom selaku dosen penguji yang telah memberikan saran dan masukan
yang membangun demi penyempurnaan skripsi ini;
5. Bapak Fajrin Nurman Arifin, S.T., M.Eng. selaku Dosen Pembimbing
Akademik (DPA) yang memberikan arahan penulis selama proses studi;
6. Seluruh dosen dan staff karyawan Fakultas Ilmu Komputer Universitas
Jember yang telah memberikan ilmu pengetahuan dan bimbingan selama
masa perkuliahan;
7. Bapak Moh. Yanto dan Ibu Siti Khotimah, selaku orang tua tercinta, atas
doa, kasih sayang, pengorbanan, serta dukungan yang tak ternilai sehingga
penulis mampu menyelesaikan studi ini;
DIGITAL REPOSITORY UNIVERSITAS JEMBER
viii

DIGITAL REPOSITORY UNIVERSITAS JEMBER
8. Mei Linda Lusiana dan Ahmad Arfa Noegraha, selaku kakak dan teman
kecil bagi penulis yang selalu membantu penulis dan terus memotivasi
untuk meraih mimpi;
9. Sahabat tercinta Melati Anggraini, Safila Elsa Vavilya, Ira Nisa Sulthoni,
dan Nafalla Aftanur Rismawanti yang selalu memberikan bantuan, doa,
masukan, serta pengalaman yang bernilai bagi penulis;
10.Teman-teman organisasi HIMASIF dan grup Ekspansi.id yang mengajarkan
banyak hal dan menemani proses masa studi sehingga lebih bermakna dan
menyenangkan;
11.Seluruh responden yang berpartisipan dalam proses penelitian ini, yang
tidak dapat penulis sebutkan satu persatu.
Penulis menyadari bahwa skripsi ini masih memiliki keterbatasan dan
kekurangan. Oleh karena itu, penulis sangat mengharapkan kritik dan saran yang
membangun demi penyempurnaan karya ini. Semoga skripsi ini dapat memberikan
manfaat bagi pembaca dan menjadi kontribusi bagi pengembangan ilmu
pengetahuan.
Jember, 03 Februari 2026
Eva Oktaviana
DIGITAL REPOSITORY UNIVERSITAS JEMBER
ix

DIGITAL REPOSITORY UNIVERSITAS JEMBER
DAFTAR ISI
PERSEMBAHAN ................................................................................................. i
MOTTO .......................................................................................................... i
PERNYATAAN ORISINALITAS ...................................................................... ii
HALAMAN PERSETUJUAN .......................................................................... iv
ABSTRACT ........................................................................................................ iv
RINGKASAN ..................................................................................................... vi
PRAKATA ...................................................................................................... viii
DAFTAR ISI ........................................................................................................ x
DAFTAR TABEL ............................................................................................. xiii
DAFTAR GAMBAR ........................................................................................ xiii
DAFTAR LAMPIRAN ..................................................................................... xv
BAB 1. PENDAHULUAN .................................................................................. 1
1.1 Latar Belakang ........................................................................................ 1
1.2 Rumusan Masalah ................................................................................... 4
1.3 Tujuan Penelitian .................................................................................... 4
1.4 Manfaat Penelitian .................................................................................. 4
1.5 Batasan Penelitian ................................................................................... 5
BAB 2. TINJAUAN PUSTAKA ......................................................................... 6
2.1 Penelitian Terdahulu ............................................................................... 6
2.2 Landasan Teori ........................................................................................ 8
2.2.1 AI Design Tools ............................................................................. 8
2.2.2 Aplikasi Figma Make .................................................................... 9
2.2.3 Technology Acceptance Model (TAM) ........................................ 10
2.2.4 Expectation Confirmation Model (ECM) .................................... 11
2.2.5 User Experience (UX) ................................................................. 12
2.2.6 Partial Least Square Structural Equation
Modelling (PL-SEM) ................................................................... 12
2.2.7 Generasi Z ................................................................................... 13
BAB 3. METODOLOGI PENELITIAN ......................................................... 14
3.1 Jenis Penelitian...................................................................................... 14
3.2 Objek Penelitian .................................................................................... 14
3.3 Waktu Penelitian ................................................................................... 14
DIGITAL REPOSITORY UNIVERSITAS JEMBER
x

DIGITAL REPOSITORY UNIVERSITAS JEMBER
3.4 Tahapan Penelitian ................................................................................ 14
3.4.1 Identifikasi Masalah dan Studi Literatur ..................................... 15
3.4.2 Penentuan Metode Penelitian ...................................................... 15
3.4.3 Penentuan Variabel dan Definisi Operasional ............................. 15
3.4.4 Penentuan Model Konseptual ...................................................... 16
3.4.5 Penyusunan Hipotesis .................................................................. 17
3.4.6 Penyusunan Populasi dan Sampel ............................................... 17
3.4.7 Penyusunan Instrumen................................................................. 18
3.4.8 Pengujian Instrumen .................................................................... 18
3.4.9 Perbaikan Instrumen .................................................................... 19
3.4.10 Pengumpulan Data .................................................................... 20
3.4.11 Analisis Data ............................................................................. 20
3.4.12 Penyusunan Rekomendasi Perbaikan ........................................ 21
3.4.13 Penarikan Kesimpulan .............................................................. 21
BAB 4. PEMBAHASAN ................................................................................... 22
4.1 Demografi Responden .......................................................................... 22
4.1.1 Distribusi Responden Berdasarkan Jenis Kelamin ...................... 22
4.1.2 Distribusi Responden Berdasarkan Pekerjaan ............................. 22
4.1.3 Distribusi Responden Berdasarkan Frekuensi Penggunaan ........ 22
4.2 Hasil Uji Instrumen ............................................................................... 23
4.2.1 Uji Validitas ................................................................................. 23
4.2.2 Uji Reliabilitas ............................................................................. 27
4.3 Analisis Data ......................................................................................... 28
4.3.1 Hasil Uji Model Fit ...................................................................... 28
4.3.2 Hasil Analisis Struktural Model .................................................. 32
4.3.3 Finalisasi Model Konseptual ....................................................... 34
4.4 Prioritas Perbaikan Figma Make untuk Meningkatkan Niat
Penggunaan Berkelanjutan Generasi Z ................................................. 35
4.4.1 Prioritas Perbaikan Berdasarkan Expectation Confirmation
Model (ECM)............................................................................... 36
4.4.2 Prioritas Perbaikan Berdasarkan Technology Acceptance
Model (TAM) ............................................................................... 36
DIGITAL REPOSITORY UNIVERSITAS JEMBER
xi

DIGITAL REPOSITORY UNIVERSITAS JEMBER
4.4.3 Prioritas Perbaikan Berdasarkan User Experience (UX) ............ 39
4.4.4 Prioritas Perbaikan Berdasarkan Karakteristik AI ....................... 40
BAB 5. PENUTUP ............................................................................................. 42
5.1 Kesimpulan ........................................................................................... 42
5.2 Saran ..................................................................................................... 43
DAFTAR PUSTAKA......................................................................................... 45
LAMPIRAN-LAMPIRAN ............................................................................... 50
DIGITAL REPOSITORY UNIVERSITAS JEMBER
xii

DIGITAL REPOSITORY UNIVERSITAS JEMBER
DAFTAR TABEL
Tabel 3. 1 Skala Likert .......................................................................................... 18
Tabel 3. 2 Indikator Uji Model Fit ........................................................................ 20
Tabel 3. 3 Indikator Analisis Struktural Model .................................................... 20
Tabel 4. 1 Hasil Uji Validitas Konvergen Tahap Pertama .................................... 24
Tabel 4. 2 Hasil Uji Validitas Konvergen Kedua .................................................. 26
Tabel 4. 3 Hasil Uji Reliabilitas............................................................................ 27
Tabel 4. 4 Hasil Uji SRMR ................................................................................... 28
Tabel 4. 5 Hasil Uji R Square (R²) ....................................................................... 30
Tabel 4. 6 Hasil Uji GoF ....................................................................................... 31
Tabel 4. 7 Uji Struktural Model ............................................................................ 32
Tabel 4. 8 Nilai Effect Size .................................................................................... 33
DIGITAL REPOSITORY UNIVERSITAS JEMBER
xiii

DIGITAL REPOSITORY UNIVERSITAS JEMBER
DAFTAR GAMBAR
Gambar 2. 1 Tampilan Figma Make .................................................................... 10
Gambar 2. 2 Metode Technology Acceptance Model (TAM) ............................... 11
Gambar 2. 3 Metode Expectation Confirmation Model (ECM) .......................... 12
Gambar 3. 1 Tahapan Penelitian .......................................................................... 14
Gambar 3. 2 Model Konseptual Awal .................................................................. 17
Gambar 4. 1 Model Konseptual dalam SmartPLS .............................................. 23
Gambar 4. 2 Hasil Outer Loading 1 pada SmartPLS .......................................... 25
Gambar 4. 3 Model Konseptual Akhir ................................................................. 35
DIGITAL REPOSITORY UNIVERSITAS JEMBER
xiv

DIGITAL REPOSITORY UNIVERSITAS JEMBER
DAFTAR LAMPIRAN
Lampiran 1 Definisi Operasional ....................................................................... 50
Lampiran 2 Hipotesis Penelitian ........................................................................ 53
Lampiran 3 Instrumen Penelitian ....................................................................... 56
Lampiran 4 Distribusi Responden ...................................................................... 58
Lampiran 5 Hasil Uji Validitas Diskriminan Cross Loading ............................. 59
Lampiran 6 Hasil Uji Validitas Diskriminan Fornell-Lacker Criterion ............. 60
Lampiran 7 Analisis Hasil Uji Hipotesis ............................................................ 61
Lampiran 8 Identifikasi Jawaban Responden ..................................................... 72
Lampiran 9 Kuesioner Penelitian ....................................................................... 76
Lampiran 10 Dokumentasi Pengumpulan Data ................................................. 77
Lampiran 11 Data Penelitian .............................................................................. 78
DIGITAL REPOSITORY UNIVERSITAS JEMBER
xv

DIGITAL REPOSITORY UNIVERSITAS JEMBER
BAB 1. PENDAHULUAN
1.1 Latar Belakang
Artificial Intelligence (AI) telah menjadi semacam kata kunci yang
ramai diperbincangkan oleh masyarakat dalam beberapa tahun terakhir (Brisco
et al., 2023). Dampak AI terutama terkonsentrasi di bidang-bidang seperti
desain UI/UX, seni, desain industri, desain grafis, dan desain arsitektur (Zhu et
al., 2024). Salah satu aplikasi yang memanfaatkan AI dalam desain adalah
Figma Make. SQ Magazine (2024) mencatat Figma telah memegang pangsa
pasar desain sebesar 40.65%, disusul Adobe XD 13.50%, InVision 7.60%, dan
tools lainnya sebesar 38.25%. Figma Make dirancang guna mendukung desain
antarmuka (UI/UX) dengan mengintegrasikan fitur generatif AI.
Pengguna aplikasi Figma Make berasal dari berbagai kalangan, mulai
dari profesional hingga mahasiswa. Pada bidang pendidikan, implementasi
Figma dapat meningkatkan keterampilan desain grafis, Human Computer
Interaction (HCI), serta teknologi informasi sehingga mampu membantu
mahasiswa (Alfina et al., 2024). Hal ini menunjukkan bahwa mahasiswa,
khususnya Generasi Z, menjadi kelompok yang cepat mengadopsi AI tools
karena terbiasa dengan teknologi digital. Kecenderungan kuat Generasi Z
terhadap pembelajaran visual, akses informasi yang cepat, dan kemampuan
multitasking membuat kalangan tersebut cocok untuk mengadopsi teknologi AI
yang memenuhi preferensi ini (Chan & Lee, 2023).
Survei awal dilakukan pada tanggal 14 November 2025 melalui
platform daring guna mengonfirmasi fenomena adopsi di lapangan yang
dilakukan kepada 50 responden. Hasil survei menunjukkan sebanyak 86%
responden (43 orang) yang merupakan Generasi Z terdiri dari mahasiswa
maupun profesional menyatakan telah mencoba menggunakan Figma Make.
Hal ini menunjukkan tingginya tingkat adopsi awal AI design tools di kalangan
pengguna muda. Hasil temuan juga menunjukkan bahwa Figma Make mampu
meningkatkan efisiensi dalam proses desain. Namun demikian, hasil survei
DIGITAL REPOSITORY UNIVERSITAS JEMBER
1

DIGITAL REPOSITORY UNIVERSITAS JEMBER
2
mengungkap adanya kesenjangan, di mana sebagian responden menilai bahwa
Figma Make belum sepenuhnya memenuhi kebutuhan pengguna. Keterbatasan
teknis, seperti kegagalan fitur prompt dalam menghasilkan desain aplikasi
dengan kompleksitas tinggi serta kualitas output generatif yang tidak konsisten
dengan ekspektasi awal, menjadi permasalahan utama. Kondisi ini
mencerminkan kesenjangan antara adopsi awal yang tinggi dan performa sistem
yang belum optimal sehingga dapat menimbulkan inkonsistensi niat
penggunaan berkelanjutan.
Di sisi lain, penerapan AI dalam aplikasi desain seperti Figma Make
juga memunculkan berbagai kekhawatiran dari perspektif etika dan
profesionalisme, seperti potensi homogenisasi kreativitas, melemahnya peran
subjektivitas desainer manusia, serta ketidaksetaraan akses terhadap teknologi
AI. Penelitian sebelumnya menunjukkan bahwa adopsi generatif AI dalam
praktik desain sering kali disertai dengan persepsi yang beragam dari pengguna,
dimana peningkatan efisiensi berjalan beriringan dengan kekhawatiran terhadap
penurunan kreativitas manusia, kepercayaan terhadap sistem, dan dampak
jangka panjang terhadap profesi desainer (Tsao et al., 2025). Kekhawatiran
tersebut menegaskan bahwa keberlanjutan penggunaan AI design tools tidak
hanya dipengaruhi oleh aspek fungsional, tetapi juga oleh persepsi pengguna
terhadap nilai etika, kepercayaan, dan dampak jangka panjang AI dalam praktik
desain. Oleh karena itu, diperlukan pemahaman yang lebih komprehensif
mengenai faktor-faktor yang memengaruhi niat penggunaan berkelanjutan AI
design tools pada Figma Make. Hal ini sejalan oleh penelitian Fan & Jiang
(2024) yang menyoroti pentingnya menganalisis faktor yang memengaruhi niat
penggunaan berkelanjutan generatif AI terutama dalam bidang desain,
meskipun penelitian tersebut terbatas pada AI drawing tools.
Beragam model teoritis diimplementasikan dalam penelitian mengenai
adopsi teknologi AI guna memahami faktor yang memengaruhi niat
penggunaan berkelanjutan aplikasi oleh pengguna. Salah satu model yang
banyak digunakan yakni Expectation Confirmation Model (ECM) yang
dikembangkan oleh Bhattacherjee pada tahun 2001 (Hariguna et al., 2023).
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
3
ECM berfokus untuk mengukur Confirmation of Expectation (CE) dan
Satisfaction (SAT) terhadap niat penggunaan berkelanjutan, salah satunya pada
teknologi AI baru (Bhattacherjee, 2001b). Model ini sering diintegrasikan
dengan model yang dikembangkan Davis (1989), yakni Technology Acceptance
Model (TAM). Integrasi kedua model ini terbukti efektif dalam menganalisis
niat penggunaan berkelanjutan pada AI design tools, seperti ditunjukkan pada
penelitian Liu Huang (2024) mengenai generatif AI Text-To-Image pada proses
ideasi desain.
Meskipun demikian, penelitian sebelumnya menunjukkan adanya
kekosongan (gap) terkait faktor eksternal yang memengaruhi keberlanjutan
penggunaan AI design tools. Dalam konteks analisis AI, aspek User Experience
(UX) menjadi faktor eksternal yang penting untuk dianalisis. UX dalam konteks
AI telah mengalami peningkatan pesat baik pada praktik maupun penelitian
selama beberapa tahun terakhir. Penelitian terkini telah mengusulkan bahwa
adopsi AI ke dalam desain UX dan Human Computer Interaction (HCI) secara
lebih umum sehingga dapat membawa banyak manfaat (Takafoli et al., 2024).
Penelitian Xu et al. (2024) menyoroti bahwa Emotional Experience (EE) dan
Interactif Experience (IE) memberikan pengaruh positif signifikan terhadap
niat penggunaan berkelanjutan AI painting tools. Selain itu, karakteristik AI
seperti Perceived Trust (PT), Perceived Intelligence (PI), Perceived Novelty
(PN), dan Perceived Playfulness (PP) juga terbukti memengaruhi niat
penggunaan berkelanjutan baik secara langsung maupun melalui variabel
mediasi (Fan & Jiang, 2024). Namun, temuan-temuan ini masih berfokus pada
AI painting dan drawing tools, belum memperluas cakupan pada AI design
tools berbasis UI/UX seperti Figma Make, sehingga meninggalkan ruang
penelitian yang belum dieksplorasi.
Berdasarkan fenomena dan kesenjangan tersebut, penelitian ini menjadi
penting untuk dilakukan. Penelitian ini mengintegrasikan model TAM dan ECM
dengan faktor eksternal UX serta karakteristik AI design tools untuk
mengidentifikasi faktor-faktor yang memengaruhi niat penggunaan
berkelanjutan aplikasi Figma Make. Penelitian ini diuji secara empiris
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
4
menggunakan metode Partial Least Squares Structural Equation Modeling
(PLS-SEM) melalui survei terhadap Generasi Z sebagai kelompok pengadopsi
awal teknologi AI yang memiliki ekspektasi tinggi terhadap kualitas
pengalaman pengguna dan nilai penggunaan sistem (Chan & Lee, 2023).
Karakteristik Generasi Z yang cepat mengadopsi sekaligus cepat meninggalkan
teknologi apabila pengalaman penggunaan tidak memenuhi ekspektasi
menjadikan kelompok ini relevan untuk dikaji. Hasil penelitian diharapkan
tidak hanya memperkuat literatur mengenai adopsi AI dalam desain, tetapi juga
memberikan rekomendasi praktis bagi pengembang dan pemangku kepentingan
dalam meningkatkan niat penggunaan berkelanjutan aplikasi Figma Make.
1.2 Rumusan Masalah
Rumusan masalah pada penelitian ini sebagai berikut:
1. Faktor apa saja yang memengaruhi niat penggunaan berkelanjutan aplikasi
Figma Make berdasarkan hasil uji model-fit integrasi model TAM dan ECM
dengan faktor eksternal UX serta memperhatikan karakteristik AI design
tools pada perspektif Generasi Z?
2. Prioritas perbaikan apa yang perlu diidentifikasi pada aplikasi Figma Make
guna meningkatkan pengalaman pengguna dan niat penggunaan
berkelanjutan berdasarkan perspektif Generasi Z?
1.3 Tujuan Penelitian
Tujuan yang akan dicapai pada penelitian ini sebagai berikut:
1. Mengidentifikasi faktor-faktor yang memengaruhi niat penggunaan
berkelanjutan aplikasi Figma Make berdasarkan hasil uji model-fit integrasi
model TAM dan ECM dengan faktor eksternal UX serta memperhatikan
karakteristik AI design tools pada perspektif Generasi Z.
2. Mengidentifikasi prioritas perbaikan yang dapat dilakukan pada aplikasi
Figma Make untuk meningkatkan pengalaman pengguna dan niat
penggunaan berkelanjutan berdasarkan perspektif Generasi Z.
1.4 Manfaat Penelitian
Manfaat penelitian yang dapat diperoleh dari penelitian ini sebagai berikut:
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
5
1. Bagi Peneliti
Diharapkan dapat memberikan pemahaman mendalam terkait kemampuan
analisis empiris serta implementasi ilmu pengetahuan di bangku
perkuliahan, terutama dalam pengembangan model integrasi TAM dan
ECM, dengan faktor eksternal UX.
2. Bagi Akademis
Diharapkan dapat berkontribusi sebagai studi literatur pada penelitian
selanjutnya, terutama terkait integerasi model TAM dan ECM dengan faktor
eksternal UX serta memperhatikan karakteristik AI design tools.
3. Bagi Objek Penelitian
Diharapkan dapat menyediakan data empiris mengenai faktor yang
memengaruhi niat penggunaan berkelanjutan aplikasi Figma Make sebagai
masukan strategis untuk meningkatkan fitur dan layanan aplikasi.
1.5 Batasan Penelitian
Responden dalam penelitian ini adalah Generasi Z berusia 16 hingga 27
tahun, baik mahasiswa maupun profesional. Penelitian difokuskan pada
pengguna yang telah menggunakan Figma Make minimal selama tiga bulan
terakhir dengan aktivitas desain minimal tiga kali.
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
BAB 2. TINJAUAN PUSTAKA
2.1 Penelitian Terdahulu
Terdapat beberapa penelitian serupa yang telah dilakukan sebelumnya
guna menganalisis faktor yang memengaruhi niat penggunaan berkelanjutan
aplikasi AI design tools, salah satunya penelitian yang dilakukan oleh Xu et al.
(2024) yang terindeks Scopus Q1 dengan judul “Persist or Abandon?
Exploring Chinese Users’ Continuance Intentions Toward AI Painting Tools”.
Penelitian ini dilakukan dengan tujuan untuk mengetahui faktor-faktor yang
memengaruhi niat penggunaan berkelanjutan pada AI design tools, khususnya
bidang AI Painting Tools (AIPT). Penelitian ini dilakukan dengan
mengintegrasikam dua model utama yakni TAM-ECM dengan faktor eksternal
UX dan memperhatikan karakteristik AIPT. Kuesioner disebarkan untuk proses
penelitian kepada pengguna AIPT di Tiongkok dengan total 532 responden.
Data yang terkumpul selanjutnya dianalisis menggunakan PLS-SEM untuk
menguji validitas data. Hasil penelitian ini menunjukkan bahwa model
integrasi TAM-ECM dengan faktor eksternal UX dan memperhatikan
karakteristik AIPT cocok untuk menganalisis niat penggunaan berkelanjutan
aplikasi desain. Faktor Emotional Experience (EE) memiliki pengaruh
signifikan terhadap variabel Continuance Intention (CI), sementara faktor
Satisfaction (SAT), Attitude (AT), Perceived Usefulness (PU), dan Perceived
Trust (PT) berpengaruh positif terhadap variabel Continuance Intention (CI).
Selain itu, karakteristik AIPT berupa Perceived Intelligence (PI) dan Perceived
Novelty (PN) terbukti memengaruhi Continuance Intention (CI) namun secara
tidak langsung, melalui variabel mediasi Perceived Trust (PT) dan Satisfaction
(SAT). Penelitian ini memiliki research gap yakni objek yang digunakan tidak
spesifik pada satu aplikasi AIPT saja. Peneliti merekomendasikan untuk
menguji model dengan spesifik pada satu aplikasi AI, yang diperluas pada alat
kreasi berbasis AI lain, misalnya pada AI design tools.
DIGITAL REPOSITORY UNIVERSITAS JEMBER
6

DIGITAL REPOSITORY UNIVERSITAS JEMBER
7
Penelitian terkait analisis niat penggunaan berkelanjutan aplikasi
desain juga dilakukan oleh Fan & Jiang (2024) yang terindeks scopus Q1
dengan judul “Exploring the Factors Influencing Continuance Intention to Use
AI Drawing Tools: Insights from Designers”. Penelitian ini dilakukan dengan
tujuan memahami faktor-faktor yang memengaruhi niat penggunaan
berkelanjutan desainer, terutama dalam menggunakan AI drawing tools.
Penelitian ini mengintegrasikan model ECM-ISP dengan mempertimbangkan
karakteristik AI drawing tools untuk meninjau niat penggunaan berkelanjutan.
Penelitian ini dilakukan dengan menyebarkan kuesioner dan didapatkan 398
responden. Kemudian data yang diperoleh dianalisis melalui PLS-SEM.
Penelitian ini memperoleh hasil bahwa Perceived Playfulness (PP) memainkan
peranan penting untuk menganalisis niat penggunaan berkelanjutan pada AI
drawing tools. Pada penelitian ini, faktor Subjective Norm (SN) dan Perceived
Risk (PR) juga menunjukkan dampak signifikan, sementara Perceived
Usefullness (PU) tidak memberikan dampak signifikan terhadap niat
penggunaan berkelanjutan. Temuan tersebut menegaskan untuk
mempertimbangkan variabel Perceived Playfulness (PP) dalam proses
penelitian terhadap AI, terutama AI design tools karena berpengaruh penting
terhadap niat penggunaan berkelanjutan.
Selain kedua paper yang telah dibahas, penelitian oleh Yu et al. (2024)
yang berjudul “Users’ Continuance Intention Towards an AI Painting
Application: An Extended Expectation Confirmation Model” terindeks scopus
Q1 juga membahas mengenai niat penggunaan berkelanjutan pada aplikasi AI
design. Pada penelitian ini mengintegrasikan model ECM, TAM, UTAUT, serta
Flow Theory pada objek AI painting tools. Penelitian ini dilakukan dengan
menyebarkan kuesioner dan didapat 443 responden valid dengan rata-rata
pengguna umum aplikasi adalah mahasiswa. Data penelitian kemudian
dianalisis menggunakan SEM (AMOS) dengan uji moderasi SPSS Process.
Hasil penelitian menunjukkan bahwa Satisfaction (SAT), Flow Theory, dan
Social Influence (SI) berpengaruh signifikan terhadap Continuance Intention
(CI). Kemudian Confirmation of Expectation (CE) berpengaruh besar terhadap
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
8
Satisfaction (SAT) dan faktor lainnya. Pada penelitian ini memiliki research
gap yakni belum memperhatikan faktor User Experience (UX) dan Perceived
Trust (PT) selama proses penelitian, sehingga penelitian selanjutnya
disarankan untuk menambahkan variabel tersebut.
Berdasarkan uraian ketiga paper yang telah dianalisis, penelitian ini
mengintegrasikan model TAM-ECM dengan faktor eksternal UX serta
memperhatikan karakteristik AI design tools untuk menganalisis niat
penggunaan berkelanjutan yang didasarkan oleh penelitian sebelumnya oleh
(Xu et al., 2024). Penelitian ini memiliki pembaruan dengan
mengimplementasikan pada AI design tools berdasarkan rekomendasi
penelitian tersebut. Kontruk pada penelitian ini akan menambahkan faktor
eksternal karakteristik AI yakni Perceived Playfulness (PP) yang merujuk pada
penelitian Fan & Jiang (2024) yang menyatakan Perceived Playfulness (PP)
memainkan peranan penting dalam memengaruhi niat penggunaan aplikasi AI.
Selanjutnya, untuk melengkapi research gap pada penelitian Yu et al. (2024),
penelitian ini akan menambahkan karakteristik AI Perceived Trust (PT). Ketiga
paper di atas akan menjadi sumber referensi utama pada proses penelitian
mengenai niat penggunaan berkelanjutan pada aplikasi AI design tools,
khususnya aplikasi Figma Make.
2.2 Landasan Teori
2.2.1 AI Design Tools
Artificial Intelligence (AI) merupakan cabang ilmu pengetahuan dan
rekayasa yang berfokus pada pengembangan mesin dan program cerdas yang
meniru kemampuan kognitif manusia untuk belajar serta menyelesaikan
masalah (Na et al., 2022). AI telah digunakan diberbagai bidang, mulai dari
pendidikan, kesehatan, hingga desain. Dalam bidang desain, AI biasa dikenal
dengan AI design tools, dimana teknologi ini mengintegrasikan generatif AI
yang dapat mendukung pengembangan proses desain, baik dalam bidang
grafis, desain produk, hingga desain antarmuka pengguna (UI/UX). Generatif
AI, sebuah bidang yang berkembang pesat dalam AI, berfokus pada penciptaan
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
9
konten baru seperti teks, gambar, musik, video, dan lainnya (Schönberger,
2025). Sistem Generatif AI berperan penting dalam meningkatkan kreativitas
manusia dan membuka peluang baru dalam bidang desain (Kwon et al., 2024).
Adanya perkembangan pesat AI design tools menghadirkan karakteristik
khas yang membedakan dari alat konvesional. Karakteristik AI design tools
menjadi hal penting untuk mengukur niat penggunaan berkelanjutan teknologi
baru. Penelitian yang dilakukan Xu et al. (2024) diantaranya
mengimplementasikan karakteristik AI yang meliputi Perceived Intelligence
(PI), Perceived Novelty (PN), Perceived Trust (PT). Karakteristik AI juga
diimplementasikan pada penelitian Fan & Jiang (2024) yakni variabel
Perceived Playfulness (PP).
2.2.2 Aplikasi Figma Make
Figma adalah platform desain berbasis website yang memungkinkan
kolaborasi real-time untuk mendesain UI/UX, prototyping, serta
pengembangan produk digital. Lu et al. (2024) menyatakan bahwa Figma
menjadi salah satu alat paling populer untuk prototyping UX. Pada event
tahunan Config 2025, Figma meluncurkan aplikasi baru bernama Figma Make,
yang mengintegrasikan teknologi generatif AI guna mendukung otomatisasi
dalam proses desain (SQ Magazine, 2025). Aplikasi Figma Make menawarkan
berbagai fitur meliputi:
1. Prompt-to-Code, fitur ini membantu pengguna untuk mengubah teks
deskripsi menjadi desain UI bahkan prototype aplikasi yang interaktif
dan bisa dijalankan.
2. Integrasi dengan desain existing, fitur ini membantu pengguna untuk
dapat mengintegrasikan dengan desain yang telah ada sebelumnya
sehingga dapat digunakan dalam file figma.
3. Pengeditan secara interaktif, fitur ini membantu pengguna untuk
mengedit dan mengubah elemen desain secara langsung.
Melalui fitur pada aplikasi Figma Make pengguna dapat dengan mudah untuk
berkolaborasi guna menghasilkan desain yang inovatif sesuai dengan intruksi
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
10
yang diberikan. Tampilan aplikasi Figma Make dapat diamati pada Gambar
2.1.
Gambar 2. 1 Tampilan Figma Make
(Sumber: Figma Make)
2.2.3 Technology Acceptance Model (TAM)
Model Technology Acceptance Model (TAM) yang diperkenalkan oleh
Davis (1989) merupakan kerangka yang digunakan untuk menjelaskan
bagaimana pengguna menerima dan menggunakan suatu teknologi baru. TAM
merupakan hasil adaptasi dari model yang dikembangkan oleh Fishbein dan
Ajzen (1975), yakni model Theory of Reasoned Action (TRA). TAM
didasarkan pada model TRA guna menjelaskan hubungan kausal antara dua
keyakinan utama: Perceived Usefulness, Perceived Ease of Use, serta Users'
Attitudes, Intentions, dan Actual Computer Adoption Behavior (Davis et al.,
1989). Metode TAM juga memiliki fleksibilitas guna mengakomodasi variabel
eksternal untuk ditambahkan guna mengetahui dampak lain dari Perceived
Usefulness dan Perceived Ease of Use. Hal itu sejalan dengan Venkatesh &
Davis (2000) yang yang menunjukkan bahwa penambahan variabel eksternal
pada metode TAM berpengaruh terhadap penerimaan pengguna, sehingga
memiliki peran penting dalam menjelaskan perilaku adopsi. Model TAM dapat
dilihat pada Gambar 2.2, sedangkan definisi untuk setiap variabel pada metode
TAM menurut Davis (1989) sebagai berikut:
1. Perceived Usefulness (PU), mengukur kepercayaan pengguna ketika
menggunakan suatu sistem tertentu akan meningkatkan kinerjanya.
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
11
2. Perceived Ease of Use (PEU), mengukur keyakinan pengguna ketika
menggunakan sistem menjadi lebih mudah.
3. Attitude Toward Using (ATT), mengukur sikap pengguna terhadap
teknologi baru yang digunakan, baik bersifat positif atau negatif.
4. Behavioral Intention (BI), mengukur kekuatan dari pengguna untuk
melakukan perilaku tertentu.
Gambar 2. 2 Metode Technology Acceptance Model (TAM)
(Sumber: Davis, 1989)
2.2.4 Expectation Confirmation Model (ECM)
Expectation Confirmation Model (ECM) adalah hasil modifikasi model
Expectation Confirmation Theory (ECT) yang berfokus untuk menganalisis
keberlanjutan penggunaan teknologi (Bhattacherjee, 2001c). ECT menyatakan
bahwa keinginan pengguna untuk kembali menggunakan suatu produk atau
layanan berangkat dari harapan awal yang mereka miliki. Setelah mencoba,
pengguna menilai kinerja produk atau layanan tersebut dan
membandingkannya dengan harapan awal untuk memutuskan apakah akan
menggunakannya lagi (Bhattacherjee, 2001c). ECM berpendapat bahwa niat
seorang pengguna untuk terus menggunakan sebuah sistem informasi
bergantung pada tiga variabel: User’s Satisfaction, User’s Confirmation of
Expectations, dan Post-Usage Perceived Usefulness (Dwivedi et al., 2012).
Ketiga variabel tersebut saling berkaitan dalam menjelaskan niat
penggunaan berkelanjutan pada teknologi. Confirmation berperan untuk
membandingkan ekspektasi awal pengguna dengan kinerja aktual dari sistem,
yang kemudian memengaruhi tingkat kepuasan pengguna (Satisfaction).
Kepuasan pengguna (Satisfaction) dan persepsi kegunaan (Perceived
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
12
Usefulness) terbukti menjadi faktor penentu utama dalam membentuk niat
penggunaan berkelanjutan. Model ECM dapat dilihat pada Gambar 2.3.
Gambar 2. 3 Metode Expectation Confirmation Model (ECM)
(Sumber: Bhattacherjee, 2001)
2.2.5 User Experience (UX)
User Experience (UX) merupakan efek dari citra merek, presentasi,
fungsionalitas, kinerja sistem, perilaku interaktif, dan kemampuan dari suatu
sistem, produk, atau layanan. Hal ini juga merupakan hasil dari kondisi internal
dan fisik pengguna akibat pengalaman sebelumnya, sikap, keterampilan,
kemampuan, dan kepribadian; serta dari konteks penggunaannya (Nascimento
et al., 2014). UX diartikan sebagai persepsi dan respon individu yang muncul
akibat penggunaan atau perkiraan penggunaan suatu produk, sistem, atau
layanan, termasuk semua Users’ Emotions, Beliefs, Preferences, Perceptions,
Comfort, Behaviours, dan Accomplishments (ISO, 2019). Hal ini sejalan
dengan penelitian yang dilakukan oleh Y. Liu & Wang (2023) dengan
membedakan dimensi User Experience pada platform seni online menjadi
empat, yakni Content Experience, Functional Experience, Interactive
Experience, dan Emotion Experience. Cheng & Jiang (2020) menyimpulkan
bahwa UX sangat penting bagi keberlanjutan penggunaan sebuah alat AI
karena secara langsung memengaruhi loyalitas pengguna dan niat mereka
untuk terus menggunakan alat tersebut.
2.2.6 Partial Least Square Structural Equation Modelling (PL-SEM)
Structural Equation Modelling (SEM) membantu peneliti secara
bersamaan memodelkan serta mengestimasi hubungan kompleks antar
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
13
berbagai variabel dependen dan independen (J. F. Hair et al., 2021). Dua
metode dasar SEM telah diajukan: Covariance-Based Structural Equation
Modeling (CB-SEM) dan Partial Least Squares Structural Equation Modeling
(PLS-SEM, juga disebut Composite-Based Structural Equation Modeling) (J.
Hair & Alamer, 2022). CB-SEM digunakan untuk mengonfirmasi atau
memverifikasi teori yang diuji secara empiris, sementara PLS-SEM lebih
berfokus pada pengembangan teori dalam konteks penelitian yang bersifat
eksploratif (J. F. Hair et al., 2017). Metode PLS-SEM ini telah
diimplementasikan untuk menganalisis teknologi diberbagai bidang, mulai dari
analisis adopsi voice assistance (Fernandes & Oliveira, 2021), teknologi e-
wallet (Al-Saedi et al., 2020), hingga teknologi AI pada bidang desain (Xu et
al., 2024). Dalam metode PLS-SEM terdapat dua komponen utama, yaitu
structural model (inner model) yang menggambarkan hubungan antar variabel
laten berdasarkan landasan teori, serta measurement model (outer model) yang
menjelaskan keterkaitan antara variabel laten dengan indikator atau variabel
manifesnya (Atmojo et al., 2022).
2.2.7 Generasi Z
Generasi Z, yang lahir setelah tahun 1995, merupakan digital natives
dengan tingkat kenyamanan dan ekspektasi tinggi terhadap teknologi digital
(Prensky M, 2001; Jayatissa, 2023). Gen Z memiliki karakteristik seperti
preferensi visual learning, kebutuhan interaksi cepat, serta kecenderungan
mengeksplorasi teknologi baru sebagai sarana ekspresi diri dan kreativitas
(Chan & Lee, 2023). Dalam bidang desain, Figma populer di kalangan Gen Z
karena bersifat kolaboratif, berbasis cloud, dan mudah dipelajari, sehingga
banyak diadopsi dalam pendidikan dan praktik desain (SQ Magazine, 2024;
Alfina et al., 2024). Adopsi teknologi AI, termasuk Figma Make, sejalan
dengan kebutuhan Gen Z akan efisiensi, otomatisasi, dan peningkatan
kreativitas. Namun, keberlanjutan penggunaan teknologi oleh Gen Z tidak
hanya ditentukan oleh adopsi awal, melainkan juga oleh faktor pasca-adopsi
seperti Confirmation of Expectation dan User Satisfaction sebagaimana
dijelaskan dalam model ECM (Bhattacherjee, 2001b).
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
BAB 3. METODOLOGI PENELITIAN
3.1 Jenis Penelitian
Penelitian ini menggunakan jenis penelitian kuantitatif, dimana penelitian
kuantitatif diartikan sebagai metode penelitian yang pada filsafat positivisme,
digunakan untuk meneliti pada populasi atau sampel tertentu, pengumpulan data
menggunakan instrumen penelitian, analisis data bersifat kuantitatif/statistik,
dengan tujuan untuk menguji hipotesis yang telah ditetapkan (Sugiyono, 2013).
3.2 Objek Penelitian
Objek yang digunakan pada penelitian ini adalah aplikasi Figma Make, yang
merupakan tools desain dengan Artificial Intelligence untuk pembuatan UI/UX
yang resmi dirilis pada tanggal 07 Mei 2025.
3.3 Waktu Penelitian
Waktu penelitian ini akan dimulai pada bulan Oktober 2025 dan berlangsung
selama periode 4 bulan, hingga Januari 2026. Selama periode tersebut, setiap tahap
akan dilaksakan secara sistematis sehingga menghasilkan penelitian yang valid,
reliabel, serta sesuai dengan tujuan penelitian.
3.4 Tahapan Penelitian
Rincian tahapan pada proses pelaksanaan penelitian yang akan dilaksanakan
dapat diamati pada Gambar 3.1.
Gambar 3. 1 Tahapan Penelitian
DIGITAL REPOSITORY UNIVERSITAS JEMBER
14

DIGITAL REPOSITORY UNIVERSITAS JEMBER
15
3.4.1 Identifikasi Masalah dan Studi Literatur
Penelitian dimulai dengan melakukan identifikasi masalah berkaitan
dengan niat keberlanjutan penggunaan aplikasi AI untuk desain. Identifikasi
masalah dilakukan melalui survei online menggunakan google form, studi
literatur pada berbagai sumber jurnal yang terindeks scopus, serta melalui
sumber referensi terkait. Survei menunjukkan meskipun banyak kalangan
pengguna Figma Make dari Generasi Z, namun aplikasi tersebut masih belum
memenuhi kebutuhan pengguna secara menyeluruh serta terdapat keterbatasan
teknis. Studi literatur menunjukkan hasil bahwa beberapa penelitian yang telah
dilakukan, niat keberlanjutan penggunaan aplikasi AI pada bidang desain
dipengaruhi oleh berbagai faktor. Berdasarkan identifikasi masalah dan studi
literatur yang dilakukan, akan menjadi dasar merumuskan pertanyaan serta
mengembangkan kerangka teoritis guna menganalisis faktor-faktor yang
memengaruhi niat penggunaan berkelanjutan aplikasi Figma Make melalui
metode TAM-ECM dengan faktor eksternal UX serta memperhatikan
karakteristik AI design tools.
3.4.2 Penentuan Metode Penelitian
Penentuan metode penelitian merupakan solusi yang digunakan untuk
menjawab permasalahan berdasarkan identifikasi masalah yang telah
dilakukan. Berdasarkan studi literatur yang dilakukan, peneliti menggunakan
metode TAM oleh Davis F.D (1989) yang diintegrasikan dengan ECM oleh
Bhattacherjee (2001) guna menjawab permasalahan yang ada. Peneliti juga
menambahkan faktor eksternal UX serta memperhatikan karakteristik AI
design tools pada penelitian ini.
3.4.3 Penentuan Variabel dan Definisi Operasional
Penentuan variabel pada penelitian ini mengadopsi dan memodifikasi
model integrasi TAM dan ECM dengan faktor eksternal UX dan karakteristik
AI design tools berdasarkan penelitian oleh (Xu et al., 2024). Modifikasi model
pada penelitian ini dilakukan dengan menambahkan karakteristik AI yakni
Perceived Playfulness (PP) yang didasarkan pada penelitian (Fan & Jiang,
2024). Berdasarkan penelitian tersebut mengemukakan hasil bahwa Perceived
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
16
Playfulness (PP) berpengaruh signifikan terhadap niat penggunaan
berkelanjutan pada layanan AI desain. Oleh karena itu terdapat 11 variabel
laten pada penelitian ini, meliputi:
1. Model TAM Inti: Perceived Usefulness (PU), Attitude Toward Using
(ATT)
2. Model ECM Inti: Confirmation of Expectation (CE), Satisfaction
(SAT), Continuance Intention (CI)
3. Faktur Eksternal UX: Emotional Experience (EE), Interactive
Experience (IE)
4. Karakteristik AI desain: Perceived Playfulness (PP), Perceived
Novelty (PN), Perceived Trust (PT), Perceived Intelligence (PI)
Pada penelitian ini, metode TAM berfokus pada variabel Perceived
Usefulness (PU) dan Attitude (ATT). Hal ini karena berdasarkan beberapa studi
empiris dari penelitian terdahulu, variabel PU dan ATT sudah cukup kuat untuk
menjelaskan niat penggunaan berkelanjutan terhadap aplikasi, sebab variabel
PU memiliki pengaruh langsung terhadap ATT (Davis F.D,1989). Sedangkan
metode ECM berfokus pada variabel CE, SAT, dan CI karena berdasarkan
penelitian Xu et al. (2024), variabel tersebut berpengaruh positif dan signifikan
terhadap niat penggunaan berkelanjutan, terutama pada konteks AI desain.
Definisi operasional variabel serta indikator yang digunakan pada penelitian
ini dapat dilihat pada Lampiran 1.
3.4.4 Penentuan Model Konseptual
Penyusunan model konseptual dibuat berdasarkan penelitian yang telah
dilakukan oleh Xu et al. (2024) dan Yu et al. (2024) yang mengintegrasikan
metode TAM-ECM dengan faktor eksternal UX serta memperhatikan
karakteristik dari AI design tools berupa Perceived Intelligence (PI), Perceived
Novelty (PN), Perceived Trust (PT). Selain itu, penyusunan model konseptual
ini juga menambahkan variabel eksternal berdasarkan penelitian oleh Fan &
Jiang (2024) yakni Perceived Playfulness (PP). Berdasarkan model konseptual
ini, total terdapat 11 variabel dengan 38 indikator. Model konseptual yang telah
dibuat dapat dilihat pada Gambar 3.2.
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
17
Gambar 3. 2 Model Konseptual Awal
3.4.5 Penyusunan Hipotesis
Penyusunan hipotesis dilakukan berdasarkan model konseptual yang
telah dibuat. Hipotesis ini merupakan pengembangan asumsi yang kemudian
didukung oleh penelitian terdahulu yang telah diuji secara empiris. Hipotesis
yang telah dibuat nantinya akan diuji. Hipotesis yang digunakan pada
penelitian ini terdapat pada Lampiran 2.
3.4.6 Penyusunan Populasi dan Sampel
Pada penelitian ini, populasi yang digunakan adalah pengguna aktif
Generasi Z pada aplikasi Figma Make di seluruh Indonesia. Populasi ini dipilih
karena Generasi Z cenderung menjadi kelompok pengguna yang terbiasa untuk
menggunakan platform khususnya AI design tools. Ukuran sampel yang
digunakan pada penelitian ini mengacu pada Jr et al. (2018), yang menyatakan
bahwa ukuran sampel setidaknya harus 5 kali lebih banyak dibandingkan
dengan jumlah variabel yang dianalisis, namun disarankan untuk
menggunakan ukuran sampel dengan rasio 10:1. Oleh karena itu, karena
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
18
penelitian ini memiliki 11 variabel, sehingga jumlah ukuran sampel yang
digunakan adalah 10 x 11 = 110 sampel.
Metode pengambilan sampel pada penelitian ini menggunakan
nonprobability sampling. Sugiyono (2013) menjelaskan bahwa nonprobability
sampling adalah teknik pengambilan sampel dimana setiap anggota populasi
tidak diberikan peluang yang sama untuk dipilih sebagai sampel. Metode ini
memiliki beberapa teknik, salah satunya purposive sampling, yang mana
penentuan sampel dilakukan berdasarkan kriteria atau tujuan tertentu yang
linier dengan fokus penelitian. Kriteria sampel untuk penelitian ini yakni
generasi Z berusia 16 hingga 27 tahun, baik mahasiswa maupun profesional.
Penelitian difokuskan pada pengguna yang telah menggunakan Figma Make
minimal selama tiga bulan terakhir dengan aktivitas desain minimal tiga kali.
3.4.7 Penyusunan Instrumen
Penyusunan instrumen dilakukan berdasarkan dengan variabel dan
indikator yang telah disusun, kemudian item disesuaikan dengan objek yang
akan digunakan pada penelitian, yakni aplikasi Figma Make. Instrumen yang
digunakan pada penelitian ini menggunakan skala likert 1-4 yang mengacu
pada Chyung (2017), dengan tujuan untuk mengurangi bias terhadap jawaban
netral dari responden. Skala likert yang digunakan dalam penelitian terdapat
pada Tabel 3.1. Instrumen pada penelitian ini dapat ditinjau pada Lampiran 3.
Tabel 3. 1 Skala Likert
Skala Pernyataan
1 Sangat Tidak Setuju (STS)
2 Tidak Setuju (TS)
3 Setuju (S)
4 Sangat Setuju (SS)
3.4.8 Pengujian Instrumen
Pengujian instrumen dilakukan dengan tujuan memastikan instrumen
benar-benar bisa mengukur terhadap pertanyaan kuesioner yang digunakan
dalam penelitian. Guna menguji kelayakan tersebut, akan disebarkan kuesioner
terhadap 30 responden dari populasi berdasarkan kriteria responden yang telah
ditetapkan. Ukuran sampel minimum setidaknya 30 responden biasanya sudah
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
19
cukup untuk menilai keandalan kuesioner (Bujang et al., 2024). Berikut adalah
cakupan tahap uji instrumen:
A. Uji Validitas
Uji validitas ditinjau berdasarkan nilai validitas konvergen dan
validitas diskriminan. Berdasarkan J. F. Hair et al. (2017) mengenai uji
validitas konvergen dilihat dari nilai outer loading maupun Average
Variance Extracted (AVE). Melalui validitas konvergen dapat dilihat
apakah konstruk dapat menjelaskan varian terhadap indikatornya. Nilai
outer loading harus > 0,7 sehingga dapat menjelaskan varian terhadap
indikatornya, sedangkan nilai AVE minimal harus > 0,5. Validitas
diskriminan bertujuan untuk menilai apakah suatu konstruk benar-benar
berbeda satu sama lain berdasarkan standar empiris. Parameter validitas
diskriminan ini dilihat berdasarkan cross-loading (> 0,7) dan Fornell-
Larcker Criterion.
B. Uji Reliabilitas
Uji reliabilitas berfungsi untuk menilai instrumen penelitian
memiliki tingkat akurasi yang baik serta konsisten. Uji reliabilitas
dinilai berdasarkan Cronbach’s Alpha (CA) dan Composite Reliability
(CR). Mengacu pada J. F. Hair et al. (2017), nilai Cronbach’s Alpha
(CA) dan Composite Reliability (CR) harus sama-sama > 0,7.
3.4.9 Perbaikan Instrumen
Tahapan penelitian selanjutnya, setelah melakukan uji instrumen yakni
melakukan perbaikan intrumen. Perbaikan dilakukan pada hasil uji dengan data
yang tidak valid dan reliabel. Apabila terdapat indikator yang tidak memenuhi
kriteria uji validitas dan reliabilitas, maka bisa dilakukan revisi terhadap
redaksi pertanyaan pada kuesioner sehingga bisa lebih jelas dan relevan
terhadap indikator. Kemudian setelah perbaikan instrumen, dilakukan
pengujian ulang dan apabila instrumen tetap tidak valid bisa dilakukan
penghapusan indikator tersebut.
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
20
3.4.10 Pengumpulan Data
Proses pengumpulan data dilakukan dengan menyebarkan kuesioner
yang telah disusun menggunakan google form terhadap responden, yakni
pengguna Figma Make dengan kriteria yang telah ditentukan. Jumlah
responden yang ditargetkan yakni 110 sesuai dengan ukuran sampel yang telah
dihitung.
3.4.11 Analisis Data
Pada tahap ini, dilakukan proses pengolahan data. Data yang terkumpul
dari hasil kuesioner kemudian dilakukan untuk mengetahui pengaruh variabel
berdasarkan model yang telah dibuat. Analisis dilakukan menggunakan
SmartPLS versi 4.0.0.9, perangkat lunak PLS-SEM yang menyediakan
antarmuka lebih intuitif, fitur visualisasi model yang lebih komprehensif, serta
kemampuan analisis yang lebih cepat dan stabil.
A. Uji Model Fit
Uji model fit bertujuan untuk mengukur model penelitian yang
telah dibangun telah sesuai dengan hubungan antarvariabel sebenarnya.
Kesesuaian model fit umumnya dinilai berdasarkan 3 indikator
parameter (J. F. Hair et al., 2017):
Tabel 3. 2 Indikator Uji Model Fit
Indikator Parameter Ketentuan
Standardized Root Mean Square Residual <0,08 fit
(SRMR) 0,08 – 0,10 Marginal Fit
Goodness-of-Fit Index (GoF) 0,1 = Rendah,
0,25 = Sedang
0,36 = Tinggi
Koofisien Determinasi (R2) R2 > 0,67 = Kuat
R2 ≤ 0,67 = Sedang
R2 ≤ 0,19 = Lemah
B. Analisis Struktural Model
Analisis Struktural Model bertujuan untuk menguji hubungan antar
variabel sesuai dengan hipotesis yang telah dibuat. Kesesuaian
struktural model umumnya dinilai berdasarkan empat parameter (J. F.
Hair et al., 2017):
Tabel 3. 3 Indikator Analisis Struktural Model
Indikator Parameter Ketentuan
T-Statistic & P-Value T-Statistic ≥ 1,96 memiliki pengaruh signifikan
P-Value ≤ 0,05 menunjukkan hubungan signifikan antar variabel
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
21
Original Sample (O) Menunjukkan arah serta besarnya pengaruh antar konstruk
Effect Size (f2) f2 < 0,02 = No effect
f2 ≥ 0,02 = Memiliki pengaruh kecil,
f2 ≥ 0,15 = Memiliki pengaruh sedang
f2 ≥ 0,35 = Memiliki pengaruh besar
Koofisien Determinasi R2 > 0,67 = Kuat
(R2) R2 ≤ 0,67 = Sedang
R2 ≤ 0,19 = Lemah
3.4.12 Penyusunan Rekomendasi Perbaikan
Hasil analisis dari data yang telah dikumpulkan mengenai niat
penggunaan berkelanjutan aplikasi Figma Make, kemudian disusun menjadi
rekomendasi. Hasil temuan penelitian ini bertujuan untuk mengetahui titik
prioritas perbaikan yang dapat dilakukan terhadap aplikasi Figma Make guna
meningkatkan efektivitas dan efisiensi sistem.
3.4.13 Penarikan Kesimpulan
Penarikan kesimpulan diambil berdasarkan analisis hasil dan
pembahasan. Pada kesimpulan ini memuat jawaban dari rumusan masalah
terhadap penelitian yang dilakukan. Selain itu, pada tahap penarikan
kesimpulan ini juga disertakan kontribusi teoritis dari penelitian.
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
BAB 4. HASIL DAN PEMBAHASAN
4.1 Demografi Responden
Data demografi bertujuan untuk menganalisis responden yang menjadi sampel
pada penelitian ini. Proses pengumpulan data dilakukan melalui penyebaran
kuesioner menggunakan sosial media seperti WhatsApp, Instagram, X, Facebook,
serta Telegram sesuai dengan karakteristik responden yang dibutuhkan.
Pengumpulan data dilakukan selama kurang lebih empat minggu mulai dari 14
Desember 2025 hingga 10 Januari 2026. Penelitian ini melibatkan 124 responden
yang telah melampaui batas minimum sebanyak 110 sampel. Penambahan jumlah
sampel ini dilakukan untuk mengakomodasi kompleksitas model yang dapat
memengaruhi uji model fit. Analisis data menggunakan nonprobability sampling
dengan pendekatan purposive sampling. Berikut adalah demografi responden
berdasarkan data yang telah terkumpul:
4.1.1 Distribusi Responden Berdasarkan Jenis Kelamin
Data distribusi responden berdasarkan jenis kelamin terdiri dari 39 orang
(31,5%) laki-laki dan 85 orang (68,5%) perempuan. Diagram demografi
berdasarkan jenis kelamin terdapat pada Lampiran 4.
4.1.2 Distribusi Responden Berdasarkan Pekerjaan
Data distribusi responden berdasarkan pekerjaan didominasi oleh
kelompok mahasiswa dengan jumlah responden 113 orang (91,1%). Selain itu
terdapat 8 orang (6,5%) freelancer, 2 orang (1,6%) desainer professional, dan
1 orang (0,8%) memiliki pekerjaan lainnya. Diagram demografi berdasarkan
pekerjaan terdapat pada Lampiran 4.
4.1.3 Distribusi Responden Berdasarkan Frekuensi Penggunaan Aplikasi
Figma Make
Data distribusi responden berdasarkan frekuensi penggunaan aplikasi
Figma Make terdiri dari 79 orang (63,7%) menggunakan 3-5 kali, 24 orang
(19,4%) menggunakan lebih dari 10 kali, dan 21 orang (16,9%) menggunakan
DIGITAL REPOSITORY UNIVERSITAS JEMBER
22

DIGITAL REPOSITORY UNIVERSITAS JEMBER
23
6-10 kali. Diagram demografi berdasarkan frekuensi penggunaan aplikasi
Figma Make terdapat pada Lampiran 4.
4.2 Hasil Uji Instrumen
Gambar 4. 1 Model Konseptual dalam SmartPLS
Pengujian instrumen dilakukan guna memastikan indikator yang digunakan
dalam penelitian valid dan reliabel untuk keakuratan pada tahapan selanjutnya.
Proses pengujian instrumen menggunakan aplikasi SmartPLS versi 4.0.0.9
Pengujian instrumen ini melibatkan 34 responden berdasarkan sampel dengan
kriteria yang telah ditentukan. Model konseptual yang telah dibentuk pada
SmartPLS terdapat pada Gambar 4.1.
4.2.1 Uji Validitas
Uji validitas dalam penelitian ini dilakukan melalui dua parameter, yakni
uji validitas konvergen dan validitas diskriminan. Uji validitas konvergen
dievaluasi menggunakan nilai outer loading dan AVE, sedangkan uji validitas
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER 24

diskriminan  dianalisis  melalui  nilai  cross  loading  dan  Fornell  Lacker
Criterion.
  Uji Validitas Konvergen
A.
Hasil uji validitas konvergen dianalisis berdasarkan nilai outer loading
dan AVE. J. F. Hair et al. (2022) menyatakan bahwa pada outer loading,
indikator dengan nilai lebih dari 0,70 dapat diterima, sedangkan indikator
dengan nilai 0,40 – 0,70 dapat dipertimbangkan untuk dihapus. Hal ini
karena nilai tersebut tidak sesuai dengan ambang batas yang ditentukan.
Kemudian, nilai AVE minimal guna memenuhi syarat yakni > 0,50. Nilai
AVE yang menunjukkan lebih dari 0,50 dapat diartikan bahwa variabel
mampu  menjelaskan  50  persen  atau  lebih  dari  varians  indikator  yang
membentuk variabel tersebut. Hasil uji validitas konvergen dapat dilihat
pada Tabel 4.1.
Tabel 4. 1 Hasil Uji Validitas Konvergen Tahap Pertama
| Variabel        | Kode  | Outer Loading  | Keterangan  | AVE    | Keterangan  |
| --------------- | ----- | -------------- | ----------- | ------ | ----------- |
| Attitude        | ATT1  | 0,721          | Valid       | 0,736  | Valid       |
| Toward Using    | ATT2  | 0,939          | Valid       |        |             |
|                 | ATT3  | 0,898          | Valid       |        |             |
| Confirmation    | CE1   | 0,878          | Valid       | 0,678  | Valid       |
| of Expectation  | CE2   | 0,874          | Valid       |        |             |
|                 | CE3   | 0,707          | Valid       |        |             |
| Continuance     | CI1   | 0,847          | Valid       | 0,711  | Valid       |
Intention
|            | CI2  | 0,937  | Valid  |        |        |
| ---------- | ---- | ------ | ------ | ------ | ------ |
|            | CI3  | 0,734  | Valid  |        |        |
| Emotional  | EE1  | 0,854  | Valid  | 0,726  | Valid  |
Experience
|              | EE2  | 0,962  | Valid  |        |        |
| ------------ | ---- | ------ | ------ | ------ | ------ |
|              | EE3  | 0,723  | Valid  |        |        |
| Interactive  | IE1  | 0,859  | Valid  | 0,662  | Valid  |
Experience
|     | IE2  | 0,801  | Valid  |        |        |
| --- | ---- | ------ | ------ | ------ | ------ |
|     | IE3  | 0,780  | Valid  |        |        |
|     | PI1  | 0,787  | Valid  | 0,572  | Valid  |
Perceived
| Intelligence  | PI2  | 0,827  | Valid        |        |        |
| ------------- | ---- | ------ | ------------ | ------ | ------ |
|               | PI3  | 0,553  | Tidak Valid  |        |        |
|               | PI4  | 0,819  | Valid        |        |        |
|               | PI5  | 0,762  | Valid        |        |        |
| Perceived     | PN1  | 0,773  | Valid        | 0,677  | Valid  |
| Novelty       | PN2  | 0,880  | Valid        |        |        |
|               | PN3  | 0,727  | Valid        |        |        |
|               | PN4  | 0,899  | Valid        |        |        |
| Perceived     | PP1  | 0,801  | Valid        | 0,687  | Valid  |
Playfulness
|            | PP2  | 0,854  | Valid  |        |        |
| ---------- | ---- | ------ | ------ | ------ | ------ |
|            | PP3  | 0,832  | Valid  |        |        |
| Perceived  | PT1  | 0,853  | Valid  | 0,704  | Valid  |
Trust
|     | PT2  | 0,852  | Valid  |     |     |
| --- | ---- | ------ | ------ | --- | --- |

|     | PT3  | 0,811  | Valid  |        |        |
| --- | ---- | ------ | ------ | ------ | ------ |
|     | PT4  | 0,839  | Valid  |        |        |
|     | PU1  | 0,784  | Valid  | 0,680  | Valid  |
Perceived
| Usefulness    | PU2   | 0,891  | Valid  |        |        |
| ------------- | ----- | ------ | ------ | ------ | ------ |
|               | PU3   | 0,873  | Valid  |        |        |
|               | PU4   | 0,742  | Valid  |        |        |
| Satisfaction  | SAT1  | 0,813  | Valid  | 0,728  | Valid  |
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
25
SAT2 0,930 Valid
SAT3 0,810 Valid
Berdasarkan pengujian pertama uji validitas konvergen pada Tabel 4.1,
indikator PI3 memiliki nilai outer loading sebesar 0,553. Indikator tersebut
menyatakan “Saya merasa aplikasi Figma Make membantu menyelesaikan
tugas dengan cepat”. Nilai 0,553 berada dalam rentang 0,40–0,70, sehingga
indikator tersebut dianggap kurang merepresentasikan variabel Perceived
Intelligence (PI) secara optimal. Oleh karena itu, indikator PI3 dapat
dihapus dari model penelitian ini. Setelah penghapusan indikator tersebut,
variabel PI direfleksikan oleh 4 indikator lainnya yakni PI1, PI2, PI4, dan
PI5. Hasil uji validitas konvergen setelah dilakukan penghapusan indikator
PI3 dapat dilihat pada Tabel 4.2.
Gambar 4. 2 Hasil Outer Loading 1 pada SmartPLS
Pada pengujian kedua uji validitas konvergen yang ditunjukkan Tabel
4.2, telah dilakukan penghapusan pada indikator PI3 dan menunjukkan nilai
valid. Penghapusan indikator PI3 yang memiliki nilai outer loading di
bawah 0,70 menyebabkan terjadinya redistribusi varians pada variabel PI.
DIGITAL REPOSITORY UNIVERSITAS JEMBER

| DIGITAL REPOSITORY UNIVERSITAS JEMBER |     |     |     |     | 26  |
| ------------------------------------- | --- | --- | --- | --- | --- |

Hal  ini  berdampak  pada  meningkatnya  nilai  outer  loading  beberapa
indikator yang lebih representatif terhadap konstruk, yaitu PI1, PI4, dan PI5.
Sementara  itu,  indikator  PI2  mengalami  sedikit  penurunan  nilai  outer
loading, yang disebabkan oleh hilangnya varians bersama dengan indikator
PI3 yang secara konseptual memiliki kemiripan. Meskipun demikian, nilai
outer loading PI2 tetap berada di atas ambang batas 0,70, sehingga indikator
tersebut masih dinyatakan valid dan layak dipertahankan. Berdasarkan tabel
tersebut, penelitian ini lulus uji validitas konvergen outer loading dan AVE.
Tabel 4. 2 Hasil Uji Validitas Konvergen Kedua
Outer Loading
| Variabel  | Kode  |        | Keterangan  | AVE    | Keterangan  |
| --------- | ----- | ------ | ----------- | ------ | ----------- |
| Attitude  | ATT1  | 0,721  | Valid       | 0,736  | Valid       |
Toward Using
|     | ATT2  | 0,939  | Valid  |        |        |
| --- | ----- | ------ | ------ | ------ | ------ |
|     | ATT3  | 0,898  | Valid  |        |        |
|     | CE1   | 0,878  | Valid  | 0,678  | Valid  |
Confirmation
| of Expectation  | CE2  | 0,874  | Valid  |        |        |
| --------------- | ---- | ------ | ------ | ------ | ------ |
|                 | CE3  | 0,707  | Valid  |        |        |
| Continuance     | CI1  | 0,846  | Valid  | 0,711  | Valid  |
| Intention       | CI2  | 0,937  | Valid  |        |        |
|                 | CI3  | 0,734  | Valid  |        |        |
| Emotional       | EE1  | 0,854  | Valid  | 0,726  | Valid  |
| Experience      | EE2  | 0,962  | Valid  |        |        |
|                 | EE3  | 0,723  | Valid  |        |        |
| Interactive     | IE1  | 0,859  | Valid  | 0,662  | Valid  |
Experience
|            | IE2  | 0,801  | Valid  |        |        |
| ---------- | ---- | ------ | ------ | ------ | ------ |
|            | IE3  | 0,780  | Valid  |        |        |
| Perceived  | PI1  | 0,803  | Valid  | 0,650  | Valid  |
Intelligence
|     | PI2  | 0,796  | Valid  |        |        |
| --- | ---- | ------ | ------ | ------ | ------ |
|     | PI4  | 0,834  | Valid  |        |        |
|     | PI5  | 0,790  | Valid  |        |        |
|     | PN1  | 0,773  | Valid  | 0,677  | Valid  |
Perceived
| Novelty      | PN2  | 0,880  | Valid  |        |        |
| ------------ | ---- | ------ | ------ | ------ | ------ |
|              | PN3  | 0,727  | Valid  |        |        |
|              | PN4  | 0,899  | Valid  |        |        |
| Perceived    | PP1  | 0,801  | Valid  | 0,687  | Valid  |
| Playfulness  | PP2  | 0,854  | Valid  |        |        |
|              | PP3  | 0,832  | Valid  |        |        |
| Perceived    | PT1  | 0,851  | Valid  | 0,704  | Valid  |
| Trust        | PT2  | 0,857  | Valid  |        |        |

|            | PT3  | 0,809  | Valid  |        |        |
| ---------- | ---- | ------ | ------ | ------ | ------ |
|            | PT4  | 0,839  | Valid  |        |        |
| Perceived  | PU1  | 0,784  | Valid  | 0,680  | Valid  |
Usefulness
|     | PU2  | 0,891  | Valid  |     |     |
| --- | ---- | ------ | ------ | --- | --- |
|     | PU3  | 0,873  | Valid  |     |     |
|     | PU4  | 0,742  | Valid  |     |     |
Satisfaction
|     | SAT1  | 0,813  | Valid  | 0,728  | Valid  |
| --- | ----- | ------ | ------ | ------ | ------ |
|     | SAT2  | 0,930  | Valid  |        |        |
|     | SAT3  | 0,810  | Valid  |        |        |

B. Uji Validitas Diskriminan
Hasil uji validitas diskriminan memiliki dua parameter yakni nilai cross
loading dan Fornell Lacker Criterion. Nilai cross loading pada indikator
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER 27

harus  lebih  tinggi  terhadap  variabelnya  sendiri  dibandingkan  indikator
tersebut terhadap variabel lainnya. Hasil uji validitas diskriminan dapat
dilihat pada Lampiran 5. Berdasarkan lampiran tersebut, menunjukkan
bahwa setiap indikator memiliki nilai lebih tinggi pada variabelnya sendiri
dibandingkan pada variabel lainya. Hal ini dapat diartikan bahwa indikator
memiliki korelasi yang kuat dengan variabel sendiri  dibanding dengan
variabel lainnya, sehingga pada penelitian ini lulus uji validitas diskriminan
cross loading.
Uji  Fornell-Lacker  Criterion  dinilai  dengan  membandingan  akar
kuadrat AVE dengan korelasi antar variabel latennya. Syarat yang harus
dipenuhi yakni akar kuadrat dari AVE pada suatu variabel harus lebih tinggi
dibandingkan dengan nilai korelasi terhadap variabel lain. Hasil uji Fornell-
Lacker Criterion dapat dilihat pada Lampiran 6. Berdasarkan lampiran
tersebut menunjukkan bahwa setiap variabel memiliki nilai akar kuadrat
lebih tinggi pada variabelnya sendiri dibandingkan pada variabel lainnya,
sehingga pada penelitian ini lulus uji diskriminan Fornell-Lacker Criterion.

4.2.2 Uji Reliabilitas
Hasil  uji  reliabilitas  dinilai  melalui  Cronbach’s  Alpha  (CA)  dan
Composite Reliability (CR). Masing-masing instrumen harus lebih dari 0,7 agar
variabel dinyatakan reliabel. Hasil uji reliabilitas penelitian ini dapat dilihat
pada Tabel 4.3.
Tabel 4. 3 Hasil Uji Reliabilitas
|     | Cronbach's alpha  | Composite  | Nilai Kritis  | Keterangan  |
| --- | ----------------- | ---------- | ------------- | ----------- |
reliability (rho_A)
| ATT  | 0,822  | 0,917  | 0,7  | Reliabel  |
| ---- | ------ | ------ | ---- | --------- |
| CE   | 0,758  | 0,774  | 0,7  | Reliabel  |
| CI   | 0,817  | 1,058  | 0,7  | Reliabel  |
| EE   | 0,832  | 1,351  | 0,7  | Reliabel  |
| IE   | 0,750  | 0,782  | 0,7  | Reliabel  |
| PI   | 0,820  | 0,821  | 0,7  | Reliabel  |
| PN   | 0,848  | 0,878  | 0,7  | Reliabel  |
| PP   | 0,774  | 0,777  | 0,7  | Reliabel  |
| PT   | 0,860  | 0,861  | 0,7  | Reliabel  |
| PU   | 0,842  | 0,868  | 0,7  | Reliabel  |
| SAT  | 0,810  | 0,825  | 0,7  | Reliabel  |

Berdasarkan tabel di atas menunjukkan bahwa semua variabel penelitian
yang digunakan memiliki nilai lebih besar dari 0.7 baik pada Cronbach’s Alpha
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
28
(CA) dan Composite Reliability (CR). Hal tersebut menunjukkan bahwa
indikator memiliki tingkat konsistensi yang baik dalam mendeskripsikan
variabel latennya, sehingga mengindikasikan bahwa penelitian ini lulus uji
reliabilitas Cronbach’s Alpha (CA) dan Composite Reliability (CR). Kemudian,
setelah melakukan uji instrumen terkait validitas dan reliabilitas, selanjutnya
dilakukan uji model fit guna mengetahui kesesuaian model.
4.3 Analisis Data
4.3.1 Hasil Uji Model Fit
Evaluasi model fit dalam penelitian ini dilakukan dengan menggunakan
pendekatan Partial Least Squares–Structural Equation Modeling (PLS-SEM).
J. F. Hair et al. (2014) menyatakan bahwa berbeda dengan pendekatan
Covariance-Based SEM (CB-SEM) yang berorientasi pada konfirmasi teori
melalui pemodelan kovarians, PLS-SEM tidak menitikberatkan evaluasi pada
global fit model melainkan pada kemampuan prediktif model dan kualitas
konstruk, dimana tujuannya adalah untuk memaksimalkan varians yang
dijelaskan pada variabel laten dependen. Oleh karena itu, penilaian model fit
dilakukan secara komprehensif dengan mempertimbangkan Standardized Root
Mean Square Residual (SRMR), nilai R Square (R²), serta Goodness of Fit
(GoF).
A. Uji Standardized Root Mean Square Residual (SRMR)
Hasil uji SRMR dapat dilihat pada Tabel 4.4 berikut:
Tabel 4. 4 Hasil Uji SRMR
SRMR Keterangan
Saturated 0.065 Fit
Estimated 0.123 Marginal Fit
SRMR merupakan ukuran approximate model fit yang
merepresentasikan rata-rata perbedaan terstandarisasi antara matriks
korelasi empiris dan matriks korelasi yang diimplikasikan oleh model.
Dalam konteks PLS-SEM, SRMR digunakan sebagai indikator pendukung
kesesuaian model dan bukan sebagai uji kelayakan absolut, sebagaimana
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
29
yang berlaku pada CB-SEM (Henseler et al., 2016). Nilai SRMR <0,08
masuk pada kategori fit serta 0,08 - 0,10 kategori marginal fit.
Berdasarkan tabel tersebut, diperoleh nilai SRMR sebesar 0,065 pada
saturated model dan 0,123 pada estimated model. Nilai SRMR pada
saturated model (0,065) menunjukkan bahwa model pengukuran memiliki
tingkat kesesuaian yang baik, karena berada di bawah batas rekomendasi
0,08. Hal ini mengindikasikan bahwa hubungan antar indikator dan
konstruk dalam model pengukuran telah direpresentasikan dengan baik.
Sementara itu, nilai SRMR pada estimated model (0,123) menunjukkan
bahwa kesesuaian model struktural berada pada kategori marginal fit, yang
masih dapat diterima dalam konteks PLS-SEM. Kondisi ini
mengindikasikan bahwa ketika hubungan struktural antar konstruk
diperhitungkan, terdapat peningkatan residual antara korelasi empiris dan
korelasi yang diimplikasikan model. Hal ini biasa terjadi pada penelitian
dengan model yang kompleks, termasuk pada penelitian ini. Liang et al.
(2025) menjelaskan bahwa kompleksitas model, seperti jumlah indikator,
faktor laten, dan parameter bebas, dapat memengaruhi perilaku fit indices
dalam SEM. Peningkatan jumlah parameter yang menunjukkan model
semakin kompleks secara teoretis dapat memengaruhi nilai fit indices, yang
bergantung pada ukuran model, tingkat korelasi antar faktor, serta ukuran
sampel yang digunakan dalam penelitian. Selain itu, Hair et al. (2019)
menegaskan bahwa SRMR dalam PLS-SEM bersifat approximate fit dan
digunakan sebagai ukuran pendukung, sehingga nilai SRMR yang relatif
lebih tinggi masih dapat diterima selama kualitas model pengukuran dan
kemampuan prediktif model menunjukkan hasil yang baik.
B. Uji R Square (R²)
Nilai R Square (R²) digunakan untuk menilai kemampuan variabel
eksogen dalam menjelaskan varians variabel endogen dalam model
struktural. Semakin tinggi nilai R², semakin besar proporsi varians variabel
endogen yang dapat dijelaskan oleh variabel independen.
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
30
Tabel 4. 5 Hasil Uji R Square (R²)
R2 Keterangan R2 Keterangan
ATT 0,400 Sedang PT 0,469 Sedang
CI 0,652 Sedang PU 0,459 Sedang
PP 0,328 Sedang SAT 0,566 Sedang
Berikut adalah analisis nilai R Square pada masing-masing variabel
endogen berdasarkan Tabel 4.5:
1. Attitude Toward Using (ATT) - R2 = 0,400 (Sedang)
Nilai R² sebesar 0,400 pada variabel Attitude Toward Using (ATT)
menunjukkan bahwa 40,0% varians sikap pengguna dapat dijelaskan
oleh variabel eksogen yang memengaruhinya dalam model penelitian
ini, yakni Perceived Usefulness (PU). Sementara itu, 60,0% sisanya
dipengaruhi oleh faktor lain di luar model yang tidak diteliti.
2. Continuance Intention (CI) – R² = 0,652 (Sedang)
Nilai R² sebesar 0,652 pada variabel Continuance Intention (CI)
menunjukkan bahwa 65,2% varians niat penggunaan berkelanjutan
dapat dijelaskan oleh variabel-variabel eksogen yang memengaruhinya
dalam model penelitian ini, yakni Attitude Toward Using (ATT),
Emotional Experience (EE), Interactive Experience (IE), Perceived
Usefulness (PU), Satisfaction (SAT), Perceived Playfulness (PP),
Perceived Novelty (PN), Perceived Intelligence (PI), dan Perceived
Trust (PT). Sementara itu, 34,8% sisanya dipengaruhi oleh faktor lain
di luar model konseptual ini.
3. Perceived Playfulness (PP) – R² = 0,328 (Sedang)
Nilai R² sebesar 0,328 pada variabel Perceived Playfulness (PP)
menunjukkan bahwa 32,8% varians tingkat persepsi kesenangan dapat
dijelaskan oleh variabel eksogen yang memengaruhinya dalam model
penelitian ini, yakni Confirmation of Expectation (CE). Sementara itu,
67,2% sisanya dipengaruhi oleh faktor lain di luar model yang tidak
diteliti.
4. Perceived Trust (PT) – R² = 0,469 (Sedang)
Nilai R² sebesar 0,469 pada variabel Perceived Trust (PT)
menunjukkan bahwa 46,9% varians kepercayaan pengguna dapat
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
31
dijelaskan oleh variabel-variabel eksogen yang memengaruhinya dalam
model penelitian ini, yakni Perceived Intelligence (PI). Sementara itu,
53,1% sisanya dipengaruhi oleh faktor lain di luar model konseptual ini.
5. Perceived Usefulness (PU) – R² = 0,459 (Sedang)
Nilai R² sebesar 0,459 pada variabel Perceived Usefulness (PU)
menunjukkan bahwa 45,9% varians tingkat persepsi kegunaan dapat
dijelaskan oleh variabel eksogen yang memengaruhinya dalam model
penelitian ini, yakni Confirmation of Expectation (CE). Sementara itu,
54,1% sisanya dipengaruhi oleh faktor lain di luar model yang tidak
diteliti.
6. Satisfaction (SAT) – R² = 0,566 (Sedang)
Nilai R² sebesar 0,566 pada variabel Satisfaction (SAT)
menunjukkan bahwa 56,6% varians kepercayaan pengguna dapat
dijelaskan oleh variabel-variabel eksogen yang memengaruhinya dalam
model penelitian ini, yakni Perceived Usefulness (PU), Perceived
Novelty (PN), dan Perceived Playfulness (PP). Sementara itu, 43,4%
sisanya dipengaruhi oleh faktor lain di luar model konseptual ini.
C. Uji Goodness of Fit (GoF)
Goodness of Fit (GoF) digunakan sebagai ukuran agregat untuk menilai
kesesuaian model secara keseluruhan dengan mengombinasikan kualitas
model pengukuran dan model struktural. GoF dihitung sebagai akar kuadrat
dari hasil perkalian antara rata-rata AVE dan rata-rata R Square.
Tabel 4. 6 Hasil Uji GoF
Rata-rata AVE Rata-rata R2 GoF Index Keterangan
0,6764 0,4745 0,566 Tinggi
Pada Tabel 4.6, nilai GoF 0,566 masuk dalam kategori tinggi yakni
lebih dari 0,36, yang mengindikasikan bahwa model penelitian secara
keseluruhan memiliki tingkat kelayakan yang baik untuk menjelaskan
fenomena yang diteliti. Berdasarkan hasil evaluasi model fit menggunakan
SRMR, R Square, dan GoF, dapat disimpulkan bahwa model penelitian ini
secara umum layak digunakan untuk pengujian hipotesis. Meskipun nilai
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER 32

SRMR  pada  estimated  model  menunjukkan  kategori  marginal  fit,  hal
tersebut dapat diterima mengingat sifat SRMR sebagai  approximate fit
dalam  PLS-SEM  serta  didukung  oleh  nilai  R  Square  dan  GoF  yang
menunjukkan kemampuan prediktif model yang memadai.
4.3.2   Hasil Analisis Struktural Model
Analisis struktural model dalam penelitian ini dilakukan untuk menguji
hubungan kausal antar konstruk laten serta menguji hipotesis penelitian yang
telah dirumuskan sebelumnya. Evaluasi model  struktural pada pendekatan
PLS-SEM  dilakukan  dengan  memperhatikan  nilai  koefisien  jalur  (path
coefficient),  nilai  T-statistics,  dan  nilai  P-values  yang  diperoleh  melalui
prosedur bootstrapping.
Menurut Hair et al. (2019), suatu hubungan antar konstruk dinyatakan
signifikan apabila nilai T-statistics > 1,96 dan P-values < 0,05 pada tingkat
signifikansi 5%. Hasil analisis struktural model pada penelitian ini disajikan
sebagai berikut.

Tabel 4. 7  Uji Struktural Model
|     | Original  | T statistics   | P values  |     | Keterangan  | Hipotesis  |
| --- | --------- | -------------- | --------- | --- | ----------- | ---------- |
sample (O)
| ATT -> CI  | 0.038  | 0.45  | 0.653  | Positif  | dan  tidak  | Ditolak  |
| ---------- | ------ | ----- | ------ | -------- | ----------- | -------- |
signifikan
| CE -> PP  | 0.577  | 6.558  | 0   | Positif dan Signifikan  |     | Diterima  |
| --------- | ------ | ------ | --- | ----------------------- | --- | --------- |
| CE -> PU  | 0.681  | 12.26  | 0   | Positif dan Signifikan  |     | Diterima  |
CE -> SAT  0.315  2.791  0.005  Positif dan Signifikan  Diterima
EE -> CI  0.268  3.324  0.001  Positif dan Signifikan  Diterima
IE -> CI  0.193  2.255  0.024  Positif dan Signifikan  Diterima
PI -> CI  0.215  2.117  0.034  Positif dan Signifikan  Diterima
PI -> PT  0.688  12.135  0  Positif dan Signifikan  Diterima
| PN -> CI  | -0.031  | 0.365  | 0.715  |          |             | Ditolak  |
| --------- | ------- | ------ | ------ | -------- | ----------- | -------- |
|           |         |        |        | Negatif  | dan  Tidak  |          |
Signifikan
PN -> SAT  0.369  3.367  0.001  Positif dan Signifikan  Diterima
| PP -> CI  | 0.015  | 0.146  | 0.884  | Positif  | dan  Tidak  | Ditolak  |
| --------- | ------ | ------ | ------ | -------- | ----------- | -------- |
Signifikan
PP -> SAT  0.172  1.778  0.075  Positif  dan  Tidak  Ditolak
Signifikan
| PT -> CI  | -0.04  | 0.37  | 0.711  | Negatif  | dan  Tidak  | Ditolak  |
| --------- | ------ | ----- | ------ | -------- | ----------- | -------- |
Signifikan
PU -> ATT  0.636  9.595  0  Positif dan Signifikan  Diterima
| PU -> CI  | 0.083  | 1.032  | 0.302  |          |             | Ditolak  |
| --------- | ------ | ------ | ------ | -------- | ----------- | -------- |
|           |        |        |        | Positif  | dan  Tidak  |          |
Signifikan
| PU -> SAT  | 0.025  | 0.23  | 0.818  | Positif  | dan  Tidak  | Ditolak  |
| ---------- | ------ | ----- | ------ | -------- | ----------- | -------- |
Signifikan
SAT -> CI  0.243  2.348  0.019  Positif dan Signifikan  Diterima

Berdasarkan pengujian hipotesis menggunakan nilai T-Statistic, P Value,
dan Original Sample pada Tabel 4.7 menunjukkan dari total 17 hipotesis,
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
33
sejumlah 7 hipotesis ditolak dan 10 hipotesis diterima. Secara umum, temuan
ini mengindikasikan bahwa Emotional Experience (EE) dan Perceived
Intelligence (PI) merupakan faktor pendorong paling dominan terhadap niat
penggunaan berkelanjutan aplikasi Figma Make, baik secara langsung maupun
tidak langsung. Secara langsung, hubungan Emotional Experience (EE)
berpengaruh signifikan terhadap variabel Continuance Intention (CI) dengan
nilai Original Sample=0,268; T-Statistic =3.324; P-Value=0,001. Sementara
itu, hubungan Perceived Intelligence (PI) memengaruhi variabel Continuance
Intention (CI) secara tidak langsung melalui Perceived Trust (PT) dengan nilai
Original Sample=0,688; T-Statistic=2,117; P-Value=0,000. Temuan ini sejalan
dengan penelitian Xu et al. (2024) yang menunjukkan bahwa pengalaman
emosional positif dapat secara langsung meningkatkan keinginan pengguna
untuk terus menggunakan aplikasi, sementara persepsi terhadap kecerdasan
sistem meningkatkan kepercayaan pengguna yang pada akhirnya mendorong
niat penggunaan berkelanjutan. Rincian analisis setiap jalur hipotesis dapat
dilihat pada Lampiran 7.
Kemudian, selain menggunakan uji signifikansi jalur, evaluasi model
struktural dalam penelitian ini juga dilengkapi dengan uji F Square (f²) untuk
menilai besarnya pengaruh (effect size) dari masing-masing variabel eksogen
terhadap variabel endogen. Uji f² digunakan untuk mengetahui sejauh mana
kontribusi suatu konstruk independen dalam meningkatkan nilai R Square (R²)
pada konstruk dependen ketika konstruk tersebut dimasukkan ke dalam model.
Nilai f2 diklasifikasikan kedalam kategori no effect (< 0,02), pengaruh kecil (≥
0,02), pengaruh sedang (≥ 0,15), dan pengaruh besar (≥ 0,35). Hasil uji f² dapat
dilihat pada Tabel 4.8.
Tabel 4. 8 Nilai Effect Size
No f² Keterangan No f² Keterangan
1 ATT -> CI 0,002 No Effect 10 PN -> CI 0,001 No Effect
2 CE -> PP 0,499 Besar 11 PN -> SAT 0,151 Sedang
3 CE -> PU 0,863 Besar 12 PP -> CI 0,000 No Effect
4 CE -> SAT 0,091 Kecil 13 PP -> SAT 0,044 Kecil
5 EE -> CI 0,088 Kecil 14 PT -> CI 0,002 No Effect
6 IE -> CI 0,050 Kecil 15 PU -> ATT 0,679 Besar
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
34
7 PI -> CI 0,049 Kecil 16 PU -> CI 0,009 No Effect
8 PI -> PT 0,898 Besar 17 PU -> SAT 0,001 No Effect
9 SAT -> CI 0,049 Kecil
Berdasarkan hasil uji F-Square (f²), terdapat 4 hipotesis yang
menunjukkan pengaruh besar antar variabel, salah satunya adalah hubungan
antara Perceived Intelligence (PI) dan Perceived Trust (PT) yang memiliki nilai
effect size paling besar, yaitu 0,898. Selain itu, terdapat 1 hipotesis yang
memiliki pengaruh sedang, 6 hipotesis yang memiliki pengaruh kecil, serta 6
hipotesis lainnya yang tidak menunjukkan pengaruh berarti (no effect),
termasuk hubungan antara Attitude Toward Using (ATT) dan Continuance
Intention (CI).
Secara keseluruhan, hasil uji f² memperkuat temuan pada uji hipotesis
dan nilai R Square (R²), dengan menunjukkan bahwa hanya konstruk-konstruk
tertentu yang memiliki dampak substantif terhadap variabel endogen. Dengan
demikian, meskipun beberapa hubungan tidak signifikan secara statistik, uji f²
memberikan gambaran yang lebih komprehensif mengenai kekuatan pengaruh
dari masing-masing jalur dalam model struktural.
4.3.3 Finalisasi Model Konseptual
Finalisasi model konseptual akhir dilakukan berdasarkan hasil uji
hipotesis pada model struktural menggunakan pendekatan PLS-SEM.
Berdasarkan hasil pengujian dari 17 hipotesis yang diuji, terdapat 10 hipotesis
yang diterima dan 7 hipotesis yang ditolak, sehingga hanya hubungan yang
terbukti signifikan secara statistik yang dipertahankan dalam model akhir.
Model konseptual akhir dapat dilihat pada Gambar 4.3.
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
35
Gambar 4. 3 Model Konseptual Akhir
4.4 Prioritas Perbaikan Figma Make untuk Meningkatkan Niat Penggunaan
Berkelanjutan Generasi Z
Pada penelitian ini, data persepsi pengguna terhadap Figma Make sebagai AI
design tools diperoleh melalui kuesioner dengan skala Likert empat poin. Untuk
memudahkan interpretasi data dan mengidentifikasi area yang memerlukan
perbaikan, jawaban responden dikategorikan ke dalam dua kelompok, yaitu
kategori positif dan kategori negatif. Kategori positif mencakup jawaban “sangat
setuju” dan “setuju”, sedangkan kategori negatif meliputi jawaban “tidak setuju”
dan “sangat tidak setuju”. Pengelompokan ini digunakan sebagai analisis
pendukung (supporting analysis) untuk melengkapi hasil utama pengujian model
struktural menggunakan SEM-PLS. Hal ini sejalan dengan penelitian sebelumnya
oleh Alfian et al. (2024) dan Hasan (2014) yang menekankan pentingnya
mengevaluasi persepsi dan umpan balik pengguna untuk mengidentifikasi masalah
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
36
serta area yang memerlukan peningkatan dalam aplikasi, salah satunya melalui
identifikasi jawaban negatif. Melalui pengumpulan dan analisis tersebut, dapat
membantu memahami kesulitan serta hal yang diperlukan oleh pengguna agar
sistem menjadi lebih efektif dan sesuai kebutuhan. Oleh karena itu, penyusunan
rekomendasi perbaikan penelitian ini dilakukan dengan mempertimbangkan dua
aspek utama, yakni jumlah dan proporsi jawaban negatif pada setiap indikator
berdasarkan hasil penelitian serta temuan penelitian terdahulu yang relevan dengan
adopsi teknologi, user experience, serta sistem berbasis kecerdasan buatan.
Guna memastikan bahwa rekomendasi perbaikan yang dihasilkan bersifat
sistematis dan memiliki landasan teoritis yang kuat, prioritas perbaikan
dikelompokkan berdasarkan empat kerangka konseptual utama, yaitu Technology
Acceptance Model (TAM), Expectation Confirmation Model (ECM), User
Experience (UX), dan Karakteristik AI. Apabila terdapat dua indikator dengan
jumlah jawaban negatif sama, maka indikator dengan rata-rata indikator yang lebih
rendah diprioritaskan karena mencerminkan tingkat ketidakpuasan pengguna yang
lebih besar. Analisis jawaban responden terdapat pada Lampiran 8.
4.4.1 Prioritas Perbaikan Berdasarkan Technology Acceptance Model
(TAM)
Berdasarkan Technology Acceptance Model (TAM), penerimaan
teknologi sangat dipengaruhi oleh persepsi kegunaan dan sikap pengguna
terhadap sistem (Davis, 1989). Temuan pada indikator PU3 yakni “Saya
merasa aplikasi Figma Make memainkan peran penting dalam memberi saya
inspirasi” dengan nilai rata-rata 3,346 menunjukkan bahwa sebagian pengguna
belum merasakan peran Figma Make sebagai sumber inspirasi desain yang
signifikan. Padahal, menurut Davis (1989) dan Venkatesh & Davis (2000),
persepsi kegunaan akan meningkat apabila sistem mampu memberikan nilai
tambah yang relevan dengan tujuan utama pengguna, dalam hal ini kreativitas
dan eksplorasi ide desain.
Selain itu, indikator ATT3 yakni “Saya terkesan menggunakan aplikasi
Figma Make” dengan nilai rata-rata 3,370 mengindikasikan bahwa aplikasi
belum memberikan impresi yang mendalam bagi pengguna. Menurut
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
37
Venkatesh et al. (2012), sikap positif terhadap teknologi terbentuk tidak hanya
dari kemudahan penggunaan, tetapi juga dari pengalaman bermakna yang
meninggalkan kesan positif. Oleh karena itu, rekomendasi perbaikan pada
aspek TAM sebagai berikut:
1. Pengembangan fitur AI yang mampu menghasilkan variasi konsep
desain berdasarkan gaya, tren, dan konteks kebutuhan pengguna
2. Menambahkan panel interaksi dimana AI tidak hanya membuatkan
gambar, tetapi bisa diajak berdiskusi tentang konsep. Hal ini sejalan
dengan Lubart (2005) yang mendefinisikan AI sebagai “Creative
Partner”. Inspirasi tidak selalu bersifat visual, tapi bisa berupa
stimulasi verbal. AI yang mampu berdialog membantu pengguna dalam
fase divergent thinking (memperluas kemungkinan ide) sebelum masuk
ke fase convergent thinking (eksekusi).
3. Meminimalkan hambatan teknis dengan menyederhanakan alur
perintah (prompting) agar pengguna dapat mengeksplorasi ide desain
tanpa perlu mempelajari instruksi yang rumit, misalnya dengan
memberikan button kategori tema desain yang akan dibuat. Sesuai
dengan teori Davis et al. (1989), jika sebuah sistem sulit digunakan
untuk mendapatkan inspirasi, maka nilai kegunaannya akan menurun.
Nielsen (1994) juga berpendapat bahwa sistem yang memberikan
kepuasan subjektif tinggi adalah sistem yang mampu memfasilitasi
kebutuhan pengguna dengan usaha mental yang minimal.
4.4.2 Prioritas Perbaikan Berdasarkan Expectation Confirmation Model
(ECM)
Pada kerangka Expectation Confirmation Model (ECM), keberlanjutan
penggunaan teknologi sangat ditentukan oleh konfirmasi ekspektasi, kepuasan
pengguna, dan niat penggunaan berkelanjutan. Hasil analisis menunjukkan
bahwa indikator CE2 yakni “Saya merasa layanan yang disediakan aplikasi
Figma Make melebihi ekspektasi saya” dengan nilai rata-rata 3,330 memiliki
jumlah jawaban negatif yang relatif tinggi, yang mengindikasikan bahwa
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
38
layanan yang disediakan oleh Figma Make belum sepenuhnya melampaui
ekspektasi awal pengguna.
Indikator SAT1 yakni “Aplikasi Figma Make memenuhi kebutuhan saya,
yang membuat saya merasa bahagia” dengan nilai rata-rata 3,354 juga
menunjukkan bahwa sebagian responden belum merasakan kepuasan yang
bersifat emosional, khususnya kepuasan yang menimbulkan perasaan bahagia
setelah menggunakan aplikasi. Kondisi ini berdampak langsung pada indikator
CI3 dengan nilai rata-rata 3,320, di mana pengguna belum sepenuhnya
menjadikan Figma Make sebagai pilihan utama dibandingkan aplikasi sejenis.
Dengan demikian, prioritas perbaikan pada aspek ECM yakni sebagai berikut:
1. Menyediakan fitur personalisasi hasil desain dengan menganalisis pola
penggunaan historis pengguna, preferensi, dan gaya pribadi mereka
yang lebih akurat agar pengguna merasa kebutuhan spesifiknya
terpenuhi. Hal ini sejalan dengan Bhattacherjee (2001) bahwa ketika
ekspektasi pengguna terkonfirmasi atau terlampaui, kepuasan dan
loyalitas akan meningkat secara signifikan.
2. Meningkatkan kualitas output desain AI agar lebih presisi, kontekstual,
dan sesuai dengan kebutuhan nyata pengguna. Penelitian Casteleiro-
pitrez (2024) menunjukkan bahwa kualitas hasil desain dan tingkat
usability merupakan faktor utama yang mempengaruhi kepuasan serta
kepercayaan pengguna terhadap teknologi generatif AI dalam proses
desain.
3. Menambahkan elemen interaktif dan eksploratif yang mendorong rasa
senang saat menggunakan AI design tools. Penelitian Rezwana &
Maher (2022) menunjukkan bahwa interaksi antara pengguna dan AI
dapat meningkatkan keterlibatan, pengalaman kolaboratif, serta
persepsi positif terhadap sistem.
4. Mengintegrasikan fitur Creative Exploration Mode yang mampu
menyajikan variasi konsep desain (seperti eksplorasi gaya visual dan
moodboard) yang berbeda dari standar pasar sehingga dapat
memberikan inspirasi desainer. Hal ini didukung oleh Limayem et al.
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
39
(2015) yang menegaskan bahwa keberlanjutan penggunaan sangat
dipengaruhi oleh persepsi superioritas sistem dibandingkan alternatif
lain.
4.4.3 Prioritas Perbaikan Berdasarkan User Experience (UX)
Cheng & Jiang (2020) menekankan pentingnya alat AI bagi desainer UX
untuk meningkatkan efektivitas keseluruhan dan kepuasan berkelanjutan dari
pekerjaan desain mereka, serta dapat memiliki dampak langsung pada loyalitas
pengguna dan niat berkelanjutan. Temuan pada indikator EE3 yakni “Saya
merasa menggunakan Figma Make membantu meningkatkan keterikatan
emosional” dengan nilai rata-rata 3,483 merefleksikan bahwa aplikasi ini
belum mampu secara optimal membangun keterikatan emosional (emotional
engagement), sementara indikator IE3 mengonfirmasi belum optimalnya
kenyamanan interaksi oleh pengguna terhadap sistem. Oleh karena itu, prioritas
perbaikan pada aspek UX diarahkan pada:
1. Meningkatkan keterikatan emosional melalui implementasi fitur desain
yang lebih berorientasi pada pengalaman afektif pengguna. Misalnya
melalui penyediaan kategori berbasis “design persona”, seperti
menyediakan pilihan emosional seperti The Authority (cocok untuk
aplikasi fintech) & The Friendly Neighbor (cocok untuk aplikasi
sosmed). Melalui pendekatan ini, aplikasi dapat secara otomatis
menyesuaikan palet warna, tipografi, komposisi ruang, dan elemen
visual sesuai dengan emosi yang dipilih, sehingga proses desain
menjadi lebih personal, intuitif, dan mampu meningkatkan emotional
engagement pengguna. Hal ini sejalan dengan Yu et al. (2024) yang
menyatakan bahwa pengembangan sistem berbasis kecerdasan buatan
tidak hanya harus berpusat pada kecanggihan teknologi, tetapi juga
wajib memprioritaskan kualitas pengalaman emosional pengguna
(Emotional Experience).
2. Menyederhanakan navigasi serta mengurangi waktu pemrosesan AI
untuk menjamin kenyamanan interaksi yang mulus. Sejalan dengan
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
40
temuan Glassberg et al. (2025) yang menunjukkan bahwa transparansi
proses AI dan umpan balik visual yang cepat sangat krusial dalam
membangun rasa nyaman dan kepercayaan pada alat kreatif berbasis
kecerdasan buatan.
4.4.4 Prioritas Perbaikan Berdasarkan Karakteristik AI
Temuan pada indikator PI2 yakni “Saya merasa aplikasi Figma Make
sangat efektif dalam menyelesaikan masalah” dengan nilai rata-rata 3,282
merefleksikan bahwa kapabilitas problem solving Figma Make belum
sepenuhnya optimal dalam menangani kompleksitas desain. Hal ini sejalan
dengan penelitian Shneiderman (2020) yang menyatakan bahwa efektivitas AI
terletak pada kemampuannya memberikan dukungan cerdas yang kontekstual
guna meningkatkan kontrol manusia, bukan sekadar menghasilkan output
otomatis. Selain aspek fungsional, indikator PN1 “Saya merasa menggunakan
aplikasi Figma Make membuat saya menemukan pengalaman baru (atau unik)”
dengan nilai rata-rata 3,483 dan PP2 “Saya merasa menggunakan aplikasi
Figma Make membuat saya menikmati proses” dengan nilai rata-rata 3,403
menunjukkan adanya defisit pada pengalaman kebaruan dan kesenangan.
Berdasarkan teori Hedonic Motivation, kesenangan dan keunikan pengalaman
menjadi motor penggerak loyalitas pengguna digital. Sementara itu, indikator
PT2 yakni “Saya merasa percaya pada sumber data yang digunakan aplikasi
Figma Make” menyoroti urgensi transparansi sumber data. Oleh karena itu,
berikut adalah daftar prioritas perbaikan berdasarkan karakteristik AI yang
didukung oleh literatur terkini:
1. Meningkatkan performa AI sehingga menghasilkan solusi desain yang
kontekstual sesuai dengan kebutuhan, tujuan, dan batasan pengguna,
terutama pada kebutuhan dengan kompleksitas yang tinggi. Hal ini
sejalan dengan temuan Cao (2025) bahwa efektivitas sistem generatif
dalam desain bergantung pada kemampuan algoritma untuk memahami
struktur visual yang kompleks secara otonom, yang memungkinkan
kolaborasi antara manusia dan AI menjadi lebih produktif.
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
41
2. Menjelaskan secara ringkas dan mudah dipahami jenis data yang
digunakan (misalnya data desain publik, template umum, atau data web
search). Shin & Park (2019) menegaskan bahwa transparansi sumber
data dan proses algoritmik berpengaruh signifikan terhadap
kepercayaan pengguna pada sistem AI, terutama pada aplikasi berbasis
kreativitas.
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
BAB 5. PENUTUP
5.1 Kesimpulan
Berdasarkan hasil analisis niat penggunaan berkelanjutan AI design tools
pada aplikasi Figma Make melalui integrasi model TAM-ECM dengan faktor
eksternal UX serta memperhatikan karakteristik AI design tools maka dapat
ditarik kesimpulan sebagai berikut:
1. Pengujian uji model fit pada PLS-SEM terhadap 124 responden
menunjukkan bahwa secara keseluruhan model layak digunakan. Hal ini
ditunjukkan melalui nilai R2 yakni 0,474 yang merepresentasikan bahwa
variabel eksogen dapat menjelaskan varians-variabel endogen dalam model
struktural dengan baik. Selain itu, nilai Goodness of Fit (GoF) 0,566 dengan
kategori baik mengindikasikan bahwa secara keseluruhan model sesuai
dengan kecocokan terhadap data. Meskipun nilai Standardized Root Mean
Square Residual (SRMR) estimated 0,123 yang berada pada kategori
marginal fit, namun hal tersebut sering terjadi pada model dengan
kompleksitas tinggi. Selain itu, nilai saturated 0,065 mengindikasikan
bahwa model pengukuran secara keseluruhan memiliki tingkat kesesuaian
yang baik.
2. Hasil uji struktural model pada penelitian ini menunjukkan bahwa dari 17
hipotesis, terdapat tujuh hipotesis ditolak dan sepuluh lainnya diterima.
Rincian hasil analisis uji hipotesis sebagai berikut:
a. Confirmation of Expectation (CE) berpengaruh positif dan
signifikan terhadap Perceived Playfulness (PP)
b. Confirmation of Expectation (CE) berpengaruh positif dan
signifikan terhadap Perceived Usefulness (PU)
c. Confirmation of Expectation (CE) berpengaruh positif dan
signifikan terhadap Satisfaction (SAT)
d. Emotional Experience (EE) berpengaruh positif dan signifikan
terhadap Continuance Intention (CI)
DIGITAL REPOSITORY UNIVERSITAS JEMBER
42

DIGITAL REPOSITORY UNIVERSITAS JEMBER
43
e. Interactive Experience (IE) berpengaruh positif dan signifikan
terhadap Continuance Intention (CI)
f. Perceived Intelligence (PI) berpengaruh positif dan signifikan
terhadap Continuance Intention (CI)
g. Perceived Intelligence (PI) berpengaruh positif dan signifikan
terhadap Perceived Trust (PT)
h. Perceived Novelty (PN) berpengaruh positif dan signifikan terhadap
Satisfaction (SAT)
i. Perceived Usefulness (PU) berpengaruh positif dan signifikan
terhadap Attitude Toward Using (ATT)
j. Satisfaction (SAT) berpengaruh positif dan signifikan terhadap
Continuance Intention (CI)
3. Berdasarkan hasil uji struktural pada kelompok Generasi Z sebagai
pengguna aplikasi Figma Make, variabel yang memiliki besar pengaruh
langsung terhadap variabel Continuance Intention (CI) adalah Emotional
Experience (EE), diikuti Satisfaction (SAT), Perceived Intelligence (PI),
dan Interactive Experience (IE). Sementara itu pengaruh tidak langsung
terbesar terhadap variabel Continuance Intention (CI) dimediasi oleh
hubungan Perceived Intelligence (PI) terhadap Perceived Trust (PT), serta
Confirmation of Expectation (CE) terhadap Perceived Usefulness (PU).
4. Sejumlah 37 indikator telah dianalisis dan menghasilkan sebelas prioritas
perbaikan yang direkomendasikan terhadap aplikasi Figma Make.
Rekomendasi ini berlandaskan hasil analisis perhitungan nilai negatif
dengan rata-rata terendah. Melalui rekomendasi ini, penelitian ini tidak
hanya berfokus untuk memberikan kontribusi teoritis dalam bidang
akademis, namun juga memberikan panduan praktis bagi pengembang
Figma Make untuk mengoptimalkan fungsi aplikasi.
5.2 Saran
Fokus penelitian ini yakni pada Generasi Z, sehingga hasil penelitian hanya
dapat digeneralisasikan pada kelompok Generasi Z. Guna memperoleh hasil yang
berbeda, penelitian selanjutnya disarankan untuk mengeksplorasi cakupan sampel
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
44
dari pengguna dengan latar belakang usia, profesi, gender, dan tingkat pendidikan
yang berbeda sehingga berpotensi memiliki persepsi serta pola interaksi yang
berbeda juga terhadap aplikasi Figma Make. Selain itu, kompleksitas model dengan
mengintegrasikan TAM–ECM, faktor UX, serta karakteristik AI pada penelitian ini
berkontribusi pada meningkatnya nilai SRMR estimated, meskipun masih berada
pada kategori marginal fit. Penelitian selanjutnya dapat mempertimbangkan
penyederhanaan model struktural sehingga kualitas model yang dihasilkan dapat
lebih optimal.
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
DAFTAR PUSTAKA
Ã, T. L. (2005). How can computers be partners in the creative process :
Classification and commentary on the Special Issue. 63, 365–369.
https://doi.org/10.1016/j.ijhcs.2005.04.002
Al-Saedi, K., Al-Emran, M., Ramayah, T., & Abusham, E. (2020). Developing a
general extended UTAUT model for M-payment adoption. Technology in
Society, 62(September 2019), 101293.
https://doi.org/10.1016/j.techsoc.2020.101293
Alfian, S. D., Sania, J. A., Aini, D. Q., Khoiry, Q. A., Griselda, M., Ausi, Y., &
Zakiyah, N. (2024). Evaluation of usability and user feedback to guide
telepharmacy application development in Indonesia : a mixed-methods study.
3, 1–14.
Alfina, A., Lathifah, A., & Kurnia, U. I. (2024). Efektivitas Penggunaan Figma
Sebagai Alat Prototyping Dalam Mata Kuliah Interaksi Manusia Dan
Komputer. Jurnal Pendidikan Teknologi Informasi (J-Diteksi), 3(2), 40–45.
https://doi.org/10.30604/diteksi.v3i2.1629
Atmojo, I. R. W., Ardiansyah, R., & Saputri, D. Y. (2022). Empowering Science-
Based Entrepreneurship (SciPreneur) Skills through CEL-BaDiS up Learning
Model on Food Biotechnology Materials. International Journal of Instruction,
15(3), 83–102. https://doi.org/10.29333/iji.2022.1535a
Balakrishnan, J., Abed, S. S., & Jones, P. (2022). The role of meta-UTAUT factors,
perceived anthropomorphism, perceived intelligence, and social self-efficacy
in chatbot-based services? Technological Forecasting and Social Change,
180(April), 121692. https://doi.org/10.1016/j.techfore.2022.121692
Belda-Medina, J., & Calvo-Ferrer, J. R. (2022). Using Chatbots as AI
Conversational Partners in Language Learning. Applied Sciences
(Switzerland), 12(17). https://doi.org/10.3390/app12178427
Bhattacherjee, A. (2001a). An empirical analysis of the antecedents of electronic
commerce service continuance. 201–214.
Bhattacherjee, A. (2001b). Bhattacherjee/lnformation Systems Continuance MIS
Qarterjy UNDERSTANDING INFORMATION SYSTEMS
CONTINUANCE: AN EXPECTATION-CONFIRMATION MODEL1
Motivation for the Study. MIS Quarterly, 25(3), 351–370.
Bhattacherjee, A. (2001c). ECM IS Model. MIS Quarterly, 25(3), 351–370.
Brisco, R., Hay, L., & Dhami, S. (2023). Exploring the Role of Text-To-Image Ai
in Concept Generation. Proceedings of the Design Society, 3(July), 1835–
1844. https://doi.org/10.1017/pds.2023.184
Bujang, M. A., Omar, E. D., Hui, D., & Foo, P. (2024). Sample size determination
for conducting a pilot study to assess reliability of a questionnaire. 49(1), 1–
8.
Cao, Q. (2025). Research on the Application Effectiveness of Generative AI in
Design Projects from Data-Driven and Sustainable Perspectives. 1–35.
Casteleiro-pitrez, J. (2024). Generative Artificial Intelligence Image Tools among
DIGITAL REPOSITORY UNIVERSITAS JEMBER
45

DIGITAL REPOSITORY UNIVERSITAS JEMBER
46
Future Designers : A Usability , User Experience , and Emotional Analysis.
316–332.
Chan, C. K. Y., & Lee, K. K. W. (2023). The AI generation gap: Are Gen Z students
more interested in adopting generative AI such as ChatGPT in teaching and
learning than their Gen X and millennial generation teachers? Smart Learning
Environments, 10(1). https://doi.org/10.1186/s40561-023-00269-3
Cheng, Y., & Jiang, H. (2020). How Do AI-driven Chatbots Impact User
Experience? Examining Gratifications, Perceived Privacy Risk, Satisfaction,
Loyalty, and Continued Use. Journal of Broadcasting and Electronic Media,
64(4), 592–614. https://doi.org/10.1080/08838151.2020.1834296
Chyung. (2017). EVIDENCE-BASED SURVEY DESIGN: THE USE OF A
MIDPOINT ON THE LIKERT SCALE. Performance Improvement, 46(9), 9–
16. https://doi.org/10.1002/pfi
Davis, F. D. (1989). Perceived Usefulness, Perceived Ease of Use, and User
Acceptance of Information Technology. Perceived Usefulness, Perceived
Ease of Use, and User Acceptance of Information Technology, 13(3), 319–
340. https://doi.org/10.5962/bhl.title.33621
Davis, F. D., Bagozzi, R. P., & Warshaw, P. R. (1989). User Acceptance of
Computer Technology: A Comparison of Two Theoretical Models.
Management Science, 35(8), 982–1003.
https://doi.org/10.1287/mnsc.35.8.982
Dwivedi, Y. K., Wade, M. R., & Schneberger, S. L. (2012). Informations Systems
Theory: Vol.2. Springer, 28(May), 461. https://doi.org/10.1007/978-1-4419-
6108-2
Fan, P., & Jiang, Q. (2024). Exploring the Factors Influencing Continuance
Intention to Use AI Drawing Tools: Insights from Designers. Systems, 12(3),
1–27. https://doi.org/10.3390/systems12030068
Fernandes, T., & Oliveira, E. (2021). Understanding consumers’ acceptance of
automated technologies in service encounters: Drivers of digital voice
assistants adoption. Journal of Business Research, 122(August 2020), 180–
191. https://doi.org/10.1016/j.jbusres.2020.08.058
Glassberg, I., Ilan, Y. B., & Zwilling, M. (2025). The key role of design and
transparency in enhancing trust in AI-powered digital agents. Journal of
Innovation & Knowledge, 10(5), 100770.
https://doi.org/10.1016/j.jik.2025.100770
Hair, J., & Alamer, A. (2022). Partial Least Squares Structural Equation Modeling
(PLS-SEM) in second language and education research: Guidelines using an
applied example. Research Methods in Applied Linguistics, 1(3), 100027.
https://doi.org/10.1016/j.rmal.2022.100027
Hair, J. F., Hult, G. T. M., Christian M. Ringle, & Marko Sarstedt. (2022). A Primer
on Partial Least Squares Structural Equation Modeling (PLS-SEM).
Hair, J. F., Hult, G. T. M., & Ringle, C. M. (2017). A primer on partial least squares
structural equation modeling (PLS-SEM).
Hair, J. F., Hult, G. T. M., Ringle, C. M., Sarstedt, M., Danks, N. P., & Ray, S.
(2021). Mediation Analysis. https://doi.org/10.1007/978-3-030-80519-7_7
Hair, J. F., Ringle, C. M., Sarstedt, M., Hair, J. F., Ringle, C. M., & Sarstedt, M.
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
47
(2014). PLS-SEM : Indeed a Silver Bullet PLS-SEM : Indeed a Silver Bullet.
January 2015, 37–41. https://doi.org/10.2753/MTP1069-6679190202
Hariguna, T., Ruangkanjanases, A., Madon, B. Bin, & Alfawaz, K. M. (2023).
Assessing Determinants of Continuance Intention Toward Cryptocurrency
Usage: Extending Expectation Confirmation Model With Technology
Readiness. SAGE Open, 13(1). https://doi.org/10.1177/21582440231160439
Hasan, L. (2014). THE USEFULNESS OF USER TESTING METHODS
IDENTIFYING PROBLEMS ON UNIVERSITY WEBSITES. 11(2), 229–256.
https://doi.org/10.4301/S1807-17752014000200002
Henseler, J., Hubona, G., & Ray, P. A. (2016). Using PLS path modeling in new
technology research : updated guidelines. 116(1), 2–20.
https://doi.org/10.1108/IMDS-09-2015-0382
Huang, Y., & Yu, Z. (2023). Understanding the Continuance Intention for Artificial
Intelligence News Anchor: Based on the Expectation Confirmation Theory.
Systems, 11(9). https://doi.org/10.3390/systems11090438
ISO. (2019). INTERNATIONAL STANDARD interactive systems iTeh STANDARD
iTeh STANDARD PREVIEW. 2019.
Jayatissa, K. A. D. . (2023). Generation Z – A New Lifeline : A Systematic Literature
Review. 3(2), 179–186.
Jr, J. F. H., Black, W. C., Babin, B. J., Anderson, R. E., Black, W. C., & Anderson,
R. E. (2018). Multivariate Data Analysis.
https://doi.org/10.1002/9781119409137.ch4
Kwon, J., Jung, E. C., & Kim, J. (2024). Designer-Generative AI Ideation Process:
Generating Images Aligned with Designer Intent in Early-Stage Concept
Exploration in Product Design. Archives of Design Research, 37(3), 7–23.
https://doi.org/10.15187/adr.2024.07.37.3.7
Lee, J. C., Tang, Y., & Jiang, S. Q. (2023). Understanding continuance intention of
artificial intelligence (AI)-enabled mobile banking applications: an extension
of AI characteristics to an expectation confirmation model. Humanities and
Social Sciences Communications, 10(1). https://doi.org/10.1057/s41599-023-
01845-1
Liang, X., Cao, C., Li, J., Edeh, E. J., & Chen, J. (2025). Sensitivity of Fit Indices
to Model Complexity and Misspecification in Exploratory Structural Equation
Modeling. 2009, 1–18.
Limayem, M., Hirt, S. G., Cheung, C. M. K., & Hirt, S. G. (2015). Qiarterly How
Habit Limits the Predictive Power Intention : The Case of Information Systems
Continuance1. 31(4), 705–737.
Lin, C. S., Wu, S., & Tsai, R. J. (2005). Integrating perceived playfulness into
expectation-confirmation model for web portal context. Information and
Management, 42(5), 683–693. https://doi.org/10.1016/j.im.2004.04.003
Liu, H., Shao, M., Liu, X., & Zhao, L. (2021). Exploring the Influential Factors on
Readers’ Continuance Intentions of E-Book APPs: Personalization,
Usefulness, Playfulness, and Satisfaction. Frontiers in Psychology,
12(February), 1–11. https://doi.org/10.3389/fpsyg.2021.640110
Liu, Y., & Wang, Y. (2023). Empirical Study on the Factors Affecting User
Stickiness of Online Visual Art Platform From the Perspective of User
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
48
Experience. IEEE Access, 11, 60763–60776.
https://doi.org/10.1109/ACCESS.2023.3284541
Lu, Y., Yang, Y., Zhao, Q., Zhang, C., & Li, T. J.-J. (2024). AI Assistance for UX:
A Literature Review Through Human-Centered AI.
http://arxiv.org/abs/2402.06089
M., P. (2001). Digital Natives, Digital Immigrants Part 1.
Moon, J. W., & Kim, Y. G. (2001). Extending the TAM for a World-Wide-Web
context. Information and Management, 38(4), 217–230.
https://doi.org/10.1016/S0378-7206(00)00061-6
Na, S., Heo, S., Han, S., Shin, Y., & Roh, Y. (2022). Acceptance Model of Artificial
Intelligence (AI)-Based Technologies in Construction Firms: Applying the
Technology Acceptance Model (TAM) in Combination with the Technology–
Organisation–Environment (TOE) Framework. Buildings, 12(2).
https://doi.org/10.3390/buildings12020090
Nascimento, R., Limeira, C. D., De Pinho, A. L. S., & Santa Rosa, J. G. (2014).
Emotion, affectivity and usability in interface design. Lecture Notes in
Computer Science (Including Subseries Lecture Notes in Artificial Intelligence
and Lecture Notes in Bioinformatics), 8520 LNCS(PART 4), 339–346.
https://doi.org/10.1007/978-3-319-07638-6_33
Nguyen, D. M., Chiu, Y. T. H., & Le, H. D. (2021). Determinants of continuance
intention towards banks’ chatbot services in vietnam: A necessity for
sustainable development. Sustainability (Switzerland), 13(14), 1–24.
https://doi.org/10.3390/su13147625
Rezwana, J., & Maher, M. Lou. (2022). Understanding User Perceptions,
Collaborative Experience and User Engagement in Different Human-AI
Interaction Designs for Co-Creative Systems. 1(1), 1–17.
https://doi.org/10.1145/3527927.3532789.
Schönberger, M. (2025). Artificial Intelligence in UX/UI Design: A Research
Framework for Exploring the Impact of Artificial Intelligence Tools on Design
Quality. In Lecture Notes in Networks and Systems: Vol. 1054 LNNS. Springer
Nature Singapore. https://doi.org/10.1007/978-981-97-5035-1_40
Shin, D., & Park, Y. J. (2019). Role of Fairness, Accountability, and Transparency
in Algorithmic Affordance. Computers in Human Behavior.
https://doi.org/10.1016/j.chb.2019.04.019
Shneiderman, B., & Shneiderman, B. (2020). Human-Centered Artificial
Intelligence : Reliable , Safe & Trustworthy Human-Centered Artificial
Intelligence : Reliable , Safe & Trustworthy. International Journal of Human–
Computer Interaction, 00(00), 1–10.
https://doi.org/10.1080/10447318.2020.1741118
Sugiyono. (2013). METODE PENELITIAN KUANTITATIF, KUALITATIF, DAN
R&D.
Sutcliffe, A., & Hart, J. (2017). Analyzing the Role of Interactivity in User
Experience. International Journal of Human-Computer Interaction, 33(3),
229–240. https://doi.org/10.1080/10447318.2016.1239797
Takafoli, M., Li, S., & Mäkelä, V. (2024). Generative AI in User Experience Design
and Research: How Do UX Practitioners, Teams, and Companies Use GenAI
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
49
in Industry? Proceedings of the 2024 ACM Designing Interactive Systems
Conference, DIS 2024, 1579–1593. https://doi.org/10.1145/3643834.3660720
Tsao, J., Xinyi, C., Collier, L., & Alice, N. (2025). Perceptions and integration of
generative artificial intelligence in creative practices and industries : a scoping
review and conceptual model. AI & SOCIETY, 0123456789.
https://doi.org/10.1007/s00146-025-02667-2
Vakratsas, D., & Wang, X. (2020). Artificial Intelligence in Advertising Creativity.
Journal of Advertising, 50(1), 39–51.
https://doi.org/10.1080/00913367.2020.1843090
Venkatesh, V., & Davis, F. D. (2000). Theoretical extension of the Technology
Acceptance Model: Four longitudinal field studies. Management Science,
46(2), 186–204. https://doi.org/10.1287/mnsc.46.2.186.11926
Venkatesh, V., Thong, J. Y. L., Chan, F. K. Y., Hu, P. J., & Brown, S. A. (2011).
UTAUT predictors and the role of context. 527–555.
https://doi.org/10.1111/j.1365-2575.2011.00373.x
Wang, Y., & Liu, Y. (2022). Evaluation System of CG Art Communication
Platform Based on User Experience. IEEE Access, 10(December), 128742–
128753. https://doi.org/10.1109/ACCESS.2022.3227931
Wells, J. D., Campbell, D. E., Valacich, J. S., & Featherman, M. (2010). The Effect
of Perceived Novelty on the Adoption of Information Technology Innovations:
A Risk/Reward Perspective. Decision Sciences, 41(4), 813–843.
https://doi.org/10.1111/j.1540-5915.2010.00292.x
Wu, J., & Song, S. (2021). Older Adults’ Online Shopping Continuance Intentions:
Applying the Technology Acceptance Model and the Theory of Planned
Behavior. International Journal of Human-Computer Interaction, 37(10),
938–948. https://doi.org/10.1080/10447318.2020.1861419
Xu, J., Ren, X., Huang, Y., Wu, R., & Pan, Y. (2024). Persist or Abandon?
Exploring Chinese Users’ Continuance Intentions Toward AI Painting Tools.
IEEE Access, 12(July), 135469–135488.
https://doi.org/10.1109/ACCESS.2024.3424946
Xu, J., Zhang, X., Li, H., Yoo, C., & Pan, Y. (2023). Is Everyone an Artist? A Study
on User Experience of AI-Based Painting System. Applied Sciences
(Switzerland), 13(11). https://doi.org/10.3390/app13116496
Yu, X., Yang, Y., & Li, S. (2024). Users’ continuance intention towards an AI
painting application: An extended expectation confirmation model. PLoS
ONE, 19(5 May), 1–25. https://doi.org/10.1371/journal.pone.0301821
Zhu, Z., Lee, H., Pan, Y., & Cai, P. (2024). AI assistance in enterprise UX design
workflows: enhancing design brief creation for designers. Frontiers in
Artificial Intelligence, 7(November).
https://doi.org/10.3389/frai.2024.1404647
DIGITAL REPOSITORY UNIVERSITAS JEMBER

| DIGITAL REPOSITORY UNIVERSITAS JEMBER |     |     |     |     |     |     |     |
| ------------------------------------- | --- | --- | --- | --- | --- | --- | --- |

LAMPIRAN-LAMPIRAN

Lampiran  1 Definisi Operasional
| Variabel  | Definisi  |     | Kode  | Indikator  |     |     | Sumber  |
| --------- | --------- | --- | ----- | ---------- | --- | --- | ------- |
Operasional
Perceived  Kepercayaan  PU1  Menggunakan  sistem  (Davis,  1989),
Usefulness (PU)  pengguna ketika  memungkinkan  saya  (Xu  et  al.,
|     | menggunakan suatu     |     |      | menyelesaikan           | tugas   | 2024),      | (Yu  et    |
| --- | --------------------- | --- | ---- | ----------------------- | ------- | ----------- | ---------- |
|     | sistem tertentu akan  |     |      | lebih cepat             |         | al., 2024)  |            |
|     | meningkatkan          |     | PU2  | Menggunakan             | sistem  | (Davis,     | 1989),     |
|     | kinerjanya (Davis,    |     |      | membuat pekerjaan saya  |         | (Fan        | &  Jiang,  |
|     | 1989).                |     |      | lebih mudah dilakukan.  |         | 2024),      | (Yu  et    |
al., 2024)
|     |     |     | PU3  | Menggunakan            | sistem  | (Davis,  | 1989),     |
| --- | --- | --- | ---- | ---------------------- | ------- | -------- | ---------- |
|     |     |     |      | memainkan              | peran   | (Fan     | &  Jiang,  |
|     |     |     |      | penting dalam memberi  |         | 2024)    |            |
saya inspirasi
|     |     |     | PU4  | Menggunakan  | sistem      | (Davis,  | 1989),    |
| --- | --- | --- | ---- | ------------ | ----------- | -------- | --------- |
|     |     |     |      | membantu     | memperkuat  | (Xu      | et  al.,  |
pengetahuan saya
|     |     |     |     |     |     | 2024),  | (Yu  et  |
| --- | --- | --- | --- | --- | --- | ------- | -------- |
al., 2024)
Attitude  Toward  Penilaian pengguna  ATT1  Menggunakan  sistem  (Davis  et  al.,
Using (ATT)
|     | terhadap               | teknologi      |       | merupakan           | ide  yang  | 1989),      | (Xu  et   |
| --- | ---------------------- | -------------- | ----- | ------------------- | ---------- | ----------- | --------- |
|     | baru  yang             | akan           |       | bagus               |            | al., 2024)  |           |
|     | digunakan,             | baik           | ATT2  | Menggunakan         | sistem     | (Davis      | et  al.,  |
|     | bersifat positif atau  |                |       | membuat saya suka   |            |             |           |
|     |                        |                |       |                     |            | 1989),      | (Xu  et   |
|     | negatif                | (Na  et  al.,  |       |                     |            | al., 2024)  |           |
|     | 2022).                 |                | ATT3  | Menggunakan         | sistem     | (Davis      | et  al.,  |
membuat saya terkesan
|     |     |     |     |     |     | 1989),  | (Xu  et  |
| --- | --- | --- | --- | --- | --- | ------- | -------- |
al., 2024)
Confirmation  of  Penilaian  dari  CE1  Pengalaman  (Bhattacherjee,
Expectation (CE)
|     | kinerja sistem yang  |           |      | menggunakan               | sistem      | 2001b), (Xu et   |     |
| --- | -------------------- | --------- | ---- | ------------------------- | ----------- | ---------------- | --- |
|     | aktual               | dengan    |      | melebihi ekspektasi saya  |             | al., 2024), (Yu  |     |
|     | ekspektasi/harapan   |           |      |                           |             | et al., 2024)    |     |
|     | pengguna             | terhadap  | CE2  |                           |             |                  |     |
|     |                      |           |      | Layanan                   | yang        | (Bhattacherjee,  |     |
|     | sistem               |           |      | disediakan                | sistem      | 2001b), (Xu et   |     |
|     | (Bhattacherjee,      |           |      | melebihi ekspektasi saya  |             | al., 2024), (Yu  |     |
|     | 2001b)               |           |      |                           |             | et al., 2024)    |     |
|     |                      |           | CE3  | Menggunakan               | sistem      | (Bhattacherjee,  |     |
|     |                      |           |      | membantu                  | memenuhi    | 2001b), (Xu et   |     |
|     |                      |           |      | layanan                   | yang  saya  | al., 2024), (Yu  |     |
|     |                      |           |      | butuhkan                  |             | et al., 2024)    |     |
Satisfaction  Persepsi  kepuasan  SAT1  Menggunakan  sistem  (Bhattacherjee,
(SAT)  pengguna  terhadap  memenuhi  kebutuhan  2001b), (Xu et
|     | sistem           |     |       | saya,  yang   | membuat       | al., 2024), (Yu  |     |
| --- | ---------------- | --- | ----- | ------------- | ------------- | ---------------- | --- |
|     | (Bhattacherjee,  |     |       | saya bahagia  |               | et al., 2024)    |     |
|     | 2001b)           |     | SAT2  | Pengalaman    |               | (Bhattacherjee,  |     |
|     |                  |     |       | menggunakan   | sistem        | 2001b), (Xu et   |     |
|     |                  |     |       | membuat       | saya  merasa  | al., 2024), (Yu  |     |
|     |                  |     |       | puas          |               | et al., 2024)    |     |
DIGITAL REPOSITORY UNIVERSITAS JEMBER
50

DIGITAL REPOSITORY UNIVERSITAS JEMBER 51

|     |     | SAT3  | Secara       | keseluruhan,  | (Bhattacherjee,  |     |
| --- | --- | ----- | ------------ | ------------- | ---------------- | --- |
|     |     |       | menggunakan  | sistem        | 2001b), (Xu et   |     |
|     |     |       | membuat      | saya  merasa  | al., 2024), (Yu  |     |
|     |     |       | puas  untuk  | membantu      | et al., 2024)    |     |
desain
Emotional  Respon  secara  EE1  Menggunakan  sistem  (Xu  et  al.,
Experience (EE)  emosional  ketika  membuat  saya  merasa  2024),  (Wang
| menggunakan           |     |      | senang dan gembira  |         | & Liu, 2022)  |           |
| --------------------- | --- | ---- | ------------------- | ------- | ------------- | --------- |
| teknologi baru oleh   |     | EE2  | Menggunakan         | sistem  | (Xu           | et  al.,  |
| pengguna (Xu et al.,  |     |      | menghasilkan        | output  | 2024),        | (Wang     |
| 2024)                 |     |      | yang  memberikan    | saya    | & Liu, 2022)  |           |
kesenangan
|     |     | EE3  | Menggunakan  | sistem  | (Xu    | et  al.,  |
| --- | --- | ---- | ------------ | ------- | ------ | --------- |
|     |     |      | membantu     |         | 2024)  |           |
meningkatkan
keterikatan emosional
Interactive  Proses  ketika  IE1  Interaksi  menggunakan  (Xu  et  al.,
Experience (IE)  pengguna  sistem terasa cepat dan  2024),  (Wang
| melakukan interaksi  |       |      | responsif         |               | & Liu, 2022)  |           |
| -------------------- | ----- | ---- | ----------------- | ------------- | ------------- | --------- |
| baik                 | pada  | IE2  | Kecepatan         | dan  akurasi  | (Xu           | et  al.,  |
| antarmuka, operasi,  |       |      | hasil  pencarian  | sistem        | 2024),        | (Wang     |
| serta  fungsi        | pada  |      | memuaskan         |               | & Liu, 2022)  |           |
| teknologi baru (Xu   |       | IE3  | Menggunakan       | sistem        | (Xu           | et  al.,  |
et al., 2024)
|     |     |     | membuat             | saya  nyaman  | 2024),        | (Wang  |
| --- | --- | --- | ------------------- | ------------- | ------------- | ------ |
|     |     |     | dalam berinteraksi  |               | & Liu, 2022)  |        |
Perceived  Persepsi  ketika  PI1  Sistem  memberikan  (Balakrishnan
Intelligence (PI)  pengguna  menilai  kecerdasan pengetahuan  et  al.,  2022;
| karakteristik  |     |     | yang          | memadai  ketika  | Lee    | et  al.,  |
| -------------- | --- | --- | ------------- | ---------------- | ------ | --------- |
| kecerdasan     |     |     | berinteraksi  | dalam            | 2023)  |           |
menyelesaikan tugas
| terhadap   | teknologi  |      |          |           |               |     |
| ---------- | ---------- | ---- | -------- | --------- | ------------- | --- |
| baru  (Xu  | et  al.,   | PI2  | Sistem   | memiliki  | (Huang & Yu,  |     |
| 2024)      |            |      | problem  |           | 2023)         |     |
solving/kemampuan
|     |     |     | menyelesaikan  | masalah  |     |     |
| --- | --- | --- | -------------- | -------- | --- | --- |
yang baik dan efektif
PI3
|     |     |     | Sistem         | membantu  | (Lee   | et  al.,  |
| --- | --- | --- | -------------- | --------- | ------ | --------- |
|     |     |     | menyelesaikan  | tugas     | 2023)  |           |
dengan cepat
PI4
|     |     |     | Sistem                  | mampu  | (Lee           | et  al.,  |
| --- | --- | --- | ----------------------- | ------ | -------------- | --------- |
|     |     |     | memahami intruksi yang  |        | 2023),         |           |
|     |     |     | saya berikan            |        | (Balakrishnan  |           |
et al., 2022)
|     |     | PI5  | Sistem dapat memahami  |                  | (Lee   | et  al.,  |
| --- | --- | ---- | ---------------------- | ---------------- | ------ | --------- |
|     |     |      | Riwayat                | interaksi  yang  | 2023)  |           |
|     |     |      | saya                   | berikan          |        |           |
sebelumnya
Perceived Novelty  Persepsi  ketika  PN1  Menggunakan  sistem  (Wells  et  al.,
(PN)
| pengguna            | menilai   |      | membuat      | saya         | 2010), (Huang  |           |
| ------------------- | --------- | ---- | ------------ | ------------ | -------------- | --------- |
| kebaruan            | dan       |      | menemukan    |              | & Yu, 2023)    |           |
| keunikan            | terhadap  |      | pengalaman   | baru  (atau  |                |           |
| teknologi baru (Xu  |           |      | unik)        |              |                |           |
| et al., 2024)       |           | PN2  | Menggunakan  | sistem       | (Wells         | et  al.,  |
|                     |           |      | membuat      | saya         | 2010), (Huang  |           |
|                     |           |      | menemukan    | hal  baru    | & Yu, 2023)    |           |
dan refreshing
DIGITAL REPOSITORY UNIVERSITAS JEMBER

| DIGITAL REPOSITORY UNIVERSITAS JEMBER |     |     |     |     |     |     |     | 52  |
| ------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |

|     |     |     | PN3  | Sistem                  |            | memberikan  | (Wells         | et  al.,  |
| --- | --- | --- | ---- | ----------------------- | ---------- | ----------- | -------------- | --------- |
|     |     |     |      | suatu hal yang berbeda  |            |             | 2010), (Huang  |           |
|     |     |     |      | dengan                  | teknologi  | yang        | & Yu, 2023)    |           |
sudah ada dan menarik
PN4
|     |     |     |     | Menggunakan  |           | sistem        | (Wells         | et  al.,  |
| --- | --- | --- | --- | ------------ | --------- | ------------- | -------------- | --------- |
|     |     |     |     | membuat      |           | saya  merasa  | 2010), (Huang  |           |
|     |     |     |     | sebagai      | cara      | sederhana     | & Yu, 2023)    |           |
|     |     |     |     | dan          | inovatif  | dalam         |                |           |
menyelesaikan tugas
Perceived  Trust  Tingkat  PT1  Saya  merasa  percaya  (Nguyen et al.,
| (PT)  | kepercayaan         |           |      | terhadap               |         | keandalan  | 2021),           | (Xu  et  |
| ----- | ------------------- | --------- | ---- | ---------------------- | ------- | ---------- | ---------------- | -------- |
|       | pengguna            | terhadap  |      | sistem                 |         |            | al., 2023)       |          |
|       | teknologi baru (Xu  |           | PT2  | Saya                   | merasa  | percaya    | (Nguyen et al.,  |          |
|       | et al., 2024)       |           |      | pada sumber data yang  |         |            | 2021),           | (Xu  et  |
|       |                     |           |      | digunakan sistem       |         |            | al., 2023)       |          |
|       |                     |           | PT3  | Saya                   |         | memiliki   | (Nguyen et al.,  |          |
|       |                     |           |      | keyakinan              |         | terhadap   | 2021),           | (Xu  et  |
|       |                     |           |      | perlindungan           |         | privasi    | al., 2023)       |          |
dari sistem
|     |     |     | PT4  | Saya                   | percaya  | bahwa  | (Nguyen et al.,  |          |
| --- | --- | --- | ---- | ---------------------- | -------- | ------ | ---------------- | -------- |
|     |     |     |      | sistem dapat membantu  |          |        | 2021),           | (Xu  et  |
|     |     |     |      | saya                   |          | dalam  | al., 2023)       |          |
menggunakannya
dengan cara yang tepat
Perceived  Sejauh  mana  PP1  Menggunakan  sistem  (Fan  &  Jiang,
Playfulness (PP)  pengguna  merasa  membuat  saya  merasa  2024),  (Moon
|     |                |           |      | tertarik          |     |         | & Kim, 2001)  |            |
| --- | -------------- | --------- | ---- | ----------------- | --- | ------- | ------------- | ---------- |
|     | fokus,  ingin  | tahu,     |      |                   |     |         |               |            |
|     | dan            | memiliki  | PP2  | Menggunakan       |     | sistem  | (Fan          | &  Jiang,  |
|     | kesenangan     | ketika    |      | membuat           |     | saya    | 2024),        | (Moon      |
|     |                |           |      | menikmati proses  |     |         | & Kim, 2001)  |            |
berinteraksi dengan
|     | teknologi  | baru     | PP3  | Sistem      |     | memberikan  | (Fan          | &  Jiang,  |
| --- | ---------- | -------- | ---- | ----------- | --- | ----------- | ------------- | ---------- |
|     | (Moon      | &  Kim,  |      | kemudahan   |     | dan         | 2024),        | (Moon      |
|     | 2001)      |          |      |             |     |             | & Kim, 2001)  |            |
|     |            |          |      | kesenangan  |     | ketika      |               |            |
menyelesaikan tugas
Continuance  Keputusan  untuk  CI1  Saya  akan  terus  (Bhattacherjee,
| Intention (CI)  |                    |          |     |              |                |         | 2001a)  |     |
| --------------- | ------------------ | -------- | --- | ------------ | -------------- | ------- | ------- | --- |
|                 | terus menggunakan  |          |     | menggunakan  |                | sistem  |         |     |
|                 | teknologi          | setelah  |     | dalam        | menyelesaikan  |         |         |     |
|                 | sebelumnya pernah  |          |     | tugas        |                |         |         |     |
CI2
|     | menggunakannya  |           |     | Saya              |       | sangat  | (Bhattacherjee,  |     |
| --- | --------------- | --------- | --- | ----------------- | ----- | ------- | ---------------- | --- |
|     | (Venkatesh      | et  al.,  |     | merekomendasikan  |       |         | 2001b)           |     |
|     | 2011)           |           |     | orang             | lain  | untuk   |                  |     |
menggunakan sistem
|     |     |     | CI3  | Saya          | lebih  | memilih  | (Venkatesh  | et  |
| --- | --- | --- | ---- | ------------- | ------ | -------- | ----------- | --- |
|     |     |     |      | menggunakan   |        | sistem   | al., 2011)  |     |
|     |     |     |      | dibandingkan  |        | dengan   |             |     |
sistem lain sejenis
|     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
DIGITAL REPOSITORY UNIVERSITAS JEMBER

| DIGITAL REPOSITORY UNIVERSITAS JEMBER |     |     |     |     |     |     |     | 53  |
| ------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |

Lampiran  2 Hipotesis Penelitian
| Variabel  | Kode  |     | Hipotesis  |     | Landasan  |     |     |     |
| --------- | ----- | --- | ---------- | --- | --------- | --- | --- | --- |
ECM  H1  Satisfaction (SAT)  (Yu et al., 2024) dalam penelitian dengan
|     |     | berpengaruh positif dan  |     | objek                                    | AI  Design  |           | Painting     | Tools  |
| --- | --- | ------------------------ | --- | ---------------------------------------- | ----------- | --------- | ------------ | ------ |
|     |     | signifikan terhadap      |     | menemukan                                | bahwa       | SAT       | berpengaruh  |        |
|     |     | Continuance Intention    |     | positif dan signifikan terhadap CI. Hal  |             |           |              |        |
|     |     | (CI)                     |     | tersebut                                 | menandakan  | apabila   | pengguna     |        |
|     |     |                          |     | merasa                                   | puas        | Ketika    | menggunakan  |        |
|     |     |                          |     | aplikasi,                                | maka        | pengguna  | akan         | terus  |
menggunakan aplikasi tersebut.
|     | H2a  | Confirmation             |     | Penelitian  | (Xu       | et  al.,  | 2024)  pada  | AI      |
| --- | ---- | ------------------------ | --- | ----------- | --------- | --------- | ------------ | ------- |
|     |      | Expectation (CE)         |     | Design      | Painting  | Tools     | menunjukkan  |         |
|     |      | berpengaruh positif dan  |     | bahwa       | terdapat  | pengaruh  | positif      | dan     |
|     |      | signifikan terhadap      |     | signifikan  | dari      | CE        | terhadap     | SAT.    |
|     |      | Satisfaction (SAT)       |     | Hipotesis   | ini       | juga      | sejalan      | dengan  |
penelitian Fan & Jiang (2024) dan Yu et
al. (2024), yang dapat diartikan bahwa
jika AI dapat memenuhi bahkan melebihi
ekspektasi dari desainer, maka desainer
|     |     |     |     | tidak  hanya  | merasa       | puas       | namun     | juga  |
| --- | --- | --- | --- | ------------- | ------------ | ---------- | --------- | ----- |
|     |     |     |     | bahwa         | tools  yang  | digunakan  | memiliki  |       |
nilai praktis dalam pekerjaan mereka
|     | H2b  | Confirmation             |     | Penemuan Xu et al. (2024) memperoleh    |                   |          |            |         |
| --- | ---- | ------------------------ | --- | --------------------------------------- | ----------------- | -------- | ---------- | ------- |
|     |      | Expectation (CE)         |     | hasil bahwa pengaruh CE terhadap PU     |                   |          |            |         |
|     |      | berpengaruh positif dan  |     | positif                                 | dan  signifikan.  |          | Ini  juga  | linier  |
|     |      | signifikan terhadap      |     | dengan                                  | penelitian        | oleh     | Fan  &     | Jiang   |
|     |      | Perceived Usefulness     |     | (2024)                                  | dan  Yu           | et  al.  | (2024)     | yang    |
|     |      | (PU)                     |     | diimplementasikan pada AI dengan objek  |                   |          |            |         |
tools AI desain gambar.
|     | H2c  | Confirmation             |     | Fan & Jiang (2024) pada objek penelitian  |          |           |              |     |
| --- | ---- | ------------------------ | --- | ----------------------------------------- | -------- | --------- | ------------ | --- |
|     |      | Expectation (CE)         |     | tools  AI                                 | desain   | gambar    | menunjukkan  |     |
|     |      | berpengaruh positif dan  |     | bahwa CE berpengaruh positif terhadap     |          |           |              |     |
|     |      | signifikan terhadap      |     | PP. Hal ini dapat diartikan bahwa jika    |          |           |              |     |
|     |      | Perceived Playfulness    |     | persepsi                                  | harapan  | pengguna  | terhadap     |     |
(PP)
aplikasi terpenuhi, mampu meningkatkan
|     |     |     |     | kesenangan  |     | pengguna  |     | dalam  |
| --- | --- | --- | --- | ----------- | --- | --------- | --- | ------ |
menggunakan aplikasi. Penelitian ini juga
|     |     |     |     | konsisten dengan H. Liu et al.  |     |     |     | (2021)  |
| --- | --- | --- | --- | ------------------------------- | --- | --- | --- | ------- |
dengan objek aplikais E-Book.
TAM  H3a  Perceived Usefulness  Dalam  penelitian  Xu  et  al.  (2024)
|     |     | (PU) berpengaruh positif  |     | menunjukkan bahwa persepsi kegunaan  |             |           |            |         |
| --- | --- | ------------------------- | --- | ------------------------------------ | ----------- | --------- | ---------- | ------- |
|     |     | dan signifikan terhadap   |     | berpengaruh                          | positif     | terhadap  | kepuasan   |         |
|     |     | Satisfaction (SAT)        |     | pengguna. Hipotesis ini juga         |             |           | konsisten  |         |
|     |     |                           |     | dengan                               | penelitian  | Wu        | &  Song    | (2021)  |
|     |     |                           |     | yang  diimplementasikan              |             |           | pada       | objek   |
aplikasi e-commerce.
|     | H3b  | Perceived Usefulness      |     | Berdasarkan penelitian Belda-Medina &   |     |     |     |     |
| --- | ---- | ------------------------- | --- | --------------------------------------- | --- | --- | --- | --- |
|     |      | (PU) berpengaruh positif  |     | Calvo-Ferrer (2022) pada objek chatbot  |     |     |     |     |
|     |      | dan signifikan terhadap   |     | menemukan pengaruh positif dari PU      |     |     |     |     |
|     |      | Continuance Intention     |     | pada CI. Hiposesis tersebut juga        |     |     |     |     |
(CI)
konsisten pada penelitian Na et al. (2022)
yang dilakukan pada objek penelitian AI.
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER 54

| H3c  | Perceived Usefulness      | Penelitian                              | Xu        | et    | al.       | (2024)     |
| ---- | ------------------------- | --------------------------------------- | --------- | ----- | --------- | ---------- |
|      | (PU) berpengaruh positif  | mengemukakan bahwa PU berpengaruh       |           |       |           |            |
|      | dan signifikan terhadap   | positif                                 | terhadap  | ATT.  | Hal  ini  | sejalan    |
|      | Attitude Toward Using     | dengan hasil penelitian Belda-Medina &  |           |       |           |            |
|      | (ATT)                     | Calvo-Ferrer                            | (2022)    |       | dengan    | objek      |
|      |                           | penelitian                              | chatbot   | AI.   | Dapat     | diartikan  |
bahwa apabila aplikasi memiliki tingkat
|     |     | kemudahan  | yang  | baik,  | pengguna  | akan  |
| --- | --- | ---------- | ----- | ------ | --------- | ----- |
memiliki sikap positif.
| H4  | Attitude Toward Using   | Penelitian Na et al. (2022) pada objek AI  |             |               |              |     |
| --- | ----------------------- | ------------------------------------------ | ----------- | ------------- | ------------ | --- |
|     | (ATT) berpengaruh       | mencatat                                   | bahwa       | ATT           | berpengaruh  |     |
|     | positif dan signifikan  | terhadap CI. Hipotesis ini juga diperkuat  |             |               |              |     |
|     | terhadap Continuance    | dengan                                     | penelitian  | Belda-Medina  |              | &   |
|     | Intention (CI)          | Calvo-Ferrer (2022) dengan objek chatbot   |             |               |              |     |
AI serta Xu et al. (2024) dengan objek AI
|     |     | desain.        | Hal  ini  | dapat  | diartikan  | bahwa     |
| --- | --- | -------------- | --------- | ------ | ---------- | --------- |
|     |     | ketika  sikap  | pengguna  |        | positif    | terhadap  |
aplikasi, niat penggunaan berkelanjutan
akan tinggi.
UX  H5  Emotional Experience  Penelitian Xu et al. (2024) menunjukkan
|     | (EE) berpengaruh positif  | bahwa hubungan EE dengan CI memiliki       |         |              |         |        |
| --- | ------------------------- | ------------------------------------------ | ------- | ------------ | ------- | ------ |
|     | dan signifikan terhadap   | pengaruh                                   | paling  | signifikan   |         | pada   |
|     | Continuance Intention     | penelitian yang dilakukan. Penelitian ini  |         |              |         |        |
|     | (CI)                      | juga didukung oleh Lu et al. (2024) dan    |         |              |         |        |
|     |                           | Cheng                                      | &       | Jiang        | (2020)  | yang   |
|     |                           | mengemukakan                               |         | bahwa        | UX      | dapat  |
|     |                           | meingkatkan                                |         | efektivitas  |         | yang   |
berpengaruh langsung terhadap loyalitas
|     |     | pengguna  | dalam  | niat  | penggunaan  |     |
| --- | --- | --------- | ------ | ----- | ----------- | --- |
berkelanjutan.
H6
|     | Interactive Experience    | Penelitian Lu et al. (2024) pada objek AI   |         |          |                  |       |
| --- | ------------------------- | ------------------------------------------- | ------- | -------- | ---------------- | ----- |
|     | (IE) berpengaruh positif  | menunjukkan                                 | bahawa  |          | IE  berpengaruh  |       |
|     | dan signifikan terhadap   | positif terhadap CI. Hal ini juga didukung  |         |          |                  |       |
|     | Continuance Intention     | oleh  Sutcliffe                             |         | &  Hart  | (2017)           | yang  |
|     | (CI)                      | menyatakan bahwa interaktivitas dalam       |         |          |                  |       |
pengalaman pengguna penting sehingga
|     |     | dapat  | mendorong  |     | penggunaan  |     |
| --- | --- | ------ | ---------- | --- | ----------- | --- |
berkelanjutan.
Karakteristik  H7a  Perceived Intelligence  Berdasarkan  penelitian  Huang  &  Yu
AI Design  (PI) berpengaruh positif  (2023)  yang  dilakukan  pada  AI  news
Tools
|     | dan signifikan terhadap  | anchor menunjukkan adanya hubungan  |               |              |       |           |
| --- | ------------------------ | ----------------------------------- | ------------- | ------------ | ----- | --------- |
|     | Perceived Trust (PT)     | positif                             | PI  terhadap  |              | PT.   | Hal  ini  |
|     |                          | menunjukkan                         | bahwa         | kecerdasan   |       | yang      |
|     |                          | dihasilkan                          | oleh          | AI  dengan   | baik  | akan      |
|     |                          | membentuk                           | tingkat       | kepercayaan  |       | yang      |
kuat dalam menggunakan aplikasi.
H7b
|     | Perceived Intelligence    | Berdasarkan                                  | penelitian  |        | Balakrishnan     | et       |
| --- | ------------------------- | -------------------------------------------- | ----------- | ------ | ---------------- | -------- |
|     | (PI) berpengaruh positif  | al.,  (2022)                                 | pada        | studi  | case             | chatbot  |
|     | dan signifikan terhadap   | menunjukkan                                  | bahwa       |        | PI  berpengaruh  |          |
|     | Continuance Intention     | positif dan signifikan terhadap CI. Hal ini  |             |        |                  |          |
|     | (CI)                      | dapat diartikan bahwa semakin tinggi PI      |             |        |                  |          |
|     |                           | dapat  memengaruhi                           |             | niat   | penggunaan       |          |
berkelanjutan pengguna.
| H8  | Perceived Trust (PT)     | Penelitian  | Nguyen         | et  | al.  (2021)  | pada  |
| --- | ------------------------ | ----------- | -------------- | --- | ------------ | ----- |
|     | berpengaruh positif dan  | chatbot     | AI  M-Banking  |     | menunjukkan  |       |
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER 55

| signifikan terhadap    | bahwa       | tingkat  | kepercayaan  |             | terhadap  |
| ---------------------- | ----------- | -------- | ------------ | ----------- | --------- |
| Continuance Intention  | aplikasi    | menjadi  |              | pengaruh    | paling    |
| (CI)                   | signifikan  | dalam    |              | penelitian  | yang      |
dilakukan. Hal tersebut juga linier dengan
penelitian Xu et al. (2024) pada AI design
|     | tools  yang  | menunjukkan  |     |     | bahwa  PT  |
| --- | ------------ | ------------ | --- | --- | ---------- |
memengaruhi signifikan terhadap CI.
| H9a  Perceived Novelty (PN)  | Penelitian Xu et al. (2024) pada objek AI  |                     |           |          |             |
| ---------------------------- | ------------------------------------------ | ------------------- | --------- | -------- | ----------- |
| berpengaruh positif dan      | design                                     | tools  menunjukkan  |           |          | bahwa  PN   |
| signifikan terhadap          | berpengaruh positif terhadap SAT. Hal ini  |                     |           |          |             |
| Satisfaction (SAT)           | juga                                       | konsisten           | dalam     |          | mendukung   |
|                              | pernyataan                                 | Vakratsas           |           | &  Wang  | (2020)      |
|                              | yang  membahas                             |                     | mengenai  |          | pentingnya  |
novelty dalam aplikasi AI.
H9b
| Perceived Novelty (PN)   | Berdasarkan penelitian Xu et al. (2024)    |        |     |          |              |
| ------------------------ | ------------------------------------------ | ------ | --- | -------- | ------------ |
| berpengaruh positif dan  | menyatakan                                 | bahwa  |     | PN       | berpengaruh  |
| signifikan terhadap      | positif pada CI namun tidak berpengaruh    |        |     |          |              |
| Continuance Intention    | langsung yang signifikan. Hal ini artinya  |        |     |          |              |
| (CI)                     | PN  memengaruhi                            |        | CI  | melalui  | variabel     |
mediasi.
H10a
| Perceived Playfulness     | Penelitian Fan & Jiang (2024) pada objek  |             |              |           |               |
| ------------------------- | ----------------------------------------- | ----------- | ------------ | --------- | ------------- |
| (PP) berpengaruh positif  | AI design tools mengemukakan bahwa PP     |             |              |           |               |
| dan signifikan terhadap   | berpengaruh                               |             | positif      | dan       | siginifikan   |
| Satisfaction (SAT)        | terhadap                                  | SAT.        | Hubungan     |           | ini  menjadi  |
|                           | salah  satu                               | hubungan    |              | paling    | kuat  pada    |
|                           | model                                     | yang        | dianalisis.  | Hal       | tersebut      |
|                           | membuktikan                               |             | bahwa        | semakin   | tinggi        |
|                           | tingkat                                   | kesenangan  |              | pengguna  | dalam         |
|                           | menggunakan                               |             | aplikasi,    | semakin   | tinggi        |
pula tingkat kepuasan yang dirasakan.
H10b
| Perceived Playfulness     | Dalam                                     | Lin  et  | al.          | (2005)      | penelitian    |
| ------------------------- | ----------------------------------------- | -------- | ------------ | ----------- | ------------- |
| (PP) berpengaruh positif  | menunjukkan bahwa PP mempengaruhi         |          |              |             |               |
| dan signifikan terhadap   | secara signifikan pengguna untuk terus    |          |              |             |               |
| Continuance Intention     | menggunakan                               |          | aplikasi.    | Penelitian  | ini           |
| (CI)                      | dapat diartikan bahwa tingkat kesenangan  |          |              |             |               |
|                           | pengguna                                  | menjadi  | salah        |             | satu  faktor  |
|                           | penting                                   | yang     | memengaruhi  |             | pengguna      |
untuk terus menggunakan aplikasi.

DIGITAL REPOSITORY UNIVERSITAS JEMBER

| DIGITAL REPOSITORY UNIVERSITAS JEMBER |     |     | 56  |
| ------------------------------------- | --- | --- | --- |

Lampiran  3 Instrumen Penelitian
| Kode  | Pernyataan  | Indikator Penilaian  |        |
| ----- | ----------- | -------------------- | ------ |
|       |             | STS  TS              | S  SS  |
|       |             | 1  2                 | 3  4   |
Perceived Usefulness (PU)
*Tingkat kepercayaan pengguna ketika menggunakan suatu sistem tertentu akan meningkatkan
kinerjanya
PU1  Saya merasa dengan menggunakan aplikasi Figma Make
memungkinkan saya untuk dapat menyelesaikan tugas
lebih cepat
PU2  Saya merasa menggunakan aplikasi Figma Make membuat
pekerjaan saya lebih mudah dilakukan.
PU3  Saya merasa aplikasi Figma Make memainkan peran
penting dalam memberi saya inspirasi
| PU4  |     |     |     |
| ---- | --- | --- | --- |
Saya merasa menggunakan aplikasi Figma Make
membantu memperkuat pengetahuan saya
Attitude Toward Using (ATT)
*Penilaian pengguna terhadap teknologi baru yang akan digunakan, baik bersifat positif atau
negatif
ATT1  Menggunakan aplikasi Figma Make merupakan ide yang
bagus bagi saya
| ATT2  Saya suka menggunakan aplikasi Figma Make   |     |     |     |
| ------------------------------------------------- | --- | --- | --- |
Saya terkesan menggunakan aplikasi Figma Make
| ATT3  |     |     |     |
| ----- | --- | --- | --- |
Confirmation of Expectation (CE)
*Penilaian dari kinerja sistem yang aktual dengan ekspektasi/harapan pengguna terhadap sistem
| CE1  Saya merasa pengalaman menggunakan Figma Make  |     |     |     |
| --------------------------------------------------- | --- | --- | --- |
melebihi ekspektasi yang saya harapkan
CE2  Saya merasa layanan yang disediakan aplikasi Figma
Make melebihi ekspektasi saya
| CE3  Saya merasa menggunakan aplikasi Figma Make  |     |     |     |
| ------------------------------------------------- | --- | --- | --- |
membantu memenuhi layanan yang saya butuhkan
Satisfaction (SAT)
*Persepsi kepuasan pengguna terhadap sistem
SAT1  Aplikasi Figma Make memenuhi kebutuhan saya, yang
membuat saya merasa bahagia
SAT2  Pengalaman menggunakan aplikasi Figma Make membuat
saya merasa puas
SAT3
| Secara keseluruhan, menggunakan aplikasi Figma Make  |     |     |     |
| ---------------------------------------------------- | --- | --- | --- |
membuat saya merasa puas untuk membantu desain
Emotional Experience (EE)
*Respon secara emosional ketika menggunakan teknologi baru oleh pengguna
EE1  Saya merasa menggunakan aplikasi Figma Make membuat
saya merasa senang dan gembira
| EE2  Saya merasa menggunakan aplikasi Figma Make  |     |     |     |
| ------------------------------------------------- | --- | --- | --- |
menghasilkan output yang memberikan saya kesenangan
| EE3  Saya merasa menggunakan Figma Make membantu  |     |     |     |
| ------------------------------------------------- | --- | --- | --- |
meningkatkan keterikatan emosional
Interactive Experience (IE)
* Proses ketika pengguna melakukan interaksi baik pada antarmuka, operasi, serta fungsi pada
teknologi baru
| IE1  |     |     |     |
| ---- | --- | --- | --- |
Saya merasa interaksi menggunakan aplikasi Figma Make
terasa cepat dan responsif
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
57
IE2 Saya merasa kecepatan dan akurasi hasil pencarian aplikasi
Figma Make memuaskan
IE3 Saya merasa menggunakan aplikasi Figma Make membuat
saya nyaman dalam berinteraksi
Perceived Intelligence (PI)
* Persepsi ketika pengguna menilai karakteristik kecerdasan terhadap teknologi baru
PI1 Saya merasa aplikasi Figma Make dapat menyelesaikan
tugas dengan cerdas
PI2 Saya merasa aplikasi Figma Make sangat efektif dalam
menyelesaikan masalah
PI3 Saya merasa aplikasi Figma Make membantu
menyelesaikan tugas dengan cepat
PI4 Saya merasa aplikasi Figma Make mampu memahami
intruksi yang saya berikan dengan baik
PI5 Saya merasa aplikasi Figma Make dapat memahami
Riwayat interaksi yang saya berikan sebelumnya
Perceived Novelty (PN)
* Persepsi ketika pengguna menilai kebaruan dan keunikan terhadap teknologi baru
PN1 Saya merasa menggunakan aplikasi Figma Make membuat
saya menemukan pengalaman baru (atau unik)
PN2 Saya merasa menggunakan aplikasi Figma Make membuat
saya menemukan hal baru dan refreshing
PN3 Saya merasa aplikasi Figma Make memberikan suatu hal
yang berbeda dengan teknologi yang sudah ada dan
menarik
PN4 Saya merasa menggunakan Figma Make menjadi cara
sederhana dan inovatif dalam menyelesaikan tugas
Perceived Trust (PT)
* Tingkat kepercayaan pengguna terhadap teknologi baru
PT1 Saya merasa percaya terhadap keandalan aplikasi Figma
Make
PT2 Saya merasa percaya pada sumber data yang digunakan
aplikasi Figma Make
PT3 Saya memiliki keyakinan terhadap perlindungan privasi
dari aplikasi Figma Make
PT4 Saya percaya bahwa aplikasi Figma Make dapat membantu
saya dalam menggunakannya dengan cara yang tepat
Perceived Playfulness (PP)
*Sejauh mana pengguna merasa fokus, ingin tahu, dan memiliki kesenangan ketika berinteraksi
dengan teknologi baru
PP1 Saya merasa menggunakan aplikasi Figma Make membuat
saya merasa tertarik
PP2 Saya merasa menggunakan aplikasi Figma Make membuat
saya menikmati proses
PP3 Saya merasa aplikasi Figma Make memberikan
kemudahan dan kesenangan ketika menyelesaikan tugas
Continuance Intention (CI)
*Keputusan untuk terus menggunakan teknologi setelah sebelumnya pernah menggunakannya
CI1 Saya akan terus menggunakan aplikasi Figma Make dalam
menyelesaikan tugas
CI2 Saya merekomendasikan orang lain untuk menggunakan
aplikasi Figma Make
CI3 Saya lebih memilih menggunakan aplikasi Figma Make
dibandingkan dengan aplikasi lain sejenis
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
58
Lampiran 4 Distribusi Responden
No Kelompok Gambar
Distribusi
1 Distribusi
Responden
Berdasarkan Jenis
Kelamin
2 Distribusi
Responden
Berdasarkan
Pekerjaan
3 Distribusi
Responden
Berdasarkan
Frekuensi
Penggunaan
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
59
Lampiran 5 Hasil Uji Validitas Diskriminan Cross Loading
ATT CE CI EE IE PI PN PP PT PU SAT
ATT1 0,721 0,566 0,217 0,612 0,562 0,506 0,361 0,533 0,515 0,278 0,483
ATT2 0,939 0,708 0,116 0,723 0,627 0,466 0,455 0,738 0,493 0,640 0,674
ATT3 0,898 0,654 0,078 0,501 0,551 0,428 0,531 0,489 0,548 0,499 0,623
CE1 0,657 0,878 0,113 0,401 0,472 0,556 0,251 0,404 0,690 0,422 0,654
CE2 0,582 0,874 0,224 0,569 0,646 0,505 0,209 0,592 0,457 0,401 0,662
CE3 0,626 0,707 0,101 0,461 0,463 0,274 0,249 0,462 0,433 0,445 0,446
-
CI1 0,181 0,282 0,846 0,237 0,151 0,129 0,050 0,102 0,135 0,105 0,176
-
CI2 0,158 0,169 0,937 0,363 0,228 0,269 0,052 0,106 0,159 0,147 0,179
- - - - -
CI3 0,094 -0,103 0,734 0.,007 0,119 0,000 0,088 0,047 -0,064 0,112 0,037
EE1 0,704 0,589 0,153 0,854 0,549 0,500 0,468 0,741 0,513 0,509 0,842
EE2 0,642 0,485 0,370 0,962 0,523 0,575 0,448 0,686 0,526 0,391 0,601
EE3 0,513 0,550 0,106 0,723 0,535 0,619 0,377 0,546 0,466 0,292 0,519
IE1 0,638 0,601 0,211 0,537 0,859 0,387 0,348 0,353 0,387 0,375 0,538
IE2 0,502 0,485 0,139 0,530 0,801 0,411 0,448 0,485 0,273 0,395 0,457
IE3 0,465 0,473 0,157 0,378 0,780 0,489 0,564 0,423 0,550 0,383 0,513
PI1 0,419 0,537 -0,076 0,342 0,333 0,803 0,510 0,514 0,707 0,572 0,411
PI2 0,395 0,377 0,274 0,485 0,285 0,796 0,468 0,468 0,580 0,265 0,378
PI4 0,435 0,465 0,190 0,539 0,452 0,834 0,451 0,565 0,542 0,461 0,510
PI5 0,444 0,392 0,287 0,660 0,593 0,790 0,358 0,451 0,632 0,358 0,599
PN1 0,277 0,146 -0,053 0,322 0,299 0,572 0,773 0,359 0,494 0,330 0,091
PN2 0,501 0,245 -0,095 0,484 0,513 0,402 0,880 0,534 0,403 0,364 0,326
PN3 0,306 0,141 0,167 0,413 0,432 0,415 0,727 0,356 0,538 0,233 0,375
PN4 0,530 0,328 -0,199 0,374 0,452 0,521 0,899 0,500 0,525 0,425 0,409
PP1 0,572 0,498 0,329 0,626 0,557 0,565 0,497 0,801 0,488 0,360 0,642
PP2 0,566 0,505 -0,082 0,633 0,367 0,410 0,360 0,854 0,440 0,395 0,643
PP3 0,586 0,472 -0,051 0,615 0,298 0,568 0,511 0,832 0,514 0,576 0,495
PT1 0,588 0,717 0,168 0,528 0,499 0,594 0,388 0,461 0,851 0,450 0,564
PT2 0,308 0,404 0,131 0,411 0,342 0,659 0,454 0,459 0,857 0,473 0,444
PT3 0,469 0,496 0,149 0,430 0,422 0,680 0,515 0,462 0,809 0,562 0,599
PT4 0,629 0,542 -0,008 0,563 0,408 0,639 0,619 0,560 0,839 0,449 0,554
PU1 0,412 0,338 0,069 0,302 0,258 0,529 0,355 0,356 0,387 0,784 0,325
PU2 0,582 0,495 -0,046 0,489 0,424 0,526 0,490 0,522 0,600 0,891 0,554
PU3 0,401 0,272 0,130 0,337 0,406 0,379 0,463 0,431 0,431 0,873 0,300
PU4 0,479 0,501 0,209 0,318 0,424 0,262 0,087 0,393 0,443 0,742 0,317
SAT1 0,569 0,567 0,099 0,722 0,483 0,492 0,289 0,607 0,501 0,361 0,813
SAT2 0,603 0,699 0,226 0,707 0,527 0,544 0,422 0,644 0,603 0,430 0,930
SAT3 0,626 0,569 0,079 0,407 0,586 0,474 0,355 0,604 0,539 0,410 0,810
DIGITAL REPOSITORY UNIVERSITAS JEMBER

| DIGITAL REPOSITORY UNIVERSITAS JEMBER |     |     |     |     |     |     |     |     | 60  |
| ------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

Lampiran  6 Hasil Uji Validitas Diskriminan Fornell-Lacker Criterion

|     | ATT  | CE  | CI  | EE  | IE  PI  | PN  PP  | PT  | PU  | SAT  |
| --- | ---- | --- | --- | --- | ------- | ------- | --- | --- | ---- |

ATT  0,858
|     |        |        |        |        |               |     |     |     |     |
| --- | ------ | ------ | ------ | ------ | ------------- | --- | --- | --- | --- |
| CE  | 0,750  | 0,824  |        |        |               |     |     |     |     |
|     |        |        |        |        |               |     |     |     |     |
| CI  | 0,142  | 0,182  | 0,843  |        |               |     |     |     |     |
|     |        |        |        |        |               |     |     |     |     |
| EE  | 0,710  | 0,582  | 0,305  | 0,852  |               |     |     |     |     |
| IE  | 0,669  | 0,647  | 0,213  | 0,594  | 0,814         |     |     |     |     |
| PI  | 0,526  | 0,549  | 0,209  | 0,630  | 0,519  0,806  |     |     |     |     |
PN  0,525  0,284  -0,065  0,493  0,540  0,554  0,823
PP  0,693  0,595  0,091  0,755  0,502  0,618  0,548  0,829
PT  0,589  0,638  0,132  0,572  0,496  0,768  0,590  0,578  0,839
PU  0,584  0,510  0,105  0,450  0,468  0,514  0,414  0,525  0,579  0,825
SAT  0,701  0,721  0,164  0,721  0,621  0,591  0,420  0,724  0,644  0,470  0,853
|     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER 61

Lampiran  7 Analisis Hasil Uji Hipotesis
| Variabel  | Hipotesis  |     |     | Analisis Hipotesis  |     |     |     | Keterangan  |
| --------- | ---------- | --- | --- | ------------------- | --- | --- | --- | ----------- |
ECM
|     | SAT -> CI  | H1: Satisfaction (SAT) berpengaruh positif dan  |     |     |     |     |     | Diterima  |
| --- | ---------- | ----------------------------------------------- | --- | --- | --- | --- | --- | --------- |
signifikan terhadap Continuance Intention (CI)

Berdasarkan hasil pengujian hipotesis pada Tabel
|     |     | 4.3.2a,          | hubungan     |                 | antara     | Satisfaction  |           | (SAT)  |
| --- | --- | ---------------- | ------------ | --------------- | ---------- | ------------- | --------- | ------ |
|     |     | terhadap         | Continuance  |                 | Intention  | (CI)          | memiliki  |        |
|     |     | nilai  Original  |              | Sample          | sebesar    |               | 0,243     | yang   |
|     |     | menunjukkan      |              | arah  hubungan  |            | positif.      | Nilai     | T-     |
Statistic sebesar 2,348 yang lebih besar dari batas
kritis 1,96, serta P-Value sebesar 0,019 yang lebih
kecil dari 0,05, menunjukkan bahwa hubungan
|     |     | tersebut  | signifikan  | secara  |     | statistik.  | Selain  | itu,  |
| --- | --- | --------- | ----------- | ------- | --- | ----------- | ------- | ----- |
nilai effect size (f²) sebesar 0,049 termasuk dalam
kategori pengaruh kecil, yang mengindikasikan
|     |     | bahwa  | kepuasan  |     | pengguna  |     | memberikan  |     |
| --- | --- | ------ | --------- | --- | --------- | --- | ----------- | --- |
kontribusi terbatas namun tetap bermakna dalam
menjelaskan niat penggunaan berkelanjutan.
|     |     | Artinya,  | semakin  |     | tinggi  | tingkat  | kepuasan  |     |
| --- | --- | --------- | -------- | --- | ------- | -------- | --------- | --- |
pengguna terhadap penggunaan sistem, baik dari
|     |     | segi  pengalaman  |         |     | penggunaan,  |     | pemenuhan  |        |
| --- | --- | ----------------- | ------- | --- | ------------ | --- | ---------- | ------ |
|     |     | harapan,          | maupun  |     | kenyamanan   |     |            | dalam  |
menyelesaikan tugas, maka niat pengguna untuk
terus menggunakan sistem akan meningkat secara
|     |     | signifikan.  | Meskipun        |             |           | pengaruhnya  |              | tidak   |
| --- | --- | ------------ | --------------- | ----------- | --------- | ------------ | ------------ | ------- |
|     |     | dominan,     | kepuasan        |             | berperan  | sebagai      |              | faktor  |
|     |     | pendukung    |                 | penting     |           | dalam        | mendorong    |         |
|     |     | penggunaan   | berkelanjutan,  |             |           | khususnya    |              | dalam   |
|     |     | konteks AI   | Design          |             | Tools     | pada         | Figma        | Make.   |
|     |     | Hubungan     | yang            | signifikan  |           | ini          | menunjukkan  |         |
bahwa temuan tersebut dapat digeneralisasikan
pada populasi penelitian.
|     | CE -> SAT  | H2a:  Confirmation  |          |     | of   | Expectation  |           | (CE)  Diterima  |
| --- | ---------- | ------------------- | -------- | --- | ---- | ------------ | --------- | --------------- |
|     |            | berpengaruh         | positif  |     | dan  | signifikan   | terhadap  |                 |
Satisfaction (SAT)

Berdasarkan hasil hipotesis pada Tabel 4.3.2a,
|     |     | menunjukkan   |        | bahwa            |           | hubungan  |           | antara  |
| --- | --- | ------------- | ------ | ---------------- | --------- | --------- | --------- | ------- |
|     |     | Confirmation  |        | of  Expectation  |           | (CE)      | terhadap  |         |
|     |     | Satisfaction  | (SAT)  |                  | memiliki  | nilai     | Original  |         |
Sample sebesar 0,315 yang menunjukkan arah
|     |     | hubungan  | positif.  | Nilai T-Statistic  |     |     | 2,791 yang  |     |
| --- | --- | --------- | --------- | ------------------ | --- | --- | ----------- | --- |
lebih besar dari 1,96 dan P-Value 0,005 yang lebih
|     |     | kecil  dari  | 0,05   | menunjukkan  |       | hubungan       |     | yang   |
| --- | --- | ------------ | ------ | ------------ | ----- | -------------- | --- | ------ |
|     |     | signifikan.  | Nilai  | effect       | size  | (f²)  sebesar  |     | 0,091  |
menunjukkan kategori pengaruh kecil. Artinya,
terpenuhinya harapan pengguna terhadap sistem
|     |     | (CE)  berperan  |     | dalam  | meningkatkan  |     |     | tingkat  |
| --- | --- | --------------- | --- | ------ | ------------- | --- | --- | -------- |
kepuasan pengguna (SAT) meskipun pengaruh
|     |     | tersebut  | relatif  | terbatas  | dibandingkan  |     |     | faktor- |
| --- | --- | --------- | -------- | --------- | ------------- | --- | --- | ------- |
faktor lain dalam model penelitian. Hasil yang
|     |     | signifikan  | pada      | penelitian  |         | ini           | menunjukkan  |     |
| --- | --- | ----------- | --------- | ----------- | ------- | ------------- | ------------ | --- |
|     |     | bahwa       | hubungan  |             | antara  | Confirmation  |              | of  |
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER 62

Expectation (CE) dan Satisfaction (SAT) dapat
|     | digeneralisasikan  |     | pada  | populasi  |     | penelitian,  |     |
| --- | ------------------ | --- | ----- | --------- | --- | ------------ | --- |
sehingga konfirmasi harapan tetap menjadi salah
|     | satu  faktor  | yang  | relevan  |     | dalam  | membentuk  |     |
| --- | ------------- | ----- | -------- | --- | ------ | ---------- | --- |
kepuasan pengguna.
| CE -> PU  | H2b:         | Confirmation  |     | of   | Expectation  |           | (CE)  Diterima  |
| --------- | ------------ | ------------- | --- | ---- | ------------ | --------- | --------------- |
|           | berpengaruh  | positif       |     | dan  | signifikan   | terhadap  |                 |
Perceived Usefulness (PU)

Berdasarkan hasil hipotesis pada Tabel 4.3.2a,
|     | menunjukkan   |             | bahwa            |          | hubungan  |           | antara  |
| --- | ------------- | ----------- | ---------------- | -------- | --------- | --------- | ------- |
|     | Confirmation  |             | of  Expectation  |          | (CE)      | terhadap  |         |
|     | Perceived     | Usefulness  |                  | (PU)     | memiliki  |           | nilai   |
|     | Original      | Sample      |                  | sebesar  |           | 0,681     | yang    |
menunjukkan arah hubungan pengaruh positif.
Nilai T-Statistic sebesar 12,260 yang lebih besar
dari 1,96 dan P-Value sebesar 0,000 yang lebih
|     | kecil  dari  | 0,05  | menunjukkan  |     | hubungan  |     | yang  |
| --- | ------------ | ----- | ------------ | --- | --------- | --- | ----- |
sangat signifikan. Nilai effect size (f²) sebesar
0,863 termasuk dalam kategori pengaruh besar,
|     | yang  menunjukkan  |        |        | bahwa  | CE         | merupakan  |     |
| --- | ------------------ | ------ | ------ | ------ | ---------- | ---------- | --- |
|     | determinan         | utama  | dalam  |        | membentuk  | persepsi   |     |
kegunaan sistem. Artinya, semakin tinggi tingkat
kesesuaian antara harapan awal pengguna (CE),
|     | maka  semakin  |           | tinggi  | pula       | persepsi  | kegunaan      |     |
| --- | -------------- | --------- | ------- | ---------- | --------- | ------------- | --- |
|     | sistem         | (PU)  di  | mata    | pengguna.  |           | Terpenuhinya  |     |
ekspektasi pengguna (CE) menjadi faktor utama
yang membentuk keyakinan bahwa sistem benar-
|     | benar                 | bermanfaat  |              | dan              | membantu    | aktivitas  |        |
| --- | --------------------- | ----------- | ------------ | ---------------- | ----------- | ---------- | ------ |
|     | pengguna              | (PU).       | Hasil        | yang             | signifikan  |            | pada   |
|     | penelitian            | ini         | menunjukkan  |                  | bahwa       | hubungan   |        |
|     | antara  Confirmation  |             |              | of  Expectation  |             | (CE)       | dan    |
|     | Perceived             |             | Usefulness   |                  | (PU)        |            | dapat  |
|     | digeneralisasikan     |             | pada         |                  | seluruh     | populasi   |        |
penelitian ini.
| CE -> PP  | H2c:         | Confirmation  |     | of   | Expectation  |           | (CE)  Diterima  |
| --------- | ------------ | ------------- | --- | ---- | ------------ | --------- | --------------- |
|           | berpengaruh  | positif       |     | dan  | signifikan   | terhadap  |                 |
Perceived Playfulness (PP)

Berdasarkan hasil hipotesis pada Tabel 4.3.2a,
|     | menunjukkan   |              | bahwa            |          | hubungan  |           | antara  |
| --- | ------------- | ------------ | ---------------- | -------- | --------- | --------- | ------- |
|     | Confirmation  |              | of  Expectation  |          | (CE)      | terhadap  |         |
|     | Perceived     | Playfulness  |                  | (PP)     | memiliki  |           | nilai   |
|     | Original      | Sample       |                  | sebesar  |           | 0,577     | yang    |
|     | menunjukkan   | arah         | hubungan         |          | positif.  | Nilai     | T-      |
Statistic sebesar 6,558 yang lebih besar dari 1,96
serta P-Value sebesar 0,000 yang lebih kecil dari
|     | 0,05  menunjukkan  |        |           | bahwa  | hubungan      | tersebut  |        |
| --- | ------------------ | ------ | --------- | ------ | ------------- | --------- | ------ |
|     | signifikan.        | Nilai  | effect    | size   | (f²)          | sebesar   | 0,499  |
|     | mengindikasikan    |        | pengaruh  |        |               | besar,    | yang   |
|     | menunjukkan        |        | bahwa     |        | Confirmation  |           | of     |
Expectation memiliki kontribusi dominan dalam
|     | membentuk  | persepsi  |     | kesenangan  |     | pengguna.  |     |
| --- | ---------- | --------- | --- | ----------- | --- | ---------- | --- |
Artinya semakin tinggi tingkat kesesuaian antara
|     | harapan  | awal  | pengguna  | (CE),  | maka  | semakin  |     |
| --- | -------- | ----- | --------- | ------ | ----- | -------- | --- |
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER 63

|     | tinggi  pula  | persepsi  | kesenangan  |     | (PP)          | yang  |     |
| --- | ------------- | --------- | ----------- | --- | ------------- | ----- | --- |
|     | dirasakan     | oleh      | pengguna.   |     | Terpenuhinya  |       |     |
ekspektasi pengguna (CE) menjadi faktor penting
|     | dalam  menciptakan  |     | pengalaman  |          | penggunaan  |        |     |
| --- | ------------------- | --- | ----------- | -------- | ----------- | ------ | --- |
|     | yang  menyenangkan  |     | dan         | menarik  | (PP).       | Hasil  |     |
yang signifikan pada penelitian ini menunjukkan
|     | bahwa  | hubungan  | antara  | Confirmation  |     |     | of  |
| --- | ------ | --------- | ------- | ------------- | --- | --- | --- |
Expectation (CE) dan Perceived Playfulness (PP)
|     | dapat  digeneralisasikan  |     | pada  | seluruh  |     | populasi  |     |
| --- | ------------------------- | --- | ----- | -------- | --- | --------- | --- |
penelitian penelitian ini.
TAM  PU -> SAT  H3a:  Perceived  Usefulness  (PU)  berpengaruh  Ditolak
positif dan tidak signifikan terhadap Satisfaction
(SAT)

Berdasarkan hasil pengujian hipotesis pada Tabel
|     | 4.3.2a,  hubungan  |     | antara  | Perceived  | Usefulness  |     |     |
| --- | ------------------ | --- | ------- | ---------- | ----------- | --- | --- |
(PU) terhadap Satisfaction (SAT) memiliki nilai
|     | Original     | Sample  | sebesar         |     | 0,025     | yang    |     |
| --- | ------------ | ------- | --------------- | --- | --------- | ------- | --- |
|     | menunjukkan  |         | arah  hubungan  |     | positif.  | Namun,  |     |
nilai T-Statistic sebesar 0,230 yang lebih kecil
dari batas kritis 1,96, serta P-Value sebesar 0,818
yang lebih besar dari 0,05, menunjukkan bahwa
|     | hubungan  | tersebut  | tidak  | signifikan  |     | secara  |     |
| --- | --------- | --------- | ------ | ----------- | --- | ------- | --- |
statistik. Selain itu, nilai effect size (f²) berada
pada kategori no effect, yang mengindikasikan
|     | bahwa             | Perceived   | Usefulness  |           | (PU)       | tidak     |     |
| --- | ----------------- | ----------- | ----------- | --------- | ---------- | --------- | --- |
|     | memberikan        | kontribusi  |             | yang      | berarti    | dalam     |     |
|     | menjelaskan       |             | varians     | kepuasan  | pengguna.  |           |     |
|     | Artinya,          | meskipun    | pengguna    |           | menilai    | bahwa     |     |
|     | sistem  memiliki  |             | kegunaan    | dalam     | membantu   |           |     |
|     | aktivitas         | mereka      | (PU),       | persepsi  |            | kegunaan  |     |
|     | tersebut          | belum       | mampu       | secara    |            | langsung  |     |
meningkatkan tingkat kepuasan pengguna (SAT).
Dalam konteks penelitian ini, kegunaan sistem
cenderung dipersepsikan sebagai kebutuhan dasar
(baseline requirement) yang sudah sewajarnya
dimiliki oleh aplikasi AI Design Tools seperti
|     | Figma      | Make.     | Oleh  karena  |              | itu,  keberadaan  |           |     |
| --- | ---------- | --------- | ------------- | ------------ | ----------------- | --------- | --- |
|     | kegunaan   | sistem    | tidak         | lagi         | menjadi           | faktor    |     |
|     | pembeda    | yang      | menentukan    | tingkat      | kepuasan,         |           |     |
|     | melainkan  | pengguna  | lebih         | dipengaruhi  |                   | oleh      |     |
|     | faktor     | lain      | seperti       | konfirmasi   |                   | harapan,  |     |
pengalaman emosional, kebaruan sistem, serta
kualitas interaksi dan kecerdasan sistem. Hasil
|     | yang  tidak  | signifikan  |     | pada  | penelitian  | ini  |     |
| --- | ------------ | ----------- | --- | ----- | ----------- | ---- | --- |
menunjukkan bahwa hubungan tersebut hanya
berlaku pada sampel yang diteliti serta tidak dapat
|     | digeneralisasikan  |     | ke  seluruh  |     | populasi  | dalam  |     |
| --- | ------------------ | --- | ------------ | --- | --------- | ------ | --- |
penelitian ini.
| PU -> CI  | H3b:  Perceived  |     | Usefulness  | (PU)  | berpengaruh  |     | Ditolak  |
| --------- | ---------------- | --- | ----------- | ----- | ------------ | --- | -------- |
positif dan tidak signifikan terhadap Continuance
Intention (CI)

Berdasarkan hasil pengujian hipotesis pada Tabel
|     | 4.3.2a,  hubungan  |     | antara  | Perceived  | Usefulness  |     |     |
| --- | ------------------ | --- | ------- | ---------- | ----------- | --- | --- |
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER 64

|     | (PU)  terhadap     |                  | Continuance  |           | Intention  (CI)  |     |
| --- | ------------------ | ---------------- | ------------ | --------- | ---------------- | --- |
|     | memiliki           | nilai  Original  |              | Sample    | sebesar  0,083   |     |
|     | yang  menunjukkan  |                  | arah         | hubungan  | positif.         |     |
Namun, nilai T-Statistic sebesar 1,032 yang lebih
kecil dari batas kritis 1,96, serta P-Value sebesar
0,302 yang lebih besar dari 0,05, menunjukkan
bahwa hubungan tersebut tidak signifikan secara
statistik. Selain itu, nilai effect size (f²) berada
|     | pada  kategori  |       | pengaruh         | kecil  | hingga  tidak  |     |
| --- | --------------- | ----- | ---------------- | ------ | -------------- | --- |
|     | bermakna,       | yang  | mengindikasikan  |        | bahwa          |     |
kontribusi Perceived Usefulness (PU) terhadap
niat penggunaan berkelanjutan sangat terbatas.
Artinya, meskipun pengguna merasakan bahwa
|     | sistem  memiliki  |          | kegunaan     | dalam     | mendukung       |     |
| --- | ----------------- | -------- | ------------ | --------- | --------------- | --- |
|     | aktivitas         | mereka,  | persepsi     | kegunaan  | tersebut        |     |
|     | belum             | cukup    | kuat  untuk  | secara    | langsung        |     |
|     | mendorong         | niat     | penggunaan   |           | berkelanjutan.  |     |
Dalam konteks penelitian ini, kegunaan sistem
cenderung berperan sebagai faktor dasar (hygiene
factor) yang perlu ada, namun tidak lagi menjadi
faktor pembeda dalam keputusan pengguna untuk
|     | terus          | menggunakan  |                   | sistem.      | Pengguna    |     |
| --- | -------------- | ------------ | ----------------- | ------------ | ----------- | --- |
|     | kemungkinan    | lebih        | mempertimbangkan  |              | faktor      |     |
|     | lain  seperti  | kepuasan,    | pengalaman        |              | emosional,  |     |
|     | kualitas       | interaksi,   | serta             | kepercayaan  | terhadap    |     |
|     | kecerdasan     | sistem       | dalam             | menentukan   | niat        |     |
penggunaan berkelanjutan. Hubungan yang tidak
|     | signifikan   | ini  menunjukkan  |             | bahwa  | pengaruh        |     |
| --- | ------------ | ----------------- | ----------- | ------ | --------------- | --- |
|     | langsung     | Perceived         | Usefulness  |        | (PU)  terhadap  |     |
|     | Continuance  | Intention         |             | (CI)   | tidak  dapat    |     |
digeneralisasikan sebagai faktor penentu utama,
melainkan lebih berperan secara tidak langsung
melalui variabel lain dalam model penelitian.
| PU -> ATT  | H3c:  Perceived  |     | Usefulness  | (PU)  | berpengaruh  | Diterima  |
| ---------- | ---------------- | --- | ----------- | ----- | ------------ | --------- |
positif dan signifikan terhadap Attitude Toward
Using (ATT)

Berdasarkan hasil pengujian hipotesis pada Tabel
|     | 4.3.2a,  hubungan  |                  | antara  | Perceived  | Usefulness      |     |
| --- | ------------------ | ---------------- | ------- | ---------- | --------------- | --- |
|     | (PU)  terhadap     | Attitude         |         | Toward     | Using  (ATT)    |     |
|     | memiliki           | nilai  Original  |         | Sample     | sebesar  0,636  |     |
yang menunjukkan arah hubungan positif. Nilai
T-Statistic sebesar 9,595 yang jauh melebihi batas
kritis 1,96, serta P-Value sebesar 0,000 yang lebih
kecil dari 0,05, menunjukkan bahwa hubungan
tersebut sangat signifikan secara statistik. Selain
itu, nilai effect size (f²) sebesar 0,679 termasuk
dalam kategori pengaruh besar, yang menandakan
|     | bahwa  Perceived  |     | Usefulness  | (PU)  | merupakan  |     |
| --- | ----------------- | --- | ----------- | ----- | ---------- | --- |
faktor kunci dalam membentuk sikap pengguna
terhadap sistem. Artinya, semakin tinggi persepsi
|     | pengguna   | terhadap  | kegunaan  |     | sistem  seperti  |     |
| --- | ---------- | --------- | --------- | --- | ---------------- | --- |
|     | kemampuan  | sistem    | dalam     |     | meningkatkan     |     |
efektivitas kerja, membantu menyelesaikan tugas
|     | dengan  | lebih  cepat,  | dan  | memberikan  | manfaat  |     |
| --- | ------- | -------------- | ---- | ----------- | -------- | --- |
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER 65

nyata (PU), maka semakin positif sikap pengguna
|     |     | terhadap  | sistem  tersebut  | (ATT).  Hasil  | ini  |
| --- | --- | --------- | ----------------- | -------------- | ---- |
menunjukkan bahwa kegunaan yang dirasakan
|     |     | pengguna     | menjadi  dasar     | utama          | dalam  |
| --- | --- | ------------ | ------------------ | -------------- | ------ |
|     |     | pembentukan  | sikap,  khususnya  | dalam konteks  |        |
penggunaan AI Design Tools seperti Figma Make,
|     |     | di  mana  | orientasi  produktivitas  | dan  | efisiensi  |
| --- | --- | --------- | ------------------------- | ---- | ---------- |
menjadi pertimbangan utama pengguna.
Hubungan yang signifikan ini mengindikasikan
bahwa Perceived Usefulness (PU) memiliki peran
yang dominan dan dapat digeneralisasikan dalam
membentuk sikap pengguna terhadap sistem pada
konteks penelitian ini.
|     | ATT -> CI  | H4: Attitude Toward Using (ATT) berpengaruh  |     |     | Ditolak  |
| --- | ---------- | -------------------------------------------- | --- | --- | -------- |
positif dan tidak signifikan terhadap Continuance
Intention (CI)

Berdasarkan hasil hipotesis pada Tabel 4.3.2a,
hubungan antara Attitude Toward Using (ATT)
|     |     | terhadap         | Continuance  Intention  | (CI)            | memiliki  |
| --- | --- | ---------------- | ----------------------- | --------------- | --------- |
|     |     | nilai  Original  | Sample                  | sebesar  0,038  | yang      |
|     |     | menunjukkan      | arah  hubungan          | positif.        | Namun,    |
nilai T-Statistic sebesar 0,450 yang lebih kecil
dari batas kritis 1,96, serta nilai P-Value sebesar
0,653 yang lebih besar dari 0,05, menunjukkan
bahwa hubungan tersebut tidak signifikan secara
statistik. Selain itu, nilai effect size (f²) sebesar
|     |     | 0,002  menunjukkan  | bahwa  | pengaruh  | ATT  |
| --- | --- | ------------------- | ------ | --------- | ---- |
terhadap CI tergolong tidak memiliki efek (no
|     |     | effect).  | Hal  ini  mengindikasikan  | bahwa       | sikap  |
| --- | --- | --------- | -------------------------- | ----------- | ------ |
|     |     | pengguna  | tidak  memberikan          | kontribusi  | yang   |
|     |     | berarti   | dalam  menjelaskan         | varians     | niat   |
penggunaan berkelanjutan. Artinya, sikap positif
pengguna terhadap sistem (ATT) tidak cukup kuat
untuk mendorong niat penggunaan berkelanjutan
(CI). Meskipun pengguna memiliki sikap yang
|     |     | baik  terhadap  | aplikasi/teknologi,  | hal               | tersebut  |
| --- | --- | --------------- | -------------------- | ----------------- | --------- |
|     |     | bukan  faktor   | penentu  utama       | dalam  keputusan  |           |
mereka untuk terus menggunakan sistem. Hasil
|     |     | yang  tidak  | signifikan  | pada  penelitian  | ini  |
| --- | --- | ------------ | ----------- | ----------------- | ---- |
menunjukkan bahwa hubungan tersebut hanya
berlaku pada sampel yang diteliti serta tidak dapat
|     |     | digeneralisasikan  | ke  seluruh  | populasi  | dalam  |
| --- | --- | ------------------ | ------------ | --------- | ------ |
penelitian ini.
| UX  | EE -> CI  |                  |                  |                        | Diterima  |
| --- | --------- | ---------------- | ---------------- | ---------------------- | --------- |
|     |           | H5a:  Emotional  | Experience       | (EE)  berpengaruh      |           |
|     |           | positif          | dan  signifikan  | terhadap  Continuance  |           |
Intention (CI)

Berdasarkan hasil hipotesis pada Tabel 4.3.2a,
menunjukkan bahwa hubungan antara Emotional
Experience (EE) terhadap Continuance Intention
(CI) memiliki nilai Original Sample sebesar 0,268
yang menunjukkan arah hubungan positif. Nilai
T-Statistic 3,324 yang lebih besar dari 1,96 dan P-
|     |     | Value  0,001  | yang  lebih  | kecil  dari  | 0,05  |
| --- | --- | ------------- | ------------ | ------------ | ----- |
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER 66

menunjukkan hubungan yang signifikan. Nilai
|     | effect  size  | (f²)  | sebesar  | 0,088  |     | menunjukkan  |     |
| --- | ------------- | ----- | -------- | ------ | --- | ------------ | --- |
kategori pengaruh kecil, yang mengindikasikan
bahwa Emotional Experience (EE) berkontribusi
|     | dalam      | menjelaskan  |        | varians  |           | Continuance  |     |
| --- | ---------- | ------------ | ------ | -------- | --------- | ------------ | --- |
|     | Intention  | (CI),        | namun  | tidak    | berperan  | sebagai      |     |
faktor dominan. Artinya, pengalaman emosional
yang dirasakan pengguna selama menggunakan
sistem (EE) memiliki peran dalam mendorong
niat untuk terus menggunakan sistem tersebut
|     | (CI),  meskipun  |     | pengaruhnya    |     | relatif  | terbatas      |     |
| --- | ---------------- | --- | -------------- | --- | -------- | ------------- | --- |
|     | dibandingkan     |     | faktor-faktor  |     | lain     | dalam  model  |     |
penelitian. Hasil penelitian yang signifikan pada
|     | penelitian         | ini        | menunjukkan  |             | bahwa  | hubungan     |     |
| --- | ------------------ | ---------- | ------------ | ----------- | ------ | ------------ | --- |
|     | antara             | Emotional  |              | Experience  |        | (EE)  dan    |     |
|     | Continuance        |            | Intention    |             | (IE)   | dapat        |     |
|     | digeneralisasikan  |            | pada         | populasi    |        | penelitian,  |     |
sehingga pengalaman emosional tetap menjadi
|     | faktor  yang  | relevan  |     | dalam  | membentuk  | niat  |     |
| --- | ------------- | -------- | --- | ------ | ---------- | ----- | --- |
penggunaan berkelanjutan.
| IE -> CI  | H5b:  Interactive  |                  | Experience  |           | (IE)  | berpengaruh  | Diterima  |
| --------- | ------------------ | ---------------- | ----------- | --------- | ----- | ------------ | --------- |
|           | positif            | dan  signifikan  |             | terhadap  |       | Continuance  |           |
Intention (CI)

Berdasarkan hasil hipotesis pada Tabel 4.3.2a,
menunjukkan bahwa hubungan antara Interactive
Experience (IE) terhadap Continuance Intention
(CI) memiliki nilai Original Sample sebesar 0,193
yang menunjukkan arah hubungan positif. Nilai
T-Statistic 2,255 yang lebih besar dari 1,96 dan P-
|     | Value  0,024  |     | yang  | lebih  | kecil  | dari  0,05  |     |
| --- | ------------- | --- | ----- | ------ | ------ | ----------- | --- |
menunjukkan hubungan yang signifikan. Nilai
|     | effect  size  | (f²)      | sebesar  | 0,050  | termasuk  | dalam        |     |
| --- | ------------- | --------- | -------- | ------ | --------- | ------------ | --- |
|     | kategori      | pengaruh  | kecil,   |        | yang      | menunjukkan  |     |
bahwa Interactive Experience (IE) memberikan
|     | kontribusi  | terhadap  |            | peningkatan  |                    | Continuance  |     |
| --- | ----------- | --------- | ---------- | ------------ | ------------------ | ------------ | --- |
|     | Intention   | (CI),     | namun      | tidak        | bersifat dominan.  |              |     |
|     | Artinya,    | kualitas  | interaksi  |              | yang               | dirasakan    |     |
pengguna saat berinteraksi dengan sistem (IE)
|     | dapat  mendorong  |            | niat        | pengguna    |            | untuk  terus    |     |
| --- | ----------------- | ---------- | ----------- | ----------- | ---------- | --------------- | --- |
|     | menggunakan       |            | sistem      | tersebut    | (CI),      | meskipun        |     |
|     | pengaruhnya       |            | relatif     | terbatas.   |            | Hal  ini        |     |
|     | menunjukkan       |            | bahwa       | pengalaman  |            | interaktif      |     |
|     | berperan          | sebagai    | faktor      |             | pendukung  | dalam           |     |
|     | membentuk         | niat       | penggunaan  |             |            | berkelanjutan,  |     |
|     | sementara         | keputusan  |             | utama       |            | untuk  terus    |     |
menggunakan sistem lebih banyak dipengaruhi
|     | oleh  faktor  |            | lain  | dalam  | model  | penelitian.  |     |
| --- | ------------- | ---------- | ----- | ------ | ------ | ------------ | --- |
|     | Meskipun      | demikian,  |       | hasil  | yang   | signifikan   |     |
menunjukkan bahwa hubungan antara Interactive
Experience (IE) dan Continuance Intention (CI)
dapat digeneralisasikan pada populasi penelitian,
sehingga kualitas interaksi tetap menjadi aspek
|     | yang  relevan  |     | dalam  | mendorong  |     | penggunaan  |     |
| --- | -------------- | --- | ------ | ---------- | --- | ----------- | --- |
sistem secara berkelanjutan.
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER 67

Karakteristik  PI -> PT  H7a:  Perceived  Intelligence  (PI)  berpengaruh  Diterima
AI Design  positif dan signifikan terhadap Perceived Trust
Tools
(PT)

Berdasarkan hasil hipotesis pada Tabel 4.3.2a,
menunjukkan bahwa hubungan antara Perceived
Intelligence (PI) terhadap Perceived Trust (PT)
|     | memiliki  | nilai  | Original  | Sample  | sebesar  | 0,688  |     |
| --- | --------- | ------ | --------- | ------- | -------- | ------ | --- |
yang menunjukkan arah hubungan positif. Nilai
T-Statistic 12,135 yang lebih besar dari 1,96 dan
|     | P-Value  | 0,000  | yang  | lebih  | kecil  | dari  0,05  |     |
| --- | -------- | ------ | ----- | ------ | ------ | ----------- | --- |
menunjukkan hubungan yang signifikan. Nilai
|     | effect  size  | (f²)      | sebesar  | 0,898   | termasuk  | dalam  |     |
| --- | ------------- | --------- | -------- | ------- | --------- | ------ | --- |
|     | kategori      | pengaruh  |          | sangat  | besar,    | yang   |     |
menandakan bahwa Perceived Intelligence (PI)
|     | memiliki     | kontribusi  |         | yang       | dominan  | dalam     |     |
| --- | ------------ | ----------- | ------- | ---------- | -------- | --------- | --- |
|     | menjelaskan  | varians     |         | Perceived  | Trust    | (PT).     |     |
|     | Artinya,     | semakin     | tinggi  | persepsi   |          | pengguna  |     |
terhadap kecerdasan sistem seperti kemampuan
sistem dalam memahami kebutuhan pengguna,
|     | memberikan    | respons      |     | yang  | akurat,        | serta  |     |
| --- | ------------- | ------------ | --- | ----- | -------------- | ------ | --- |
|     | menghasilkan  | rekomendasi  |     |       | yang  relevan  | (PI)   |     |
maka semakin tinggi pula tingkat kepercayaan
pengguna terhadap sistem tersebut (PT). Hasil ini
|     | menunjukkan  |     | bahwa  | kecerdasan  |     | sistem  |     |
| --- | ------------ | --- | ------ | ----------- | --- | ------- | --- |
merupakan faktor kunci dan penentu utama dalam
membangun kepercayaan pengguna. Dengan kata
|     | lain,  kepercayaan  |     | pengguna  |         | terhadap  | sistem  |     |
| --- | ------------------- | --- | --------- | ------- | --------- | ------- | --- |
|     | sangat  bergantung  |     | pada      | sejauh  | mana      | sistem  |     |
dipersepsikan sebagai cerdas, andal, dan mampu
|     | mendukung  | tujuan  | pengguna  |     | secara  | efektif.  |     |
| --- | ---------- | ------- | --------- | --- | ------- | --------- | --- |
Hubungan yang sangat signifikan dan memiliki
pengaruh besar ini menunjukkan bahwa temuan
tersebut dapat digeneralisasikan pada populasi
penelitian, sehingga Perceived Intelligence (PI)
menjadi variabel strategis dalam meningkatkan
|     | kepercayaan  | pengguna  |     | terhadap  | penggunaan  |     |     |
| --- | ------------ | --------- | --- | --------- | ----------- | --- | --- |
sistem secara berkelanjutan.
| PI -> CI  | H7b:  Perceived  |                  | Intelligence  |           | (PI)  berpengaruh  |     | Diterima  |
| --------- | ---------------- | ---------------- | ------------- | --------- | ------------------ | --- | --------- |
|           | positif          | dan  signifikan  |               | terhadap  | Continuance        |     |           |
Intention (CI)

Berdasarkan hasil hipotesis pada Tabel 4.3.2a,
menunjukkan bahwa hubungan antara Perceived
Intelligence (PI) terhadap Continuance Intention
(CI) memiliki nilai Original Sample sebesar 0,215
yang menunjukkan arah hubungan positif. Nilai
T-Statistic 2,117 yang lebih besar dari 1,96 dan P-
|     | Value  0,034  |     | yang  | lebih  | kecil  | dari  0,05  |     |
| --- | ------------- | --- | ----- | ------ | ------ | ----------- | --- |
menunjukkan hubungan yang signifikan. Nilai
|     | effect  size  | (f²)          | sebesar  | 0,049        | menunjukkan    |        |     |
| --- | ------------- | ------------- | -------- | ------------ | -------------- | ------ | --- |
|     | pengaruh      | kecil,        | yang     | menunjukkan  |                | bahwa  |     |
|     | Perceived     | Intelligence  |          | (PI)         | berkontribusi  |        |     |
terhadap peningkatan Continuance Intention (CI),
namun tidak berperan sebagai faktor dominan.
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER 68

Artinya, persepsi pengguna terhadap kecerdasan
|     | sistem  | seperti  | kemampuan  |     | sistem  dalam  |     |
| --- | ------- | -------- | ---------- | --- | -------------- | --- |
memberikan rekomendasi yang relevan, respons
yang tepat, atau fitur berbasis kecerdasan bautan
(PI) dapat mendorong niat pengguna untuk terus
|     | menggunakan  | sistem     | tersebut    |             | (CI),  meskipun  |     |
| --- | ------------ | ---------- | ----------- | ----------- | ---------------- | --- |
|     | pengaruhnya  |            | relatif     | terbatas.   | Hal  ini         |     |
|     | menunjukkan  | bahwa      | aspek       | kecerdasan  | sistem           |     |
|     | berfungsi    | sebagai    | faktor      | pendukung   | dalam            |     |
|     | membentuk    | niat       | penggunaan  |             | berkelanjutan,   |     |
|     | sementara    | keputusan  | pengguna    |             | untuk  terus     |     |
menggunakan sistem lebih banyak dipengaruhi
|     | oleh  faktor  | lain       | dalam  | model  | penelitian.  |     |
| --- | ------------- | ---------- | ------ | ------ | ------------ | --- |
|     | Meskipun      | demikian,  | hasil  | yang   | signifikan   |     |
menunjukkan bahwa hubungan antara Perceived
Intelligence (CI) dan Continuance Intention (CI)
dapat digeneralisasikan pada populasi penelitian,
|     | sehingga  | persepsi  | kecerdasan  |     | sistem  tetap  |     |
| --- | --------- | --------- | ----------- | --- | -------------- | --- |
menjadi faktor yang relevan dalam mendorong
penggunaan sistem secara berkelanjutan.
| PT -> CI  | H8: Perceived Trust (PT) berpengaruh negatif dan  |     |     |     |     | Ditolak  |
| --------- | ------------------------------------------------- | --- | --- | --- | --- | -------- |
tidak signifikan terhadap Continuance Intention
(CI)

Berdasarkan hasil pengujian hipotesis pada Tabel
|     | 4.3.2a,          | hubungan     | antara     | Perceived  | Trust  (PT)     |     |
| --- | ---------------- | ------------ | ---------- | ---------- | --------------- | --- |
|     | terhadap         | Continuance  | Intention  |            | (CI)  memiliki  |     |
|     | nilai  Original  |              | Sample     | sebesar    | –0,040  yang    |     |
|     | menunjukkan      | arah         | hubungan   | negatif.   | Nilai T-        |     |
Statistic sebesar 0,370 yang lebih kecil dari batas
kritis 1,96, serta P-Value 0,711 yang lebih besar
dari 0,05, menunjukkan bahwa hubungan tersebut
tidak signifikan secara statistik. Selain itu, nilai
effect size (f²) berada pada kategori no effect, yang
|     | mengindikasikan  |             | bahwa     | Perceived  | Trust  tidak    |     |
| --- | ---------------- | ----------- | --------- | ---------- | --------------- | --- |
|     | memberikan       | kontribusi  |           | yang       | berarti  dalam  |     |
|     | menjelaskan      |             | varians   | niat       | penggunaan      |     |
|     | berkelanjutan.   |             | Artinya,  | tingkat    | kepercayaan     |     |
pengguna terhadap sistem (PT) belum menjadi
faktor utama yang mendorong niat penggunaan
berkelanjutan (CI) pada konteks penelitian ini.
Meskipun kepercayaan sering dianggap sebagai
|     | faktor  penting  | dalam     | adopsi      | dan            | penggunaan   |     |
| --- | ---------------- | --------- | ----------- | -------------- | ------------ | --- |
|     | teknologi,       | hasil     | penelitian  | ini            | menunjukkan  |     |
|     | bahwa            | pengguna  | Figma       |                | Make  lebih  |     |
|     | memprioritaskan  |           | aspek       | lain  seperti  | kegunaan     |     |
sistem, pengalaman emosional, kualitas interaksi,
serta persepsi kecerdasan sistem dibandingkan
faktor kepercayaan semata. Arah hubungan yang
|     | negatif,  | meskipun  |     | tidak  | signifikan,  |     |
| --- | --------- | --------- | --- | ------ | ------------ | --- |
mengindikasikan bahwa kepercayaan pengguna
cenderung bersifat baseline requirement (sudah
diasumsikan ada), sehingga tidak lagi menjadi
|     | pembeda      | dalam    | keputusan  |     | untuk  terus  |     |
| --- | ------------ | -------- | ---------- | --- | ------------- | --- |
|     | menggunakan  | sistem.  | Hubungan   |     | yang  tidak   |     |
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER 69

|     | signifikan  | ini  menunjukkan  |           | bahwa  pengaruh    |     |
| --- | ----------- | ----------------- | --------- | ------------------ | --- |
|     | Perceived   | Trust  (PT)       | terhadap  | Continuance        |     |
|     | Intention   | (CI)  hanya       | berlaku   | pada  sampel       |     |
|     | penelitian  | serta  tidak      | dapat     | digeneralisasikan  |     |
sebagai faktor penentu utama dalam mendorong
niat penggunaan berkelanjutan.
| PN -> SAT  | H9a: Perceived Novelty (PN) berpengaruh positif  |     |     |     | Diterima  |
| ---------- | ------------------------------------------------ | --- | --- | --- | --------- |
dan signifikan terhadap Satisfaction (SAT)

Berdasarkan hasil hipotesis pada Tabel 4.3.2a,
menunjukkan bahwa hubungan antara Perceived
|     | Novelty   | (PN)  terhadap  | Satisfaction  | (SAT)            |     |
| --- | --------- | --------------- | ------------- | ---------------- | --- |
|     | memiliki  | nilai  nilai    | Original      | Sample  sebesar  |     |
0,369 yang menunjukkan arah hubungan positif.
Nilai T-Statistic sebesar 3,367 yang lebih besar
dari 1,96 dan P-Value sebesar 0,001 yang lebih
kecil dari 0,05 menunjukkan bahwa hubungan
tersebut signifikan secara statistik. Nilai effect
size (f²) sebesar 0,151 termasuk dalam kategori
pengaruh sedang yang mengindikasikan bahwa
Perceived Novelty (PN) memberikan kontribusi
yang cukup berarti dalam menjelaskan varians
kepuasan pengguna. Artinya, persepsi pengguna
terhadap kebaruan, keunikan, dan inovasi yang
ditawarkan oleh sistem seperti pengalaman baru,
|     | fitur  yang  | terasa  | berbeda  | dari  teknologi  |     |
| --- | ------------ | ------- | -------- | ---------------- | --- |
sebelumnya, serta cara yang lebih sederhana dan
inovatif dalam menyelesaikan tugas (PN) mampu
meningkatkan tingkat kepuasan pengguna secara
signifikan (SAT). Hasil ini menunjukkan bahwa
|     | meskipun        | unsur  kebaruan   |         | tidak  berperan   |     |
| --- | --------------- | ----------------- | ------- | ----------------- | --- |
|     | langsung        | dalam  mendorong  |         | niat  penggunaan  |     |
|     | berkelanjutan,  | kebaruan          | sistem  | tetap  memiliki   |     |
peran penting dalam membentuk respons afektif
|     | pengguna,  | khususnya  | rasa  | puas  terhadap  |     |
| --- | ---------- | ---------- | ----- | --------------- | --- |
penggunaan sistem. Hubungan yang signifikan
ini menunjukkan bahwa temuan tersebut dapat
digeneralisasikan pada populasi penelitian.
| PN -> CI  | H9b: Perceived Novelty (PN) berpengaruh negatif  |             |           |              | Ditolak  |
| --------- | ------------------------------------------------ | ----------- | --------- | ------------ | -------- |
|           | dan  tidak                                       | signifikan  | terhadap  | Continuance  |          |
Intention (CI)

Berdasarkan hasil hipotesis pada Tabel 4.3.2a,
menunjukkan bahwa hubungan antara Perceived
|     | Novelty  | (PN)  terhadap  | Continuance  | Intention  |     |
| --- | -------- | --------------- | ------------ | ---------- | --- |
(CI) memiliki nilai Original Sample sebesar -
0,031 yang menunjukkan arah hubungan negatif.
Nilai T-Statistic sebesar 0,365 yang lebih kecil
dari 1,96 dan P-Value sebesar 0,715 yang lebih
besar dari 0,05 menunjukkan bahwa hubungan
tersebut tidak signifikan secara statistik. Nilai
effect size (f²) sebesar 0,001 mengindikasikan
|     | bahwa  | pengaruh  Perceived  |     | Novelty  terhadap  |     |
| --- | ------ | -------------------- | --- | ------------------ | --- |
Continuance Intention tergolong tidak memiliki
|     | efek  (no  | effect).  Artinya,  | meskipun  | pengguna  |     |
| --- | ---------- | ------------------- | --------- | --------- | --- |
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER 70

merasakan kebaruan, keunikan, pengalaman baru,
serta inovasi dalam penggunaan aplikasi Figma
Make, seperti cara baru yang lebih sederhana dan
|     | inovatif  | dalam     | menyelesaikan  |        | tugas  (PN),  |     |
| --- | --------- | --------- | -------------- | ------ | ------------- | --- |
|     | persepsi  | tersebut  | tidak          | cukup  | kuat  untuk   |     |
mendorong niat penggunaan berkelanjutan (CI).
Kebaruan sistem cenderung memberikan dampak
pada fase awal penggunaan (initial adoption),
|     | namun  | seiring  | waktu  | pengguna  | lebih  |     |
| --- | ------ | -------- | ------ | --------- | ------ | --- |
memprioritaskan aspek kegunaan, kepercayaan,
|     | kepuasan,  | dan  | pengalaman  |     | fungsional  |     |
| --- | ---------- | ---- | ----------- | --- | ----------- | --- |
dibandingkan rasa “baru” atau “menarik”. Arah
|     | hubungan  | yang  | negatif,  | meskipun  | tidak  |     |
| --- | --------- | ----- | --------- | --------- | ------ | --- |
signifikan, mengindikasikan bahwa setelah fase
eksplorasi awal, unsur kebaruan dapat kehilangan
daya tariknya (novelty effect), sehingga tidak lagi
|     | menjadi             | faktor  | penentu  | bagi  pengguna  | untuk    |     |
| --- | ------------------- | ------- | -------- | --------------- | -------- | --- |
|     | terus  menggunakan  |         | sistem.  | Dalam           | konteks  |     |
Generasi Z sebagai responden penelitian, hasil ini
|     | menunjukkan  |     | bahwa  | pengguna  | cenderung  |     |
| --- | ------------ | --- | ------ | --------- | ---------- | --- |
bersikap utilitarian dan goal-oriented, di mana
keberlanjutan penggunaan lebih ditentukan oleh
manfaat nyata dan efisiensi kerja dibandingkan
sekadar pengalaman baru atau inovatif. Dengan
|     | demikian,  | hasil  | penelitian  | ini  | menunjukkan  |     |
| --- | ---------- | ------ | ----------- | ---- | ------------ | --- |
bahwa Perceived Novelty (PN) berperan sebagai
faktor pendukung awal, namun bukan determinan
utama dalam membentuk Continuance Intention
|     | (CI).  Hubungan  |     | yang  | tidak  | signifikan  ini  |     |
| --- | ---------------- | --- | ----- | ------ | ---------------- | --- |
menunjukkan bahwa pengaruh kebaruan terhadap
|     | niat  penggunaan   |     | berkelanjutan  |         | tidak  dapat  |     |
| --- | ------------------ | --- | -------------- | ------- | ------------- | --- |
|     | digeneralisasikan  |     | sebagai        | faktor  | utama  pada   |     |
populasi penelitian.
| PP -> SAT  | H10a: Perceived Playfulness (PP) berpengaruh  |     |     |     |     | Ditolak  |
| ---------- | --------------------------------------------- | --- | --- | --- | --- | -------- |
positif dan tidak signifikan terhadap Satisfaction
(SAT)

Berdasarkan hasil pengujian hipotesis pada Tabel
4.3.2a, hubungan antara Perceived Playfulness
(PP) terhadap Satisfaction (SAT) memiliki nilai
|     | Original     | Sample  | sebesar         |           | 0,172  yang  |     |
| --- | ------------ | ------- | --------------- | --------- | ------------ | --- |
|     | menunjukkan  |         | arah  hubungan  | positif.  | Namun,       |     |
nilai T-Statistic sebesar 1,778 yang lebih kecil
dari batas kritis 1,96, serta P-Value sebesar 0,075
yang lebih besar dari 0,05, menunjukkan bahwa
|     | hubungan  | tersebut  | tidak  | signifikan  | secara  |     |
| --- | --------- | --------- | ------ | ----------- | ------- | --- |
statistik. Selain itu, nilai effect size (f²) sebesar
0,044 termasuk dalam kategori pengaruh kecil,
|     | yang       | mengindikasikan  |       | bahwa     | kontribusi  |     |
| --- | ---------- | ---------------- | ----- | --------- | ----------- | --- |
|     | Perceived  | Playfulness      | (PP)  | terhadap  | kepuasan    |     |
pengguna terbatas. Artinya, meskipun pengguna
|     | merasakan   | adanya  | unsur               | kesenangan  | atau   |     |
| --- | ----------- | ------- | ------------------- | ----------- | ------ | --- |
|     | pengalaman  |         | yang  menyenangkan  |             | dalam  |     |
penggunaan sistem, persepsi tersebut (PP) belum
|     | cukup  | kuat  | untuk  meningkatkan  |     | kepuasan  |     |
| --- | ------ | ----- | -------------------- | --- | --------- | --- |
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER 71

|     | pengguna     | secara  | signifikan  |           | (SAT).  | Hal  ini  |     |
| --- | ------------ | ------- | ----------- | --------- | ------- | --------- | --- |
|     | menunjukkan  |         | bahwa       | kepuasan  |         | pengguna  |     |
terhadap sistem Figma Make lebih dipengaruhi
|     | oleh  faktor  |           | dibandingkan  |              | aspek       | kesenangan  |     |
| --- | ------------- | --------- | ------------- | ------------ | ----------- | ----------- | --- |
|     | semata.       | Hubungan  |               | yang  tidak  | signifikan  | ini         |     |
menunjukkan bahwa pengaruh kebaruan terhadap
|     | niat  penggunaan   |     | berkelanjutan  |         |     | tidak  dapat  |     |
| --- | ------------------ | --- | -------------- | ------- | --- | ------------- | --- |
|     | digeneralisasikan  |     | sebagai        | faktor  |     | utama  pada   |     |
populasi penelitian.
| PP -> CI  | H10b: Perceived Playfulness (PP) berpengaruh  |     |     |     |     |     | Ditolak  |
| --------- | --------------------------------------------- | --- | --- | --- | --- | --- | -------- |
positif dan tidak signifikan terhadap Continuance
Intention (CI)

Berdasarkan hasil hipotesis pada Tabel 4.3.2a,
menunjukkan bahwa hubungan antara Perceived
Playfulness (PP) terhadap Continuance Intention
(CI) memiliki nilai Original Sample sebesar 0,015
yang menunjukkan arah hubungan positif. Nilai
T-Statistic 0,146 yang lebih kecil dari 1,96 dan P-
|     | Value        | 0,884  | yang   | lebih     | besar     | dari  0,05  |     |
| --- | ------------ | ------ | ------ | --------- | --------- | ----------- | --- |
|     | menunjukkan  |        | bahwa  | hubungan  | tersebut  | tidak       |     |
signifikan secara statistik. Nilai effect size (f²)
|     | 0,00  berada     |                 | pada   | kategori     |           | no  effect     |     |
| --- | ---------------- | --------------- | ------ | ------------ | --------- | -------------- | --- |
|     | mengindikasikan  |                 | bahwa  |              | bahwa     | Perceived      |     |
|     | Playfulness      | (PP)            | tidak  | memberikan   |           | kontribusi     |     |
|     | yang  berarti    |                 | dalam  | menjelaskan  |           | varians  niat  |     |
|     | penggunaan       | berkelanjutan.  |        |              | Artinya,  | meskipun       |     |
pengguna mungkin merasakan kesenangan atau
|     | rasa  menyenangkan  |           |       | saat  menggunakan  |        | sistem       |     |
| --- | ------------------- | --------- | ----- | ------------------ | ------ | ------------ | --- |
|     | (PP),  aspek        | tersebut  |       | tidak              | cukup  | kuat  untuk  |     |
|     | mendorong           |           | niat  | mereka             | untuk  | terus        |     |
menggunakan sistem secara berkelanjutan (CI).
Hasil ini menunjukkan bahwa rasa bermain atau
kesenangan bersifat sekunder dan bukan faktor
|     | utama        | dalam       | keputusan  |            | pengguna  | untuk        |     |
| --- | ------------ | ----------- | ---------- | ---------- | --------- | ------------ | --- |
|     | melanjutkan  | penggunaan  |            | aplikasi.  |           | Hasil  yang  |     |
tidak signifikan pada penelitian ini menunjukkan
|     | bahwa     | pengaruh     | Perceived  |            | Playfulness  | (PP)         |     |
| --- | --------- | ------------ | ---------- | ---------- | ------------ | ------------ | --- |
|     | terhadap  | Continuance  |            | Intention  |              | (CI)  hanya  |     |
berlaku pada sampel penelitian serta tidak dapat
digeneralisasikan sebagai faktor penentu utama
|     | niat  penggunaan  |     | berkelanjutan  |     | pada  | populasi  |     |
| --- | ----------------- | --- | -------------- | --- | ----- | --------- | --- |
secara luas.

DIGITAL REPOSITORY UNIVERSITAS JEMBER

| DIGITAL REPOSITORY UNIVERSITAS JEMBER |     |     |     |     | 72  |
| ------------------------------------- | --- | --- | --- | --- | --- |

Lampiran  8 Identifikasi Jawaban Responden
Prioritas Perbaikan Berdasarkan Technology Acceptance Model (TAM)
| Kode  | Pernyataan  |          | Indikator Penilaian  |            |       |
| ----- | ----------- | -------- | -------------------- | ---------- | ----- |
|       |             | Jawaban  | Jawaban              | Rata-Rata  | Rata- |
|       |             | Positif  | Negatif              | Indikator  | Rata  |
Variabel
Perceived Usefulness (PU)
| PU1  Saya merasa dengan       |     | 122  | 2   | 3,524  |        |
| ----------------------------- | --- | ---- | --- | ------ | ------ |
| menggunakan aplikasi Figma    |     |      |     |        |        |
| Make memungkinkan saya        |     |      |     |        |        |
| untuk dapat menyelesaikan     |     |      |     |        |        |
| tugas lebih cepat             |     |      |     |        |        |
| PU2  Saya merasa menggunakan  |     | 121  | 3   | 3,580  |        |
| aplikasi Figma Make membuat   |     |      |     |        | 3,487  |
pekerjaan saya lebih mudah
dilakukan.
| PU3  Saya merasa aplikasi Figma  |     | 116  | 8   | 3,346  |     |
| -------------------------------- | --- | ---- | --- | ------ | --- |
Make memainkan peran
penting dalam memberi saya
inspirasi
| PU4  |     | 118  | 6   | 3,5  |     |
| ---- | --- | ---- | --- | ---- | --- |
Saya merasa menggunakan
aplikasi Figma Make
membantu memperkuat
pengetahuan saya
Attitude Toward Using (ATT)
| ATT1  Menggunakan aplikasi Figma  |     | 118  | 6   | 3,491  |     |
| --------------------------------- | --- | ---- | --- | ------ | --- |

Make merupakan ide yang
bagus bagi saya
3,430
| ATT2  Saya suka menggunakan  |     | 113  | 11  | 3,427  |     |
| ---------------------------- | --- | ---- | --- | ------ | --- |
aplikasi Figma Make
| ATT3  Saya terkesan menggunakan  |     | 113  | 11  | 3,370  |     |
| -------------------------------- | --- | ---- | --- | ------ | --- |
aplikasi Figma Make

Prioritas Perbaikan Berdasarkan Expectation Confirmation Model (ECM)
| Kode  | Pernyataan  |          | Indikator Penilaian  |            |            |
| ----- | ----------- | -------- | -------------------- | ---------- | ---------- |
|       |             | Jawaban  | Jawaban              | Rata-Rata  | Rata-Rata  |
|       |             | Positif  | Negatif              | Indikator  | Variabel   |
Confirmation of Expectation (CE)
| CE1  Saya merasa pengalaman    |     | 110  | 14  | 3,274  |     |
| ------------------------------ | --- | ---- | --- | ------ | --- |
| menggunakan Figma Make         |     |      |     |        |     |
| melebihi ekspektasi yang saya  |     |      |     |        |     |
| harapkan                       |     |      |     |        |     |
3,346
| CE2  Saya merasa layanan yang  |     | 109  | 15  | 3,330  |     |
| ------------------------------ | --- | ---- | --- | ------ | --- |
disediakan aplikasi Figma
Make melebihi ekspektasi
saya
| CE3  Saya merasa menggunakan  |     | 112  | 12  | 3,435  |     |
| ----------------------------- | --- | ---- | --- | ------ | --- |
aplikasi Figma Make
membantu memenuhi layanan
yang saya butuhkan
Satisfaction (SAT)
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER 73

| SAT1  Aplikasi Figma Make  |     | 114  | 10  | 3,354  |     |
| -------------------------- | --- | ---- | --- | ------ | --- |

memenuhi kebutuhan saya,
| yang membuat saya merasa  |     |      |     |        |        |
| ------------------------- | --- | ---- | --- | ------ | ------ |
| bahagia                   |     |      |     |        |        |
| SAT2                      |     | 117  | 7   | 3,451  | 3,448  |
Pengalaman menggunakan
aplikasi Figma Make
membuat saya merasa puas
| SAT3  |     | 118  | 6   | 3,540  |     |
| ----- | --- | ---- | --- | ------ | --- |
Secara keseluruhan,
menggunakan aplikasi Figma
Make membuat saya merasa
puas untuk membantu desain
Continuance Intention (CI)
| CI1  Saya akan terus menggunakan  |     | 114  | 10  | 3,282  |     |
| --------------------------------- | --- | ---- | --- | ------ | --- |

aplikasi Figma Make dalam
| menyelesaikan tugas         |     |      |     |        |     |
| --------------------------- | --- | ---- | --- | ------ | --- |
| CI2  Saya merekomendasikan  |     | 114  | 10  | 3,387  |     |
3,306
orang lain untuk
menggunakan aplikasi Figma
Make
| CI3  |     | 107  | 17  | 3,250  |     |
| ---- | --- | ---- | --- | ------ | --- |
Saya lebih memilih
menggunakan aplikasi Figma
Make dibandingkan dengan
aplikasi lain sejenis

Prioritas Perbaikan Berdasarkan User Experience (UX)
| Kode  | Pernyataan  |          | Indikator Penilaian  |            |            |
| ----- | ----------- | -------- | -------------------- | ---------- | ---------- |
|       |             | Jawaban  | Jawaban              | Rata-Rata  | Rata-Rata  |
|       |             | Positif  | Negatif              | Indikator  | Variabel   |
Emotional Experience (EE)
| EE1  |     | 116  | 8   | 3,362  |     |
| ---- | --- | ---- | --- | ------ | --- |
Saya merasa menggunakan
| aplikasi Figma Make membuat   |     |      |     |        |        |
| ----------------------------- | --- | ---- | --- | ------ | ------ |
| saya merasa senang dan        |     |      |     |        |        |
| gembira                       |     |      |     |        |        |
| EE2  Saya merasa menggunakan  |     | 115  | 9   | 3,620  |        |
| aplikasi Figma Make           |     |      |     |        | 3,489  |
menghasilkan output yang
memberikan saya kesenangan
| EE3  Saya merasa menggunakan  |     | 112  | 12  | 3,483  |     |
| ----------------------------- | --- | ---- | --- | ------ | --- |
Figma Make sistem membantu
meningkatkan keterikatan
emosional
Interactive Experience (IE)
| IE1  Saya merasa interaksi  |     | 119  | 5   | 3,379  |     |
| --------------------------- | --- | ---- | --- | ------ | --- |
| menggunakan aplikasi Figma  |     |      |     |        |     |

Make terasa cepat dan
responsif

| IE2  Saya merasa kecepatan dan  |     | 117  | 7   | 3,443  | 3,397  |
| ------------------------------- | --- | ---- | --- | ------ | ------ |

akurasi hasil pencarian aplikasi
Figma Make memuaskan
| IE3  Saya merasa menggunakan  |     | 112  | 12  | 3,370  |     |
| ----------------------------- | --- | ---- | --- | ------ | --- |
aplikasi Figma Make membuat
saya nyaman dalam
berinteraksi
DIGITAL REPOSITORY UNIVERSITAS JEMBER

| DIGITAL REPOSITORY UNIVERSITAS JEMBER |     |     |     |     | 74  |
| ------------------------------------- | --- | --- | --- | --- | --- |

Prioritas Perbaikan Berdasarkan Karakteristik AI
| Kode  | Pernyataan  |          | Indikator Penilaian  |            |            |
| ----- | ----------- | -------- | -------------------- | ---------- | ---------- |
|       |             | Jawaban  | Jawaban              | Rata-Rata  | Rata-Rata  |
|       |             | Positif  | Negatif              | Indikator  | Variabel   |
Perceived Intelligence (PI)
| PI1  Saya merasa aplikasi Figma  |     | 115  | 9   | 3,419  |        |
| -------------------------------- | --- | ---- | --- | ------ | ------ |
| Make dapat menyelesaikan         |     |      |     |        |        |
| tugas dengan cerdas              |     |      |     |        |        |
| PI2  Saya merasa aplikasi Figma  |     | 113  | 11  | 3,282  |        |
| Make sangat efektif dalam        |     |      |     |        |        |
| menyelesaikan masalah            |     |      |     |        |        |
| PI4  Saya merasa aplikasi Figma  |     | 116  | 8   | 3,322  | 3,350  |
Make mampu memahami
intruksi yang saya berikan
dengan baik
| PI5  Saya merasa aplikasi Figma  |     | 115  | 9   | 3,379  |     |
| -------------------------------- | --- | ---- | --- | ------ | --- |
Make dapat memahami
Riwayat interaksi yang saya
berikan sebelumnya
Perceived Novelty (PN)
| PN1  Saya merasa menggunakan  |     | 118  | 6   | 3,483  |     |
| ----------------------------- | --- | ---- | --- | ------ | --- |
| aplikasi Figma Make membuat   |     |      |     |        |     |

saya menemukan pengalaman
baru (atau unik)

| PN2  Saya merasa menggunakan  |     | 120  | 4   | 3,508  |     |
| ----------------------------- | --- | ---- | --- | ------ | --- |

aplikasi Figma Make membuat
| saya menemukan hal baru dan  |     |     |     |     | 3,487  |
| ---------------------------- | --- | --- | --- | --- | ------ |
refreshing
| PN3  |     | 120  | 4   | 3,435  |     |
| ---- | --- | ---- | --- | ------ | --- |
Saya merasa aplikasi Figma
Make memberikan suatu hal
yang berbeda dengan teknologi
yang sudah ada dan menarik
| PN4  Saya merasa menggunakan  |     | 120  | 4   | 3,379  |     |
| ----------------------------- | --- | ---- | --- | ------ | --- |
Figma Make menjadi cara
sederhana dan inovatif dalam
menyelesaikan tugas
Perceived Trust (PT)
| PT1  |     | 111  | 13  | 3,379  |     |
| ---- | --- | ---- | --- | ------ | --- |
Saya merasa percaya terhadap
keandalan aplikasi Figma Make

| PT2  Saya merasa percaya pada  |     | 107  | 17  | 3,25  |     |
| ------------------------------ | --- | ---- | --- | ----- | --- |

sumber data yang digunakan
aplikasi Figma Make

| PT3  Saya memiliki keyakinan  |     | 109  | 15  | 3,217  | 3,312  |
| ----------------------------- | --- | ---- | --- | ------ | ------ |
terhadap perlindungan privasi
dari aplikasi Figma Make
| PT4  Saya percaya bahwa aplikasi  |     | 117  | 7   | 3,403  |     |
| --------------------------------- | --- | ---- | --- | ------ | --- |
Figma Make dapat membantu
saya dalam menggunakannya
dengan cara yang tepat
Perceived Playfulness (PP)
DIGITAL REPOSITORY UNIVERSITAS JEMBER

| DIGITAL REPOSITORY UNIVERSITAS JEMBER |     |     | 75  |
| ------------------------------------- | --- | --- | --- |

| PP1  Saya merasa menggunakan  | 119  | 5  3,51  |     |
| ----------------------------- | ---- | -------- | --- |

aplikasi Figma Make membuat
saya merasa tertarik

| PP2  Saya merasa menggunakan  | 113  | 11  3,403  |     |
| ----------------------------- | ---- | ---------- | --- |
3,440
aplikasi Figma Make membuat
saya menikmati proses
| PP3  Saya merasa aplikasi Figma  | 117  | 7  3,419  |     |
| -------------------------------- | ---- | --------- | --- |
Make memberikan kemudahan
dan kesenangan ketika
menyelesaikan tugas

DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
76
Lampiran 9 Kuesioner Penelitian
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER 77

Lampiran  10 Dokumentasi Pengumpulan Data
|     |     |     |     |
| --- | --- | --- | --- |

Pengumpulan Data Melalui  Pengumpulan Data Melalui  Pengumpulan Data Melalui
| Platform Instagram  | Platform Telegram  | Platform WhatsApp  |     |
| ------------------- | ------------------ | ------------------ | --- |
|                     |                    |                    |     |
Pengumpulan Data Melalui  Pengumpulan Data Melalui  Pengumpulan Data Melalui
| Platform Facebook  | Platform X  | Broadcast Tele Univ  |     |
| ------------------ | ----------- | -------------------- | --- |
DIGITAL REPOSITORY UNIVERSITAS JEMBER

DIGITAL REPOSITORY UNIVERSITAS JEMBER
78
Lampiran 11 Data Penelitian
QR Code Data Penelitian
DIGITAL REPOSITORY UNIVERSITAS JEMBER