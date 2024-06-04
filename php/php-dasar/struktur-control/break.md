# Break

Break pada PHP adalah sebuah pernyataan yang digunakan untuk menghentikan eksekusi dari loop (perulangan) atau switch (pilihan). Misalnya, dalam sebuah loop for atau while, jika kalian ingin menghentikan loop tersebut sebelum mencapai kondisi akhirnya, kalian dapat menggunakan pernyataan break.

Contohnya, kita punya sebuah loop for yang menghitung angka dari 1 sampai 10. Namun, kita ingin menghentikan loop tersebut saat angka mencapai 5:

```php
for ($i = 1; $i <= 10; $i++) {
    echo $i . " ";
    if ($i == 5) {
        break; // Menghentikan loop jika i sama dengan 5
    }
}
```

Hasilnya akan seperti ini:

```
1 2 3 4 5
```

Dalam kasus tersebut, ketika nilai `$i` mencapai 5, pernyataan `break` akan dieksekusi, sehingga loop dihentikan, dan eksekusi program dilanjutkan ke pernyataan di luar loop.

Penting untuk diingat bahwa break hanya akan menghentikan loop atau switch yang berada di dalamnya. Jika ada nested loop (loop bersarang), break akan menghentikan loop terdalam di mana break tersebut ditemukan. Jadi, jika kita memiliki beberapa loop bersarang, kita harus berhati-hati dalam menggunakan break agar tidak mengganggu alur eksekusi program.
