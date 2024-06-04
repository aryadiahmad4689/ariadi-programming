# Continue

`continue` dalam PHP digunakan dalam perulangan untuk melompati sisa kode di dalam blok perulangan dan melanjutkan dengan iterasi berikutnya.

Misalnya, jika kalian memiliki sebuah loop `for` yang menghitung bilangan dari 1 hingga 10, tapi kalian hanya ingin mencetak bilangan ganjil, kalian bisa menggunakan `continue` untuk melewati bilangan genap:

```php
for ($i = 1; $i <= 10; $i++) {
    if ($i % 2 == 0) {
        continue; // Melompati iterasi berikutnya jika bilangan genap
    }
    echo $i . " "; // Cetak bilangan ganjil
}
```

Dalam contoh ini, ketika `$i` adalah bilangan genap, `continue` akan menghentikan eksekusi kode di dalam loop dan langsung melanjutkan ke iterasi berikutnya. Sehingga hanya bilangan ganjil yang dicetak.

Penting untuk diingat bahwa `continue` hanya berlaku di dalam loop (`for`, `while`, atau `do-while`), dan tidak berlaku di luar loop. Jadi pastikan kalian menempatkannya di tempat yang benar agar berfungsi dengan baik.
