# Perulangan Do While

Mirip dengan `while`, namun perulangan `do-while` menjamin bahwa blok kode akan dijalankan setidaknya satu kali sebelum kondisi diperiksa.

```php
<?php
$i = 1;
do {
    echo $i . " ";
    $i++;
} while ($i <= 5);
// Output: 1 2 3 4 5

$i = 10;
do {
    echo $i . " ";
    $i++;
} while ($i <= 5);
// Output: 10
?>

?>
```
