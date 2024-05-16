# Jenis Jenis Database

Keberhasilan suatu aplikasi perangkat lunak sering kali bergantung pada pemilihan database yang tepat. Sebagai pengembang, kita dihadapkan pada beragam pilihan basis data. Penting bagi kita untuk memahami perbedaan antara opsi-opsi ini dan cara memilih opsi yang paling sesuai dengan kebutuhan proyek. Sebuah aplikasi yang kompleks biasanya menggunakan beberapa database yang berbeda, masing-masing melayani aspek spesifik dari kebutuhan aplikasi.

<figure><img src="../.gitbook/assets/image (92).png" alt=""><figcaption></figcaption></figure>

Dibawah kita akan membahas jenis-jenis database dan karakteristiknya.

<figure><img src="../.gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>

## Memahami Jenis Basis Data

Untuk membuat keputusan terbaik untuk proyek kalian, penting untuk memahami berbagai jenis database yang tersedia. Di bagian ini, kita mengeksplorasi karakteristik utama dari berbagai tipe database, termasuk opsi populer untuk masing-masing tipe database, dan membandingkan kasus penggunaannya.

<figure><img src="../.gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

### Basis Data Relasional

Basis data relasional didasarkan pada model relasional, yang mengatur data ke dalam tabel dengan baris dan kolom. Basis data ini telah menjadi pilihan standar untuk banyak aplikasi karena konsistensinya yang kuat, dukungan untuk kueri yang kompleks, dan kepatuhan terhadap properti ACID (Atomicity, Consistency, Isolation, Durability). Fitur dan manfaat utama dari database relasional meliputi:

* Organisasi data terstruktur: Data dalam database relasional disimpan dalam tabel dengan skema yang telah ditentukan sebelumnya, sehingga menerapkan struktur yang konsisten di seluruh database. Organisasi ini mempermudah pengelolaan dan pemeliharaan data, terutama ketika menangani data terstruktur dalam jumlah besar.
* Hubungan dan integritas referensial: Hubungan antar tabel dalam database relasional ditentukan oleh kunci utama dan asing, yang memastikan integritas referensial. Fitur ini memungkinkan kueri data terkait secara efisien dan mendukung hubungan data yang kompleks.
* Dukungan SQL: Basis data relasional menggunakan Structured Query Language (SQL) untuk membuat kueri, memanipulasi, dan mengelola data. SQL adalah bahasa yang kuat dan diadopsi secara luas yang memungkinkan pengembang melakukan kueri kompleks dan manipulasi data.
* Properti Transaksi dan ACID: Basis data relasional mendukung transaksi, yang merupakan kumpulan operasi terkait yang berhasil atau gagal secara keseluruhan. Fitur ini memastikan properti ACID – Atomicity, Consistency, Isolation, dan Durability – dipertahankan, menjamin konsistensi dan integritas data.
* Pengindeksan dan pengoptimalan: Basis data relasional menawarkan berbagai teknik pengindeksan dan strategi pengoptimalan kueri, yang membantu meningkatkan kinerja kueri dan mengurangi konsumsi sumber daya.

Basis data relasional juga memiliki beberapa kelemahan:

* Skalabilitas terbatas: Menskalakan database relasional secara horizontal (menambahkan lebih banyak node) dapat menjadi tantangan, terutama jika dibandingkan dengan beberapa database NoSQL yang dirancang untuk lingkungan terdistribusi.
* Kekakuan: Skema yang telah ditentukan sebelumnya dalam database relasional dapat mempersulit adaptasi terhadap perubahan persyaratan, karena mengubah skema mungkin memerlukan modifikasi signifikan pada data dan aplikasi yang ada.
* Masalah kinerja dengan kumpulan data yang besar: Seiring dengan bertambahnya volume data, database relasional mungkin mengalami masalah kinerja, terutama ketika menangani kueri yang kompleks dan manipulasi data berskala besar.
* Tidak efisien untuk data tidak terstruktur atau semi terstruktur: Database relasional dirancang untuk data terstruktur, yang mungkin tidak cocok untuk mengelola data tidak terstruktur atau semi terstruktur, seperti data media sosial atau data sensor.

Database relasional yang populer termasuk MySQL, PostgreSQL, Microsoft SQL Server, dan Oracle. Masing-masing opsi ini memiliki fitur, kekuatan, dan kelemahan uniknya sendiri, sehingga cocok untuk berbagai kasus penggunaan dan kebutuhan. Saat mempertimbangkan database relasional, penting untuk mengevaluasi kebutuhan spesifik aplikasi dalam hal konsistensi data, dukungan untuk kueri yang kompleks, dan skalabilitas, dan faktor-faktor lainnya.

<figure><img src="../.gitbook/assets/image (95).png" alt=""><figcaption></figcaption></figure>

_Lisensi proprietary (lisensi hak milik) adalah jenis lisensi perangkat lunak di mana pemilik perangkat lunak tersebut mempertahankan hak cipta penuh dan memberikan izin kepada pengguna untuk menggunakan perangkat lunak tersebut di bawah syarat dan ketentuan tertentu._

### No SQL

Basis data NoSQL dikembangkan sebagai respons terhadap keterbatasan basis data relasional, khususnya dalam hal skalabilitas, fleksibilitas, dan kinerja dalam kondisi tertentu. Tidak seperti database relasional, database NoSQL tidak sepenuhnya mengikuti model relasional atau penyimpanan berbasis tabel tradisional. Mereka dapat menyimpan data dalam berbagai format, sehingga cocok untuk beragam kasus penggunaan. Basis data NoSQL secara luas dapat dikategorikan menjadi empat subtipe, masing-masing dengan karakteristik uniknya:

* Basis data berbasis dokumen menyimpan data dalam dokumen semi terstruktur, seperti JSON atau BSON. Format ini memberikan fleksibilitas lebih besar dalam pemodelan data. Hal ini memungkinkan skema yang lebih dinamis yang dapat berkembang seiring perubahan persyaratan aplikasi. Basis data berbasis dokumen sangat cocok untuk aplikasi yang berhubungan dengan struktur data hierarki atau bersarang, seperti sistem manajemen konten, platform e-niaga, dan aplikasi analitik. Beberapa database berbasis dokumen yang populer termasuk MongoDB dan Couchbase.
* Basis data berbasis kolom, juga dikenal sebagai penyimpanan kolom lebar atau penyimpanan keluarga kolom, mengatur data dalam kolom, bukan baris. Struktur ini mengoptimalkan kueri berbasis kolom, memberikan peningkatan kompresi dan kinerja membaca yang lebih baik. Basis data berbasis kolom dirancang untuk aplikasi yang perlu menyimpan dan menanyakan data dalam jumlah besar di banyak node, menjadikannya pilihan populer untuk aplikasi data besar dan analitik, serta aplikasi dengan beban kerja tulis dan baca yang tinggi. Beberapa database berbasis kolom yang terkenal adalah Apache Cassandra dan HBase.
* Penyimpanan nilai kunci menyediakan cara sederhana dan efisien untuk menyimpan data sebagai pasangan nilai kunci. Basis data ini ideal untuk kasus penggunaan yang memerlukan pembacaan dan penulisan berkecepatan tinggi, serta skalabilitas horizontal. Penyimpanan nilai kunci dapat berfungsi sebagai lapisan cache, penyimpanan sesi, atau penyimpanan konfigurasi, dan kegunaan lainnya. Mereka sering digunakan dalam aplikasi yang mengutamakan kinerja dan akses latensi rendah ke data, seperti platform game, sistem analisis real-time, dan mesin rekomendasi. Contoh penyimpanan nilai kunci yang populer mencakup Redis dan Amazon DynamoDB.
* Basis data grafik fokus pada penyimpanan data sebagai node dan tepi dalam grafik. Ini memungkinkan pemrosesan hubungan kompleks, traversal, dan algoritma berbasis grafik yang efisien. Jenis database ini sangat berguna untuk aplikasi yang melibatkan hubungan rumit antar entitas, seperti jaringan sosial, sistem deteksi penipuan, dan mesin rekomendasi. Basis data grafik memberikan kemampuan kueri yang kuat untuk melintasi dan menganalisis data yang saling berhubungan, menjadikannya pilihan yang menarik untuk kasus penggunaan ini. Neo4j dan Amazon Neptune adalah contoh database grafik.

Penting untuk dicatat bahwa database NoSQL memiliki kelemahannya sendiri:

* Kurangnya standarisasi: Tidak seperti database relasional, yang mengikuti bahasa kueri SQL standar, database NoSQL sering kali menggunakan bahasa kueri atau API mereka sendiri. Hal ini dapat menyebabkan peningkatan kurva pembelajaran dan kesulitan saat bermigrasi antara database NoSQL yang berbeda atau mengintegrasikannya dengan sistem lain.
* Konsistensi yang lebih lemah: Banyak database NoSQL yang menggunakan model konsistensi akhir untuk mencapai performa dan ketersediaan yang lebih tinggi. Meskipun ini mungkin cocok untuk beberapa aplikasi, hal ini dapat menyebabkan masalah jika diperlukan konsistensi data yang ketat.
* Dukungan terbatas untuk kueri dan transaksi kompleks: Beberapa database NoSQL, seperti penyimpanan nilai kunci dan database berbasis kolom, tidak dirancang untuk kueri kompleks atau transaksi multi-catatan. Hal ini dapat mempersulit penerapan logika bisnis atau persyaratan pelaporan tertentu secara langsung di dalam database.

<figure><img src="../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>

Setiap subtipe NoSQL memiliki kekuatan dan kelemahannya masing-masing, sehingga cocok untuk aplikasi yang berbeda tergantung pada kebutuhan spesifik. Saat mempertimbangkan database NoSQL, penting untuk mengevaluasi kebutuhan spesifik aplikasi dalam hal skalabilitas, pemodelan data, pola kueri, dan kinerja untuk menentukan yang paling sesuai.

### New SQL

Basis data NewSQL adalah pendekatan modern untuk menggabungkan kekuatan basis data relasional dan NoSQL. Mereka mempertahankan model relasional, properti ACID, dan dukungan SQL, sekaligus menawarkan peningkatan skalabilitas, arsitektur terdistribusi, dan peningkatan kinerja yang umumnya dikaitkan dengan database NoSQL. Basis data NewSQL dirancang untuk mengatasi tantangan aplikasi modern, seperti menangani beban kerja berskala besar, terdistribusi, dan sangat bersamaan, tanpa mengorbankan konsistensi dan integritas data.

* Arsitektur terdistribusi: Database NewSQL didistribusikan. Mereka memanfaatkan partisi dan replikasi data di beberapa node atau bahkan pusat data. Arsitektur ini memungkinkan toleransi kesalahan yang lebih baik, ketersediaan tinggi, dan skala global.
* Skalabilitas: Basis data NewSQL dapat diskalakan secara horizontal. Mereka mengakomodasi peningkatan beban kerja dengan menambahkan lebih banyak node ke sistem. Fitur ini membuatnya cocok untuk aplikasi yang menuntut konsistensi yang kuat dan kemampuan menangani transaksi atau pengguna dalam jumlah besar.
* Kontrol konkurensi: Mekanisme kontrol konkurensi tingkat lanjut, seperti kontrol konkurensi multi-versi (MVCC) atau kontrol konkurensi optimis, digunakan oleh database NewSQL. Mekanisme ini memungkinkan penanganan efisien sejumlah besar transaksi simultan. Hal ini penting untuk aplikasi modern dengan persyaratan konkurensi tinggi.
* Dukungan dan kompatibilitas SQL: Mempertahankan bahasa SQL yang familiar untuk membuat kueri dan memanipulasi data, database NewSQL menyederhanakan kurva pembelajaran bagi pengembang. Mereka sering kali menyediakan kompatibilitas dengan database dan alat relasional yang ada, sehingga memudahkan proses migrasi.

Penting untuk mempertimbangkan kelemahan NewSQL:

* Kompleksitas: Arsitektur terdistribusi dan fitur-fitur canggih dari database NewSQL dapat menimbulkan kompleksitas tambahan dalam hal konfigurasi, pemeliharaan, dan pemecahan masalah dibandingkan dengan database relasional tradisional.
* Penguncian vendor: Beberapa database NewSQL ditawarkan sebagai layanan terkelola oleh vendor tertentu, yang dapat menyebabkan penguncian vendor dan membatasi fleksibilitas untuk berpindah penyedia.
* Kurangnya kematangan: Sebagai teknologi yang relatif baru, database NewSQL mungkin kurang memiliki kematangan dan ekosistem yang luas dibandingkan database relasional tradisional, sehingga dapat mengakibatkan terbatasnya dukungan, dokumentasi, dan sumber daya komunitas.

Basis data NewSQL yang populer termasuk CockroachDB, Google Spanner, dan TiDB. Setiap opsi menawarkan fitur dan kemampuan unik, sehingga cocok untuk berbagai kasus penggunaan dan kebutuhan. Saat mempertimbangkan database NewSQL, penting untuk mengevaluasi kebutuhan spesifik aplikasi dalam hal skalabilitas, konsistensi data, kinerja, dan pemahaman pengembang untuk menentukan yang paling sesuai.

<figure><img src="../.gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>

### Time Series

Basis data time series(deret waktu) mengkhususkan diri dalam menangani data yang diberi stempel waktu, yang dicirikan oleh sifat berurutan dan pengurutan berdasarkan waktu. Data deret waktu umum digunakan di berbagai domain, seperti pasar keuangan, IoT, dan sistem pemantauan. Basis data ini dirancang untuk mengoptimalkan penyimpanan, pengambilan, dan analisis data dengan cap waktu. Mereka menawarkan fitur yang secara khusus memenuhi tantangan unik yang ditimbulkan oleh data deret waktu.

* Kinerja penulisan dan kueri yang tinggi: Basis data deret waktu dioptimalkan untuk menangani aliran data berkecepatan tinggi, yang memerlukan kinerja penulisan yang efisien. Mereka juga memberikan kinerja kueri yang cepat, memungkinkan analisis data deret waktu secara real-time atau hampir real-time.
* Kompresi data: Karena banyaknya volume data yang dihasilkan oleh beban kerja deret waktu, database deret waktu menggunakan berbagai teknik kompresi data untuk mengurangi kebutuhan penyimpanan dan meningkatkan kinerja kueri.
* Kebijakan penyimpanan data berbasis waktu: Basis data rangkaian waktu memungkinkan pengelolaan kebijakan penyimpanan data berdasarkan waktu dengan mudah. Fitur ini memungkinkan penuaan data otomatis, yang membantu menjaga efisiensi penyimpanan dan memastikan relevansi data.
* Fungsi deret waktu bawaan: Basis data deret waktu biasanya menyertakan fungsi dan alat bawaan untuk memfasilitasi analisis data deret waktu, seperti agregasi, downsampling, dan perkiraan. Fungsi-fungsi ini menyederhanakan proses bekerja dengan data deret waktu dan dapat membantu pengembang membangun aplikasi yang lebih efisien.
* Skalabilitas: Basis data rangkaian waktu dirancang untuk diskalakan secara horizontal, memungkinkannya menangani data dalam jumlah besar dan tingkat penyerapan yang tinggi. Fitur ini penting untuk aplikasi yang perlu menyimpan dan menganalisis data deret waktu dalam jumlah besar, seperti aplikasi IoT atau sistem pemantauan.

Basis data deret waktu yang populer mencakup InfluxDB dan TimescaleDB. Masing-masing opsi ini menawarkan fitur dan kemampuan unik yang disesuaikan dengan manajemen dan analisis data deret waktu, sehingga cocok untuk berbagai kasus penggunaan dan persyaratan. Saat mempertimbangkan database deret waktu, penting untuk mengevaluasi kebutuhan spesifik aplikasi dalam hal tingkat penyerapan data, kinerja kueri, retensi data, dan skalabilitas.

<figure><img src="../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>

**Kesimpulan**

Untuk membandingkan tipe database dan kasus penggunaannya, kita harus mempertimbangkan berbagai faktor, seperti tipe data yang ditangani, skalabilitas, kinerja, konsistensi, dan kompleksitasnya. Misalnya, database relasional umumnya lebih baik untuk aplikasi yang memerlukan konsistensi data yang ketat dan kueri yang kompleks, sedangkan database NoSQL lebih cocok untuk proyek yang menangani data tidak terstruktur dalam jumlah besar atau memerlukan skalabilitas tinggi.
