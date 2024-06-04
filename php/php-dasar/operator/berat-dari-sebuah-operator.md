# Berat Dari Sebuah Operator

Operator Precedence (urutan prioritas operator) dalam PHP. Ini adalah hal yang penting untuk dipahami oleh para programmer, terutama yang masih pemula.

Operator Precedence adalah aturan yang menentukan urutan mana operator yang dievaluasi terlebih dahulu dalam suatu ekspresi. Ini mirip dengan aturan matematika dasar seperti perkalian sebelum penjumlahan. Ini penting karena dapat mempengaruhi hasil dari ekspresi yang kita tulis.

Sebagai contoh, kita punya ekspresi:

```php
$result = 10 + 5 * 2;
```

Sekarang, berdasarkan aturan Operator Precedence, perkalian akan dievaluasi terlebih dahulu sebelum penambahan. Jadi, hasilnya akan menjadi:

```
10 + (5 * 2) = 10 + 10 = 20
```

Ini berarti hasil dari ekspresi di atas adalah 20, bukan 30. Ini karena perkalian memiliki prioritas lebih tinggi daripada penambahan dalam PHP.

Penting untuk dicatat bahwa jika kita ingin mengubah urutan evaluasi, kita bisa menggunakan tanda kurung. Contohnya:

```php
$result = (10 + 5) * 2;
```

Dalam hal ini, penambahan akan dievaluasi terlebih dahulu karena berada di dalam tanda kurung, menghasilkan hasil yang berbeda:

```php
(10 + 5) * 2 = 15 * 2 = 30
```

Jadi, pemahaman tentang Operator Precedence sangat penting saat menulis kode PHP agar kita bisa mendapatkan hasil yang diinginkan. Terutama dalam ekspresi yang kompleks, memahami urutan prioritas operator akan membantu kita menghindari kesalahan dalam logika program kita.
