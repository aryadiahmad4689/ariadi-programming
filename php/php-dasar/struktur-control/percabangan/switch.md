# Switch

**Switch**

switch`digunakan untuk membandingkan satu nilai dengan banyak nilai lainnya. Ini sering digunakan sebagai alternatif yang lebih sederhana dan lebih terstruktur daripada banyak`if`-`else\` jika hanya membandingkan satu variabel dengan beberapa konstanta

```php
<?php
$nilai = 'A';
switch ($nilai) {
  case 'A':
    echo "Luar Biasa!";
    break;
  case 'B':
    echo "Sangat Baik!";
    break;
  case 'C':
    echo "Cukup";
    break;
  default:
    echo "Nilai tidak diketahui";
}
?>
```
