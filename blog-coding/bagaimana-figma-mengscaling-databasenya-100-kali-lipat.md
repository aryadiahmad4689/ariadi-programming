# Bagaimana Figma Mengscaling Databasenya 100 Kali Lipat

Figma, sebuah platform desain kolaboratif, telah mengalami pertumbuhan yang luar biasa selama beberapa tahun terakhir. Basis penggunanya telah meningkat hampir 200% sejak 2018, dengan sekitar 3 juta pengguna bulanan.

Saat semakin banyak pengguna bergabung, tim infrastruktur Figma menghadapi tantangan untuk dengan cepat menskalakan basis data mereka agar dapat memenuhi permintaan yang terus meningkat.

Basis data Figma seperti tulang punggungnya, menyimpan dan mengelola semua metadata penting seperti izin, informasi file, dan komentar. Dan sejak 2020, ukurannya tumbuh hingga 100 kali lipat!

Ini adalah masalah yang bagus untuk dimiliki, tetapi juga berarti tim harus kreatif dalam mencari solusi.

Dalam artikel ini, kita akan membahas perjalanan Figma dalam menskalakan basis data mereka. Kita akan menjelajahi tantangan yang mereka hadapi, keputusan yang mereka buat, dan solusi inovatif yang mereka temukan. Pada akhir artikel, Anda akan memiliki pemahaman yang lebih baik tentang apa yang diperlukan untuk menskalakan basis data untuk perusahaan yang tumbuh cepat seperti Figma.

**Kondisi Awal Basis Data Figma**

Pada tahun 2020, Figma masih menggunakan satu basis data Amazon RDS besar untuk menyimpan sebagian besar metadata. Meskipun ini cukup efektif, satu mesin memiliki batasannya.

Selama lalu lintas puncak, pemanfaatan CPU berada di atas 65% yang mengakibatkan latensi basis data yang tidak terduga.

Meskipun jenuh total masih jauh, tim infrastruktur Figma ingin secara proaktif mengidentifikasi dan memperbaiki masalah skalabilitas. Mereka memulai dengan beberapa perbaikan taktis seperti:

* Mengupgrade basis data ke instance terbesar yang tersedia (dari r5.12xlarge ke r5.24xlarge).
* Membuat beberapa replika baca untuk menskalakan lalu lintas baca.
* Mendirikan basis data baru untuk kasus penggunaan baru guna membatasi pertumbuhan basis data asli.
* Menambahkan PgBouncer sebagai connection pooler untuk membatasi dampak dari semakin banyaknya koneksi.

Perbaikan ini memberi mereka tambahan waktu sekitar satu tahun, tetapi masih ada keterbatasan:

* Berdasarkan lalu lintas basis data, mereka menemukan bahwa operasi tulis menyumbang sebagian besar pemanfaatan keseluruhan.
* Tidak semua operasi baca dapat dipindahkan ke replika karena beberapa kasus penggunaan sensitif terhadap dampak dari replikasi lag.

Jelas bahwa mereka membutuhkan solusi jangka panjang.

**Langkah Pertama: Partisi Vertikal**

Ketika tim infrastruktur Figma menyadari bahwa mereka perlu menskalakan basis data mereka, mereka tidak bisa begitu saja menutup semuanya dan memulai dari awal. Mereka membutuhkan solusi untuk menjaga Figma tetap berjalan lancar sementara mereka mengatasi masalah tersebut.

Disinilah partisi vertikal masuk.

Pikirkan partisi vertikal seperti mengatur ulang lemari pakaian Anda. Alih-alih memiliki satu tumpukan besar yang berantakan, Anda membaginya menjadi beberapa bagian terpisah. Dalam istilah basis data, ini berarti memindahkan tabel-tabel tertentu ke basis data terpisah.

Bagi Figma, partisi vertikal sangat membantu. Mereka memindahkan tabel-tabel dengan lalu lintas tinggi seperti "Figma Files" dan "Organizations" ke basis data terpisah. Ini memberi mereka ruang bernapas yang sangat dibutuhkan.

Untuk mengidentifikasi tabel-tabel yang akan dipartisi, Figma mempertimbangkan dua faktor:

* Dampak: Memindahkan tabel-tabel ini harus memindahkan sebagian besar beban kerja.
* Isolasi: Tabel-tabel tersebut sebaiknya tidak terhubung erat dengan tabel lainnya.

Untuk mengukur dampak, mereka melihat rata-rata sesi aktif (AAS) untuk query. Statistik ini menggambarkan jumlah rata-rata thread aktif yang didedikasikan untuk query tertentu pada waktu tertentu.

Mengukur isolasi sedikit lebih rumit. Mereka menggunakan validator runtime yang terhubung dengan ActiveRecord, ORM Ruby mereka. Validator ini mengirimkan informasi query dan transaksi produksi ke Snowflake untuk analisis, membantu mereka mengidentifikasi tabel yang ideal untuk dipartisi berdasarkan pola query dan hubungan tabel.

Setelah tabel diidentifikasi, Figma perlu memigrasikan tabel-tabel ini antar basis data tanpa downtime. Mereka menetapkan tujuan berikut untuk solusi migrasi mereka:

* Membatasi dampak terhadap ketersediaan hingga kurang dari 1 menit.
* Mengotomatisasi prosedur sehingga mudah diulang.
* Memiliki kemampuan untuk membatalkan partisi yang baru saja dilakukan.

Karena mereka tidak menemukan solusi yang sudah jadi yang dapat memenuhi persyaratan ini, Figma membangun solusi sendiri. Secara garis besar, solusinya bekerja sebagai berikut:

1. Mempersiapkan aplikasi klien untuk query dari beberapa partisi basis data.
2. Mereplikasi tabel dari basis data asli ke basis data baru hingga lag replikasi mendekati 0.
3. Menghentikan aktivitas pada basis data asli.
4. Menunggu basis data untuk sinkronisasi.
5. Mengalihkan lalu lintas query ke basis data baru.
6. Melanjutkan aktivitas.

Untuk membuat migrasi ke basis data terpartisi lebih lancar, mereka menciptakan layanan PgBouncer terpisah untuk membagi lalu lintas secara virtual. Grup keamanan diterapkan untuk memastikan hanya PgBouncer yang dapat langsung mengakses basis data.

Mempartisi lapisan PgBouncer terlebih dahulu memberi beberapa kelonggaran pada klien untuk merutekan query secara tidak tepat karena semua instance PgBouncer awalnya memiliki target basis data yang sama. Selama waktu ini, tim juga dapat mendeteksi ketidakcocokan rute dan melakukan koreksi yang diperlukan.

Diagram berikut menunjukkan proses migrasi ini:

**Mengimplementasikan Replikasi**

Replikasi data adalah cara yang bagus untuk menskalakan operasi baca untuk basis data Anda. Ketika datang ke replikasi data untuk partisi vertikal, Figma memiliki dua opsi dalam Postgres: replikasi streaming atau replikasi logis.

Mereka memilih replikasi logis untuk tiga alasan utama:

1. Replikasi logis memungkinkan mereka untuk memindahkan sebagian subset tabel sehingga mereka dapat memulai dengan jejak penyimpanan yang jauh lebih kecil di basis data tujuan.
2. Ini memungkinkan mereka untuk mereplikasi data ke basis data yang menjalankan versi mayor Postgres yang berbeda.
3. Terakhir, ini memungkinkan mereka untuk mengatur replikasi balik untuk membatalkan operasi jika diperlukan.

Namun, replikasi logis lambat. Penyalinan data awal bisa memakan waktu berhari-hari atau bahkan berminggu-minggu untuk diselesaikan.

Figma sangat ingin menghindari proses panjang ini, tidak hanya untuk meminimalkan jendela kegagalan replikasi tetapi juga untuk mengurangi biaya memulai ulang jika terjadi kesalahan.

Namun, apa yang membuat proses ini begitu lambat?

Penyebabnya adalah bagaimana Postgres memelihara indeks di basis data tujuan. Sementara proses replikasi menyalin baris dalam jumlah besar, itu juga memperbarui indeks satu baris pada satu waktu. Dengan menghapus indeks di basis data tujuan dan membangunnya kembali setelah penyalinan data, Figma mengurangi waktu penyalinan menjadi beberapa jam.

**Kebutuhan untuk Skalabilitas Horizontal**

Seiring pertumbuhan basis pengguna dan fitur Figma, demikian pula permintaan terhadap basis data mereka.

Meskipun upaya terbaik mereka, partisi vertikal memiliki keterbatasan, terutama untuk tabel terbesar Figma. Beberapa tabel berisi beberapa terabyte data dan miliaran baris, membuatnya terlalu besar untuk satu basis data.

Beberapa masalah yang terutama menonjol:

* Masalah Vacuum Postgres: Vacuuming adalah proses latar belakang penting di Postgres yang mengklaim kembali penyimpanan yang ditempati oleh baris yang dihapus atau usang. Tanpa vacuuming reguler, basis data pada akhirnya akan kehabisan ID transaksi dan berhenti total. Namun, vacuuming tabel besar dapat menghabiskan sumber daya dan menyebabkan masalah kinerja serta downtime.
* Maksimum Operasi IO Per Detik: Tabel tulis tertinggi Figma tumbuh begitu cepat sehingga mereka akan segera melebihi batas IOPS maksimum Amazon RDS.

Untuk perspektif yang lebih baik, bayangkan sebuah perpustakaan dengan koleksi buku yang tumbuh dengan cepat. Awalnya, perpustakaan mungkin mengatasinya dengan menambahkan lebih banyak rak (partisi vertikal). Tetapi akhirnya, gedung itu sendiri akan kehabisan ruang. Tidak peduli seberapa efisien Anda mengatur rak, Anda tidak dapat memasukkan jumlah buku yang tak terbatas ke dalam satu gedung. Di situlah Anda perlu mulai memikirkan membuka cabang perpustakaan.

Ini adalah pendekatan sharding horizontal.

Bagi Figma, sharding horizontal adalah cara untuk membagi tabel besar di beberapa basis data fisik, memungkinkan mereka untuk menskalakan melampaui batas satu mesin.

Diagram berikut menunjukkan pendekatan ini:

Namun, sharding horizontal adalah proses yang kompleks yang membawa tantangannya sendiri:

* Beberapa query SQL menjadi tidak efisien untuk didukung.
* Kode aplikasi harus diperbarui untuk merutekan query secara efisien ke shard yang benar.
* Perubahan skema harus dikoordinasikan di semua shard.
* Postgres tidak lagi dapat menegakkan kunci asing dan indeks yang unik secara global.
* Transaksi melibatkan beberapa shard, yang berarti Postgres tidak dapat digunakan untuk menegakkan transactionalitas.

**Menjelajahi Solusi Alternatif**

Tim engineering di Figma mengevaluasi opsi SQL alternatif seperti CockroachDB, TiDB, Spanner, dan Vitess serta basis data NoSQL.

Namun, pada akhirnya mereka memutuskan untuk membangun solusi sharding horizontal di atas infrastruktur RDS Postgres yang telah mereka partisi

vertikal.

Ada beberapa alasan untuk mengambil keputusan ini:

* Mereka dapat memanfaatkan keahlian mereka yang ada dengan RDS Postgres, yang telah mereka jalankan dengan andal selama bertahun-tahun.
* Mereka dapat menyesuaikan solusi dengan kebutuhan spesifik Figma, daripada menyesuaikan aplikasi mereka agar sesuai dengan solusi sharding umum.
* Jika terjadi masalah, mereka dapat dengan mudah kembali ke basis data Postgres yang tidak ter-shard.
* Mereka tidak perlu mengubah model data relasional kompleks yang dibangun di atas arsitektur Postgres ke pendekatan baru seperti NoSQL. Ini memungkinkan tim untuk terus membangun fitur baru.

**Implementasi Sharding Unik Figma**

Pendekatan Figma untuk sharding horizontal disesuaikan dengan kebutuhan spesifik mereka serta arsitektur yang ada. Mereka membuat beberapa pilihan desain yang tidak biasa yang membedakan implementasi mereka dari solusi umum lainnya.

Mari kita lihat komponen kunci dari pendekatan sharding Figma:

**Colos (Colocations) untuk Pengelompokan Tabel Terkait**

Figma memperkenalkan konsep “colos” atau kolokasi, yang merupakan sekelompok tabel terkait yang berbagi kunci sharding yang sama dan tata letak sharding fisik yang sama.

Untuk membuat colos, mereka memilih beberapa kunci sharding seperti UserId, FileId, atau OrgID. Hampir setiap tabel di Figma dapat di-shard menggunakan salah satu kunci ini.

Ini memberikan abstraksi yang ramah bagi pengembang untuk berinteraksi dengan tabel yang di-shard secara horizontal.

Tabel dalam colo mendukung join lintas tabel dan transaksi penuh ketika dibatasi pada satu kunci sharding. Sebagian besar kode aplikasi sudah berinteraksi dengan basis data dengan cara yang sama, yang meminimalkan pekerjaan yang diperlukan oleh aplikasi untuk membuat tabel siap untuk sharding horizontal.

Diagram berikut menunjukkan konsep colos:

**Sharding Logis vs Sharding Fisik**

Figma memisahkan konsep “sharding logis” di lapisan aplikasi dari “sharding fisik” di lapisan Postgres.

Sharding logis melibatkan pembuatan beberapa tampilan per tabel, masing-masing sesuai dengan subset data di shard tertentu. Semua operasi baca dan tulis ke tabel dikirim melalui tampilan ini, membuat tabel terlihat seperti di-shard secara horizontal meskipun data secara fisik berada di satu host basis data.

Pemisahan ini memungkinkan Figma untuk mendekopling dua bagian dari migrasi mereka dan mengimplementasikannya secara independen. Mereka dapat melakukan rollout sharding logis yang lebih aman dan berisiko rendah sebelum menjalankan sharding fisik yang lebih berisiko.

Mengembalikan sharding logis adalah perubahan konfigurasi sederhana, sedangkan mengembalikan operasi shard fisik akan memerlukan koordinasi yang lebih kompleks untuk memastikan konsistensi data.

**DBProxy Query Engine untuk Routing dan Eksekusi Query**

Untuk mendukung sharding horizontal, tim engineering Figma membangun layanan baru bernama DBProxy yang berada di antara aplikasi dan lapisan connection pooling seperti PGBouncer.

DBProxy mencakup mesin query ringan yang mampu memparsing dan mengeksekusi query yang di-shard secara horizontal. Ini terdiri dari tiga komponen utama:

* Parser query yang membaca SQL yang dikirim oleh aplikasi dan mengubahnya menjadi Abstract Syntax Tree (AST).
* Perencana logis yang memparsing AST, mengekstrak jenis query (insert, update, dll.), dan ID shard logis dari rencana query.
* Perencana fisik yang memetakan query dari ID shard logis ke basis data fisik dan menulis ulang query untuk dieksekusi pada shard fisik yang sesuai.

Diagram berikut menunjukkan penggunaan praktis dari tiga komponen ini dalam alur kerja pemrosesan query:

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Selalu ada trade-off ketika berhubungan dengan query di dunia yang di-shard secara horizontal. Query untuk satu kunci shard relatif mudah diimplementasikan. Mesin query hanya perlu mengekstrak kunci shard dan merutekan query ke basis data fisik yang sesuai.

Namun, jika query tidak mengandung kunci sharding, mesin query harus melakukan operasi “scatter-gather” yang lebih kompleks. Operasi ini mirip dengan permainan petak umpet di mana Anda mengirim query ke setiap shard (scatter), dan kemudian menyusun jawaban dari masing-masing shard (gather).

Diagram berikut menunjukkan bagaimana query single-shard bekerja dibandingkan dengan query scatter-gather:

Seperti yang Anda lihat, ini meningkatkan beban pada basis data, dan memiliki terlalu banyak query scatter-gather dapat merusak skalabilitas horizontal.

Untuk mengelola semuanya dengan lebih baik, DBProxy menangani load-shedding, dukungan transaksi, manajemen topologi basis data, dan peningkatan observabilitas.

**Framework Kesiapan Aplikasi Bayangan**

Figma menambahkan framework "kesiapan aplikasi bayangan" yang mampu memprediksi bagaimana lalu lintas produksi langsung akan berperilaku di bawah berbagai kunci sharding potensial.

Framework ini membantu mereka menjaga DBProxy tetap sederhana sambil mengurangi pekerjaan yang diperlukan untuk pengembang aplikasi dalam menulis ulang query yang tidak didukung.

Semua query dan rencana terkait dicatat ke basis data Snowflake, di mana mereka dapat menjalankan analisis offline. Berdasarkan data yang dikumpulkan, mereka dapat memilih bahasa query yang mendukung 90% query umum sambil menghindari kompleksitas terburuk di mesin query.

**Kesimpulan**

Tim infrastruktur Figma meluncurkan tabel sharding horizontal pertama mereka pada September 2023, menandai tonggak penting dalam perjalanan skalabilitas basis data mereka.

Ini adalah implementasi yang sukses dengan dampak minimal pada ketersediaan. Selain itu, tim tidak melihat adanya regresi dalam latensi atau ketersediaan setelah operasi sharding.

Tujuan akhir Figma adalah untuk melakukan sharding horizontal pada setiap tabel dalam basis data mereka dan mencapai skalabilitas yang hampir tak terbatas. Mereka telah mengidentifikasi beberapa tantangan yang perlu diselesaikan seperti:

* Mendukung pembaruan skema yang di-shard secara horizontal
* Menghasilkan ID yang unik secara global untuk kunci primer yang di-shard secara horizontal
* Menerapkan transaksi lintas shard yang atomik untuk kasus penggunaan yang kritis bagi bisnis
* Mengaktifkan indeks yang unik secara global yang terdistribusi
* Mengembangkan model ORM untuk meningkatkan kecepatan pengembang
* Operasi reshard otomatis untuk memungkinkan pembagian shard dengan sekali klik.

Terakhir, setelah mencapai jangka waktu yang cukup, mereka juga berencana untuk mengevaluasi kembali pendekatan mereka saat ini dalam menggunakan sharding horizontal RDS in-house dibandingkan beralih ke alternatif open-source atau terkelola di masa depan.\
\
**Referensi:**

* [How Figma’s databases team lived to tell the scale](https://www.figma.com/blog/how-figmas-databases-team-lived-to-tell-the-scale/)
* [The growing pains of database architecture](https://www.figma.com/blog/how-figma-scaled-to-multiple-databases/)
* [Features of PgBouncer](https://www.pgbouncer.org/features.html)
* [Figma User Statistics](https://zipdo.co/statistics/figma-user/)

