# Constructor Dan Destructor

**Constructor** adalah metode khusus yang secara otomatis dipanggil saat objek dibuat. Ini biasanya digunakan untuk menginisialisasi properti objek atau menjalankan tugas setup yang diperlukan. Di PHP, constructor didefinisikan dengan menggunakan fungsi `__construct()`.

Contoh

```
 public function __construct()
```

**Destructor** adalah metode yang secara otomatis dipanggil saat objek tidak lagi digunakan atau objek tersebut dihapus. Destructor biasanya digunakan untuk membersihkan atau melepaskan sumber daya yang telah dialokasikan oleh objek, seperti menutup koneksi file atau database. Di PHP, destructor didefinisikan dengan menggunakan fungsi `__destruct()`.

```
 public function __destruct()
```

_<mark style="color:orange;">Note: Kedua method diatas adalah bawaan dari php. untuk method descrut itu tidak perlu di panggil karena dia akan melakukan destruct sendiri ketika selesai</mark>_

Contoh Penggunaan umum

```php
<?php

class User {
    protected $nama;
    protected $umur;

    // Constructor untuk menginisialisasi nama dan umur user
    public function __construct($nama, $umur) {
        $this->nama = $nama;
        $this->umur = $umur;
    }

    // Destructor untuk membersihkan ketika objek tidak lagi digunakan
    public function __destruct() {
        // Biasanya digunakan untuk melepaskan sumber daya atau melakukan pembersihan
        echo "Destructor dipanggil: Menghancurkan objek User\n";
    }

    // Method untuk menampilkan data user
    public function display() {
        echo "Nama: {$this->nama}, Umur: {$this->umur}\n";
    }
}

// Membuat objek User
$user = new User("Ariadi", 20);

// Menampilkan data user
$user->display();

// Destructor akan secara otomatis dipanggil ketika skrip selesai atau ketika objek tidak lagi digunakan
?>

```
