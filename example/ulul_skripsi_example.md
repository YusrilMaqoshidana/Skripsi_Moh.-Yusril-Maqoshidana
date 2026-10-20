SISTEM REKOMENDASI MATA KULIAH PILIHAN
MENGGUNAKAN GRAPH NEURAL NETWORK PADA
KNOWLEDGE GRAPH DATA AKADEMIK MAHASISWA
(STUDI KASUS: FAKULTAS ILMU KOMPUTER
UNIVERSITAS JEMBER)
Diajukan untuk memenuhi sebagian persyaratan memperoleh gelar Sarjana pada
program studi Teknologi Informasi
SKRIPSI
Oleh
Ulul ‘Azmi
222410102068
KEMENTERIAN PENDIDIKAN TINGGI, SAINS, DAN TEKNOLOGI
UNIVERSITAS JEMBER
FAKULTAS ILMU KOMPUTER
PROGRAM STUDI TEKNOLOGI INFORMASI
JEMBER
2026

PERSEMBAHAN
Skripsi ini saya persembahkan dengan penuh rasa syukur dan cinta kasih kepada:
1. Allah SWT yang telah memberikan rahmat, karunia, dan kemudahan
dalam setiap langkah penyusunan skripsi ini.
2. Kedua orang tua penulis serta keluarga besar yang senantiasa mendoakan,
memberikan dukungan moral dan material, serta pengorbanan yang tak
terhingga sehingga penulis dapat menyelesaikan pendidikan tingkat
sarjana.
3. Bapak Priza Pandunata, S.Kom., M.Sc. selaku Dosen Pembimbing Utama
yang telah meluangkan waktu dan memberikan arahan serta masukan
selama proses penyusunan skripsi.
4. Seluruh dosen yang telah memberikan ilmu kepada penulis serta civitas
akademik Fakultas Ilmu Komputer Universitas Jember yang telah
membantu selama proses pengumpulan data.
5. Seluruh teman penulis yang telah memberikan doa dan dukungan.
6. Almamater Program Studi Teknologi Informasi Fakultas Ilmu Komputer
Universitas Jember.
ii

MOTTO
“Mengeluh tidak pernah menyelesaikan masalah”
Ulul ‘Azmi
iii

iv

v

ABSTRACT
The academic planning process is a crucial phase for students at the Faculty of
Computer Science, Universitas Jember. However, many students face difficulties
in selecting elective courses that align with their capabilities and the faculty's
recommended learning paths, often leading to suboptimal study durations. This
research aims to develop an intelligent course recommendation system utilizing a
Graph Neural Network (GNN) on a Knowledge Graph (KG) to address these
issues. The methodology involves constructing a Heterogeneous Knowledge
Graph derived from two primary faculty datasets: the official curriculum and
historical academic transcripts of students from the 2020-2022 cohorts. The
extracted graph structurally models students, courses, explicit prerequisite rules,
and academic performances. A Graph Attention Network (GAT) architecture was
implemented to perform link regression tasks, predicting the relevance score of
un-taken courses based on multi-hop dependencies and self-attention
mechanisms. The model evaluation demonstrated outstanding performance with
an RMSE of 0.5487, Precision of 0.9494, Recall of 0.9981, F1-Score of 0.9732,
MAP of 0.9715, and NDCG of 0.9939. Furthermore, an ablation study proved that
the GAT significantly outperformed conventional aggregation algorithms by
successfully assigning higher attention weights to relevant prerequisite courses.
The study concludes that integrating prerequisite structures into the Knowledge
Graph acts as a logical pacing mechanism, accurately guiding students along
realistic learning paths. The resulting recommendation model was successfully
integrated into a mobile application prototype, allowing students to filter course
recommendations based on their specific career interests.
Keywords: Course Recommendation, Graph Neural Network, Knowledge Graph,
Graph Attention Network, Educational Data Mining.
vi

RINGKASAN
Penelitian ini dilatarbelakangi oleh kesulitan mahasiswa Fakultas Ilmu
Komputer Universitas Jember dalam menentukan mata kuliah pilihan yang sesuai
dengan kemampuan akademik dan learning path yang direkomendasikan fakultas.
Kesalahan dalam perencanaan studi seringkali berdampak pada keterlambatan
masa studi, terutama saat mahasiswa harus menentukan topik skripsi tanpa bekal
mata kuliah prasyarat yang linier. Untuk mengatasi masalah tersebut, penelitian
ini mengembangkan sebuah sistem rekomendasi mata kuliah cerdas yang
mengkombinasikan keunggulan teknologi Knowledge Graph (KG) dan Graph
Neural Network (GNN).
Data mentah yang digunakan terdiri dari dokumen kurikulum resmi dan
transkrip nilai mahasiswa angkatan 2020–2022. Data tersebut dimodelkan
menjadi Heterogeneous Knowledge Graph yang memetakan hubungan antara
mahasiswa, mata kuliah, riwayat nilai, serta aturan sekuensial prasyarat hasil
validasi Koordinator Program Studi. Model prediksi dibangun menggunakan
arsitektur Graph Attention Network (GAT) untuk mengeksekusi tugas link
regression. Mekanisme attention pada GAT memungkinkan sistem untuk
memberikan bobot prioritas tertinggi secara implisit pada mata kuliah yang
prasyarat dasarnya telah dilulusi dengan nilai baik oleh mahasiswa terkait.
Hasil pengujian eksperimental menunjukkan bahwa model GAT mencapai
konvergensi yang sangat baik dengan nilai RMSE sebesar 0.5487, Precision
0.9494, dan NDCG 0.9939. Analisis pada studi ablasi juga membuktikan bahwa
arsitektur GAT secara signifikan mengungguli algoritma agregasi graf
konvensional yang tidak menggunakan atensi. Sistem rekomendasi ini kemudian
diimplementasikan dalam bentuk Application Programming Interface (API) yang
diintegrasikan ke dalam antarmuka prototipe aplikasi mobile. Melalui aplikasi ini,
mahasiswa dapat memperoleh rekomendasi mata kuliah yang difilter secara
spesifik sesuai dengan kategori minat atau topik skripsi yang mereka pilih. Secara
keseluruhan, integrasi struktur prasyarat kurikulum ke dalam jaringan graf
vii

terbukti memberikan kontribusi krusial sebagai rem dan akselerator akademis
guna menjaga akurasi jalur pembelajaran.
viii

PRAKATA
Puji syukur kehadirat Allah SWT atas segala rahmat, hidayah, dan
karunia-Nya, sehingga penulis dapat menyelesaikan penyusunan skripsi yang
berjudul “Sistem Rekomendasi Mata Kuliah Pilihan Menggunakan Graph Neural
Network pada Knowledge Graph Data Akademik Mahasiswa (Studi Kasus:
Fakultas Ilmu Komputer Universitas Jember)”. Skripsi ini disusun untuk
memenuhi salah satu syarat akademik dalam menyelesaikan pendidikan Strata
Satu (S1) pada Program Studi Teknologi Informasi Fakultas Ilmu Komputer
Universitas Jember.
Penulis menyadari bahwa proses penyusunan skripsi ini tidak lepas dari
bimbingan, arahan, dan dukungan dari berbagai pihak. Oleh karena itu, pada
kesempatan ini penulis ingin menyampaikan ucapan terima kasih yang
sebesar-besarnya kepada:
1. Kedua orang tua penulis serta keluarga besar yang senantiasa mendoakan,
memberikan dukungan moral dan material untuk keberhasilan pendidikan
penulis.
2. Bapak Prof. Drs. Antonius Cahya Prihandoko, M.App.Sc., Ph.D., selaku
Dekan Fakultas Ilmu Komputer Universitas Jember.
3. Bapak Priza Pandunata, S.Kom., M.Sc. selaku Dosen Pembimbing Utama
yang telah meluangkan waktu, tenaga, dan pikiran untuk memberikan
bimbingan, diskusi, serta arahan yang sangat berharga sejak awal hingga
skripsi ini selesai.
4. Bapak Prof. Drs. Slamin, M.Comp.Sc., Ph.D. dan Bapak Rizky Alfanio
Atmoko, S.Si., M.Sc. selaku Dosen Penguji yang telah memberikan ujian,
saran, dan masukan yang konstruktif demi kesempurnaan laporan skripsi
ini.
5. Bapak/Ibu Koordinator Program Studi Teknologi Informasi, Sistem
Informasi, dan Informatika Fakultas Ilmu Komputer Universitas Jember
atas dukungan dan validasi data akademik yang diberikan.
ix

6. Bapak Mohammad Zarkasi, S.Kom., M.Kom. selaku Dosen Pembimbing
Akademik yang telah mendampingi, memberikan motivasi, dan
memberikan arahan rencana studi selama masa perkuliahan penulis.
7. Seluruh Dosen dan Staf Tenaga Kependidikan Fakultas Ilmu Komputer
Universitas Jember atas segala transfer ilmu pengetahuan dan layanan
administrasi yang responsif.
8. Teman-teman angkatan, teman-teman KKN, serta keluarga HIMATIF atas
segala dukungan dan kebersamaan yang telah membentuk penulis hingga
sampai pada titik ini.
9. Semua pihak yang tidak dapat disebutkan satu per satu, yang telah
mendoakan dan memberikan dukungan baik moral maupun material.
Penulis menyadari bahwa karya tulis ilmiah ini masih jauh dari kata
sempurna dan memiliki berbagai keterbatasan. Oleh karena itu, kritik dan saran
yang membangun sangat diharapkan untuk perbaikan di masa mendatang. Akhir
kata, semoga skripsi ini dapat memberikan manfaat nyata bagi pengembangan
ilmu pengetahuan di bidang Kecerdasan Buatan dan memberikan sumbangsih
positif bagi pembaca pada umumnya.
Jember, 24 April 2026
Penulis
x

DAFTAR ISI
HALAMAN JUDUL...............................................................................................i
PERSEMBAHAN..................................................................................................ii
MOTTO.................................................................................................................iii
PERNYATAAN ORISINALITAS........................................................................iv
HALAMAN PERSETUJUAN...............................................................................v
ABSTRACT...........................................................................................................vi
RINGKASAN.......................................................................................................vii
PRAKATA.............................................................................................................ix
DAFTAR ISI..........................................................................................................xi
DAFTAR TABEL................................................................................................xiii
DAFTAR GAMBAR...........................................................................................xiv
DAFTAR LAMPIRAN........................................................................................xv
BAB 1. PENDAHULUAN.....................................................................................1
1.1 Latar Belakang.............................................................................................1
1.2 Rumusan Masalah........................................................................................3
1.3 Tujuan Penelitian..........................................................................................3
1.4 Manfaat Penelitian.......................................................................................4
1.5 Batasan Penelitian........................................................................................4
BAB 2. TINJAUAN PUSTAKA............................................................................5
2.1 Penelitian Terdahulu.....................................................................................5
2.2 Sistem Rekomendasi....................................................................................5
2.3 Educational Data Mining dan Learning Analytics.......................................8
2.4 Knowledge Graph (KG)...............................................................................8
2.5 Graph Neural Network (GNN).....................................................................9
2.6 Graph Attention Network (GAT)...............................................................10
2.7 Evaluasi Model...........................................................................................10
BAB 3. METODOLOGI PENELITIAN............................................................13
3.1 Jenis Penelitian...........................................................................................13
3.2 Objek Penelitian.........................................................................................13
3.3 Tempat dan Waktu Penelitian.....................................................................13
3.4 Tahapan Penelitian.....................................................................................14
3.4.1 Studi Literatur...................................................................................14
3.4.2 Pengumpulan Data............................................................................14
3.4.3 Pra-pemrosesan dan Konstruksi Knowledge Graph (KG)................15
3.4.4 Implementasi Model GNN................................................................16
3.4.5 Evaluasi Model..................................................................................19
xi

3.4.6 Pengembangan Sistem......................................................................20
BAB 4. HASIL DAN PEMBAHASAN...............................................................21
4.1 Pengumpulan dan Pra-pemrosesan Data....................................................21
4.2 Konstruksi Knowledge Graph untuk Data Akademik...............................24
4.2.1 Relasi Akademik Historis.................................................................24
4.2.2 Relasi Aturan Kurikulum..................................................................25
4.3 Implementasi dan Pelatihan Model GNN..................................................26
4.3.1 Hasil Optimasi Hyperparameter........................................................27
4.4 Analisis Hasil Evaluasi Model...................................................................28
4.4.1 Evaluasi Skenario Data Leakage.......................................................30
4.5 Analisis Hasil Studi Ablasi........................................................................30
4.6 Implementasi Sistem Rekomendasi...........................................................32
4.6.1 Skenario Pengujian Rekomendasi.....................................................34
BAB 5. KESIMPULAN........................................................................................35
5.1 Kesimpulan.................................................................................................35
5.2 Saran...........................................................................................................35
DAFTAR PUSTAKA............................................................................................36
LAMPIRAN..........................................................................................................39
xii

DAFTAR TABEL
Tabel 2.1 Penelitian Terdahulu.................................................................................6
Tabel 4.1 Data mata kuliah.....................................................................................21
Tabel 4.2 Data prasyarat mata kuliah.....................................................................23
Tabel 4.3 Data transkrip mahasiswa angkatan 2020-2022.....................................23
xiii

DAFTAR GAMBAR
Gambar 3.1 Tahapan Penelitian.............................................................................14
Gambar 3.2 Skema konstruksi KG.........................................................................16
Gambar 3.3 Arsitektur GNN..................................................................................17
Gambar 3.4 Pelatihan model GNN........................................................................18
Gambar 3.6 Diagram arsitektur sistem...................................................................20
Gambar 4.1 Distribusi mata kuliah pilihan berdasarkan kategori minat/learning
path.........................................................................................................................23
Gambar 4.2 Distribusi Label Nilai pada Dataset Transkrip Akademik.................24
Gambar 4.3 Visualisasi konstruksi Knowledge Graph untuk satu mahasiswa......25
Gambar 4.4 Kurva penurunan MSE Loss selama pelatihan GAT..........................26
Gambar 4.5 Analisis Optimasi Hyperparameter....................................................27
Gambar 4.6 Hasil evaluasi metrik performa model pada test set...........................29
Gambar 4.7 Confusion Matrix Prediksi Model GAT.............................................29
Gambar 4.8 Hasil Evaluasi Skenario Data Leakage..............................................30
Gambar 4.9 Hasil perbandingan GraphSAGE dan GAT........................................31
Gambar 4.10 Antarmuka aplikasi mobile implementasi sistem rekomendasi.......33
xiv

DAFTAR LAMPIRAN
Lampiran 1. Mockup Aplikasi...............................................................................39
xv

BAB 1. PENDAHULUAN
1.1 Latar Belakang
Perguruan tinggi termasuk Universitas Jember berada dalam arus
transformasi digital yang menuntut peningkatan kualitas layanan akademik dan
administrasi (Shenkoya & Kim, 2023). Dalam konteks akademik, salah satu
momen paling krusial bagi mahasiswa di setiap awal semester adalah perencanaan
studi. Keputusan yang diambil pada fase ini sangat menentukan efektivitas jalur
studi, pencapaian kompetensi, dan keselarasan lulusan dengan kebutuhan industri.
Kebijakan pemerintah saat ini, seperti program Magang Berdampak semakin
menekankan fleksibilitas dan personalisasi jalur studi, mendorong mahasiswa
untuk merancang kurikulum yang sesuai dengan kemampuan spesifik mereka.
Universitas Jember telah melakukan digitalisasi proses ini melalui Sistem
Informasi Akademik (SIAKAD). Namun, digitalisasi belum sepenuhnya
menjawab aspek pengambilan keputusan yang optimal. Hal ini terlihat signifikan
di Fakultas Ilmu Komputer, di mana mahasiswa dihadapkan pada fenomena
keharusan memilih sejumlah mata kuliah pilihan. Namun, alih-alih merencanakan
studi yang selaras dengan kemampuan, keputusan mahasiswa seringkali
didasarkan pada strategi yang kurang optimal, seperti popularitas mata kuliah,
nama dosen, mengikuti teman sebaya, atau bahkan spekulasi. Berdasarkan survei
kuesioner pada tanggal 8 hingga 9 Juni 2025 (n=51), ditemukan bahwa 66,7%
mahasiswa Fakultas Ilmu Komputer Universitas Jember mengalami kesulitan
signifikan dalam pengambilan keputusan untuk memilih mata kuliah pilihan.
Survei dilakukan dengan metode probability sampling untuk memastikan bahwa
mahasiswa program studi Sistem Informasi, Teknologi Informasi, dan Informatika
memiliki peluang yang sama dan dapat digeneralisasi.
Fakultas Ilmu Komputer telah menyediakan pedoman jalur peminatan
(learning path), namun implementasi di lapangan belum berjalan optimal.
Berdasarkan hasil wawancara dengan Wakil Dekan 1 Bidang Akademik, kendala
utamanya adalah kurangnya kesadaran mahasiswa terhadap arah minat atau topik
1

2
skripsi mereka sejak awal. Akibatnya, mahasiswa masih banyak yang memilih
mata kuliah hanya dengan mengikuti teman sebaya. Hal ini berdampak fatal pada
masa studi, di mana banyak mahasiswa terhambat dan membutuhkan waktu lama
saat pengerjaan skripsi karena mengambil topik dari nol tanpa membekali diri
dengan mata kuliah prasyarat yang relevan. Oleh karena itu, sistem rekomendasi
ini dibangun untuk membantu eksekusi learning path fakultas secara terstruktur
agar mahasiswa lebih menyadari arah minatnya.
Volume data akademik yang besar dihasilkan dari percepatan adopsi
teknologi pasca-pandemi, kini membuka peluang untuk mengatasi masalah
pengambilan keputusan ini melalui inovasi berbasis data (Molleví Bortoló et al.,
2023). Data historis mahasiswa merupakan aset strategis, jika dikelola dengan
baik dapat diolah menggunakan Kecerdasan Buatan (AI) dan Data Mining
(Thajchayapong & Goel, 2025). Perkembangan AI memungkinkan transisi dari
sistem administrasi data (SIAKAD) menjadi sistem panduan studi cerdas.
Penerapan Sistem Rekomendasi, yang telah sukses terbukti di industri
e-commerce (Gulzar et al., 2023) sangat potensial untuk diaplikasikan dalam
konteks akademik. Tujuannya adalah menavigasi mahasiswa dalam kurikulum
akademik dengan menganalisis pola yang selaras dengan kemampuan mereka
sebelumnya (Beutling & Spahic-Bogdanovic, 2024).
Penerapan sistem rekomendasi dalam konteks akademik masih
menghadapi tantangan yang sulit diselesaikan oleh model konvensional. Data
akademik memiliki struktur yang heterogen dan relasional yang kompleks.
Hubungan antar mata kuliah dan performa historis mahasiswa merupakan
informasi kontekstual yang sulit dimodelkan hanya menggunakan matriks biasa.
Akibatnya, model tradisional seringkali kesulitan menangani data sparsity dan
cold start, serta gagal menangkap dependensi multi-step yang tersirat dalam
struktur kurikulum (Wang et al., 2024). Oleh karena itu, diperlukan pendekatan
yang lebih canggih untuk memodelkan dan memahami konteks hubungan data
secara holistik.
Untuk menjawab tantangan pemodelan data yang kompleks dan relasional
tersebut, penelitian ini mengusulkan penggunaan Knowledge Graph (KG) sebagai

3
representasi data dan Graph Neural Network (GNN) sebagai model prediktif. KG
memiliki kemampuan untuk memodelkan entitas yang bermacam-macam seperti
mahasiswa, mata kuliah, serta hubungan kompleks di antara mereka (Zhang et al.,
2021). Sementara itu, GNN dirancang khusus untuk menangani data dalam bentuk
graf, memungkinkannya belajar representasi fitur dari setiap entitas dengan
menganalisis struktur koneksi di sekitarnya (Khemani et al., 2024). Dengan
pendekatan tersebut, penelitian ini bertujuan untuk mengembangkan sistem
rekomendasi yang tidak hanya akurat, tetapi juga mampu memberikan
rekomendasi yang relevan bagi mahasiswa serta menjadi panduan cerdas dalam
proses perencanaan studi di Universitas Jember.
1.2 Rumusan Masalah
1. Bagaimana merancang Knowledge Graph yang mampu
merepresentasikan entitas data akademik dan struktur prasyarat
kurikulum secara terstruktur?
2. Bagaimana mengimplementasikan model Graph Neural Network (GNN)
dengan arsitektur Graph Attention Network (GAT) untuk mempelajari
pola dari Knowledge Graph tersebut?
3. Seberapa besar kontribusi struktur prasyarat kurikulum dalam
meningkatkan kualitas rekomendasi GNN?
1.3 Tujuan Penelitian
1. Membangun sebuah model Knowledge Graph yang komprehensif untuk
data akademik dan struktur prasyarat kurikulum di Fakultas Ilmu
Komputer Universitas Jember.
2. Mengimplementasikan dan melatih model Graph Neural Network (GNN)
dengan arsitektur Graph Attention Network (GAT) yang mampu
memberikan rekomendasi mata kuliah pilihan berdasarkan pemenuhan
prasyarat dan riwayat akademik mahasiswa.
3. Mengetahui kontribusi struktur prasyarat kurikulum dalam meningkatkan
kualitas rekomendasi GNN.

4
1.4 Manfaat Penelitian
1. Membantu mahasiswa dalam mengambil keputusan KRS yang lebih
tepat, personal, dan strategis serta mengurangi resiko kesalahan dalam
perencanaan studi.
2. Mendukung institusi pendidikan tinggi dalam menyediakan alat bantu
bimbingan akademik yang lebih efisien, sehingga meningkatkan
pengalaman mahasiswa dan potensi kelulusan tepat waktu.
3. Memberikan pendekatan baru dalam pengembangan sistem rekomendasi
mata kuliah dengan mengintegrasikan Knowledge Graph dan Graph
Neural Network.
4. Menjadi referensi dan landasan bagi penelitian selanjutnya yang ingin
mengembangkan sistem serupa di fakultas atau universitas lain.
1.5 Batasan Penelitian
1. Penelitian ini hanya berfokus pada data kurikulum dari Fakultas Ilmu
Komputer Universitas Jember periode terbaru.
2. Data riwayat akademik yang digunakan terbatas pada data mahasiswa
angkatan 2020 - 2022 sejumlah 698 mahasiswa.
3. Model rekomendasi tidak mempertimbangkan faktor non-akademik
seperti jadwal kuliah dan jumlah SKS karena model berfokus pada
relevansi konten.
4. Sistem rekomendasi ini mempertimbangkan variabel preferensi atau
minat eksplisit dari mahasiswa yang akan dicocokkan dengan learning
path pada representasi Knowledge Graph.
5. Luaran penelitian ini adalah sebuah model dan aplikasi prototipe, bukan
sebuah aplikasi yang terintegrasi langsung dengan Sistem Informasi
Akademik (SIAKAD) Universitas Jember karena keterbatasan hak akses
pada sistem tersebut.

BAB 2. TINJAUAN PUSTAKA
2.1 Penelitian Terdahulu
Tabel 1 menunjukkan bahwa penelitian oleh (Ramazanova et al., 2025)
dan (Hua et al., 2025) sangat canggih dalam menggunakan Knowledge Graph
(KG) dan GNN untuk menghubungkan kurikulum dengan data eksternal
(lowongan kerja dan MOOCs) guna menentukan relevansi karir. Sebaliknya,
penelitian oleh (Atalla et al., 2023) dan (Chetoui Ismail & Bachari, 2025) tidak
menggunakan GNN yang bisa menangani dependensi multi-step, sementara
Chetoui et al. berfokus pada interaksi yang ada tanpa memodelkan tujuan karir
(career goals) yang dinyatakan oleh mahasiswa. Penelitian ini mengisi celah
tersebut dengan pengembangan sistem rekomendasi hibrida yang menggunakan
GNN di atas Knowledge Graph yang murni bersifat internal untuk memodelkan
tiga elemen sekaligus, yaitu struktur kurikulum dan riwayat akademik mahasiswa.
2.2 Sistem Rekomendasi
Sistem rekomendasi merupakan jenis teknologi yang diperlukan untuk
memperoleh informasi guna merekomendasikan item yang relevan dengan
perilaku dan preferensi yang jelas dinyatakan oleh pengguna. Sistem rekomendasi
menganalisis kumpulan data yang besar dan berfokus pada penyediaan
rekomendasi konten yang andal bagi pengguna (Bohra & Bartere, 2022).
Penelitian (Uta et al., 2024) menyatakan bahwa sistem rekomendasi memiliki tiga
pendekatan konvensional, yaitu Collaborative Filtering (CF) dan Content-Based
Filtering (CBF), dan Knowledge-Based Recommender (KBR). CF berfokus pada
pemberian rekomendasi dengan membandingkan pada kasus yang serupa dari
pengguna lain. CBF memberikan rekomendasi berdasarkan persamaan
atribut/fitur dari item itu sendiri. KBR berfokus pada pengetahuan umum dan
kebutuhan eksplisit pengguna. Pendekatan konvensional tersebut masih memiliki
banyak tantangan, diantaranya cold start, kelangkaan data, dan masalah
skalabilitas (R. Gao, 2024).
5

6
Tabel 2.1 Penelitian Terdahulu
| No  | Judul  |     | Hasil  |     | Gap  |     | Kebaruan  |     |
| --- | ------ | --- | ------ | --- | ---- | --- | --------- | --- |
1  An  Intelligent  Recommendation  Mengembangkan  sistem  Tidak  menggunakan  GNN  yang  Menggunakan GNN (Graph Neural
System for Automating Academic  rekomendasi  akademik  bisa  digunakan  untuk dependensi  Network)  yang  mampu menangkap
Advising  Based  on  Curriculum  menggunakan  Bayesian  Belief  multi-step  untuk  menangkap  dependensi multi-step dari kurikulum
Analysis  and  Performance  Network (BBN) dengan akurasi  hubungan  kompleks  dalam  data  berupa  mata  kuliah  dengan
Modeling (Atalla et al., 2023)  hingga  86%  dan  recall  86%.  akademik.  prasyaratnya.
|     |     | Sistem            | mengintegrasikan  | teori  |     |     |     |     |
| --- | --- | ----------------- | ----------------- | ------ | --- | --- | --- | --- |
|     |     | graf,  pemodelan  | performa,         | dan    |     |     |     |     |
machine learning untuk analisis
|     |     | kurikulum  | dan  prediksi   | nilai  |     |     |     |     |
| --- | --- | ---------- | --------------- | ------ | --- | --- | --- | --- |
|     |     | mahasiswa  | di  University  | of     |     |     |     |     |
Dubai.
2  Personalized  Learning  Mengembangkan  model  Tidak  memodelkan  struktur  Membangun  Knowledge  Graph
Recommendations  Based  on  rekomendasi  pembelajaran  kurikulum  secara  eksplisit. Tidak  komprehensif  yang  memodelkan
Graph Neural Networks (Chetoui  menggunakan  GCN  dan  GAT  mempertimbangkan  aturan  struktur kurikulum termasuk aturan
& El Bachari, 2025)  dengan  F1-score  78.9%,  prasyarat mata kuliah.  prasyarat. Mengintegrasikan riwayat
|     |     | precision                          | 78.3%,  dan       | recall  |     | akademik    | dan  aturan            | kurikulum    |
| --- | --- | ---------------------------------- | ----------------- | ------- | --- | ----------- | ---------------------- | ------------ |
|     |     | 76.2%                              | pada  dataset     | OULAD.  |     | dalam       | satu  model.           | Menggunakan  |
|     |     | Model                              | mengintegrasikan  | data    |     | GNN  untuk  | mempelajari pola dari  |              |
|     |     | demografis, interaksi, dan metrik  |                   |         |     | Knowledge   | Graph  yang            | mencakup     |
|     |     | performa mahasiswa.                |                   |         |     | entitas     | beragam  (mahasiswa,   | mata         |
kuliah, dan prasyaratnya).
3  Knowledge Graph Convolutional  Mengembangkan  model  Fokus  pada  rekomendasi  kursus  Membangun  Knowledge  Graph
Networks with User Preferences  KGCN-UP  yang  online  (MOOC)  eksternal,  tidak  internal yang memodelkan kurikulum
for  Course  Recommendation  mengintegrasikan  preferensi  terintegrasi  dengan  kurikulum  akademik  lengkap  dengan  aturan
(Hua et al., 2025)  pengguna  dengan  Knowledge  internal  universitas.  Tidak  prasyarat. Mengintegrasikan riwayat
|     |     | Graph untuk rekomendasi kursus  |                  | mempertimbangkan  |            | riwayat  akademik mahasiswa (transkrip nilai)  |         |               |
| --- | --- | ------------------------------- | ---------------- | ----------------- | ---------- | ---------------------------------------------- | ------- | ------------- |
|     |     | MOOC.                           | Model  mencapai  | akademik          | mahasiswa  | di  institusi  sebagai                         | bagian  | dari  sistem  |

7
| performa             | superior             | dengan  | pendidikan           | tinggi.  | Tidak      | rekomendasi.  |          |               | Memberikan  |
| -------------------- | -------------------- | ------- | -------------------- | -------- | ---------- | ------------- | -------- | ------------- | ----------- |
| MAP@5                | sebesar  0.5739      | dan     | memodelkan           | aturan   | prasyarat  | rekomendasi   |          | mata  kuliah  | pilihan     |
| NDCG@5               | sebesar 0.6973 pada  |         | kurikulum akademik.  |          |            | dalam         | konteks  | kurikulum     | formal      |
| dataset real-world.  |                      |         |                      |          |            | universitas,  |          | bukan  hanya  | kursus      |
online eksternal.
4  Curriculum–Vacancy–Course  Mengembangkan  model  Mengintegrasikan  data  eksternal  Fokus pada rekomendasi mata kuliah
Recommendation  Model  Based  rekomendasi  yang  (lowongan kerja dan MOOC) tetapi  pilihan  internal  berdasarkan
on Knowledge Graphs, Sentence  mengintegrasikan  kurikulum  tidak fokus pada rekomendasi mata  kurikulum Fakultas Ilmu Komputer
Transformers, and Graph Neural  universitas, lowongan kerja, dan  kuliah pilihan internal universitas.  Universitas  Jember.  Menggunakan
Networks  (Ramazanova  et  al.,  kursus online menggunakan HGT  Tidak secara spesifik memodelkan  riwayat akademik mahasiswa untuk
2025)  (Heterogeneous  Graph  riwayat  akademik  individual  personalisasi  yang  lebih  dalam.
| Transformer).               | Model                | mencapai  | mahasiswa                           | untuk  personalisasi  |           | Membangun                  |            | Knowledge   | Graph         |
| --------------------------- | -------------------- | --------- | ----------------------------------- | --------------------- | --------- | -------------------------- | ---------- | ----------- | ------------- |
| NDCG@10 sebesar 0.7139 dan  |                      |           | rekomendasi.                        | Knowledge             | Graph     | internal                   | yang       | murni       | memodelkan    |
| MAP@10                      | sebesar              | 0.5508,   | yang  dibangun                      | lebih                 | kompleks  | struktur                   | kurikulum  |             | dan  riwayat  |
| menunjukkan                 | kemampuan            |           | dengan tiga sumber data eksternal,  |                       |           | akademik                   |            | mahasiswa   | tanpa         |
| superior                    | dalam  menghasilkan  |           | bukan internal kurikulum.           |                       |           | bergantung                 |            | pada  data  | eksternal     |
| rekomendasi                 | yang                 | relevan   |                                     |                       |           | lowongan kerja atau MOOC.  |            |             |               |
dengan tren pasar kerja.

8
2.3 Educational Data Mining dan Learning Analytics
Ketersediaan data pendidikan telah meningkat seiring dengan
perkembangan teknologi dan lingkungan pendidikan digital (Kharis & Zili, 2022).
Data yang berlimpah tersebut telah mendorong peneliti dan dan praktisi untuk
mengumpulkan dan menganalisis data guna mengungkap pola-pola yang dapat
diterapkan untuk memprediksi siswa yang kesulitan, meningkatkan proses belajar,
dan membuat keputusan yang bermanfaat bagi peserta didik. Educational Data
Mining (EDM) dan Learning Analytics (LA) merupakan dua bidang ilmu yang
berfokus pada eksplorasi data yang dikumpulkan dari lingkungan pendidikan
untuk meningkatkan proses dan hasil pembelajaran.
Penelitian (Baek & Doleck, 2023) menyebutkan bahwa EDM adalah
disiplin ilmu yang muncul dan berfokus pada pengembangan metode untuk
mengeksplorasi jenis data unik yang berasal dari lingkungan pendidikan. LA
merupakan bidang ilmu untuk pengukuran, pengumpulan, analisis, dan pelaporan
data tentang peserta didik dan konteksnya, dengan tujuan untuk memahami dan
mengoptimalkan pembelajaran dan lingkungan di mana hal itu terjadi (De
Andrade et al., 2021). Keduanya bertujuan meningkatkan proses pengajaran dan
pembelajaran dengan meningkatkan evaluasi, memahami masalah pendidikan,
dan merencanakan intervensi.
2.4 Knowledge Graph (KG)
Tantangan utama dalam memodelkan data akademik adalah sifatnya yang
multi sumber dan heterogen sehingga sulit ditangani oleh struktur data tradisional
(Lin et al., 2021). Data akademik yang kompleks melibatkan berbagai jenis entitas
seperti mahasiswa, mata kuliah, serta relasi-relasi implisit seperti prasyarat mata
kuliah. Keterbatasan ini dapat ditangani dengan menggunakan Knowledge Graph
(KG), yang telah muncul sebagai alat transformatif untuk meningkatkan sistem
rekomendasi personal (Dandu et al., 2023). KG mengorganisir informasi ke dalam
sebuah jaringan terstruktur, yang terdiri dari entitas (node) dan relasi (edge) di
antara mereka. Keunggulan utama KG adalah kemampuan untuk
mengintegrasikan kumpulan data yang beragam ke dalam satu tampilan

9
menyeluruh, memungkinkan penangkapan informasi kontekstual dan hubungan
timbal balik yang kompleks.
Dalam domain pendidikan, ini sangat krusial karena KG mampu
memodelkan relasi yang bersifat kognitif dan implisit, seperti relasi prasyarat
antara satu mata kuliah dengan mata kuliah lainnya (Li et al., 2024). Pendekatan
KG dapat mengurangi masalah data sparsity dan cold start dengan memperkaya
user-item bipartite graph dengan pengetahuan eksternal. Pemanfaatan KG dalam
penelitian ini adalah mengintegrasikan data heterogen, yaitu riwayat nilai
mahasiswa dan aturan kurikulum ke dalam satu model data yang seragam. KG
juga digunakan untuk memfasilitasi pemahaman konteks hubungan kompleks dan
dependensi multi-step kurikulum.
2.5 Graph Neural Network (GNN)
Model machine learning tradisional seperti CNN atau RNN dirancang
untuk data euclidean dengan dimensi dan urutan tetap, bukan data non-euclidean
seperti graf (Liang et al., 2022). Graph Neural Network (GNN) hadir sebagai
kelas arsitektur deep learning yang dirancang khusus untuk beroperasi langsung
pada struktur graf. Sebagian besar GNN mengikuti paradigma message-passing
(Finkelshtein et al., 2024) atau yang serupa, yaitu agregasi lingkungan
(neighborhood aggregation), di mana representasi dari sebuah node diperbarui
secara iteratif berdasarkan agregasi informasi dari node-node tetangganya. GNN
akan menangkap informasi struktural dan mempelajari node embeddings yang
mencerminkan konteks sebuah node di dalam jaringan.
Proses ini memungkinkan GNN untuk menangkap informasi struktural dan
konektivitas tingkat tinggi (high-order connectivity) dalam Knowledge Graph.
Kemampuan GNN dalam menangkap konektivitas tingkat tinggi sangat penting
karena model tradisional seringkali gagal menangkap dependensi multi-step dari
kurikulum (prasyarat). Dengan memodelkan hubungan multi-hop pada KG, GNN
dapat mereplikasi efek collaborative filtering (Gao et al., 2023) dan
menyimpulkan relevansi mata kuliah yang belum diambil dari jalur akademik.

10
2.6 Graph Attention Network (GAT)
Graph Attention Network (GAT) merupakan arsitektur GNN yang
beroperasi pada data berstruktur graf dengan memanfaatkan lapisan masked
self-attentional untuk mengatasi kekurangan metode konvolusi graf sebelumnya
(Veličković et al., 2018). GAT memungkinkan penentuan bobot secara implisit
pada node yang berbeda dalam satu lingkungan, memberikan peningkatan
kapasitas model dibandingkan dengan arsitektur lain. Keunggulan tersebut sangat
krusial dalam penelitian ini karena Knowledge Graph yang dibangun bersifat
heterogen, mengintegrasikan data riwayat akademik dan prasyarat kurikulum.
Dengan kapabilitas memberikan bobot (atensi) yang berbeda pada node tetangga
berdasarkan relevansinya, GAT berfungsi untuk memproses data heterogen dan
memastikan representasi vektor mahasiswa menangkap informasi kontekstual
yang paling relevan, seperti prasyarat mata kuliah.
2.7 Evaluasi Model
Metode evaluasi yang digunakan dalam penelitian ini dibagi menjadi tiga,
yaitu evaluasi klasifikasi (precision, recall, F1-score), evaluasi berbasis peringkat
(NDCG dan MAP), evaluasi untuk link regression (MRSE), dan validasi model
menggunakan studi ablasi.
2.7.1 Precision
Precision mengukur proporsi rekomendasi yang relevan dari semua
rekomendasi yang diberikan oleh sistem (Chetoui & El Bachari, 2025). Rumus
Precision adalah sebagai berikut:
𝑇𝑃
𝑃𝑟𝑒𝑐𝑖𝑠𝑖𝑜𝑛 =
𝑇𝑃+𝐹𝑃
2.7.2 Recall
Recall mengukur proporsi rekomendasi yang relevan yang berhasil
ditemukan oleh sistem dari semua mata kuliah yang sebenarnya relevan (Chetoui
& El Bachari, 2025). Rumus Recall adalah sebagai berikut:
𝑇𝑃
𝑅𝑒𝑐𝑎𝑙𝑙 =
𝑇𝑃+𝐹𝑁

11
2.7.3  F1-Score
F1-Score  adalah  rata-rata  harmonis  dari  Precision  dan  Recall,  yang
memberikan keseimbangan antara kedua matriks tersebut (Chetoui & El Bachari,
2025). Rumus F1-Score adalah sebagai berikut:
|     |     |     | 𝐹1 𝑆𝑐𝑜𝑟𝑒 |     | =   | 2 × 𝑃𝑟𝑒𝑐𝑖𝑠𝑖𝑜𝑛×𝑅𝑒𝑐𝑎𝑙𝑙 |     |     |     |
| --- | --- | --- | -------- | --- | --- | -------------------- | --- | --- | --- |
𝑃𝑟𝑒𝑐𝑖𝑠𝑖𝑜𝑛+𝑅𝑒𝑐𝑎𝑙𝑙

2.7.4  Normalized Discounted Cumulative Gain (NDCG)
| NDCG  |     | mengukur  |     | kualitas  |     | peringkat  | rekomendasi  |     | dengan  |
| ----- | --- | --------- | --- | --------- | --- | ---------- | ------------ | --- | ------- |
mempertimbangkan posisi item relevan dalam daftar rekomendasi (Ramazanova
et al., 2025). Semakin tinggi posisi item relevan, semakin baik skornya. NDCG
dihitung dengan rumus:
𝐷𝐶𝐺@𝑘
|     | 𝑁𝐷𝐶𝐺@𝑘 | =   |     |     |     |     |     | (1)  |     |
| --- | ------ | --- | --- | --- | --- | --- | --- | ---- | --- |
𝐼𝐷𝐶𝐺@𝑘
𝑘
𝑟𝑒𝑙
|     |       |     |     | 2 𝑖−1     |     |     |     |      |     |
| --- | ----- | --- | --- | --------- | --- | --- | --- | ---- | --- |
|     | 𝐷𝐶𝐺@𝑘 | =   | ∑   |           |     |     |     | (2)  |     |
|     |       |     |     | 𝑙𝑜𝑔 (𝑖+1) |     |     |     |      |     |
|     |       |     | 𝑖=1 | 2         |     |     |     |      |     |
𝑟𝑒𝑙*
𝑘
|     |       |     |     | 2 𝑖 −1    |     |     |     |      |     |
| --- | ----- | --- | --- | --------- | --- | --- | --- | ---- | --- |
|     | 𝐷𝐶𝐺@𝑘 | =   | ∑   |           |     |     |     | (3)  |     |
|     |       |     |     | 𝑙𝑜𝑔 (𝑖+1) |     |     |     |      |     |
|     |       |     | 𝑖=1 | 2         |     |     |     |      |     |

2.7.5  Mean Average Precision (MAP)
MAP  menghitung  rata-rata  dari  Average  Precision  (AP) untuk semua
query atau pengguna (Ramazanova et al., 2025). Average Precision untuk satu
query dihitung dengan:
𝑘
1
| 𝐴𝑃@𝑘 | =   |     | ∑   | 𝑃𝑟𝑒𝑐𝑖𝑠𝑖𝑜𝑛@𝑖 |     |     |     | (4)  |     |
| ---- | --- | --- | --- | ----------- | --- | --- | --- | ---- | --- |
𝑚𝑖𝑛(𝑚,𝑘)
𝑖=1
|𝑄|
|     | 𝑀𝐴𝑃@𝑘 | =   | 1 ∑ | 𝐴𝑃@𝑘 |     |     |     | (5)  |     |
| --- | ----- | --- | --- | ---- | --- | --- | --- | ---- | --- |
|     |       |     | |𝑄| |      | 𝑞   |     |     |      |     |
𝑞=1
2.7.6  Root Mean Square Error (RMSE)
RMSE mengukur rata-rata kesalahan kuadrat antara skor relevansi yang
diprediksi oleh model dengan skor relevansi yang sebenarnya (Ramazanova et al.,
2025). RMSE memberikan gambaran tentang seberapa jauh prediksi model dari

12
nilai aktual. Semakin kecil nilai RMSE, semakin baik performa model. Rumus
RMSE adalah sebagai berikut:
𝑁
|        | 1      | 2    |
| ------ | ------ | ---- |
| 𝑅𝑀𝑆𝐸 = | ∑ (ŷ − | 𝑦)   |
|        | 𝑁 𝑖    | 𝑖    |
𝑖=1
2.7.7  Studi Ablasi
Studi ablasi dilakukan untuk memahami kontribusi dari setiap komponen
utama dalam model terhadap performa keseluruhan sistem rekomendasi (Chetoui
&  El  Bachari,  2025).  Dalam  penelitian  ini,  studi  ablasi  dilakukan  dengan
membuat beberapa varian model yang menghilangkan komponen tertentu.

BAB 3. METODOLOGI PENELITIAN
3.1 Jenis Penelitian
Jenis penelitian yang akan dilakukan adalah penelitian kuantitatif. Fokus
utama dari penelitian ini adalah pada perancangan dan implementasi sebuah
sistem cerdas untuk menyelesaikan permasalahan nyata dalam perencanaan studi
mahasiswa. Pendekatan penelitian bersifat kuantitatif-eksperimental, dimana
fokus eksperimennya adalah menguji performa dan akurasi model GNN dalam
memberikan rekomendasi mata kuliah pilihan. Variabel yang diuji adalah
kapabilitas model GNN untuk mempelajari pola dari Knowledge Graph (KG) dan
memprediksi skor relevansi (Link Regression). Model yang dikembangkan akan
diimplementasikan menjadi sebuah API dan diintegrasikan dengan aplikasi mobile
untuk diuji kinerjanya. Validasi utama pada model dijelaskan melalui skema
pembagian data training dan testing.
3.2 Objek Penelitian
Objek penelitian ini adalah Knowledge Graph (KG) yang dikonstruksi dari
data akademik riwayat nilai dan aturan kurikulum Mahasiswa Fakultas Ilmu
Komputer Universitas Jember. KG yang dihasilkan ini berfungsi sebagai
representasi data terstruktur untuk mempelajari dan memprediksi skor relevansi
mata kuliah pilihan menggunakan Graph Neural Network (GNN). Proses
konstruksi KG melibatkan transformasi data multi-sumber menjadi struktur graf
yang terdiri dari entitas (node) dan hubungan (edge).
3.3 Tempat dan Waktu Penelitian
Penelitian berlangsung di Fakultas Ilmu Komputer, Universitas Jember.
Durasi penelitian berlangsung selama 3 bulan, dimulai pada Januari hingga Maret
2026.
13

14
3.4 Tahapan Penelitian
Gambar 3.1 Tahapan Penelitian
3.4.1 Studi Literatur
Tahapan studi literatur bertujuan untuk membangun landasan teoritis yang
kuat dan memahami posisi penelitian terkini terkait sistem rekomendasi mata
kuliah, Knowledge Graph (KG), dan Graph Neural Network (GNN) dalam
konteks pendidikan. Pencarian literatur dilakukan melalui basis data akademik
bereputasi dengan menggunakan kata kunci yang relevan. Literatur yang
diperoleh akan dianalisis secara untuk mengidentifikasi konsep fundamental,
metodologi yang pernah diterapkan beserta kelebihan dan kekurangannya, serta
celah penelitian (research gap).
3.4.2 Pengumpulan Data
Tahapan ini dilakukan untuk mendapatkan seluruh data mentah yang
diperlukan pada proses pembangunan Knowledge Graph dan pelatihan model
GNN. Proses pengumpulan dimulai dari data mata kuliah dan riwayat akademik
mahasiswa yang diperoleh dari pihak akademik Fakultas Ilmu Komputer
Universitas Jember setelah mendapatkan izin resmi. Data mata kuliah mencakup
daftar seluruh mata kuliah (kode, nama, SKS, jenis), deskripsi/silabus, dan

15
struktur prasyarat antar mata kuliah. Sedangkan data riwayat akademik mencakup
data transkrip nilai mahasiswa dari angkatan 2020-2022. Untuk menjaga privasi
dan memenuhi etika penelitian, seluruh data akan dianonimkan sepenuhnya
(mengganti NIM asli dengan ID acak) sebelum digunakan. Selain data kuantitatif
berupa kurikulum dan transkrip nilai, pengumpulan data kualitatif juga dilakukan
melalui wawancara mendalam dengan Wakil Dekan 1 Fakultas Ilmu Komputer.
Wawancara ini bertujuan untuk memvalidasi urgensi masalah pengambilan mata
kuliah pilihan, mengkonfirmasi penerapan aturan prasyarat kurikulum di
lapangan, serta menentukan variabel tambahan seperti minat mahasiswa agar hasil
rekomendasi selaras dengan pedoman learning path fakultas.
3.4.3 Pra-pemrosesan dan Konstruksi Knowledge Graph (KG)
a. Pra-pemrosesan Data
Pada tahapan ini dilakukan pembersihan, transformasi, dan integrasi data
agar siap digunakan dalam struktur Knowledge Graph. Pembersihan data
dilakukan untuk menangani inkonsistensi, data yang hilang (missing values), atau
kesalahan format pada data kurikulum dan transkrip. Transformasi data adalah
langkah krusial di mana label relevansi target untuk training model didefinisikan.
Nilai huruf historis dari transkrip mahasiswa atau data KRS historis akan diubah
menjadi nilai numerik. Nilai numerik ini dijadikan skor relevansi target yang
mengindikasikan tingkat penguasaan akademik dan keberhasilan mahasiswa pada
mata kuliah yang telah diambil. Nilai tinggi dijustifikasi sebagai bukti
keberhasilan belajar yang kuat dan relevan karena model bertujuan memprediksi
mata kuliah di mana mahasiswa memiliki potensi terbesar untuk berhasil di masa
depan, bukan hanya mata kuliah yang diminati tanpa kemampuan. Bobot numerik
secara eksplisit berfungsi sebagai skor relevansi target untuk tugas Link
Regression dan merepresentasikan performa akademik mahasiswa pada mata
kuliah yang telah diambil. Data lain yaitu data mata kuliah akan diintegrasikan
berdasarkan kunci unik seperti ID mahasiswa dan kode mata kuliah.
b. Konstruksi Knowledge Graph
Tahapan konstruksi KG akan menentukan skema final dari dataset yang
digunakan. Data yang sudah bersih dari tahap pra-pemrosesan akan diekstrak

16
menjadi entitas yang spesifik dan hubungan antar entitas sesuai dengan skema
yang telah ditentukan. Knowledge Graph yang dibangun memodelkan entitas
mahasiswa dan mata kuliah, serta relasi nilai dan prasyarat. Berikut contoh
representasi Knowledge Graph:
1. [Mahasiswa_01, mengambil_nilai_4.0, Pemrograman_Dasar]:
Merepresentasikan riwayat akademik (fakta historis).
2. [Pemrograman_Dasar, merupakan_prasyarat_dari, Pemrograman_Lanjut]:
Merepresentasikan aturan kurikulum (pengetahuan eksternal).
3. [Pemrograman_Lanjut, berkaitan_dengan, Pengembangan_Aplikasi]:
Merepresentasikan keterhubungan topik antar mata kuliah dalam
kurikulum.
Berdasarkan validasi wawancara dengan Wakil Dekan 1, implementasi
aturan prasyarat mata kuliah di lapangan saat ini tidak selalu bersifat kaku (Hard
Constraint), melainkan lebih fleksibel (Soft Constraint) sehingga banyak
mahasiswa yang dapat mengambil topik skripsi meski belum lulus mata kuliah
yang berkaitan. Oleh karena itu, pendekatan Knowledge Graph terbukti relevan
dan tidak menyalahi aturan karena sistem tidak akan memblokir relasi secara
mutlak, melainkan mengandalkan perhitungan GNN untuk memberikan bobot
prioritas tertinggi pada mata kuliah yang prasyaratnya telah dipenuhi. Untuk
memastikan struktur topologi relasional tetap terjaga selama pemrosesan, data
akan dikelola dalam format basis data graf, agar keutuhan representasi Knowledge
Graph tetap terjamin saat diproses oleh GNN.
Gambar 3.2 Skema konstruksi KG
3.4.4 Implementasi Model GNN
Knowledge Graph yang telah dibangun akan digunakan sebagai input
untuk melatih model GNN. Tujuannya adalah mempelajari representasi vektor

17
(node embeddings) yang kaya makna untuk setiap entitas (mahasiswa dan mata
kuliah) guna melakukan prediksi relevansi sebagai dasar rekomendasi. Proses
implementasi tersebut memiliki beberapa tahapan sebagai berikut:
a. Mempersiapkan Arsitektur GNN
Jenis GNN yang akan digunakan adalah Graph Attention Network (GAT).
Jenis ini dipilih karena kemampuannya menangani graf heterogen dengan
memberikan bobot (atensi) yang berbeda pada node tetangga berdasarkan
relevansinya. Model akan terdiri dari dua lapisan GAT untuk menangkap
informasi hingga tetangga dua-hop (2-hop) sesuai dengan arsitektur Knowledge
Graph dengan 2 tetangga, yaitu mahasiswa dengan mata kuliah dan mata kuliah
dengan prasyaratnya.
Gambar 3.3 Arsitektur GNN
Sebelum graf dapat diproses oleh layer GNN, entitas pada Knowledge
Graph tidak diproses secara langsung dalam bentuk mentahnya, melainkan harus
melalui tahap vektorisasi atau inisialisasi embedding. Proses ini mengubah entitas
diskrit menjadi representasi vektor numerik berdimensi tetap yang dapat dihitung
oleh mesin. Pada arsitektur model ini, entitas mata kuliah memiliki fitur awal
yang diekstraksi dari SKS dan CPL, yang kemudian dilewatkan pada linear
projection layer untuk membentuk vektor fitur berdimensi seragam. Di sisi lain,
entitas mahasiswa yang pada awalnya tidak memiliki fitur atribut eksplisit,
diinisialisasi menggunakan matriks representasi vektor acak. Vektor-vektor
embedding awal inilah yang kemudian menjadi input pada lapisan GAT untuk
diperbarui maknanya secara iteratif melalui mekanisme message passing antar
tetangga graf.
Tugas rekomendasi akan diformulasikan sebagai Link Regression.
Tujuannya adalah melatih model untuk memprediksi skor relevansi antara node
mahasiswa dan node mata kuliah yang belum terhubung, berdasarkan embeddings

18
mereka. Skor yang lebih tinggi menandakan rekomendasi yang lebih kuat, dan
skor ini merupakan fungsi dari embeddings yang diperkaya oleh KRS historis
mahasiswa. KRS historis akan menyediakan skor relevansi target yang digunakan
untuk Link Regression.
b. Melatih Model GNN
Data yang telah diproses dan dimodelkan ke dalam Knowledge Graph
(KG) akan dibagi secara acak menjadi dua subset utama, yaitu data training dan
data testing. Data yang digunakan untuk pembagian ini adalah data nilai yang ada
pada tautan (hubungan mahasiswa-mata kuliah), yang dianggap sebagai indikator
tautan positif. Data training digunakan untuk melatih model GNN dengan tugas
Link Regression. Selama pelatihan, setiap lapisan GAT akan menerima pesan atau
embedding dari tetangganya, memberikan bobot, mengagregasi, dan memperbarui
embedding-nya sendiri. Optimasi model dilakukan dengan menghitung loss antara
skor relevansi yang diprediksi model (ŷ) dan skor relevansi target (𝑦)
𝑖 𝑖
menggunakan Mean Squared Error (MSE). Adam Optimizer digunakan untuk
memperbarui parameter GNN guna meminimalkan loss tersebut.
Gambar 3.4 Pelatihan model GNN
Pelatihan dilakukan hingga mendapatkan hasil dengan loss yang tidak
turun signifikan, menghasilkan node embeddings akhir untuk semua entitas
mahasiswa dan mata kuliah.
c. Optimasi Hyperparameter dan Tuning Model
Optimasi hyperparameter dilakukan untuk mengoptimalkan kinerja model
dan memastikan pembelajaran yang efisien. Proses ini melibatkan penentuan
konfigurasi parameter optimal yang digunakan selama pelatihan model. Pada
dimensi embedding diukur kapasitas model dalam mengodekan informasi tanpa
memperkenalkan noise yang berlebihan yang dapat menyebabkan overfitting.
Meskipun model dirancang dengan dua lapisan GAT, pengujian akan dilakukan

19
untuk memvalidasi bahwa h=2 adalah jumlah hop yang optimal, karena nilai h
yang terlalu besar dapat meningkatkan noise dan berdampak negatif pada kinerja.
Parameter lain yang diuji adalah jumlah neighbor sampling (mengidentifikasi
jumlah tetangga optimal yang diagregasi) dan dropout rate (memvalidasi
efektivitas dropout dalam mencegah overfitting dan meningkatkan generalisasi
model). Nilai parameter ditentukan menggunakan Grid Search.
d. Melakukan Prediksi untuk Rekomendasi
Menghitung similarity score dilakukan untuk memastikan sistem
rekomendasi akurat. Mahasiswa dengan embedding u akan dihitung skor relevansi
dengan setiap mata kuliah c yang belum diambil menggunakan Dot Product
antara eu dan ec (Hua et al., 2025). Skor relevansi yang diprediksi dalam penelitian
ini merepresentasikan potensi keberhasilan akademik dan kewajaran pengambilan
mata kuliah berdasarkan struktur kurikulum. Sistem akan memanfaatkan input
variabel minat eksplisit yang dimasukkan oleh mahasiswa pada antarmuka
aplikasi. Input minat ini akan dicocokkan dengan struktur learning path yang
terpetakan dalam Knowledge Graph untuk memastikan relevansi rekomendasi
dengan tujuan karir mahasiswa. Selanjutnya, model GAT akan memproses data
tersebut untuk menangkap preferensi implisit tambahan melalui mekanisme
message passing. Jika seorang mahasiswa mendapatkan nilai A pada mata kuliah
prasyarat, sistem akan menganggap relevansi tinggi secara kompetensi. Namun,
jika pola data historis dari mahasiswa lain yang serupa menunjukkan
kecenderungan untuk tidak melanjutkan ke mata kuliah lanjutan tersebut, model
akan menyesuaikan skor relevansi melalui bobot atensi yang dipelajari dari
tetangga strukturalnya. Hasilnya akan diurutkan berdasarkan skor tertinggi untuk
memberikan rekomendasi yang paling akurat.
𝑛
𝑑𝑜𝑡 𝑝𝑟𝑜𝑑𝑢𝑐𝑡 = ∑ 𝑢𝑐
𝑖 𝑖
𝑖=1
3.4.5 Evaluasi Model
Tahap evaluasi model dilakukan untuk mengukur performa model dalam
memberikan rekomendasi yang akurat dan relevan. Proses ini adalah inti dari
aspek eksperimental penelitian. Evaluasi dilakukan menggunakan data testing.

20
Model GNN yang sudah dilatih digunakan untuk memprediksi skor relevansi
untuk semua pasangan dalam data testing. Hasil prediksi ini dibandingkan dengan
data sebenarnya di data training menggunakan matrik evaluasi yang sesuai. Hasil
matrik dianalisis untuk memahami kekuatan dan kelemahan model. Matrik
evaluasi yang digunakan meliputi precision, recall, F1-score, Normalized
Discounted Cumulative Gain (NDCG), Mean Average Precision (MAP), dan Root
Mean Square Error (RMSE). Validasi model juga dilakukan menggunakan studi
ablasi untuk membuktikan efektivitas setiap modul dalam arsitektur GNN dan
teknik optimasi.
3.4.6 Pengembangan Sistem
Sistem rekomendasi mata kuliah pilihan yang dibangun menggunakan
Knowledge Graph dan GNN diimplementasikan ke dalam aplikasi berbasis
mobile menggunakan framework flutter dan flask python.
Gambar 3.6 Diagram arsitektur sistem
Flutter digunakan untuk mengembangkan tampilan dari aplikasi mobile
sebagaimana pada Lampiran 1. Flask python digunakan untuk implementasi
model yang telah dibuat kemudian akan di-deploy dan menjadi API untuk aplikasi
mobile.

BAB 4. HASIL DAN PEMBAHASAN
4.1 Pengumpulan dan Pra-pemrosesan Data
Tahap pengumpulan data dari pihak Fakultas Ilmu Komputer Universitas
Jember pada dasarnya menghasilkan dua dataset mentah utama, yaitu dokumen
resmi kurikulum program studi dan data riwayat akademik berupa transkrip nilai
mahasiswa angkatan 2020–2022. Karena pihak fakultas tidak memiliki tabel
prasyarat yang terpusat, maka dilakukan proses ekstraksi data secara mandiri dari
dokumen kurikulum untuk membangun struktur relasi mata kuliah beserta
prasyaratnya. Ekstraksi relasi sekuensial ini dilakukan secara deduktif dengan
menyilangkan matriks Capaian Pembelajaran Lulusan (CPL) dan rumpun Bahan
Kajian dengan daftar sebaran mata kuliah di tiap semester.
Draf struktur prasyarat dan learning path (kategori minat) yang telah
dibentuk kemudian divalidasi secara langsung kepada Koordinator Program Studi
(Korprodi) masing-masing program studi. Validasi ini memberikan justifikasi
akademik bahwa rancangan aturan pada Knowledge Graph yang akan dibangun
100% selaras dengan kompetensi dan pedoman kurikulum fakultas. Selain itu,
berdasarkan hasil wawancara kualitatif dengan Wakil Dekan 1, sistem disarankan
mengakomodasi peminatan mahasiswa yang sejalan dengan learning path
kurikulum. Oleh karena itu, pada tahap pra-pemrosesan dilakukan penambahan
atribut ‘kategori_minat’ pada data mata kuliah pilihan berdasarkan kurikulum
masing-masing program studi. Data mata kuliah dan sebaran minat dapat dilihat
pada Tabel 4.1.
Tabel 4.1 Data mata kuliah
kategori_
course_id nama_matkul sks jenis semester prodi
minat
MKU900 Bahasa 2 Wajib 1 Teknologi Umum
7 Indonesia Informasi
KST1101 Jaringan 3 Wajib 1 Teknologi Umum
Komputer Informasi
KST1102 Sistem Basis 3 Wajib 1 Teknologi Umum
21

22
|          | Data         |             | Informasi      |             |
| -------- | ------------ | ----------- | -------------- | ----------- |
| KST1103  | Arsitektur   | 2  Wajib    | 1  Teknologi   | Umum        |
|          | Komputer     |             | Informasi      |             |
| KST1104  | Matematika   | 3  Wajib    | 1  Teknologi   | Umum        |
|          | Dasar        |             | Informasi      |             |
| …        | …            | …  …        | …  …           | …           |
| KFU1523  | Graf         | 3  Pilihan  |   Informatika  | Kecerdasan  |
|          | Pengetahuan  |             |                | Buatan      |

Pengelompokan atribut kategori_minat pada mata kuliah pilihan (seperti
pada  Gambar  4.1)  tidak  dirancang  secara  acak,  melainkan  diekstraksi
menggunakan  pendekatan  deduktif  dari  dokumen  resmi  kurikulum  fakultas.
Untuk Program Studi Sistem Informasi, kategori minat dipetakan secara langsung
berdasarkan rumpun peminatan yang tersedia. Sementara itu, untuk Program Studi
Teknologi Informasi dan Informatika, pemetaan dilakukan dengan menyilangkan
matriks Capaian Pembelajaran Lulusan (CPL) dengan Profil Lulusan. Langkah ini
telah divalidasi oleh Koordinator Program Studi terkait untuk memastikan bahwa
label  minat  yang  ada  pada  Knowledge  Graph  100%  merepresentasikan  visi
kompetensi lulusan program studi.

23
Gambar 4.1 Distribusi mata kuliah pilihan berdasarkan kategori minat/learning path
Hasil pra-pemrosesan menunjukkan terdapat 691 entitas mahasiswa unik
dari total 698 data mahasiswa dan 187 entitas mata kuliah. Selisih hasil jumlah
mahasiswa  dikarenakan  pada  data  awal  terdapat  beberapa  mahasiswa  yang
memiliki  transkrip kosong sehingga tidak dimasukkan ke dalam dataset. Fitur
node  untuk  mata  kuliah  dan  relasinya  diekstraksi  dari  bobot  dan  Capaian
Pembelajaran  Lulusan  (CPL),  sementara  fitur  mahasiswa  diinisialisasi
menggunakan random embedding yang dilatih. Hasil ini dapat dilihat pada Tabel
4.2 dan 4.3.
Tabel 4.2 Data prasyarat mata kuliah
|     | course_id  |     | prerequisite_id  |     |
| --- | ---------- | --- | ---------------- | --- |
|     | KSU1207    |     | KSU1101          |     |
|     | KSU1207    |     | KSF1101          |     |
|     | KSF1205    |     | KSF1102          |     |
|     | KSF1206    |     | KSU1205          |     |
|     | KSF1206    |     | KSU1107          |     |
|     | …          |     | …                |     |
|     | KTU1602    |     | KST1407          |     |

Tabel 4.3 Data transkrip mahasiswa angkatan 2020-2022
| student_id    | course_id  | semester  | nilai_huruf  | nilai_numerik  |
| ------------- | ---------- | --------- | ------------ | -------------- |
| 202410101001  | KST1409    | 1         | A            | 4              |
| 202410101001  | KST1104    | 1         | A            | 4              |
| 202410101001  | MKU9001-5  | 1         | A            | 4              |
| 202410101001  | UNU9008    | 1         | A            | 4              |
| 202410101001  | MKI9002    | 1         | B            | 3              |
| …             | …          | …         | …            | …              |
| 222410103095  | KTU101     |           | E            | 0              |

24
Gambar 4.2 Distribusi Label Nilai pada Dataset Transkrip Akademik
Pada tahap pra-pemrosesan ini juga dilakukan analisis terhadap distribusi
label nilai historis dari transkrip mahasiswa. Berdasarkan visualisasi pada Gambar
4.2, terlihat jelas bahwa data bersifat tidak seimbang (imbalanced). Mayoritas
data, yaitu sebesar 86.2% (26.898 relasi), berada pada kategori nilai Sangat Baik
(A dan AB), sementara kategori Cukup/Kurang hanya merepresentasikan 2.3%
dari keseluruhan data. Ketidakseimbangan ini merupakan cerminan riil dari
performa akademik mahasiswa yang cenderung lulus dengan nilai memuaskan
pada mata kuliah di semester-semester awal, yang nantinya akan mempengaruhi
kecenderungan bias prediksi model pada tahap evaluasi.
4.2 Konstruksi Knowledge Graph untuk Data Akademik
Data tabular yang telah dibersihkan kemudian dikonstruksi menjadi
Heterogeneous Knowledge Graph menggunakan library PyTorch Geometric. Graf
ini mendefinisikan dua node (mahasiswa dan mata kuliah) serta dua jenis edge
utama, yaitu:
4.2.1 Relasi Akademik Historis
Relasi ini merupakan hubungan antara dua node yaitu mahasiswa dan mata
kuliah yang telah diambil dan direpresentasikan dengan hubungan ‘student’,
‘takes’, ‘course’. Relasi ini memiliki atribut bobot berupa ‘nilai_numerik’ dengan
skala 0.0–4.0.

25
4.2.2 Relasi Aturan Kurikulum
Relasi ini merupakan hubungan antara node mata kuliah dengan node mata
kuliah lainnya yang menjadi lanjutan sebagai representasi sekuensial kurikulum.
Hubungan ini digambarkan dengan ‘course’, ‘prerequisite_of’, ‘course’.
Gambar 4.3 Visualisasi konstruksi Knowledge Graph untuk satu mahasiswa
Gambar 4.3 menunjukkan terdapat penyesuaian dimensi otomatis oleh
model dengan menjadikan mata kuliah yang tidak sesuai kurikulum saat ini
menjadi ‘nan’. Model juga menyesuaikan node mata kuliah menjadi 206 node
untuk menampung padding dari beberapa mata kuliah yang tidak sesuai dengan
kurikulum terbaru. Total edge interaksi mahasiswa dengan mata kuliah yang
terbentuk adalah 34.332 relasi. Perancangan Knowledge Graph untuk data
akademik terbukti berhasil memodelkan struktur akademik secara holistik.
Berbeda dengan sistem berbasis aturan kaku (rule-based), arsitektur graf ini
mampu mengakomodasi implementasi aturan prasyarat di fakultas yang bersifat
Soft Constraint (berdasarkan validasi dengan Wakil Dekan 1). Relasi
‘prerequisite_of’ bertindak sebagai jalur pengetahuan tanpa memblokir

26
mahasiswa secara mutlak, sehingga rekomendasi tetap dapat diproses meski ada
ketidakteraturan pada riwayat historis mahasiswa.
4.3 Implementasi dan Pelatihan Model GNN
Pelatihan model dilakukan menggunakan arsitektur Graph Attention
Network (GAT) sebanyak 2 layer untuk menangkap dependensi 2-hop (mahasiswa
→ mata kuliah → prasyarat mata kuliah). Dari total relasi historis, data dibagi
menjadi 27.465 train edges (80%) dan 6.867 test edges (20%). Tugas prediksi
diformulasikan sebagai Link Regression menggunakan Dot Product, dioptimasi
menggunakan Adam Optimizer dan Mean Squared Error (MSE) Loss. Hasil
pelatihan selama 100 epoch menunjukkan model berhasil mencapai konvergensi
yang sangat baik, di mana nilai MSE Loss turun secara signifikan dari 13.9869
pada epoch pertama menjadi 0.2875 pada epoch ke-100. Hasil pelatihan model ini
dapat dilihat pada Gambar 4.4 berikut.
Gambar 4.4 Kurva penurunan MSE Loss selama pelatihan GAT
Arsitektur Graph Attention Network (GAT) sukses mengeksekusi tugas
rekomendasi berbasis link regression. Melalui mekanisme message passing dalam
dua hop/layer, GAT tidak hanya sekedar merekomendasikan mata kuliah yang
populer, melainkan mengevaluasi bobot dari fondasi (riwayat) nilai mahasiswa.
GAT terbukti mampu mempelajari preferensi secara implisit meskipun input
awalnya hanya berupa transkrip numerik.

27
4.3.1 Hasil Optimasi Hyperparameter
Optimasi hyperparameter digunakan untuk memastikan model belajar
dengan efisien tanpa mengalami overfitting atau over-smoothing. Optimasi ini
dilakukan menggunakan metode Grid Search. Pengujian mengevaluasi variasi
kapasitas encoding (hidden_channels), dimensi embedding (out_channels),
kedalaman hop (num_layers), regularisasi (dropout), dan jumlah sampel tetangga
(num_neighbors). Berdasarkan evaluasi Root Mean Square Error (RMSE), model
mencapai performa paling optimal (RMSE terendah sebesar 0.557) pada
konfigurasi: hidden_channels = 64, out_channels = 8, num_layers = 2, dan
dropout = 0.0.
Gambar 4.5 Analisis Optimasi Hyperparameter
Analisis pada visualisasi boxplot menunjukkan beberapa temuan kritis
pada arsitektur graf:
a. Kedalaman Layer (Hop)
Penggunaan 2 layer sangat stabil dan optimal. Hal ini
membuktikan hipotesis bahwa arsitektur 2-hop sudah cukup untuk

28
menangkap relasi (Mahasiswa → Mata Kuliah → Prasyarat Mata Kuliah).
Sebaliknya, penggunaan 3 layer justru meningkatkan RMSE secara drastis
(di atas 1.4) karena memicu masalah over-smoothing, di mana model
mencampuradukkan terlalu banyak informasi yang tidak relevan dari node
yang jauh.
b. Efek Regularisasi (Dropout)
Model berkinerja paling baik dengan dropout 0.0. Penggunaan
dropout 0.3 atau 0.5 justru menurunkan akurasi, yang mengindikasikan
bahwa setiap edge (jalur prasyarat) pada Knowledge Graph kurikulum
bersifat krusial, sehingga membuang bobot secara acak akan merusak
pemahaman struktural sekuensial model.
c. Neighbor Sampling
Perubahan batas maksimal tetangga (5, 10, 20) tidak memberikan
perbedaan hasil yang signifikan (RMSE statis di angka 0.557 pada
konfigurasi terbaik). Hal ini mengonfirmasi bahwa rata-rata mata kuliah
hanya memiliki 1 hingga 3 prasyarat terdekat (seperti terlihat pada Tabel
4.2), sehingga batasan 5 tetangga sudah lebih dari cukup untuk menangkap
struktur utuh tanpa perlu komputasi berlebih.
4.4 Analisis Hasil Evaluasi Model
Evaluasi performa model pada test set dilakukan menggunakan enam
metrik untuk menilai kualitas regresi, klasifikasi rekomendasi, dan ranking. Hasil
eksperimen dapat dilihat pada Gambar 4.6 yang menunjukkan capaian metrik
RMSE (0.5487), Precision (0.9494), Recall (0.9981), F1-Score (0.9732), MAP
(0.9715), dan NDCG (0.9939). Angka evaluasi yang sangat tinggi (di atas 95%)
disebabkan oleh karakteristik dataset transkrip nilai riil yang sangat tidak
seimbang (imbalanced). Berdasarkan distribusi data, mayoritas nilai mahasiswa
berada pada rentang aman atau memuaskan (3.0 hingga 4.0 atau B hingga A).
Model secara agresif belajar dari bias positif ini sehingga presisi prediksi
kelulusan mata kuliah menjadi sangat tinggi.

29
Gambar 4.6 Hasil evaluasi metrik performa model pada test set
Untuk memvalidasi bias prediksi akibat ketidakseimbangan data latih
tersebut, dilakukan pengujian lebih lanjut menggunakan Confusion Matrix seperti
yang ditunjukkan pada Gambar 4.7 di bawah. Hasil evaluasi membuktikan bahwa
tingginya nilai metrik didorong oleh kemampuan model yang sangat presisi
(mencapai akurasi 97.9%) dalam mengenali kelas mayoritas, yaitu kelas Sangat
Baik (A/AB). Sebaliknya, model memiliki kecenderungan untuk menebak secara
aman (safe prediction) pada rentang nilai tinggi, sehingga evaluasi menggunakan
skenario khusus diperlukan untuk memastikan bahwa model benar-benar
mempelajari struktur graf dan bukan sekadar menghafal bias kelas.
Gambar 4.7 Confusion Matrix Prediksi Model GAT

30
4.4.1 Evaluasi Skenario Data Leakage
Sesuai dengan batasan sistem di mana fitur rekomendasi ditujukan bagi
mahasiswa yang minimal telah menempuh semester 5, maka dilakukan pengujian
spesifik menggunakan inductive evaluation. Pengujian ini dirancang untuk
menjawab potensi kebocoran data (transductive data leakage) yang sering terjadi
pada evaluasi Graph Neural Network jika menggunakan pembagian relasi secara
acak. Pada skenario pengujian ini, dilakukan penghapusan 10% data mahasiswa
dan seluruh edge yang dimiliki dari data uji. Kemudian model dilatih dengan 90%
data mahasiswa. Saat evaluasi, edge 10% mahasiswa di-inject kembali ke graf
(sebagai konteks embedding) lalu model memprediksi nilai mereka. Hasil evaluasi
sebagaimana pada Gambar 4.8 menunjukkan bahwa model tetap mampu
memprediksi masa depan akademik mahasiswa dengan tingkat error yang rendah,
dibuktikan dengan capaian nilai RMSE sebesar 0.4695. Hal ini memvalidasi
secara empiris bahwa model GAT tidak mengalami kebocoran data dari masa
depan ke masa lalu, dan tidak sekedar menghafal ID mahasiswa (overfitting).
Gambar 4.8 Hasil Evaluasi Skenario Data Leakage
4.5 Analisis Hasil Studi Ablasi
Studi ablasi dilakukan untuk memvalidasi kontribusi mekanisme attention
pada model. Eksperimen dilakukan dengan melatih graf yang sama menggunakan
GraphSAGE standar tanpa mekanisme pemberian bobot self-attention, lalu
membandingkannya dengan GAT.

31
Gambar 4.9 Hasil perbandingan GraphSAGE dan GAT
Berdasarkan Gambar 4.9, hasil ablasi menunjukkan bahwa GAT
mengungguli GraphSAGE dalam memprediksi link regression. Hal ini
membuktikan bahwa kemampuan GAT dalam memberikan bobot atensi yang
tidak seragam dengan memprioritaskan mata kuliah yang prasyarat dasarnya telah
ditempuh dengan nilai baik sangat krusial untuk meningkatkan akurasi
rekomendasi dibandingkan algoritma agregasi graf rata-rata biasa. Keunggulan
GAT dibandingkan arsitektur GraphSAGE standar membuktikan pentingnya
mekanisme self-attention dalam jaringan akademik. Model GraphSAGE gagal
memberikan rekomendasi yang presisi karena mengagregasi seluruh node
tetangganya (baik mata kuliah dasar maupun prasyarat) dengan rata-rata yang
seragam. Sebaliknya, GAT mampu memberikan bobot atensi secara dinamis.
Misalnya, jika seorang mahasiswa mendapatkan nilai 'A' pada mata kuliah
Matematika Dasar dan Algoritma Pemrograman, GAT akan secara implisit
memberikan skor atensi yang jauh lebih besar pada jalur tersebut untuk
merekomendasikan mata kuliah lanjutan yang memiliki prasyarat logika serupa,
sehingga menghasilkan prediksi regresi (Link Regression) yang lebih akurat.

32
4.6 Implementasi Sistem Rekomendasi
Model yang telah dilatih kemudian diimplementasikan ke dalam Flask API
yang bertindak sebagai Application Layer untuk melayani permintaan dari
aplikasi berbasis mobile (Flutter). Pada tahap ini, variabel ‘Minat’ (topik
skripsi/karir) dari mahasiswa diproses sebagai filter post-processing. Model GNN
memprediksi skor relevansi untuk seluruh mata kuliah pilihan, memberikan nilai
prediksi regresi maksimum batas rasional 4.0, lalu sistem menyaring hasil tersebut
agar hanya menampilkan 8 mata kuliah teratas yang berada pada jalur/kategori
minat yang dipilih oleh mahasiswa pada interface aplikasi. Meskipun model GAT
dilatih menggunakan satu Knowledge Graph global yang memuat seluruh
populasi mahasiswa dan kurikulum, output rekomendasi yang dihasilkan oleh
sistem bersifat unik dan terpersonalisasi secara spesifik untuk masing-masing
mahasiswa. Hal ini dijamin melalui mekanisme inferensi model pada Application
Layer.
Ketika seorang mahasiswa melakukan permintaan rekomendasi melalui
aplikasi, sistem akan mengekstrak ID Mahasiswa tersebut dan hanya mengambil
satu vektor embedding milik mahasiswa bersangkutan. Model kemudian
menghitung kedekatan ruang vektor menggunakan operasi Dot Product murni
antara vektor embedding mahasiswa tersebut dengan vektor embedding mata
kuliah pilihan yang belum diambilnya. Karena setiap mahasiswa memiliki riwayat
pengambilan mata kuliah yang unik, posisi representasi vektor mereka di dalam
ruang graf akan berbeda-beda setelah proses training. Akibatnya, skor probabilitas
relevansi yang dihasilkan oleh Dot Product akan menghasilkan urutan
rekomendasi mata kuliah yang berbeda untuk setiap mahasiswa, menjadikannya
sistem yang sepenuhnya adaptif terhadap kemampuan individu. Proses pemilihan
minat dan pemberian rekomendasi didapatkan saat mahasiswa melakukan KRS
sebagaimana dapat dilihat pada Gambar 4.10 berikut.

33
Gambar 4.10 Antarmuka aplikasi mobile implementasi sistem rekomendasi
Penyertaan struktur prasyarat ke dalam graf memberikan kontribusi berupa
efek pengereman serta percepatan yang logis dan sekuensial. Karena graf
dimodelkan berdasarkan prasyarat terdekat (immediate prerequisite) sesuai Bahan
Kajian dan CPL, algoritma GNN melakukan penelusuran mundur ke semester
awal. Mahasiswa yang tidak memiliki fondasi baik di mata kuliah prasyarat
(misalnya Algoritma Pemrograman), akan mendapatkan skor prediksi regresi
yang rendah untuk mata kuliah tingkat lanjutnya, yang pada gilirannya
mendorong mahasiswa untuk tetap berada pada learning path yang realistis dan
mencegah keterlambatan studi saat mengambil topik skripsi.
4.6.1 Skenario Pengujian Rekomendasi
Untuk menguji validitas logika rekomendasi di lapangan, dilakukan
pengujian skenario berbasis user-case pada mahasiswa yang akan merencanakan
studi. Skenario Mahasiswa Demo dengan NIM 232410102068 dari Program Studi

34
Teknologi Informasi telah mengambil mata kuliah wajib dengan rata-rata nilai
tinggi untuk mata kuliah yang berhubungan dengan data dan analitik. Melalui
antarmuka aplikasi, mahasiswa ini memilih kategori minat 'Data dan Analitik'.
Hasilnya, Sistem GNN pertama-tama melakukan prediksi skor untuk seluruh mata
kuliah yang belum diambil berdasarkan riwayat nilai historis. Karena nilai
fundamental data mahasiswa tersebut sangat kuat, model memberikan prediksi
bobot regresi yang tinggi pada jalur tersebut. Selanjutnya, algoritma filtering
aplikasi mengeliminasi mata kuliah di luar jalur minat yang dipilih. Sebagai hasil
akhir, sistem merekomendasikan mata kuliah Data Warehousing (KTU114)
dengan tingkat kepercayaan tinggi, karena mata kuliah ini berada tepat dalam
learning path data dan analitik. Hal ini memvalidasi bahwa sistem tidak
menyimpang dari struktur pengetahuan kurikulum.

BAB 5. KESIMPULAN
5.1 Kesimpulan
Berdasarkan hasil penelitian, perancangan sistem, dan evaluasi pengujian
yang telah dilakukan, maka dapat ditarik kesimpulan sebagai berikut:
1. Knowledge Graph (KG) terbukti berhasil mereduksi kompleksitas data
akademik dengan memodelkannya menjadi jaringan heterogen
(Heterogeneous Graph).
2. Implementasi arsitektur Graph Attention Network (GAT) terbukti sangat
efektif dalam mengeksekusi tugas Link Regression untuk sistem rekomendasi.
Model beroperasi secara optimal pada kedalaman 2-hop dengan hasil evaluasi
metrik yang sangat tinggi, yaitu RMSE (0.5487), Precision (0.9494), MAP
(0.9715), dan NDCG (0.9939). Mekanisme self-attention pada GAT juga
terbukti secara signifikan mengungguli arsitektur GraphSAGE konvensional
karena kemampuannya memberikan bobot atensi secara spesifik pada riwayat
mata kuliah yang paling relevan.
3. Penyertaan struktur prasyarat ke dalam Knowledge Graph terbukti
memberikan kontribusi yang krusial dalam menjaga akurasi jalur
pembelajaran (learning path). Hal ini mencegah rekomendasi yang
menyimpang dari struktur pengetahuan kurikulum dan mendorong mahasiswa
untuk memilih topik yang sesuai dengan kapasitas akademik mereka.
5.2 Saran
Berdasarkan keterbatasan pada penelitian yang telah dilakukan, terdapat
beberapa saran yang dapat digunakan untuk pengembangan penelitian
selanjutnya, yaitu integrasi data non-akademik seperti jadwal kuliah dan kuota per
kelas, penanganan imbalanced data karena banyaknya data dengan nilai tinggi
(A/AB/B), dan integrasi dengan sistem akademik universitas yang sudah ada
sehingga penggunaan bisa lebih optimal.
35

36
DAFTAR PUSTAKA
Atalla, S., Daradkeh, M., Gawanmeh, A., Khalil, H., Mansoor, W., Miniaoui, S.,
& Himeur, Y. (2023). An Intelligent Recommendation System for
Automating Academic Advising Based on Curriculum Analysis and
Performance Modeling. Mathematics, 11(5), 1098.
https://doi.org/10.3390/math11051098
Baek, C., & Doleck, T. (2023). Educational Data Mining versus Learning
Analytics: A Review of Publications From 2015 to 2019. Interactive
Learning Environments, 31(6), 3828–3850.
https://doi.org/10.1080/10494820.2021.1943689
Beutling, N., & Spahic-Bogdanovic, M. (2024). Personalised Course
Recommender: Linking Learning Objectives and Career Goals through
Competencies. Proceedings of the AAAI Symposium Series, 3(1), 72–81.
https://doi.org/10.1609/aaaiss.v3i1.31185
Bohra, S., & Bartere, M. M. (2022). Hybrid Recommendation Algorithm for
Personalization of Customer Experience. 2022 IEEE 7th International
Conference for Convergence in Technology (I2CT), 1–9.
https://doi.org/10.1109/I2CT54291.2022.9824545
Chetoui, I., Bachari E. E. (2025). Personalized Learning Recommendations Based
on Graph Neural Networks. International Journal of Electrical and
Computer Engineering (IJECE).
De Andrade, T. L., Rigo, S. J., & Barbosa, J. L. V. (2021). Active Methodology,
Educational Data Mining and Learning Analytics: A Systematic Mapping
Study. Informatics in Education. https://doi.org/10.15388/infedu.2021.09
Finkelshtein, B., Huang, X., Bronstein, M., & Ceylan, İ. İ. (2024). Cooperative
Graph Neural Networks (arXiv:2310.01267). arXiv.
https://doi.org/10.48550/arXiv.2310.01267
Gao, C., Zheng, Y., Li, N., Li, Y., Qin, Y., Piao, J., Quan, Y., Chang, J., Jin, D.,
He, X., & Li, Y. (2023). A Survey of Graph Neural Networks for
Recommender Systems: Challenges, Methods, and Directions. ACM
Transactions on Recommender Systems, 1(1), 1–51.
https://doi.org/10.1145/3568022
Gao, R. (2024). Exploring the landscape of recommendation systems: A
qualitative analysis of types, challenges, and potential solutions. Applied
and Computational Engineering, 64(1), 216–221.
https://doi.org/10.54254/2755-2721/64/20241444
Gulzar, Y., Alwan, A. A., Abdullah, R. M., Abualkishik, A. Z., & Oumrani, M.
(2023). OCA: Ordered Clustering-Based Algorithm for E-Commerce

37
Recommendation System. Sustainability, 15(4), 2947.
https://doi.org/10.3390/su15042947
Hua, Z., Yang, J., & Ji, W. (2025). Knowledge graph convolutional networks with
user preferences for course recommendation. Scientific Reports, 15(1),
30256. https://doi.org/10.1038/s41598-025-14150-5
Kharis, S. A. A., & Zili, A. H. A. (2022). Learning Analytics dan Educational
Data Mining pada Data Pendidikan. JURNAL RISET PEMBELAJARAN
MATEMATIKA SEKOLAH, 6(1), 12–20.
https://doi.org/10.21009/jrpms.061.02
Khemani, B., Patil, S., Kotecha, K., & Tanwar, S. (2024). A review of graph
neural networks: Concepts, architectures, techniques, challenges, datasets,
applications, and future directions. Journal of Big Data, 11(1), 18.
https://doi.org/10.1186/s40537-023-00876-4
Li, Y., Liang, Y., Yang, R., Qiu, J., Zhang, C., & Zhang, X. (2024). CourseKG: An
Educational Knowledge Graph Based on Course Information for Precision
Teaching. Applied Sciences, 14(7), 2710.
https://doi.org/10.3390/app14072710
Liang, F., Qian, C., Yu, W., Griffith, D., & Golmie, N. (2022). Survey of Graph
Neural Networks and Applications. Wireless Communications and Mobile
Computing, 2022(1), 9261537. https://doi.org/10.1155/2022/9261537
Lin, Q., Zhu, Y., Lu, H., Shi, K., & Niu, Z. (2021). Improving University Faculty
Evaluations via multi-view Knowledge Graph. Future Generation
Computer Systems, 117, 181–192.
https://doi.org/10.1016/j.future.2020.11.021
Molleví Bortoló, G., Álvarez Valdés, J., & Nicolas-Sans, R. (2023). Sustainable,
technological, and innovative challenges post Covid-19 in health,
economy, and education sectors. Technological Forecasting and Social
Change, 190, 122424. https://doi.org/10.1016/j.techfore.2023.122424
Murali Mohana Krishna Dandu, Vishwasrao Salunkhe, Shashwat Agrawal,
Prof.(Dr) Punit Goel, & Vikhyat Gupta. (2023). Knowledge Graphs for
Personalized Recommendations. Innovative Research Thoughts, 9(1),
450–479. https://doi.org/10.36676/irt.v9.i1.1497
Ramazanova, V., Sambetbayeva, M., Serikbayeva, S., Yerimbetova, A.,
Lamasheva, Z., Sadirmekova, Z., & Kalman, G. (2025).
Curriculum–Vacancy–Course Recommendation Model Based on
Knowledge Graphs, Sentence Transformers, and Graph Neural Networks.
Technologies, 13(8), 340. https://doi.org/10.3390/technologies13080340
Shenkoya, T., & Kim, E. (2023). Sustainability in Higher Education: Digital
Transformation of the Fourth Industrial Revolution and Its Impact on Open

38
Knowledge. Sustainability, 15(3), 2473.
https://doi.org/10.3390/su15032473
Thajchayapong, P., & Goel, A. K. (n.d.). Personalized Learning through
AI-Driven Data Pipeline.
Uta, M., Felfernig, A., Le, V.-M., Tran, T. N. T., Garber, D., Lubos, S., &
Burgstaller, T. (2024). Knowledge-based recommender systems: Overview
and research directions. Frontiers in Big Data, 7, 1304439.
https://doi.org/10.3389/fdata.2024.1304439
Veličković, P., Cucurull, G., Casanova, A., Romero, A., Liò, P., & Bengio, Y.
(2018). Graph Attention Networks (arXiv:1710.10903). arXiv.
https://doi.org/10.48550/arXiv.1710.10903
Wang, L., Du, W., & Chen, Z. (2024). Multi-Feature-Enhanced Academic Paper
Recommendation Model with Knowledge Graph. Applied Sciences,
14(12), 5022. https://doi.org/10.3390/app14125022
Zhang, S., Rao, X., Tay, Y., & Zhang, C. (2021). Knowledge Router: Learning
Disentangled Representations for Knowledge Graphs. Proceedings of the
2021 Conference of the North American Chapter of the Association for
Computational Linguistics: Human Language Technologies, 1–10.
https://doi.org/10.18653/v1/2021.naacl-main.1

39
LAMPIRAN
Lampiran 1. Mockup Aplikasi
a. Fitur Autentikasi

40
b. Menu Home dan Profile

41
c. Fitur Rencana Studi

42
d. Fitur Rekomendasi Mata Kuliah

43
e. Menu Hasil Transkrip