# Perbedaan Pemrogramman Prosedural Dan OOP

Perbedaan utama antara pemrograman prosedural dan pemrograman berorientasi objek (OOP) terletak pada cara kedua paradigma tersebut menyusun kode dan mengelola data dalam program. Berikut adalah beberapa perbedaan kunci antara keduanya:

1. **Struktur Kode**:
   * **Pemrograman Prosedural**: Program dibagi menjadi prosedur atau fungsi yang melakukan tugas-tugas tertentu. Pendekatan ini cenderung mengikuti alur eksekusi dari atas ke bawah, dan fungsi mungkin saling berbagi data global.
   * **OOP**: Program dibagi menjadi objek, yang menggabungkan data dan fungsi-fungsi yang beroperasi atas data tersebut (dikenal sebagai metode). Objek merupakan instansi dari kelas, di mana kelas mendefinisikan struktur dan perilaku objek tersebut.
2. **Pengelolaan Data**:
   * **Pemrograman Prosedural**: Data sering kali tidak terikat dalam struktur tertentu dan dapat diakses secara bebas oleh fungsi apapun dalam program, yang bisa menimbulkan masalah keamanan data.
   * **OOP**: Data biasanya terenkapsulasi di dalam objek, dan akses ke data tersebut dikontrol melalui metode. Ini memberikan kontrol yang lebih baik atas data dan mencegah akses yang tidak sah atau tidak sengaja ke data.
3. **Reusabilitas Kode**:
   * **Pemrograman Prosedural**: Fungsi dapat digunakan kembali dalam program, tetapi reusabilitas secara keseluruhan terbatas jika tidak didesain dengan baik.
   * **OOP**: Menyediakan mekanisme seperti inheritance (pewarisan) dan polymorphism yang memudahkan reusabilitas dan ekstensi kode. Kelas dapat diwariskan, memodifikasi perilaku kelas dasar untuk keperluan spesifik tanpa mengubah kelas asli.
4. **Skalabilitas dan Pemeliharaan**:
   * **Pemrograman Prosedural**: Mungkin lebih sulit untuk memelihara dan meningkatkan, terutama saat aplikasi tumbuh lebih besar dan lebih kompleks.
   * **OOP**: Lebih mudah dikelola dan diperluas berkat enkapsulasi dan modularitas. Memperbarui atau menambahkan fitur baru dapat dilakukan dengan mengubah atau menambahkan kelas tanpa memengaruhi komponen lain dari program.
5. **Fokus**:
   * **Pemrograman Prosedural**: Fokus pada membuat fungsi dan blok kode yang efisien untuk menyelesaikan tugas.
   * **OOP**: Fokus pada pembuatan objek yang merepresentasikan entitas dunia nyata dengan perilaku dan atribut yang sesuai.

#### Pemrograman Prosedural

Pemrograman prosedural adalah paradigma yang berfokus pada penulisan kode sebagai urutan instruksi atau prosedur yang harus dijalankan oleh komputer. Di sini, data dan fungsi dipisahkan, dan program biasanya dibagi menjadi fungsi yang lebih kecil yang mungkin saling memanggil satu sama lain.

**Contoh:** Dalam konteks PHP, misalnya Kalian ingin menampilkan informasi pengguna dari database, Kalian mungkin menulis sebuah fungsi untuk setiap tugas:

```php
phpCopy codefunction connectDatabase() {
    // Kode untuk menghubungkan ke database
}

function fetchUserData($userId) {
    // Kode untuk mengambil data pengguna berdasarkan ID
}

function displayUser($user) {
    // Kode untuk menampilkan informasi pengguna
}

// Memanggil fungsi
$db = connectDatabase();
$userData = fetchUserData(1);
displayUser($userData);
```

#### Pemrograman Berorientasi Objek (OOP)

OOP adalah paradigma di mana kode dan data dibundel menjadi satu unit yang disebut "objek". Objek adalah instansi dari "kelas" yang mendefinisikan tipe data bersama dengan metode (fungsi) yang dapat operasikan data tersebut. OOP mendorong penggunaan prinsip seperti encapsulation, inheritance, dan polymorphism.

**Contoh:** Dalam OOP, Kalian akan mendefinisikan kelas yang mengelola semua fungsi terkait pengguna:

```php
phpCopy codeclass User {
    private $userId;
    private $userData;

    function __construct($userId) {
        $this->userId = $userId;
        $this->connectDatabase();
        $this->fetchUserData();
    }

    private function connectDatabase() {
        // Kode untuk menghubungkan ke database
    }

    private function fetchUserData() {
        // Kode untuk mengambil data pengguna berdasarkan ID
        $this->userData = "Data Pengguna"; // Contoh hasil
    }

    public function display() {
        // Kode untuk menampilkan informasi pengguna
        echo $this->userData;
    }
}

// Membuat objek User dan menampilkan data pengguna
$user = new User(1);
$user->display();
```

#### Perbedaan Utama

1. **Struktur**: Di OOP, kode dan data dikemas bersama sebagai objek yang interaksi melalui metode kelas. Di pemrograman prosedural, kode dan data biasanya dipisah dan dikelola secara terpisah.
2. **Pendekatan**: OOP menggunakan pendekatan yang lebih modular dan dapat digunakan kembali dengan memanfaatkan konsep seperti warisan dan polimorfisme. Di sisi lain, pemrograman prosedural lebih fokus pada urutan langkah-langkah atau prosedur.
3. **Manajemen Data**: OOP memungkinkan lebih baik dalam hal pengelolaan dan pengamanan data dengan menggunakan encapsulation, sementara di pemrograman prosedural, data biasanya lebih terpapar dan tidak dilindungi secara internal oleh fungsi-fungsi tersebut.
