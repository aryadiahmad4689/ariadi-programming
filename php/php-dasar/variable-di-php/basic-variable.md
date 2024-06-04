# Basic Variable

Di PHP, variabel ditandai dengan simbol dolar ($) diikuti dengan nama variabel. Nama variabel harus dimulai dengan huruf atau underscore, diikuti oleh kombinasi huruf, angka, atau underscore. Variabel bersifat sensitif terhadap huruf besar atau kecil.

Contoh:

```php
<?php
$nama = 'Dewi';  // Mendeklarasikan variabel $nama huruf awal kecil
$Nama = 'Dewa'; // Mendeklarasikan variabel $nama huruf awal kapital

echo $nama;  // Menampilkan 'Dewi'
echo $Nama;  // Menampilkan 'Dewa'
?>
```

PHP juga mendukung penugasan referensi, yang berarti nilai yang ditugaskan menjadi referensi untuk variabel aslinya. Perubahan pada variabel baru atau asli akan mempengaruhi yang lain.

Contoh:

```php
<?php
$nama1 = 'Dewi';
$nama2 = &$nama1;  // $nama2 sekarang referensi ke $nama1
$nama2 = 'Budi';  // Mengubah $nama2 juga mengubah $nama1
echo $nama1;  // Menampilkan 'Budi'
?>
```

Variabel yang tidak diinisialisasi memiliki nilai default berdasarkan konteks penggunaannya, misalnya, nilai default untuk tipe boolean adalah `false`.

Untuk informasi lebih lanjut, Anda dapat mengunjungi [manual PHP tentang variabel](https://www.php.net/manual/en/language.variables.basics.php).
