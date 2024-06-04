# Polimorpysm

Polymorphism adalah salah satu konsep penting dalam pemrograman berorientasi objek (OOP) yang memungkinkan objek untuk diolah melalui referensi yang mempunyai banyak bentuk atau dapat berperilaku berbeda tergantung pada kelasnya. Istilah "polymorphism" berasal dari kata Yunani yang berarti "banyak bentuk". Dalam konteks OOP, ini berarti bahwa satu nama fungsi bisa digunakan untuk jenis atau objek yang berbeda.

#### Contoh Polymorphism

Untuk memahamkan konsep ini, mari kita gunakan contoh sederhana dengan kelas hewan dalam PHP. Bayangkan kita memiliki kelas dasar `Hewan` dan beberapa subclass seperti `Kucing` dan `Anjing` yang mewarisi dari `Hewan`.

```php
<?php
// Kelas dasar
class Hewan {
    public function bersuara() {
        return "Suara hewan";
    }
}

// Subclass Kucing
class Kucing extends Hewan {
    public function bersuara() {
        return "Meong";
    }
}

// Subclass Anjing
class Anjing extends Hewan {
    public function bersuara() {
        return "Guk guk";
    }
}
?>

```

Implementasi

Kita akan membuat sebuah fungsi yang menerima objek `Hewan` sebagai parameter dan memanggil metode `bersuara()`. Berkat polymorphism, meskipun fungsi tersebut menerima tipe `Hewan`, ia dapat memanggil implementasi `bersuara()` yang tepat berdasarkan jenis objek yang sebenarnya dioperasikan.

```php
<?php
function buatHewanBersuara($hewan) {
    echo $hewan->bersuara() . "\n";
}

// Membuat objek dari kelas Hewan, Kucing, dan Anjing
$hewan = new Hewan();
$kucing = new Kucing();
$anjing = new Anjing();

// Memanggil fungsi dengan berbagai jenis objek
buatHewanBersuara($hewan);  // Output: Suara hewan
buatHewanBersuara($kucing); // Output: Meong
buatHewanBersuara($anjing); // Output: Guk guk
?>

```
