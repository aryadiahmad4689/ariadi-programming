# Variable Di PHP

Variabel dalam PHP adalah sebuah simbol atau nama yang digunakan untuk menyimpan nilai. Nilai tersebut bisa berupa teks, angka, array, atau bahkan objek dari kelas. PHP adalah bahasa pemrograman yang menggunakan konvensi penamaan variabel dengan awalan tKalian dollar ($) diikuti oleh nama variabel itu sendiri. Nama variabel dapat terdiri dari huruf, angka, dan underscore, tetapi harus dimulai dengan huruf atau underscore.

Contoh Variable

```php
<?php
$nama = "Ariadi Ahmad";
$umur = 30; 
?>
```

Fitur Penting Variabel di PHP:

1 .Case Sensitive: Nama variabel dalam PHP peka terhadap huruf besar dan kecil. Misalnya, $Umur dan $umur dianggap sebagai dua variabel yang berbeda.&#x20;

2 Scope Variabel: PHP mendefinisikan variabel dalam konteks tertentu yang dikenal dengan scope. Ada beberapa jenis scope seperti lokal, global, dan statis.&#x20;

3 Variabel Global dan Lokal: Variabel yang didefinisikan di luar fungsi memiliki scope global, sedangkan yang didefinisikan di dalam fungsi memiliki scope lokal. Untuk mengakses variabel global dalam sebuah fungsi, Kalian harus menggunakan kata kunci global atau array $GLOBALS.&#x20;

4 Variabel Dinamis: PHP memungkinkan penggunaan variabel dinamis, di mana nama dari sebuah variabel dapat dinamis berdasarkan nilai variabel lain.
