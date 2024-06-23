# Memahami Konsep Chaos Engineering

#### Menguji Perangkat Lunak di Lingkungan Produksi: Mengapa Tidak?

Bayangkan kita berada di awal tahun 2000-an, sebagai seorang pengembang dengan ide berani: menguji perangkat lunak bukan di lingkungan yang aman dan terkontrol, tetapi langsung di lingkungan produksi di mana pengguna nyata berinteraksi dengan sistem. Pada masa itu, ide ini mungkin akan mendapat tatapan aneh dari atasan kita. Namun kini, pengujian di dunia nyata tidak hanya diterima tetapi seringkali direkomendasikan.

Apa yang menyebabkan perubahan besar ini? Beberapa alasan utama mencuat. Sistem saat ini lebih kompleks dari sebelumnya, mendorong kita untuk berinovasi lebih cepat dan memastikan layanan kita andal dan kuat. Kemajuan teknologi cloud, mikroservis, dan sistem terdistribusi telah mengubah permainan. Kita harus menyesuaikan metode dan pola pikir kita sesuai dengan perkembangan ini.

Tujuan kita sekarang adalah membuat sistem yang dapat menangani apa saja—baik itu perlambatan atau gangguan besar. Masuklah Chaos Engineering.

#### Apa Itu Chaos Engineering?

Chaos Engineering adalah cara untuk menghadapi masalah tak terduga dalam pengembangan perangkat lunak dan menjaga sistem tetap berjalan. Ada yang berpikir bahwa server yang menjalankan aplikasi akan terus berjalan tanpa hambatan selamanya, sementara yang lain percaya bahwa masalah adalah bagian dari perjalanan dan downtime tidak bisa dihindari.

Chaos Engineering berada di tengah-tengah pandangan ini. Ini mengakui bahwa hal-hal bisa salah tetapi menegaskan bahwa kita bisa mengambil langkah-langkah untuk mencegah masalah ini mempengaruhi sistem dan kinerja aplikasi kita.

Pendekatan ini melibatkan eksperimen pada sistem produksi langsung untuk mengidentifikasi titik lemah dan area yang kurang andal. Ini tentang mengukur seberapa besar kepercayaan kita terhadap ketahanan sistem dan berupaya meningkatkan kepercayaan tersebut.

Namun, penting untuk dipahami bahwa menjadi 100% yakin tidak ada yang akan salah adalah tidak realistis. Melalui Chaos Engineering, kita secara sengaja memperkenalkan kejadian tak terduga untuk mengungkap kerentanan. Kejadian ini bisa bervariasi luas, seperti mematikan server secara acak, mengganggu pusat data, atau mengotak-atik load balancer dan replika aplikasi.

#### Definisi Chaos Engineering

Ada banyak cara untuk menggambarkan Chaos Engineering, tetapi berikut ini adalah definisi yang menangkap esensinya dengan baik, yang bersumber dari https://principlesofchaos.org/.

“Chaos Engineering adalah disiplin eksperimen pada sistem untuk membangun kepercayaan pada kemampuan sistem tersebut untuk bertahan dari kondisi turbulen di lingkungan produksi.”

#### Perbedaan Antara Performance Engineering dan Chaos Engineering

Saat kita berbicara tentang memastikan sistem berjalan dengan lancar, dua konsep sering muncul: performance engineering dan chaos engineering. Mari kita bahas apa yang membedakan keduanya dan bagaimana keduanya mungkin tumpang tindih.

Performance engineering adalah tentang menggunakan kombinasi alat, proses, dan teknologi untuk memantau kinerja sistem kita dan melakukan perbaikan terus-menerus. Ini termasuk mengadakan berbagai jenis pengujian seperti load, stress, dan endurance tests, semuanya bertujuan untuk meningkatkan kinerja aplikasi kita.

Sebaliknya, chaos engineering adalah tentang sengaja "merusak" sesuatu. Ya, ini termasuk stress testing, tetapi lebih tentang mengamati bagaimana sistem merespons di bawah tekanan tak terduga. Stress testing bisa dilihat sebagai bentuk eksperimen chaos. Jadi, satu cara untuk melihatnya adalah menganggap performance engineering sebagai subset dari chaos engineering atau sebaliknya, tergantung pada bagaimana kita menerapkan praktik-praktik ini.

#### Chaos Engineering dalam Praktik

Mari kita lihat contoh untuk lebih memahami chaos engineering. Bayangkan kita memiliki sistem dengan load balancer yang mengarahkan permintaan ke server web. Server ini kemudian terhubung ke layanan pembayaran, yang berinteraksi dengan API pihak ketiga dan layanan cache, semuanya berada di Availability Zone A. Jika layanan pembayaran gagal berkomunikasi dengan API pihak ketiga atau cache, permintaan harus dialihkan ke Availability Zone B untuk mempertahankan ketersediaan tinggi.

Pengaturan ini umum di platform e-commerce berbasis cloud, di mana layanan didistribusikan secara strategis di berbagai zona untuk meningkatkan ketahanan. Tantangannya adalah memastikan bahwa jika Zona A mengalami downtime, sistem dapat dengan mulus beralih ke Zona B. Chaos engineering memainkan peran penting di sini. Dengan sengaja menyuntikkan gangguan yang terkendali, tim dapat mengidentifikasi titik lemah, memperbaiki respons kegagalan, dan terus meningkatkan ketahanan dan ketersediaan sistem.

#### Langkah-Langkah Chaos Engineering

Chaos engineering bukan hanya tentang "merusak" sesuatu untuk melihat apa yang terjadi. Ini adalah pendekatan metodis yang bertujuan memperkuat sistem kita. Mari kita melalui enam langkah kunci dalam melakukan eksperimen chaos engineering.

1. **Formulasi Hipotesis** Ini adalah langkah awal. Membuat hipotesis adalah menebak dengan cerdas tentang perilaku sistem kita di bawah tekanan. Misalnya, kita mungkin berhipotesis bahwa jika layanan cache kita down, kita bisa mengalihkan permintaan ke zona cadangan untuk menjaga semuanya berjalan lancar. Penting untuk mendasarkan hipotesis kita pada pemahaman yang kuat tentang arsitektur dan dependensi sistem kita.
2. **Desain Eksperimen** Setelah kita memiliki hipotesis, kita merancang eksperimen untuk mengujinya. Langkah ini melibatkan perencanaan yang cermat untuk memastikan bahwa eksperimen kita terkendali dan dampaknya dapat diukur dengan akurat. Dalam contoh kita, eksperimen mungkin melibatkan mensimulasikan skenario di mana layanan cache di satu zona sengaja dinonaktifkan. Ini tentang mengatur panggung untuk gangguan yang terkendali yang meniru kondisi dunia nyata sedekat mungkin.
3. **Injeksi Chaos** Setelah merancang eksperimen kita, kita masuk ke fase injeksi chaos. Di sinilah kita dengan sengaja memperkenalkan gangguan yang direncanakan ke dalam sistem kita. Melanjutkan contoh kita, ini berarti mematikan layanan cache di zona yang ditentukan. Penting untuk memantau sistem dengan cermat selama fase ini untuk memastikan eksperimen tetap terkendali dan mencegah konsekuensi yang tidak diinginkan.
4. **Pengamatan Sistem (Monitoring & Logging)** Saat chaos terjadi, mengamati respons sistem adalah hal yang kritis. Alat pemantauan dan logging memungkinkan kita melacak perilaku sistem secara real-time dan mengumpulkan data untuk analisis. Langkah ini membantu kita mengumpulkan bukti tentang apakah sistem kita bereaksi sesuai harapan atau jika ada perilaku atau kegagalan yang tidak terduga.
5. **Analisis Perilaku Sistem** Dengan data di tangan, kita menganalisis bagaimana sistem mengatasi chaos. Analisis ini membantu kita mengidentifikasi kelemahan, celah ketahanan, dan area untuk perbaikan. Jika sistem kita gagal mengalihkan permintaan seperti yang dihipotesiskan, kita perlu memahami mengapa dan bagaimana kita bisa memperbaikinya. Langkah ini tentang mengubah pengamatan menjadi wawasan yang dapat ditindaklanjuti.
6. **Pembelajaran dan Iterasi** Akhirnya, kita menutup loop dengan pembelajaran dan iterasi. Wawasan yang diperoleh dari eksperimen kita menginformasikan perubahan dan perbaikan pada infrastruktur atau proses sistem kita. Ini adalah proses berulang dalam menerapkan pelajaran yang dipetik untuk membuat sistem kita lebih tangguh terhadap gangguan di masa depan.

#### Prinsip-Prinsip Chaos Engineering

Selain langkah-langkah melakukan eksperimen chaos engineering, prinsip-prinsip yang memandu memastikan bahwa pengujian ini efektif, aman, dan menghasilkan wawasan berharga. Berikut adalah beberapa prinsip dasar yang harus diikuti saat mempraktikkan chaos engineering:

1. **Ukur dalam Jangka Waktu yang Lebih Lama** Observasi jangka pendek mungkin tidak mengungkapkan dampak penuh dari chaos pada sistem kita. Penting untuk mengukur efeknya dalam jangka waktu yang panjang, karena masalah mungkin tidak muncul segera. Kadang-kadang, konsekuensi dari memperkenalkan chaos bisa memakan waktu berjam-jam atau bahkan berhari-hari untuk menjadi jelas. Prinsip ini memastikan bahwa kurangnya masalah langsung tidak menenangkan kita secara salah.
2. **Fokus pada Eksperimen yang Berbasis Hipotesis** Chaos engineering bukan tentang menyebabkan gangguan acak. Sebaliknya, ini berfokus pada pengujian hipotesis spesifik tentang bagaimana dan di mana sistem kita mungkin gagal. Sebelum memulai eksperimen apa pun, definisikan dengan jelas apa yang kita uji dan hasil apa yang kita harapkan. Pendekatan ini memastikan bahwa eksperimen memiliki tujuan dan bahwa hasilnya dapat ditindaklanjuti.
3. **Simulasikan Kejadian Dunia Nyata** Eksperimen chaos yang paling efektif mensimulasikan skenario yang bisa terjadi di dunia nyata. Ini termasuk kejadian seperti crash server, kegagalan hard drive, gangguan jaringan, dan kesalahan aplikasi. Melakukan eksperimen ini secara teratur atau terus-menerus untuk mempersiapkan sistem menghadapi gangguan nyata.
4. **Minimalkan Radius Ledakan** Memulai dari yang kecil adalah kunci untuk chaos engineering yang efektif. Dengan awalnya membatasi dampak (atau "radius ledakan") dari eksperimen, kita mengurangi risiko menyebabkan gangguan besar pada layanan. Pendekatan hati-hati ini memungkinkan kita mengukur ketahanan sistem tanpa membebani. Seiring kita mendapatkan kepercayaan pada kemampuan sistem dalam menangani gangguan, kita dapat secara bertahap memperluas cakupan eksperimen.
5. **Kemampuan Rollback** Kemampuan untuk cepat membalikkan perubahan sangat penting dalam chaos engineering. Meskipun direncanakan dengan hati-hati, eksperimen dapat menghasilkan hasil yang tak terduga. Rencana rollback yang kuat memastikan bahwa kita dapat dengan cepat mengembalikan sistem ke keadaan stabil jika eksperimen tidak berjalan sesuai rencana. Jaring pengaman ini sangat penting untuk mengurangi risiko gangguan yang berkepanjangan pada layanan.

#### Contoh Dunia Nyata Chaos Engineering

Chaos engineering mungkin terlihat seperti strategi berisiko tinggi pada pandangan pertama, tetapi jika dilakukan dengan benar, ini adalah metode yang kuat untuk meningkatkan ketahanan sistem. Mari kita lihat bagaimana beberapa nama terbesar dalam teknologi telah menggunakan chaos engineering untuk memperkuat sistem mereka terhadap gangguan yang tidak terduga.

**Netflix** Netflix, pelopor dalam chaos engineering, mengembangkan alat yang dikenal sebagai Chaos Monkey. Alat ini dengan sengaja mengganggu lingkungan produksi Netflix dengan mematikan instance mesin virtual secara acak. Tujuannya? Merancang layanan yang tahan terhadap kegagalan instance. Pendekatan proaktif Chaos Monkey memungkinkan Netflix untuk terus menguji dan meningkatkan ketahanan sistemnya, memastikan bahwa platform dapat menangani kegagalan yang tidak terduga tanpa dampak yang signifikan pada pengalaman pengguna.

**Amazon** Amazon menggunakan praktik chaos engineering untuk menguji ketahanan jaringan layanan mereka yang luas. Salah satu alat terkenal adalah Chaos Gorilla, bagian dari suite Simian Army yang dikembangkan oleh Netflix, yang mensimulasikan gangguan skala besar. Pengujian semacam ini sangat penting bagi Amazon. Ini mengungkap dan menangani potensi kelemahan dalam infrastruktur mereka dan meningkatkan ketangguhan serta keandalan layanan cloud mereka.

**Microsoft Azure** Microsoft Azure menggunakan chaos engineering untuk menjaga keandalan dan ketersediaan platform cloud mereka. Melalui penggunaan Chaos Studio, insinyur Azure mensimulasikan berbagai skenario kegagalan, termasuk malfungsi perangkat keras dan gangguan jaringan. Pengujian reguler dengan Chaos Studio memungkinkan Azure mengidentifikasi potensi kerentanan dan menerapkan perbaikan secara proaktif.

**Spotify** Spotify, dikenal dengan layanan streaming musiknya, juga mengadopsi chaos engineering untuk memastikan keandalan infrastruktur mereka. Perusahaan ini mengembangkan alat chaos engineering mereka sendiri yang bernama Chaos Kong. Alat ini memungkinkan tim engineering Spotify untuk mensimulasikan kegagalan di seluruh sistem terdistribusi mereka, menguji seberapa baik mereka bisa bertahan dari gangguan. Wawasan yang diperoleh dari eksperimen ini membantu Spotify terus menyempurnakan dan memperkuat layanannya.

#### Manfaat Chaos Engineering

Chaos engineering menawarkan berbagai keuntungan dalam meningkatkan ketahanan dan keandalan sistem modern. Beberapa manfaat utamanya termasuk:

1. **Identifikasi Kerentanan Lebih Awal** Dengan sengaja menyebabkan gangguan, kita dapat mengidentifikasi titik lemah dalam sistem sebelum masalah tersebut menjadi gangguan besar yang tidak terduga.
2. **Peningkatan Ketahanan** Eksperimen chaos membantu kita memahami bagaimana sistem merespons situasi tak terduga, memungkinkan kita membuat perbaikan untuk meningkatkan ketahanan keseluruhan.
3. **Kepercayaan Diri yang Lebih Besar** Melalui pengujian yang ketat dan berulang, kita dapat membangun kepercayaan diri bahwa sistem kita dapat menangani berbagai gangguan tanpa menyebabkan downtime yang signifikan.
4. **Peningkatan Proses Respon Kegagalan** Dengan sering menguji respons sistem terhadap kegagalan, tim dapat mengasah kemampuan mereka dalam menangani gangguan dengan cepat dan efektif.

#### Tantangan Chaos Engineering

Meskipun chaos engineering menawarkan manfaat signifikan, ini juga menghadirkan beberapa tantangan. Mari kita jelajahi beberapa hambatan yang mungkin kita hadapi saat menerapkan praktik chaos engineering.

1. **Keselamatan di Utamakan** Keselamatan harus selalu diutamakan dalam chaos engineering. Sebelum memulai pengujian, penting untuk mencadangkan semua data produksi yang kritis. Memiliki rencana yang solid untuk membalikkan perubahan atau menghentikan pengujian jika terjadi hal yang tidak terduga juga sangat penting. Jaring pengaman ini membantu mencegah konsekuensi yang tidak diinginkan yang dapat mempengaruhi layanan atau pelanggan kita.
2. **Intensitas Sumber Daya** Chaos engineering membutuhkan investasi waktu dan sumber daya yang signifikan. Penting untuk menimbang biaya dan manfaat sebelum memulai. Pertimbangkan apa yang dapat diberikan oleh organisasi secara realistis dalam hal waktu, sumber daya manusia, dan infrastruktur. Fokus pada eksperimen yang menawarkan nilai paling besar dan sesuai dengan tujuan bisnis akan membantu memastikan bahwa upaya dalam chaos engineering efektif dan efisien.

#### Alat-Alat Chaos Engineering

Ada banyak alat chaos engineering yang populer, beberapa di antaranya termasuk:

* **Chaos Monkey**: Dikembangkan oleh Netflix, alat ini mematikan instance mesin virtual secara acak di lingkungan produksi.
* **Gremlin**: Platform yang menawarkan berbagai alat untuk menguji ketahanan sistem melalui gangguan yang terkendali.
* **Chaos Toolkit**: Alat open-source yang memungkinkan kita mendefinisikan dan menjalankan eksperimen chaos dengan mudah.
* **AWS Fault Injection Simulator**: Layanan AWS yang memungkinkan simulasi gangguan pada infrastruktur cloud AWS.

#### Penutup

Kita telah mengeksplorasi kekuatan chaos engineering dalam meningkatkan ketahanan dan keandalan sistem dalam pengembangan perangkat lunak modern. Kami memulai dengan menelusuri evolusi praktik pengujian, dari keengganan tradisional untuk menguji di lingkungan produksi hingga penerimaan eksperimen chaos saat ini sebagai sarana untuk memperkuat sistem terhadap kegagalan. Kami kemudian membahas konsep inti chaos engineering dan menjelaskan bagaimana hal ini berbeda dari performance engineering.

Kami juga menguraikan prinsip-prinsip kunci untuk memandu praktik chaos engineering yang efektif dan menggambarkan dampak nyata chaos engineering dari pemimpin industri seperti Netflix, Amazon, Microsoft Azure, dan Spotify.

Chaos engineering menawarkan pendekatan proaktif dan sistematis untuk meningkatkan ketahanan dan keandalan sistem dalam lanskap teknologi yang kompleks dan terus berubah saat ini.

Kami berharap Anda menikmati membaca edisi ini sebanyak kami menikmati menulisnya.
