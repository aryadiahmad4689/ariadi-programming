# Require\_Once

`require_once` pada PHP adalah sebuah perintah yang digunakan untuk memasukkan dan mengeksekusi file PHP di dalam file PHP yang lain. Ini sering digunakan ketika kita ingin menggunakan kode yang sama di beberapa halaman web tanpa harus menuliskannya ulang di setiap halaman.

Misalnya, kita memiliki dua file PHP: `file1.php` dan `file2.php`. Di dalam `file2.php`, kita ingin menggunakan fungsi atau variabel yang didefinisikan di `file1.php`. Untuk melakukannya, kita bisa menggunakan `require_once`.

Berikut adalah contoh penggunaan `require_once`:

```php
// file1.php
<?php
$nama = "John";
?>
```

```php
// file2.php
<?php
require_once 'file1.php';
echo "Halo, " . $nama;
?>
```

Dalam contoh di atas, `file2.php` menggunakan variabel `$nama` yang telah didefinisikan di `file1.php`. Dengan menggunakan `require_once`, kita memastikan bahwa kode dari `file1.php` hanya dimasukkan sekali ke dalam `file2.php`, bahkan jika `require_once 'file1.php';` dipanggil lebih dari satu kali di dalam `file2.php`.

Penting untuk diingat bahwa `require_once` akan menghasilkan fatal error (kesalahan fatal) jika file yang diarahkan tidak ditemukan atau tidak dapat diakses. Oleh karena itu, pastikan nama file yang diarahkan dan path-nya benar dan file tersebut ada di lokasi yang diharapkan.
