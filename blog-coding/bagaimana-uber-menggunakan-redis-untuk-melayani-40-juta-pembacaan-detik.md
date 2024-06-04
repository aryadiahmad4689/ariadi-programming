# Bagaimana Uber Menggunakan Redis untuk Melayani 40 Juta Pembacaan/Detik?

Pada tahun 2020, Uber meluncurkan database terdistribusi internal mereka yang diberi nama Docstore.

Itu dibangun di atas MySQL dan mampu menyimpan puluhan petabyte data sambil melayani puluhan juta permintaan per detik.

Selama bertahun-tahun, Docstore diadopsi oleh semua vertikal bisnis di Uber untuk membangun layanan mereka. Sebagian besar aplikasi ini memerlukan latensi rendah, kinerja lebih tinggi, dan skalabilitas dari database, sekaligus mendukung beban kerja yang lebih tinggi.

## Tantangan Pembacaan Data Sebuah Database

Setiap database menghadapi tantangan ketika berhadapan dengan aplikasi yang memerlukan akses baca latensi rendah dengan desain yang sangat skalabel.

Beberapa tantangan tersebut adalah sebagai berikut:

1. **Batasan Kecepatan Disk**: Kecepatan pengambilan data dari disk memiliki batasan maksimal. Kalian tidak bisa meningkatkan kinerja hanya dengan menyempurnakan model data dan kueri aplikasi untuk mengurangi waktu tunggu.
2. **Keterbatasan Penskalaan Vertikal**: Menambah sumber daya dengan beralih ke server yang lebih canggih bisa membantu, tetapi hanya sampai titik tertentu. Lama-kelamaan, sistem database itu sendiri akan menjadi penghambat.
3. **Kompleksitas Penskalaan Horizontal**: Membagi database menjadi beberapa partisi bisa jadi solusi, tetapi ini menambah kompleksitas operasional dan tidak sepenuhnya mengatasi isu seperti partisi yang kelebihan beban.
4. **Biaya:** Strategi penskalaan vertikal dan horizontal memerlukan biaya besar dalam jangka panjang. Sebagai referensi, biaya dikalikan 6X untuk menangani tiga node stateful di dua wilayah.

Untuk mengatasi tantangan ini, layanan mikro biasanya menggunakan caching.&#x20;

Uber mulai menawarkan Redis sebagai solusi caching terdistribusi untuk berbagai tim. Mereka mengikuti pola desain caching yang khas di mana layanan menulis ke database dan cache sambil melayani pembacaan langsung dari cache.

Diagram di bawah menunjukkan pola ini:

<figure><img src="../.gitbook/assets/image (99).png" alt=""><figcaption><p>Cache Awal Uber</p></figcaption></figure>

Namun, pola caching normal di mana layanan menangani pengelolaan cache memiliki beberapa masalah pada skala Uber.

* Setiap tim harus mengelola cluster cache Redisnya sendiri.
* Logika pembatalan cache diduplikasi di beberapa layanan mikro dan ada kemungkinan penyimpangan.
* Layanan harus menjaga replikasi cache agar tetap aktif jika terjadi kegagalan wilayah.

Poin utamanya adalah setiap tim yang membutuhkan caching harus mengeluarkan banyak upaya untuk membangun dan memelihara solusi caching khusus.

Untuk menghindari hal ini, Uber memutuskan untuk membangun solusi caching terintegrasi yang dikenal sebagai CacheFront.

### Rancang Sasaran dengan CacheFront

Saat membangun CacheFront, Uber memikirkan beberapa tujuan desain penting:

1. **Kurangi Kebutuhan Penskalaan**: Tujuannya adalah untuk mengurangi kebutuhan memperbesar atau menambah server agar bisa menangani permintaan dengan waktu tanggapan yang cepat.
2. **Perbaikan dan Stabilisasi Latensi**: Meningkatkan kecepatan respons pada umumnya (P50 dan P99) dan mengurangi lonjakan waktu tanggapan yang tiba-tiba.
3. **Kurangi Penggunaan Sumber Daya**: Mengurangi jumlah sumber daya yang dibutuhkan oleh lapisan database, seperti memori dan CPU.
4. **Standardisasi Solusi Caching**: Menggantikan berbagai solusi penyimpanan sementara yang dibuat khusus oleh tiap tim dengan satu solusi umum, memindahkan tanggung jawab pemeliharaan dan dukungan Redis ke tim Docstore.
5. **Transparansi Caching**: Membuat sistem penyimpanan sementara tidak terlihat oleh layanan yang menggunakan sistem tersebut, memungkinkan tim untuk fokus pada pengembangan logika bisnis mereka.
6. **Pisahkan Caching dari Skema Partisi**: Membuat solusi penyimpanan sementara yang tidak terikat dengan skema partisi database utama untuk menghindari masalah partisi yang kelebihan beban.
7. **Dukung Penskalaan Horizontal yang Hemat Biaya**: Mendukung kemampuan untuk meningkatkan kapasitas penyimpanan sementara dengan menambah server yang lebih terjangkau dan efisien biaya.

### Arsitektur Tingkat Tinggi dengan CacheFront

Untuk mendukung tujuan desain ini, Uber menciptakan solusi caching terintegrasi yang terkait dengan Docstore.

Diagram di bawah menunjukkan arsitektur tingkat tinggi Docstore bersama dengan CacheFront:

<figure><img src="../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

#### Menyerahkan Bacaan Cache

CacheFront menggunakan strategi penyingkiran cache atau penyisihan saat membaca.

Langkah-langkah di bawah ini menjelaskan cara kerjanya:

1. **Penerimaan Permintaan**: Ketika ada permintaan untuk mengakses data, lapisan mesin kueri (Query Engine) menerima permintaan ini. Permintaan bisa berupa meminta satu atau lebih baris data.
2. **Mencari di Redis**: Mesin kueri terlebih dahulu mencoba mencari baris data yang diminta di dalam Redis, yaitu sistem penyimpanan cepat yang digunakan untuk mempercepat akses data.
3. **Mengirimkan Respons ke Pengguna**: Jika data ditemukan di Redis, data tersebut langsung dikirim ke pengguna. Ini membuat prosesnya cepat karena tidak perlu mencari data di tempat lain.
4. **Mengambil dari Database Jika Perlu**: Jika data tidak ditemukan di Redis, mesin kueri akan mencarinya di database. Dalam gambar, database ini digambarkan dengan MySQL yang memiliki satu pemimpin (Leader) dan beberapa pengikut (Follower).
5. **Memperbarui Redis**: Setelah data ditemukan di database, mesin kueri akan menyimpan data tersebut ke dalam Redis secara asinkron. Ini berarti pembaruan ke Redis dilakukan di belakang layar tanpa mengganggu pengguna.
6. **Streaming Data yang Tersisa**: Jika ada data lain yang masih perlu dikirim ke pengguna, data tersebut akan terus dikirim secara bertahap.

<figure><img src="../.gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>

### Hasil dan Kesimpulan

Proyek Uber yang mengimplementasikan cache Redis terintegrasi dengan Docstore cukup berhasil.

Mereka menciptakan solusi caching transparan yang terukur dan berhasil meningkatkan latensi, mengurangi beban, dan menurunkan biaya.

Berikut beberapa statistik yang menunjukkan hasilnya:

1. **Perbaikan Kecepatan Layanan**: Kecepatan layanan meningkat secara signifikan, dengan pengurangan waktu tunggu hingga 75% untuk sebagian besar permintaan, dan lebih dari 67% untuk permintaan yang sangat lambat. Ini juga berhasil mengurangi tiba-tiba lonjakan waktu tunggu.
2. **Konsistensi Data Tinggi**: Metode pembatalan cache yang mereka gunakan memastikan bahwa data yang tersimpan tetap akurat dan konsisten hampir 100% dari waktu, yang penting untuk menjaga kualitas layanan.
3. **Skalabilitas dan Keandalan**: Sistem mereka mampu menangani lebih dari 6 juta permintaan baca per detik dengan tingkat keberhasilan mencapai data yang diinginkan (cache hit) 99% dari waktu, bahkan saat beralih ke server cadangan di lokasi lain jika ada masalah.
4. **Pengurangan Biaya**: Biaya operasional turun drastis. Untuk kasus yang sama dengan 6 juta pembacaan per detik, sebelumnya dibutuhkan sekitar 60 ribu inti CPU. Namun, dengan menggunakan CacheFront, mereka hanya membutuhkan 3 ribu inti Redis, yang jauh lebih sedikit.
5. **Kapasitas Besar**: Saat ini, CacheFront mampu menangani lebih dari 40 juta permintaan per detik dan jumlah ini terus bertambah setiap hari, menunjukkan betapa mampu dan efisiennya sistem ini.

**Referensi:**

* [Bagaimana Uber Melayani Lebih dari 40 juta permintaan per detik menggunakan cache terintegrasi?](https://www.uber.com/en-IN/blog/how-uber-serves-over-40-million-reads-per-second-using-an-integrated-cache/)
* [Penjelasan tentang fungsi Redis EVAL](https://redis.io/commands/eval/)
* [CacheFront Uber](https://www.infoq.com/news/2024/02/uber-cachefront/)
* [Redis Cache Selain Disederhanakan](https://redis.com/blog/redis-smart-cache)
