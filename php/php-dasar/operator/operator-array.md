# Operator Array

Operator array adalah cara kita memanipulasi atau melakukan operasi pada array.

Misalkan kita punya array seperti ini:

```php
$angka = array(1, 2, 3, 4, 5);
```

Di sini kita memiliki array dengan nama `$angka` yang berisi beberapa angka. Sekarang, mari kita lihat beberapa operator array PHP yang penting:

1.  **Operator Kurung Siku `[ ]`:** Ini adalah cara standar untuk mengakses elemen di dalam array. Kalian bisa menggunakan indeks untuk mengakses elemen tertentu. Contohnya:

    ```php
    echo $angka[0]; // Output: 1
    ```

    Ini akan mencetak elemen pertama dari array `$angka`, yang nilainya adalah 1.
2.  **Operator Penambahan (`+`):** Operator ini digunakan untuk menggabungkan dua array bersama-sama. Misalnya:

    ```php
    $angka2 = array(4, 5, 8);
    $hasil = $angka + $angka2;
    print_r($hasil);
    ```

    Outputnya akan menjadi:

    ```
    Array
    (
        [0] => 1
        [1] => 2
        [2] => 3
        [3] => 4
        [4] => 5
        [5] => 8
    )
    ```

    Kalian bisa melihat bahwa elemen dari `$angka` dipertahankan, dan hanya elemen unik dari `$angka2` yang ditambahkan ke akhirnya.
3.  **Operator Gabungan (`.`):** Ini digunakan untuk menggabungkan dua array menjadi satu. Misalnya:

    ```php
    $hasil = $angka . $angka2;
    print_r($hasil);
    ```

    Outputnya akan menjadi:

    ```
    Array
    (
        [0] => 1
        [1] => 2
        [2] => 3
        [3] => 4
        [4] => 5
        [5] => 6
        [6] => 7
        [7] => 8
    )
    ```

    Kita mendapatkan array baru yang berisi semua elemen dari kedua array asal.
