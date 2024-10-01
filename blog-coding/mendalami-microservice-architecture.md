---
hidden: true
---

# Mendalami Microservice Architecture

#### Database Per Service Pattern

Database Per Service Pattern menyarankan agar setiap microservice memiliki database sendiri yang terpisah. Hal ini memastikan isolasi data dan otonomi masing-masing layanan.

Dalam pola ini, tidak ada microservice yang dapat langsung mengakses atau mengubah data yang dikelola oleh microservice lain. Pertukaran atau manipulasi data harus dilakukan melalui API yang disediakan oleh microservice yang memiliki data tersebut. Ini mempromosikan pemisahan tanggung jawab yang jelas dan keterkaitan yang longgar antara microservices.

Pola ini lebih mudah diimplementasikan pada aplikasi baru. Namun, ketika memigrasi aplikasi monolitik ke arsitektur microservices, memisahkan kepemilikan data menjadi lebih sulit karena bagian-bagian dari sistem sering saling terhubung secara informal.

**Hal yang Perlu Dipertimbangkan:**

1. **Mendefinisikan Bounded Contexts:** Setiap microservice harus memiliki batasan yang jelas sesuai domainnya.
2. **Transaksi Bisnis Multi Microservice:** Transaksi bisnis sering melibatkan beberapa microservices sehingga memerlukan teknik seperti Saga untuk menjaga konsistensi data.

**Manfaat:** Pola ini memberikan isolasi data yang lebih baik, memungkinkan evolusi data model independen, dan bisa menggunakan teknologi database yang berbeda sesuai kebutuhan microservice.

**Tantangan:** Konsistensi data antar microservices, mengelola transaksi yang melibatkan banyak layanan, dan menangani kueri kompleks antar layanan.

***

#### API Gateway Pattern

Pola API Gateway berfungsi sebagai perantara antara aplikasi klien dan microservices backend. API Gateway adalah titik masuk tunggal yang menyederhanakan komunikasi dan mengurangi kompleksitas.

**Bagaimana API Gateway Bekerja:**

* **Reverse Proxy:** Mengarahkan permintaan klien ke microservices yang tepat.
* **Agregasi Permintaan:** API Gateway dapat menggabungkan beberapa permintaan microservices dan mengirimkannya kembali ke klien sebagai satu respons.
* **Masalah Cross-Cutting:** Mengatasi masalah umum seperti autentikasi, otorisasi, dan logging di satu tempat.

**Manfaat:** Pola ini mengurangi jumlah perjalanan data antara klien dan layanan, menyederhanakan komunikasi, dan meningkatkan keamanan.

**Tantangan:** Potensi menjadi titik kegagalan tunggal atau menjadi bottleneck.

***

#### Backends-for-Frontends (BFF) Pattern

Pola BFF menyarankan penggunaan backend terpisah untuk setiap antarmuka depan (frontend). Setiap frontend, seperti aplikasi web atau mobile, memiliki backend khusus yang disesuaikan dengan kebutuhannya.

**Bagaimana BFF Bekerja:**

* **Backend Terpisah:** Setiap UI memiliki backend sendiri.
* **API Kustom:** Setiap BFF menyediakan API yang dioptimalkan untuk frontend spesifiknya.

**Manfaat:** Pola ini memungkinkan pengalaman pengguna yang lebih baik, menyederhanakan logika layanan bagi pengembang frontend, dan meningkatkan kinerja.

**Tantangan:** Meningkatkan kompleksitas dengan adanya banyak backend yang harus dikelola.

***

#### Command Query Responsibility Segregation (CQRS) Pattern

Pola CQRS memisahkan operasi baca dan tulis dari aplikasi ke jalur yang berbeda. Pola ini memungkinkan peningkatan kinerja dan skala independen antara operasi baca dan tulis.

**Bagaimana CQRS Bekerja:**

* **Domain Events:** Setiap perubahan status dalam microservice memicu event yang diikuti oleh pembaruan basis data baca (read database).
* **Melayani Kueri:** Kueri diambil dari basis data baca yang dioptimalkan.

**Manfaat:** Memungkinkan optimasi kueri yang kompleks dan pemisahan jalur baca dan tulis yang lebih efisien.

**Tantangan:** Memerlukan koordinasi yang cermat untuk menjaga konsistensi data.

***

#### Event Sourcing Pattern

Dalam pola ini, perubahan pada data tidak langsung memodifikasi basis data. Sebaliknya, setiap perubahan disimpan sebagai event yang dicatat dalam event store. Pola ini sering dipasangkan dengan CQRS.

**Bagaimana Event Sourcing Bekerja:**

* **Event Store:** Menyimpan semua event yang terjadi dalam sistem.
* **Rekayasa Ulang Status:** Sistem dapat memutar ulang event untuk merekonstruksi status entitas di masa lalu.

**Manfaat:** Menyediakan jejak audit lengkap, dan materialized view dapat dioptimalkan untuk operasi baca.

**Tantangan:** Peningkatan kompleksitas, terutama dalam versi event dan evolusi skema.

***

#### Saga Pattern

Pola Saga digunakan untuk menangani transaksi yang melibatkan beberapa microservices. Pola ini memecah transaksi bisnis besar menjadi serangkaian transaksi lokal kecil yang ditangani oleh layanan yang berbeda.

**Pendekatan Implementasi:**

* **Orkestrasi:** Saga dikoordinasikan oleh orkestrator pusat.
* **Koreografi:** Setiap layanan berkomunikasi melalui event tanpa orkestrator pusat.

**Manfaat:** Memastikan sistem tetap dalam keadaan konsisten meskipun terjadi kegagalan.

**Tantangan:** Koordinasi antar transaksi bisa menjadi kompleks dan memerlukan compensating transactions untuk menangani kegagalan.

***

#### Sidecar Pattern

Pola Sidecar menempatkan fitur operasional seperti logging dan monitoring di kontainer terpisah yang berjalan bersama aplikasi utama.

**Bagaimana Sidecar Bekerja:**

Sidecar container menangani fungsi operasional tanpa mengganggu logika inti aplikasi.

**Manfaat:** Memisahkan tanggung jawab operasional dari aplikasi, meningkatkan skalabilitas, dan memungkinkan pengelolaan sumber daya yang lebih baik.

**Tantangan:** Menambah kompleksitas dan konsumsi sumber daya.

***

#### Circuit Breaker Pattern

Pola ini berfungsi sebagai mekanisme untuk menangani kegagalan komunikasi antara microservices. Circuit breaker akan menghentikan permintaan ketika jumlah kegagalan mencapai ambang batas tertentu.

**Bagaimana Circuit Breaker Bekerja:**

* **Closed State:** Layanan berjalan normal.
* **Open State:** Permintaan dihentikan setelah ambang kegagalan tercapai.
* **Half-Open State:** Memungkinkan beberapa permintaan untuk diuji ulang setelah jeda waktu.

**Manfaat:** Meningkatkan ketahanan sistem dan memberikan perilaku fail-fast.

**Tantangan:** Menentukan ambang kegagalan dan waktu tunggu yang optimal bisa sulit.

***

Semua pola ini memiliki manfaat dan tantangannya masing-masing, tergantung pada kasus penggunaan dan lingkungan implementasi.
