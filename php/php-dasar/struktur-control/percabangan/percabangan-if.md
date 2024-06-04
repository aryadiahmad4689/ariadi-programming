# Percabangan IF

Pengkondisian dalam pemrograman digunakan untuk membuat keputusan berdasarkan kondisi tertentu.

`if` digunakan untuk menjalankan blok kode jika kondisi yang diberikan bernilai `true`.

```php
<?php
$nilai = 75;
if ($nilai > 70) {
  echo "Selamat, Kalian lulus!";
}
?>
```

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

**Kapan Menggunakan IF dan Switch?**

Gunakan if ketika:

1. Kondisi yang Dibandingkan Kompleks: if lebih fleksibel karena dapat mengevaluasi ekspresi boolean yang kompleks, bukan hanya perbandingan kesamaan.
2. Rentang Nilai yang Dinamis: Ketika Kalian perlu mengecek rentang nilai atau kondisi yang tidak dapat ditentukan dengan kesamaan nilai sederhana.
3. Logika yang Membutuhkan Detil Lebih: Jika logika keputusan Kalian membutuhkan serangkaian pengecekan kondisi yang spesifik dan detail, termasuk kondisi bersarang.

```php
<?php
    $umur = 20;
    if ($umur < 18) {
        echo "Kalian masih di bawah umur.";
    } elseif ($umur >= 18 && $umur <= 30) {
        echo "Kalian berada di usia produktif.";
    } else {
        echo "Kalian berada di usia matang.";
    }
?>
```

Gunakan switch ketika:

1. Pengecekan Kesamaan Sederhana: switch ideal untuk kasus di mana Kalian hanya perlu membandingkan satu variabel dengan serangkaian nilai konstan.
2. Kode Lebih Bersih dan Terstruktur: Dalam beberapa kasus, menggunakan switch bisa membuat kode Kalian lebih mudah dibaca dan dipahami dibandingkan dengan banyak if-else yang bersarang
3. Perlu Aksi Default: switch menyediakan default sebagai opsi untuk menangani kasus ketika tidak ada kasus lain yang cocok.

```php
<?php
    $hari = "Senin";
    switch ($hari) {
        case "Senin":
            echo "Hari ini adalah hari Senin.";
            break;
        case "Selasa":
            echo "Hari ini adalah hari Selasa.";
            break;
        default:
            echo "Bukan awal minggu.";
    }
?>
```
