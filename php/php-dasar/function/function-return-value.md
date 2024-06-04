# Function Return Value

"returning values function" dalam PHP, kita sebenarnya berbicara tentang bagaimana sebuah fungsi (function) dapat mengembalikan (return) nilai (value) setelah dijalankan.

Contohnya, mari kita buat sebuah fungsi sederhana dalam PHP yang menghitung jumlah dari dua angka dan mengembalikan hasilnya:

```php
function tambah($angka1, $angka2) {
    $hasil = $angka1 + $angka2;
    return $hasil;
}
```

Dalam contoh di atas, kita mendefinisikan sebuah fungsi bernama `tambah`. Fungsi ini menerima dua parameter yaitu `$angka1` dan `$angka2`. Selanjutnya, kita menjumlahkan kedua parameter tersebut dan menyimpannya dalam variabel `$hasil`. Lalu, kita mengembalikan nilai dari variabel `$hasil` menggunakan pernyataan `return`.

Ini adalah cara kerja umum dari "returning values function" dalam PHP. Ketika kalian memanggil fungsi ini dan memberikan nilai ke parameter-nya, fungsi akan mengembalikan hasil perhitungan tersebut.

Informasi penting yang perlu kalian pahami adalah bahwa nilai yang dikembalikan oleh fungsi bisa berupa berbagai jenis data, seperti integer, string, array, atau bahkan objek. Selain itu, kalian bisa menggunakan nilai yang dikembalikan oleh fungsi tersebut dalam bagian kode program lainnya, seperti menyimpannya dalam variabel atau langsung menggunakannya dalam operasi perhitungan atau operasi lainnya.
