---
coverY: 0
---

# Bagaima Paypal Menggunakan Kafka Untuk Mengirim 1.3 Triliun Pesan/Hari

#### Kafka di PayPal

Apache Kafka adalah platform open-source untuk streaming acara terdistribusi.

PayPal mengadopsi Kafka pada tahun 2015 dan menggunakannya untuk membangun pipeline streaming data, integrasi, dan injeksi data.

Saat ini, armada Kafka di PayPal terdiri dari lebih dari 1500 broker yang mengelola 20.000 topik. Lebih dari 85 kluster diharapkan dapat mempertahankan ketersediaan 99,99%.

Selama bertahun-tahun, PayPal telah melihat pertumbuhan yang luar biasa dalam data streaming dan mereka ingin memastikan ketersediaan tinggi, toleransi kesalahan, dan kinerja optimal.

#### Penggunaan Spesifik Kafka di PayPal

Beberapa kasus penggunaan spesifik di mana PayPal menggunakan Kafka adalah sebagai berikut:

1. **Pelacakan Pihak Pertama**: Melacak interaksi pengguna dan data klik di situs web dan aplikasi seluler PayPal untuk analitik waktu nyata dan personalisasi.
2. **Metrik Kesehatan Aplikasi**: Mengumpulkan dan mengagregasi metrik kinerja dari berbagai layanan PayPal untuk memantau kesehatan sistem dan mendeteksi anomali.
3. **Sinkronisasi Basis Data**: Menyinkronkan data antara basis data utama PayPal dan basis data sekunder untuk pemulihan bencana dan ketersediaan tinggi.
4. **Agregasi Log Aplikasi**: Mengumpulkan dan memusatkan data log dari berbagai aplikasi dan layanan PayPal untuk pemecahan masalah, pemantauan, dan analisis.
5. **Pemrosesan Batch**: Memproses batch besar data transaksi pembayaran menggunakan Kafka sebagai buffer untuk memisahkan tahap injeksi dan pemrosesan data.
6. **Deteksi dan Manajemen Risiko**: Streaming data pembayaran waktu nyata melalui Kafka untuk memasok model deteksi penipuan dan penilaian risiko.
7. **Analitik dan Kepatuhan**: Menangkap dan menganalisis data transaksi keuangan secara real-time untuk pelaporan regulasi dan audit.

#### Cara PayPal Mengoperasikan Kafka

Infrastruktur PayPal tersebar di beberapa pusat data dan zona keamanan yang tersebar secara geografis. Kluster Kafka dideploy di seluruh zona ini.

Terdapat beberapa perbedaan kunci antara pusat data dan zona keamanan:

* **Pusat Data**: Fasilitas fisik yang menampung infrastruktur komputasi.
* **Zona Keamanan**: Partisi logis di dalam pusat data atau di seluruh pusat data, dibuat melalui segmentasi jaringan.

Pusat data membantu dengan isolasi dan ketersediaan, sementara zona keamanan memberikan tingkat isolasi tambahan di luar batas fisik.

Zona keamanan sering kali didefinisikan berdasarkan tingkat klasifikasi data, seperti data sangat sensitif, rahasia, atau publik.

Dalam konteks PayPal, kluster Kafka yang menangani data pembayaran sensitif mungkin ditempatkan di zona keamanan tinggi dengan akses terbatas. Kluster yang memproses data yang kurang sensitif mungkin berada di zona keamanan yang berbeda.

Namun, ada satu kesamaan:

Baik di pusat data atau zona keamanan, MirrorMaker digunakan untuk mencerminkan data di seluruh pusat data, yang membantu dengan pemulihan bencana dan komunikasi di seluruh zona keamanan.

Sebagai referensi, Kafka MirrorMaker adalah alat untuk mencerminkan data antara kluster Apache Kafka. Ini memanfaatkan kerangka kerja Kafka Connect untuk mereplikasi data, yang meningkatkan ketahanan.

#### Mengelola Kafka di Skala PayPal

Mengoperasikan Kafka dengan skala sebesar PayPal adalah tugas yang menantang. Untuk mengelola armada kluster Kafka yang terus berkembang, PayPal berfokus pada beberapa area kunci seperti:

* Manajemen Kluster
* Pemantauan dan Peringatan
* Manajemen Konfigurasi
* Peningkatan dan Otomatisasi

#### Manajemen Kluster

Manajemen kluster berkaitan dengan mengendalikan kluster Kafka dan mengurangi beban operasional. Beberapa peningkatan kunci dilakukan di area seperti:

* Layanan Konfigurasi Kafka
* ACL (Access Control Lists)
* Perpustakaan Kafka untuk PayPal
* Lingkungan QA

#### Layanan Konfigurasi Kafka

PayPal membangun layanan konfigurasi Kafka khusus untuk memudahkan klien terhubung ke kluster Kafka.

Sebelum adanya layanan konfigurasi ini, klien harus menghardcode IP broker dalam konfigurasi koneksi.

Ini menciptakan mimpi buruk pemeliharaan karena dua alasan:

1. Mengganti broker untuk peningkatan, patching, atau kegagalan disk memerlukan pembaruan pada klien. Jika satu IP broker tidak diperbarui, sering kali terjadi insiden ganda.
2. Kafka memiliki banyak konfigurasi, membuat pengembang kesulitan menemukan set konfigurasi yang sesuai. Sering kali, klien Kafka akan mengubah properti tertentu tanpa mengetahui dampaknya, yang menyebabkan masalah dukungan karena perilaku yang tidak terduga.

Layanan konfigurasi Kafka menyelesaikan masalah ini. Layanan ini memudahkan klien Kafka mengikuti konfigurasi standar, yang pada akhirnya mengurangi beban operasional dan dukungan di seluruh tim.

#### ACL (Access Control Lists)

Awalnya, aplikasi PayPal mana pun bisa terhubung ke topik Kafka yang ada. Ini menjadi risiko operasional karena platform ini mengalirkan data penting bisnis.

Untuk memastikan akses yang terkontrol ke kluster Kafka, diperkenalkan ACL.

ACL digunakan untuk mendefinisikan pengguna, grup, atau proses yang memiliki akses ke objek tertentu seperti file, direktori, aplikasi, atau sumber daya jaringan.

Dengan pengenalan ACL, aplikasi harus mengotentikasi dan mengotorisasi akses ke kluster dan topik Kafka.

Selain membuat platform lebih aman, ACL juga menyediakan catatan setiap aplikasi yang mengakses topik atau kluster tertentu.

#### Perpustakaan Kafka untuk PayPal

Untuk memastikan kluster Kafka dan klien yang terhubung ke mereka beroperasi dengan aman, serta untuk memastikan integrasi yang mudah ke berbagai kerangka kerja dan bahasa pemrograman, PayPal membangun beberapa perpustakaan penting:

* **Perpustakaan Klien Tahan Lama**: Saat klien mencoba membuat koneksi ke kluster, perpustakaan ini mendapatkan detail broker Kafka dan konfigurasi yang diperlukan untuk aplikasi produser atau konsumen.
* **Perpustakaan Pemantauan**: Perpustakaan ini mempublikasikan metrik kritis untuk aplikasi klien, memungkinkan aplikasi menetapkan peringatan dan menerima notifikasi jika ada masalah.
* **Perpustakaan Keamanan Kafka**: Perpustakaan ini menangani sertifikat dan token yang diperlukan untuk mengaktifkan otentikasi SSL bagi aplikasi yang terhubung ke kluster Kafka. Ini menghindari banyak beban seputar manajemen kunci, pembaruan sertifikat, dan rotasi kunci.

#### Platform QA

Salah satu hal terbaik yang dilakukan PayPal adalah menyiapkan platform QA yang mirip produksi untuk Kafka agar pengembang dapat menguji perubahan dengan percaya diri.

Ini adalah masalah umum di banyak organisasi di mana pengujian yang dilakukan oleh pengembang jarang mencerminkan lingkungan produksi, yang menyebabkan masalah setelah peluncuran.

Platform QA khusus memecahkan masalah ini dengan menyediakan pemetaan langsung antara kluster produksi dan QA.

Standar keamanan yang sama diikuti. Topik yang sama dihosting di kluster dengan broker yang tersebar di beberapa zona dalam Google Cloud Platform.

#### Pemantauan dan Peringatan

Pemantauan dan peringatan adalah aspek yang sangat penting untuk sistem yang beroperasi pada skala tinggi. Tim ingin mengetahui masalah dan insiden dengan cepat sehingga kegagalan beruntun dapat dihindari.

Di PayPal, platform Kafka terintegrasi dengan sistem pemantauan dan peringatan.

Apache Kafka menyediakan banyak metrik. Namun, mereka mengambil subset metrik yang membantu mereka mengidentifikasi masalah lebih cepat.

Perpustakaan Metrik Kafka menyaring metrik dan mengirimkannya ke backend SignalFX melalui agen SignalFX yang berjalan di semua broker, Zookeepers, MirrorMakers, dan klien Kafka. Peringatan individu yang terkait dengan metrik ini dipicu setiap kali ambang batas abnormal dilanggar.

#### Manajemen Konfigurasi

Mengoperasikan sistem yang kritis memerlukan perlindungan terhadap kehilangan data. Ini tidak hanya berlaku untuk data aplikasi tetapi juga untuk informasi infrastruktur.

Bagaimana jika infrastruktur terhapus dan kita harus membangunnya kembali dari awal?

Di PayPal, manajemen konfigurasi membantu mereka menyimpan detail infrastruktur lengkap. Ini adalah sumber kebenaran tunggal yang memungkinkan PayPal membangun kembali kluster dalam beberapa jam jika diperlukan.

Mereka menyimpan metadata Kafka seperti detail topik, kluster, dan aplikasi dalam sistem manajemen konfigurasi internal. Metadata ini juga dicadangkan untuk memastikan mereka memiliki data terbaru jika diperlukan untuk membuat ulang kluster dan topik dalam kasus pemulihan.

#### Peningkatan dan Otomatisasi

Sistem berskala besar memerlukan alat khusus untuk melaksanakan tugas operasional secepat mungkin.

PayPal membangun beberapa alat penting untuk mengoperasikan kluster Kafka mereka. Mari kita lihat beberapa yang penting:

**Patching Kerentanan Keamanan** PayPal menggunakan BareMetal untuk deploy broker Kafka dan mesin virtual untuk Zookeeper dan MirrorMakers.

Semua host ini perlu dipatch pada interval yang sering untuk memperbaiki kerentanan keamanan.

Patching memerlukan restart BM yang dapat menyebabkan partisi tertinggal. Ini juga dapat menyebabkan kehilangan data dalam kasus topik Kafka yang dikonfigurasi dengan set replika tiga.

Mereka membangun plugin untuk memeriksa apakah partisi tertinggal sebelum mempatch host, sehingga memastikan hanya satu broker dipatch pada satu waktu tanpa kemungkinan kehilangan data.

**Onboarding Topik** Tim aplikasi memerlukan topik untuk fungsionalitas aplikasi mereka. Untuk membuat proses ini standar, PayPal membangun Dasbor Onboarding untuk mengajukan permintaan topik baru.

Sebuah tim review khusus memeriksa persyaratan kapasitas untuk topik baru dan mengonboardingnya ke salah satu kluster yang tersedia. Mereka menggunakan alat analisis kapasitas yang terintegrasi ke dalam alur kerja onboarding untuk membuat keputusan.

Untuk setiap aplikasi baru yang di-onboard ke sistem Kafka, token unik dihasilkan. Token ini digunakan untuk mengotentikasi akses klien ke topik Kafka. Seperti yang dibahas sebelumnya, ACL dibuat untuk aplikasi dan topik spesifik berdasarkan peran mereka.

**Onboarding MirrorMaker** Seperti disebutkan sebelumnya, PayPal menggunakan MirrorMaker untuk mencerminkan data dari satu kluster ke kluster lainnya.

Untuk pengaturan ini, pengembang juga menggunakan UI Onboarding Kafka untuk mendaftarkan persyaratan mereka. Setelah pemeriksaan oleh tim Kafka, instance MirrorMaker disediakan.

#### Kesimpulan

Platform Kafka di PayPal adalah kunci untuk memungkinkan integrasi yang mulus antara beberapa aplikasi dan mendukung skala operasi mereka.

Beberapa pembelajaran penting yang bisa diambil dari studi ini adalah sebagai berikut:

1. Alat sangat diperlukan saat mengoperasikan Kafka pada skala besar. Ini mencakup operasi seperti instalasi kluster, manajemen topik, patching VM, dll.
2. Ketersediaan sebesar kemampuan sistem peringatan dan pemantauan untuk memberikan masukan tepat waktu kepada tim infrastruktur.
3. ACL adalah cara yang bagus untuk memiliki pemahaman yang lebih baik tentang bagaimana berbagai aplikasi terhubung dengan Kafka.
4. Lingkungan QA khusus sangat penting bagi pengembang untuk meluncurkan perubahan dengan percaya diri dan cepat.

**Referensi:**

* [Scaling Kafka to Support PayPal’s Data Growth](https://medium.com/paypal-tech/scaling-kafka-to-support-paypals-data-growth-a0b4da420fab)
* [Marching towards a Trillion Kafka Messages Per Day](https://www.confluent.io/resources/kafka-summit-2020/marching-toward-a-trillion-kafka-messages-per-day-running-kafka-at-scale-at-paypal/)
* [Demystifying Kafka MirrorMaker2](https://developers.redhat.com/articles/2023/11/13/demystifying-kafka-mirrormaker-2-use-cases-and-architecture)
* [Kafka Use Cases](https://kafka.apache.org/uses)
