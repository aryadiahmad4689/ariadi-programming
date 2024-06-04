# Operator Logika

Operator logika dalam PHP digunakan untuk menggabungkan dua atau lebih kondisi (expression) dan membentuk satu kondisi baru yang hasilnya berupa nilai Boolean, yaitu `true` atau `false.`

```php

<!-- ### 1. AND (`&&` atau `and`)
Operator ini menghasilkan nilai `true` jika **kedua** kondisi bernilai `true`. -->
<?php
$x = 6;
$y = 3;
if ($x > 5 && $y > 2) {
  echo "Kedua kondisi terpenuhi.";
}
// Output: Kedua kondisi terpenuhi.
?>

<!-- ### 2. OR (`||` atau `or`)
Operator ini menghasilkan nilai `true` jika **salah satu** dari kondisi tersebut bernilai `true`. -->
<?php
$x = 4;
$y = 2;
if ($x > 5 || $y > 1) {
  echo "Salah satu kondisi terpenuhi.";
}
// Output: Salah satu kondisi terpenuhi.
?>

<!-- ### 3. NOT (`!`)
Operator ini mengubah nilai `true` menjadi `false` dan sebaliknya. -->
<?php
$x = 4;
if (!$x > 5) {
  echo "Kondisi terpenuhi.";
}
// Output: Kondisi terpenuhi.
?>

<!-- ### 4. XOR
Operator `xor` menghasilkan nilai `true` jika **salah satu** kondisi bernilai `true`, tetapi tidak keduanya. -->
<?php
$x = 4;
$y = 2;
if ($x > 5 xor $y > 1) {
  echo "Salah satu kondisi terpenuhi, tetapi tidak keduanya.";
} else {
  echo "Kedua kondisi terpenuhi atau tidak ada yang terpenuhi.";
}
// Output: Kedua kondisi terpenuhi atau tidak ada yang terpenuhi.
?>

```
