# Function Argumen

&#x20;"function argument" adalah nilai yang kita berikan kepada sebuah fungsi saat kita memanggilnya. Ini seperti memberi tahu fungsi apa yang harus dilakukan atau dengan apa harus beroperasi.

Misalkan kita punya fungsi sederhana untuk menambahkan dua angka:

```php
function tambah($angka1, $angka2) {
    echo $angka1 + $angka2;
}
```

Di sini, `$angka1` dan `$angka2` adalah "function arguments". Ketika kita memanggil fungsi ini, kita memberikan dua nilai yang akan dijumlahkan:

```php
$hasil = tambah(3, 5);
echo $hasil; // Output: 8
```

Jadi, dalam contoh ini, kita memberi tahu fungsi `tambah()` bahwa `$angka1` adalah 3 dan `$angka2` adalah 5.

Informasi penting yang perlu diketahui adalah:

1. Jumlah dan tipe dari "function arguments" harus sesuai dengan yang didefinisikan dalam fungsi. Jika tidak sesuai, PHP akan menghasilkan kesalahan.
2. "Function arguments" bisa berupa nilai yang keras (seperti angka atau string) atau variabel yang sudah ada sebelumnya.
3. Dalam PHP, kita bisa memiliki "default arguments", yang berarti kita bisa memberikan nilai default kepada argumen tersebut jika nilai tidak diberikan saat pemanggilan fungsi.
