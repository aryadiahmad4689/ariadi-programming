# Perulangan Foreach

Perulangan `foreach` dirancang khusus untuk array. Ia memudahkan iterasi over setiap elemen dalam array tanpa perlu menggunakan penghitung.

```php
<?php
    $colors = ["merah", "hijau", "biru"];
    foreach ($colors as $color) {
        echo $color . " ";
    }
    // Output: merah hijau biru
?>
```
