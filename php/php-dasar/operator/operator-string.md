# Operator String

Operator string adalah cara untuk melakukan operasi pada teks atau string di dalam bahasa pemrograman PHP.

Mari kita bahas dengan contoh sederhana. Katakan kita memiliki dua string:

```php
$string1 = "Hello";
$string2 = "world";
```

Sekarang, mari kita lihat beberapa operator string yang umum digunakan dalam PHP:

1. **Operator Penggabungan (.)**: Operator ini digunakan untuk menggabungkan dua string menjadi satu. Misalnya:

```php
$result = $string1 . $string2;
echo $result; // Output: Helloworld
```

2. **Operator Concatenation Assignment (.=)**: Operator ini digunakan untuk menambahkan string kedua ke string pertama. Misalnya:

```php
$string1 .= $string2;
echo $string1; // Output: Helloworld
```

3. **Operator Pemotongan (\[])**: Operator ini digunakan untuk mengakses karakter individual dalam string berdasarkan posisi indeksnya. Indeks dalam string dimulai dari 0. Contohnya:

```php
$char = $string1[0];
echo $char; // Output: H
```

4. **Operator Pemotongan (substring)**: Dalam PHP, kita juga bisa menggunakan fungsi `substr()` untuk mengambil sebagian string berdasarkan posisi awal dan panjangnya. Contoh:

```php
$substring = substr($string1, 0, 3);
echo $substring; // Output: Hel
```

5. **Operator Pencarian**: PHP memiliki fungsi-fungsi seperti `strpos()` dan `strstr()` untuk mencari substring dalam string. Contohnya:

```php
$pos = strpos($string1, "llo");
echo $pos; // Output: 2 (posisi "llo" dimulai dari indeks ke-2)
```

6. **Operator Pembanding**: PHP juga mendukung operasi perbandingan pada string menggunakan operator seperti `==`, `!=`, `<`, `>`, `<=`, `>=`. Contohnya:

```php
if ($string1 == "Hello") {
    echo "String sama dengan 'Hello'";
}
```

7. **Operator Pemotongan (explode)**: Fungsi `explode()` digunakan untuk memecah string menjadi array berdasarkan pemisah tertentu. Misalnya:

```php
$string = "Hello,world";
$array = explode(",", $string);
print_r($array); // Output: Array([0] => Hello [1] => world)
```
