# Mendalami Database Sharding

Seiring dengan meningkatnya popularitas sebuah aplikasi, jumlah pengguna aktif dan fitur-fitur tambahan yang dimasukkan juga akan bertambah. Pertumbuhan ini menyebabkan peningkatan data yang dihasilkan setiap hari, yang merupakan indikator positif dari perspektif bisnis.

Namun, hal ini juga bisa menimbulkan tantangan pada arsitektur aplikasi, terutama dalam hal skalabilitas basis data.

Basis data adalah komponen penting dari setiap aplikasi, tetapi juga merupakan salah satu komponen yang paling sulit untuk di-skala secara horizontal. Ketika aplikasi menerima peningkatan lalu lintas dan volume data, basis data dapat menjadi hambatan kinerja, yang mempengaruhi pengalaman pengguna.

Sharding adalah teknik yang mengatasi tantangan skalabilitas basis data secara horizontal. Teknik ini melibatkan pembagian basis data menjadi unit-unit yang lebih kecil dan lebih mudah dikelola yang disebut shard.

Dalam postingan ini, kita akan membahas dasar-dasar sharding basis data, menjelajahi berbagai pendekatannya, pertimbangan teknis, dan studi kasus dunia nyata yang menunjukkan bagaimana perusahaan-perusahaan telah mengimplementasikan sharding untuk menskalakan basis data mereka.

#### Apa itu Sharding?

Sharding adalah pola arsitektur yang mengatasi tantangan dalam mengelola dan melakukan query pada kumpulan data besar di basis data. Teknik ini melibatkan pembagian basis data besar menjadi bagian-bagian yang lebih kecil dan lebih mudah dikelola yang disebut shard.

Sharding membangun konsep partisi horizontal, yang melibatkan pembagian baris-baris dalam sebuah tabel menjadi beberapa tabel berdasarkan kunci partisi. Tabel-tabel ini dikenal sebagai partisi. Distribusi data antar partisi mengurangi usaha yang diperlukan untuk melakukan query dan manipulasi data.

Berikut adalah diagram yang menggambarkan contoh partisi horizontal:

<figure><img src="../.gitbook/assets/image (103).png" alt=""><figcaption><p>Partisi Horizontal</p></figcaption></figure>

Sharding basis data mengambil partisi horizontal ke tingkat berikutnya. Sementara partisi menyimpan semua kelompok data dalam komputer yang sama, sharding mendistribusikannya ke berbagai komputer atau node. Pendekatan ini memungkinkan skalabilitas dan kinerja yang lebih baik dengan memanfaatkan sumber daya dari banyak mesin.

Perlu dicatat bahwa terminologi yang digunakan untuk sharding berbeda-beda pada setiap basis data.

* Di MongoDB, partisi disebut shard.
* Couchbase menggunakan istilah vBucket untuk mewakili shard.
* Cassandra menyebut shard sebagai vNode.

Meskipun ada perbedaan dalam terminologi, konsep dasar yang mendasarinya tetap sama: membagi data menjadi unit yang lebih kecil dan mudah dikelola untuk meningkatkan kinerja query dan skalabilitas.

#### Manfaat Sharding Basis Data

Sharding basis data menawarkan beberapa manfaat utama:

1. **Skalabilitas:** Motivasi utama di balik sharding adalah mencapai skalabilitas. Dengan mendistribusikan kumpulan data besar ke beberapa shard, beban query dapat disebar ke beberapa node. Untuk query yang beroperasi pada satu shard, setiap node dapat secara independen mengeksekusi query untuk data yang ditugaskan padanya. Selain itu, shard baru dapat ditambahkan secara dinamis saat runtime tanpa perlu mematikan aplikasi untuk pemeliharaan.
2. **Kinerja yang Ditingkatkan:** Mengambil data dari satu basis data besar bisa memakan waktu lama. Query harus mencari melalui sejumlah besar baris untuk menemukan data yang diperlukan. Sebaliknya, shard berisi subset baris yang lebih kecil dibandingkan seluruh basis data. Ruang pencarian yang lebih kecil ini menghasilkan pengambilan data yang lebih cepat, karena query memiliki lebih sedikit baris untuk diproses.
3. **Ketersediaan:** Dalam arsitektur basis data monolitik, jika node yang menghosting basis data gagal, aplikasi yang bergantung juga mengalami downtime. Sharding basis data mengurangi risiko ini dengan mendistribusikan data ke beberapa node. Dalam kasus kegagalan node, aplikasi dapat terus beroperasi menggunakan shard yang tersisa.

#### Sharding dan Replikasi

Sharding sering digunakan bersama replikasi untuk mencapai ketersediaan tinggi dan toleransi kesalahan dalam sistem basis data terdistribusi.

Replikasi melibatkan pembuatan beberapa salinan data dan menyimpannya di node yang berbeda. Dalam model replikasi pemimpin-pengikut, satu node bertindak sebagai pemimpin dan menangani operasi tulis, sementara node pengikut mereplikasi data pemimpin dan menangani operasi baca.

Dengan mereplikasi setiap shard ke beberapa node, sistem memastikan bahwa data tetap dapat diakses bahkan jika node individu gagal. Sebuah node dapat menyimpan beberapa shard, yang masing-masing dapat menjadi pemimpin atau pengikut dalam model replikasi pemimpin-pengikut.

Berikut adalah diagram yang menggambarkan pengaturan di mana pemimpin setiap shard ditugaskan ke satu node, dan pengikutnya didistribusikan ke node lain:

<figure><img src="../.gitbook/assets/image (105).png" alt=""><figcaption><p>Sharding dan Replikasi</p></figcaption></figure>

Dalam pengaturan ini, sebuah node dapat secara bersamaan berfungsi sebagai pemimpin untuk beberapa partisi dan pengikut untuk yang lain. Arsitektur terdistribusi ini memungkinkan sistem untuk mempertahankan ketersediaan data dan ketahanan dalam kasus kegagalan node atau gangguan jaringan.

#### Jenis-Jenis Sharding

Tujuan utama dari sharding basis data adalah untuk mendistribusikan data dan beban query secara merata ke beberapa node.

Namun, jika partisi data tidak seimbang, beberapa shard mungkin akan menangani jumlah data atau query yang jauh lebih tinggi dibandingkan yang lain. Skenario ini dikenal sebagai shard yang miring, dan mengurangi manfaat sharding.

Dalam kasus ekstrim, strategi sharding yang buruk dapat menghasilkan satu shard yang menanggung seluruh beban sementara shard lainnya tetap menganggur.

Situasi ini disebut sebagai hot spot, di mana satu node menjadi kewalahan dengan beban yang sangat tinggi.

Untuk mengurangi risiko shard yang miring dan hot spot, penting untuk memilih strategi sharding yang tepat yang memastikan distribusi data dan query yang merata di seluruh shard.

Mari kita memahami beberapa strategi sharding yang umum digunakan:

**Sharding Berdasarkan Rentang**

Sharding berdasarkan rentang adalah teknik yang membagi baris basis data berdasarkan rentang nilai.

Dalam pendekatan ini, setiap shard diberi rentang kunci yang kontinu, mulai dari nilai minimum hingga nilai maksimum. Kunci dalam setiap shard dipertahankan dalam urutan yang terurut untuk memungkinkan pemindaian rentang yang efisien.

Untuk menggambarkan konsep ini, mari kita pertimbangkan basis data produk yang menyimpan informasi produk.

Sharding berdasarkan rentang dapat diterapkan untuk membagi basis data menjadi shard yang berbeda berdasarkan rentang harga produk. Misalnya, satu shard dapat menyimpan semua produk dalam rentang harga $0 hingga $75, sementara shard lain dapat berisi produk dalam rentang harga $76 hingga $150.

Perlu dicatat bahwa rentang kunci tidak harus memiliki jarak yang sama. Dalam aplikasi dunia nyata, distribusi data mungkin tidak seragam, dan rentang kunci dapat disesuaikan sesuai untuk mencapai distribusi data yang seimbang di seluruh shard.

Namun, sharding berdasarkan rentang memiliki potensi kelemahan.

Pola akses tertentu dapat menyebabkan terbentuknya hot spot. Misalnya, jika sebagian besar produk dalam basis data berada dalam rentang harga tertentu, shard yang bertanggung jawab untuk menyimpan rentang tersebut dapat mengalami beban yang jauh lebih tinggi, sementara shard lainnya tetap tidak terpakai.

**Sharding Berdasarkan Kunci atau Hash**

Sharding berdasarkan kunci, juga dikenal sebagai sharding berdasarkan hash, adalah teknik yang menetapkan kunci tertentu ke shard menggunakan fungsi hash.

Fungsi hash yang dirancang dengan baik memainkan peran penting dalam mencapai distribusi kunci yang seimbang. Alih-alih menetapkan rentang kunci ke setiap shard, sharding berdasarkan hash menetapkan rentang hash ke setiap shard. Consistent Hashing adalah salah satu teknik yang sering digunakan untuk mengimplementasikan sharding berdasarkan hash.

Berikut adalah diagram yang menggambarkan konsep dasar sharding berdasarkan kunci atau hash:

<figure><img src="../.gitbook/assets/image (107).png" alt=""><figcaption><p>Shard By Has Key</p></figcaption></figure>

Salah satu kelebihan utama dari sharding berdasarkan hash adalah kemampuannya untuk mendistribusikan kunci secara adil di antara shard. Dengan menerapkan fungsi hash pada kunci, teknik ini membantu mengurangi risiko hot spot.

Namun, sharding berdasarkan hash memiliki trade-off. Dengan menggunakan hash dari kunci alih-alih kunci itu sendiri, kita kehilangan kemampuan untuk melakukan query rentang yang efisien. Hal ini karena kunci yang berdekatan mungkin tersebar di berbagai partisi, dan urutan alami mereka hilang dalam proses tersebut.

Perlu dicatat bahwa meskipun sharding berdasarkan hash membantu mengurangi hot spot, teknik ini tidak dapat menghilangkannya sepenuhnya. Dalam kasus ekstrim di mana semua operasi baca dan tulis terkonsentrasi pada satu kunci, semua permintaan masih mungkin diarahkan ke partisi yang sama. Misalnya, pada situs media sosial, pengguna selebriti dapat memposting konten yang menghasilkan volume tulis yang besar ke kunci yang sama.

**Sharding Berdasarkan Direktori**

Sharding berdasarkan direktori adalah pendekatan yang mengandalkan tabel pencarian untuk menentukan distribusi catatan di seluruh shard.

Tabel pencarian berfungsi sebagai direktori atau buku alamat, memetakan hubungan antara data dan shard spesifik di mana data tersebut berada. Tabel ini disimpan terpisah dari shard itu sendiri.

Berikut adalah diagram yang menggambarkan konsep sharding berdasarkan direktori, menggunakan field "Lokasi" sebagai kunci shard:

<figure><img src="../.gitbook/assets/image (108).png" alt=""><figcaption><p>Sharding Berdasarkan Direktori</p></figcaption></figure>

Salah satu kelebihan utama dari sharding berdasarkan direktori adalah fleksibilitasnya dibandingkan strategi sharding lainnya. Teknik ini memungkinkan kontrol yang lebih besar terhadap penempatan data di seluruh shard, karena pemetaan antara data dan shard secara eksplisit didefinisikan dalam tabel pencarian.

Namun, sharding berdasarkan direktori juga memiliki kelemahan signifikan: teknik ini sangat bergantung pada tabel pencarian. Masalah atau kegagalan terkait tabel pencarian dapat mempengaruhi kinerja dan ketersediaan basis data secara keseluruhan.

#### Faktor yang Perlu Dipertimbangkan Saat Memilih Kunci Shard

Memilih kunci shard yang sesuai sangat penting untuk mengimplementasikan strategi sharding yang efektif. Desainer basis data harus mempertimbangkan beberapa faktor kunci saat membuat keputusan ini:

* **Kardinalitas:** Kardinalitas mengacu pada jumlah kemungkinan nilai yang dapat dimiliki oleh kunci shard. Kardinalitas menentukan jumlah maksimum shard yang dapat dibuat. Misalnya, jika field data boolean dipilih sebagai kunci shard, sistem akan terbatas pada dua shard saja. Untuk memaksimalkan manfaat dari skalabilitas horizontal, disarankan untuk memilih kunci shard dengan kardinalitas tinggi.
* **Frekuensi:** Frekuensi kunci shard menggambarkan seberapa sering nilai kunci shard tertentu muncul dalam kumpulan data. Jika sebagian besar catatan hanya mengandung subset dari kemungkinan nilai kunci shard, shard yang bertanggung jawab untuk menyimpan subset tersebut mungkin menjadi hot spot. Misalnya, jika basis data situs web kebugaran menggunakan usia sebagai kunci shard, sebagian besar catatan mungkin berakhir di shard yang mengandung pelanggan berusia antara 30 dan 45 tahun, yang mengarah pada distribusi data yang tidak merata.
* **Perubahan Monoton:** Perubahan monoton mengacu pada nilai kunci shard yang meningkat atau menurun seiring waktu untuk catatan tertentu. Jika kunci shard didasarkan pada nilai yang meningkat atau menurun secara monoton, hal ini dapat menghasilkan shard yang tidak seimbang. Pertimbangkan skema sharding untuk basis data yang menyimpan komentar pengguna. Shard A menyimpan data untuk pengguna dengan kurang dari 10 komentar. Shard B menyimpan data untuk pengguna dengan 11-20 komentar. Shard C menyimpan data untuk pengguna dengan lebih dari 30 komentar. Seiring waktu, saat pengguna terus menambahkan komentar, mereka akan berangsur-angsur berpindah ke Shard C, membuatnya lebih tidak seimbang dibandingkan Shard A dan B.

#### Menyeimbangkan Kembali Shard

Seiring waktu, basis data mengalami berbagai perubahan yang memerlukan redistribusi data dan beban kerja di seluruh node. Perubahan ini meliputi:

* Peningkatan throughput query memerlukan sumber daya CPU tambahan.
* Pertumbuhan ukuran dataset membutuhkan lebih banyak kapasitas penyimpanan.
* Kegagalan mesin tertentu mengakibatkan mesin lain mengambil alih tanggung jawabnya.

Semua skenario ini memiliki tema umum: kebutuhan untuk memindahkan data dan permintaan dari satu node ke node lain dalam kluster. Proses ini dikenal sebagai penyeimbangan kembali shard.

Penyeimbangan kembali shard bertujuan untuk mencapai beberapa tujuan utama:

1. Distribusi Beban yang Adil: Setelah proses penyeimbangan kembali, beban kerja harus didistribusikan secara merata di antara node dalam kluster.
2. Gangguan Minimal: Basis data harus terus menerima operasi baca dan tulis selama proses penyeimbangan kembali.
3. Pergerakan Data yang Efisien: Jumlah data yang dipindahkan antara node harus diminimalkan.

Mempertimbangkan tujuan ini, beberapa pendekatan dapat digunakan untuk penyeimbangan kembali shard, masing-masing dengan trade-off dan pertimbangan tersendiri.

**Jumlah Shard Tetap**

Dalam konfigurasi partisi tetap, jumlah shard ditentukan ketika basis data pertama kali diatur dan biasanya tetap tidak berubah setelahnya.

Misalnya, pertimbangkan basis data yang berjalan pada kluster 10 node. Basis data ini dapat dibagi menjadi 100 shard, dengan 10 shard ditugaskan ke setiap node. Total jumlah shard (100 dalam hal ini) tetap tetap.

Jika node baru ditambahkan ke kluster, sistem dapat menyeimbangkan kembali shard dengan memigrasikan beberapa shard dari node yang ada ke node baru untuk mempertahankan distribusi yang adil.

Berikut adalah diagram yang menggambarkan konsep partisi tetap:

<figure><img src="../.gitbook/assets/image (109).png" alt=""><figcaption><p>Partisi Tetap</p></figcaption></figure>

Perlu dicatat bahwa dalam pendekatan ini, baik jumlah shard maupun penugasan kunci ke shard tidak berubah. Hanya shard yang dipindahkan di antara node selama proses penyeimbangan kembali.

Namun, pendekatan partisi tetap menghadirkan tantangan dalam memilih jumlah shard yang sesuai jika ukuran total data sangat bervariasi.

Memutuskan ukuran shard tunggal juga memerlukan beberapa pertimbangan:

* Jika shard terlalu besar, penyeimbangan kembali dan pemulihan dari kegagalan node bisa memakan waktu dan sumber daya yang besar.
* Di sisi lain, jika shard terlalu kecil, terdapat overhead yang meningkat dalam pemeliharaan dan pengelolaan shard.

**Shard Dinamis**

Sharding dinamis adalah pendekatan yang menyesuaikan jumlah shard berdasarkan total volume data yang disimpan dalam basis data.

Ketika kumpulan data relatif kecil, sharding dinamis mempertahankan jumlah shard yang rendah, meminimalkan overhead yang terkait dengan manajemen dan pemeliharaan shard.

Seiring pertumbuhan kumpulan data dan mencapai ukuran yang signifikan, sharding dinamis secara otomatis meningkatkan jumlah shard untuk mengakomodasi volume data yang berkembang. Ukuran setiap partisi biasanya dibatasi hingga ambang batas maksimum yang dapat dikonfigurasi.

Saat menambahkan shard baru, sistem mendistribusikan ulang sebagian data dari shard yang ada ke shard baru yang dibuat. Proses ini memastikan bahwa data tetap didistribusikan secara merata di semua shard.

Salah satu kelebihan utama dari sharding dinamis adalah fleksibilitasnya. Teknik ini dapat diterapkan pada strategi sharding berbasis rentang dan berbasis hash.

#### Routing Permintaan dalam Basis Data Sharded

Setelah sharding kumpulan data, pertimbangan paling kritis adalah menentukan bagaimana klien mengetahui node mana yang harus dihubungi untuk permintaan yang masuk.

Masalah ini menjadi menantang karena shard dapat di-rebalancing, dan penugasan shard ke node dapat berubah secara dinamis.

Ada tiga pendekatan utama untuk mengatasi tantangan ini:

1. **Node yang Sadar Shard:** Dalam pendekatan ini, klien dapat menghubungi node mana pun menggunakan load balancer round-robin. Jika node yang dihubungi memiliki shard yang relevan dengan permintaan, node tersebut dapat menangani permintaan secara langsung. Jika tidak, node tersebut meneruskan permintaan ke shard yang sesuai dan mengarahkan respons kembali ke klien.
2. **Lapisan Routing:** Dalam pendekatan ini, permintaan klien dikirim ke lapisan routing khusus yang menentukan node yang bertanggung jawab untuk menangani setiap permintaan. Lapisan routing meneruskan permintaan ke node yang sesuai dan mengembalikan respons ke klien. Aplikasi berkomunikasi dengan lapisan routing, bukan langsung dengan node.
3. **Klien yang Sadar Shard:** Dalam pendekatan ini, klien mengetahui distribusi shard di seluruh node. Klien pertama-tama menghubungi server konfigurasi untuk memperoleh pemetaan shard-ke-node saat ini. Dengan pengetahuan ini, klien kemudian dapat langsung menghubungi node yang sesuai untuk setiap permintaan.

Berikut adalah diagram yang menggambarkan tiga pendekatan tersebut:

<figure><img src="../.gitbook/assets/image (110).png" alt=""><figcaption><p>Routing Permintaan</p></figcaption></figure>

Terlepas dari pendekatan yang dipilih, ada keputusan umum yang harus diambil: bagaimana cara menjaga komponen yang membuat keputusan routing tetap diperbarui tentang pemetaan shard-ke-node.

Basis data yang berbeda menggunakan mekanisme yang berbeda untuk mencapai ini:

* LinkedIn’s Espresso menggunakan Helix untuk manajemen kluster, yang mengandalkan Zookeeper untuk menyimpan informasi konfigurasi.
* MongoDB memanfaatkan server konfigurasi terpisah dan lapisan routing khusus.
* Cassandra menggunakan protokol gossip antar node untuk menyebarkan perubahan pemetaan di seluruh node.

#### Arsitektur Sharding MongoDB - Studi Kasus

Setelah menjelajahi konsep sharding, mari kita lihat bagaimana basis data populer mengimplementasikan sharding dalam praktik.

Kita akan menggunakan MongoDB, salah satu basis data dokumen yang paling banyak digunakan, sebagai contoh. Arsitektur sharding MongoDB menunjukkan bagaimana komponen yang telah kita bahas (shard, routing, dan konfigurasi) bekerja sama untuk menciptakan basis data terdistribusi yang dapat diskalakan.

Arsitektur sharding MongoDB mengandalkan kluster server yang saling terhubung, juga dikenal sebagai node. Kluster ini, yang disebut sebagai kluster sharded, terdiri dari tiga komponen utama:

1. **Shard**
2. **Mongos Router**
3. **Config Servers**

Berikut adalah diagram yang menunjukkan hubungan antara ketiga komponen ini:

<figure><img src="../.gitbook/assets/image (111).png" alt=""><figcaption><p>Arsitektur Sharding MongoDB</p></figcaption></figure>

**Shard**

Shard adalah subset dari data dalam kluster.

Setiap shard diimplementasikan sebagai set replika, yang merupakan kluster dari instance MongoDB individu.

Dengan menerapkan setiap shard sebagai set replika, MongoDB memungkinkan replikasi data dalam shard. Pilihan desain ini memastikan ketersediaan tinggi dan toleransi kesalahan.

**Mongos Router**

Mongos Router adalah pusat dari kluster. Komponen ini berfungsi sebagai titik masuk utama yang mengatur interaksi antara aplikasi klien dan shard.

Mongos Router melakukan dua fungsi penting:

* **Query Routing dan Load Balancing:** Router bertindak sebagai titik masuk tunggal untuk aplikasi klien. Router menerima query yang masuk dan mengarahkan mereka ke shard yang sesuai berdasarkan kunci shard dan distribusi data.
* **Metadata Caching:** Router juga mempertahankan cache metadata yang memetakan data ke shard yang sesuai. Router mengambil metadata

ini dari server konfigurasi dan menyimpannya secara lokal untuk kinerja yang lebih baik.

**Config Servers**

Config Server menyimpan dan mengelola metadata untuk seluruh kluster.

Metadata yang disimpan dalam server konfigurasi mencakup detail seperti:

* **Konfigurasi Shard:** Informasi tentang setiap shard, termasuk nama, host, dan port.
* **Distribusi Chunk:** Pemetaan chunk data ke shard tertentu, memungkinkan pengambilan data yang efisien.
* **Status Kluster:** Status saat ini dan kesehatan kluster sharded, termasuk status shard individu dan instance Mongos.

Instance Mongos sangat mengandalkan server konfigurasi untuk membuat keputusan routing yang tepat.

#### Studi Kasus Industri Dunia Nyata dari Sharding

Mari kita lihat beberapa studi kasus dunia nyata dari organisasi yang menggunakan sharding untuk menskalakan basis data mereka dan tantangan yang mereka hadapi.

**Notion**

Pada pertengahan 2020, Notion, platform produktivitas dan kolaborasi yang populer, menghadapi ancaman eksistensial.

Perusahaan telah mengandalkan basis data PostgreSQL monolitik selama lima tahun, yang mendukung pertumbuhan besar-besaran melalui beberapa urutan besarnya. Namun, seiring dengan terus berkembangnya Notion secara cepat, basis data mengalami kesulitan untuk mengimbangi.

Beberapa indikator menunjukkan tekanan yang meningkat pada basis data:

* Lonjakan CPU yang sering pada node basis data.
* Migrasi yang tidak aman.
* Volume permintaan on-call yang tinggi.

Selain itu, dua masalah utama muncul ke permukaan:

1. **VACUUM Stalling:** Proses VACUUM PostgreSQL, yang bertanggung jawab untuk membersihkan dan mengklaim kembali ruang disk, mulai terhenti. Hal ini berarti basis data tidak secara efektif mengelola penyimpanannya, yang mengarah pada penurunan kinerja.
2. **TXID Wraparound:** Notion menghadapi ancaman eksistensial dalam bentuk TXID wraparound. Masalah ini terjadi ketika penghitung ID transaksi di PostgreSQL mencapai nilai maksimum dan berbalik menjadi nol. Jika tidak diatasi, masalah ini dapat menyebabkan korupsi data dan kegagalan.

Dihadapkan dengan tantangan ini, tim teknik Notion memutuskan untuk mengimplementasikan sharding basis data.

Sementara mereka menjajaki scaling vertikal sebagai opsi, teknik ini terbukti sangat mahal pada skala mereka.

Namun, untuk memastikan keberhasilan proses sharding, Notion perlu mengembangkan strategi sharding yang baik.

Beberapa pertimbangan utama termasuk:

1. **Memilih Tabel untuk Di-Shard** Model data Notion berputar di sekitar konsep blok, di mana setiap item pada halaman Notion diwakili sebagai blok. Blok yang lebih besar dapat terdiri dari blok yang lebih kecil, membentuk struktur hierarkis.Tabel Block muncul sebagai kandidat utama untuk di-shard karena signifikansinya dalam model data Notion.Namun, tabel Block memiliki ketergantungan pada tabel lain, seperti Workspace dan Discussions. Untuk mempertahankan integritas data dan menghindari query cross-shard yang kompleks (yang dapat mempengaruhi kinerja), Notion memutuskan untuk shard semua tabel yang berhubungan secara transitif dengan tabel Block.
2. **Memilih Kunci Sharding** Kunci sharding yang baik sangat penting untuk sharding yang efisien.Karena Notion adalah produk berbasis tim di mana sebuah Blok milik Workspace, mereka memutuskan untuk menggunakan ID Workspace sebagai kunci partisi.Keputusan ini bertujuan untuk meminimalkan join cross-shard saat mengambil data, karena blok yang terkait dengan Workspace yang sama akan disimpan dalam shard yang sama.
3. **Jumlah Shard** Menentukan jumlah shard yang optimal adalah keputusan penting lainnya karena secara langsung berdampak pada skalabilitas Notion. Tujuannya adalah untuk mengakomodasi volume data yang ada sambil mempertimbangkan proyeksi penggunaan selama 2 tahun.Setelah analisis, Notion tiba pada konfigurasi berikut:480 shard didistribusikan di 32 node, menghasilkan 15 shard per node. Pendekatan ini sesuai dengan strategi jumlah shard tetap, di mana jumlah shard ditentukan sebelumnya.Batas penyimpanan maksimal 500 GB per tabel.

**Pelajaran yang Dipetik** Pada akhirnya, Notion berhasil melakukan migrasi ke basis data yang di-shard. Beberapa pelajaran berharga yang mereka pelajari dalam proses tersebut adalah sebagai berikut:

* Optimalisasi prematur itu buruk. Namun, menunggu terlalu lama sebelum melakukan sharding juga dapat menciptakan kendala.
* Mengupayakan migrasi tanpa downtime adalah penting untuk pengalaman pengguna yang baik.
* Memilih kunci sharding yang tepat adalah bahan terpenting untuk hasil yang menguntungkan.

**Discord**

Discord, platform sosial untuk pesan instan, memiliki masalah menarik dengan sharding basis datanya yang layak untuk dibahas.

Pada tahun 2017, Discord menyimpan miliaran pesan dari pengguna di seluruh dunia dan memutuskan untuk bermigrasi dari MongoDB ke Cassandra dalam upaya mencari solusi basis data yang dapat diskalakan, toleran kesalahan, dan pemeliharaannya rendah.

Seiring dengan pertumbuhan basis pengguna Discord dan volume pesan selama beberapa tahun berikutnya, mereka menemukan diri mereka menyimpan triliunan pesan. Kluster basis data mereka berkembang dari 12 menjadi 177 node Cassandra. Namun, meskipun jumlah node meningkat, kluster tersebut menghadapi masalah kinerja yang parah.

Meskipun beberapa faktor berkontribusi pada penurunan kinerja, alasan utamanya adalah strategi sharding Discord.

Dalam skema basis data mereka, setiap pesan milik saluran tertentu dan disimpan dalam tabel yang disebut "messages." Tabel messages dipartisi berdasarkan dua field: "channel\_id" dan "bucket." Field "bucket" mewakili jendela waktu statis di mana pesan berada.

Implikasinya adalah bahwa semua pesan dalam saluran dan periode tertentu (bucket) disimpan pada partisi yang sama. Akibatnya, server Discord yang populer dengan ratusan ribu pengguna aktif dapat menghasilkan volume pesan yang sangat besar dalam waktu singkat, yang membebani shard tertentu.

Karena struktur LSM-Tree Cassandra membuat operasi baca umumnya lebih mahal dibandingkan tulis, baca bersamaan dalam saluran Discord dengan volume tinggi dapat menciptakan hot spot pada shard tertentu. Hot spot ini menyebabkan masalah latensi yang berkelanjutan di seluruh kluster basis data, yang pada akhirnya mempengaruhi pengalaman pengguna akhir.

Untuk mengatasi tantangan ini, Discord melakukan beberapa perubahan pada arsitekturnya, termasuk:

1. **Migrasi ke ScyllaDB:** Discord bermigrasi dari Cassandra ke ScyllaDB, basis data yang kompatibel dengan Cassandra yang menjanjikan kinerja dan isolasi sumber daya yang lebih baik.
2. **Optimasi Akses Data:** Discord memperkenalkan layanan perantara yang disebut layanan data antara API dan kluster basis data mereka. Layanan ini menerapkan penggabungan permintaan dan routing berbasis hash yang konsisten untuk meminimalkan beban pada basis data dan mendistribusikan lalu lintas lebih merata di seluruh shard.

Pengalaman Discord menunjukkan bahwa strategi sharding yang baik di bawah pola akses tertentu dapat menciptakan masalah kinerja yang tidak terduga dalam aplikasi. Dengan mengoptimalkan strategi sharding dan pola akses data mereka, Discord berhasil mengatasi masalah hot spot dan meningkatkan kinerja serta skalabilitas sistem penyimpanan pesan mereka.

#### Ringkasan

Dalam artikel ini, kita telah mengeksplorasi sharding basis data secara mendetail, mencakupnya dari berbagai aspek.

Berikut adalah ringkasan poin-poin utama:

* **Dasar-dasar Sharding:** Sharding basis data adalah teknik untuk menskalakan basis data secara horizontal dengan mempartisi ke beberapa node.
* **Strategi Sharding:** Ada tiga jenis utama strategi sharding: sharding berbasis rentang, berbasis kunci atau hash, dan berbasis direktori. Setiap strategi memiliki kelebihan dan kekurangan, dengan sharding berbasis hash yang paling umum digunakan karena kemampuannya untuk mendistribusikan data secara merata di seluruh shard.
* **Pemilihan Kunci Shard:** Desainer basis data harus mempertimbangkan faktor-faktor seperti kardinalitas, frekuensi, dan perubahan monoton saat memilih kunci shard. Kunci shard yang dipilih dengan baik sangat penting untuk memastikan distribusi yang merata dan meminimalkan hot spot.
* **Penyeimbangan Kembali Shard:** Basis data tidak statis dan terus berubah, yang mengakibatkan perlunya penyeimbangan kembali shard. Berbagai pendekatan seperti partisi tetap dan sharding dinamis dapat digunakan untuk menangani penyeimbangan kembali.
* **Routing Permintaan:** Ada beberapa pendekatan untuk mengarahkan permintaan ke shard yang sesuai: klien yang sadar shard, router sentral, dan node yang sadar shard.
* **Arsitektur Sharding MongoDB:** Arsitektur ini terdiri dari router sentral dan server konfigurasi independen untuk merutekan permintaan ke shard yang benar.
* **Studi Kasus Dunia Nyata:** Perjalanan Notion dari basis data monolitik ke arsitektur sharded menyoroti pentingnya sharding untuk mendukung pertumbuhan cepat. Pengalaman Discord menunjukkan bagaimana strategi sharding dapat menghasilkan hot spot karena pola akses tertentu.

**Referensi:**

* [How Discord Stores Trillions of Messages?](https://discord.com/blog/how-discord-stores-trillions-of-messages)
* [Herding elephants: Lessons learned from sharding Postgres at Notion](https://www.notion.so/blog/sharding-postgres-at-notion)
* [Sharding in MongoDB](https://www.mongodb.com/resources/products/capabilities/sharding)
