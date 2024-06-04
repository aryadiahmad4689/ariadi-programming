# Require

&#x20;`require` sebenarnya adalah sebuah fungsi yang digunakan untuk memasukkan kode dari file lain ke dalam file PHP yang sedang aktif.

Misalnya, jika kita memiliki dua file PHP yang berbeda, `file1.php` dan `file2.php`, dan kita ingin menggunakan kode yang ada di `file2.php` di dalam `file1.php`, kita dapat menggunakan fungsi `require` untuk memasukkan kode dari `file2.php` ke dalam `file1.php`. Ini akan membuat semua kode di `file2.php` tersedia di `file1.php`, sehingga kita bisa menggunakan fungsionalitas atau variabel yang ada di dalamnya.

Contoh penggunaan `require` adalah sebagai berikut:

```php
// file2.php
$pesan = "Halo dari file2.php";

// file1.php
require 'file2.php';
echo $pesan;
```

Pada contoh di atas, kita menggunakan `require` untuk memasukkan kode dari `file2.php` ke dalam `file1.php`. Kemudian kita mencetak variabel `$pesan` yang telah didefinisikan di `file2.php`.

Hal yang penting untuk diingat adalah bahwa jika file yang kita masukkan dengan `require` tidak ditemukan, atau ada masalah dalam memasukkan kode dari file tersebut, maka akan menghasilkan error yang dapat menghentikan eksekusi skrip PHP. Jadi, pastikan bahwa file yang akan dimasukkan menggunakan `require` ada di lokasi yang benar dan berfungsi dengan baik.
