# Overidding Method

**Overriding Metode** adalah konsep dalam pemrograman berorientasi objek di mana metode di kelas turunan memiliki implementasi yang berbeda dari metode dengan nama yang sama di kelas induknya. Hal ini memungkinkan kelas turunan untuk memodifikasi atau mengganti fungsionalitas dari metode yang diwarisi.

#### Tujuan Overriding

Tujuan utama dari overriding adalah untuk memungkinkan kelas turunan memiliki perilaku yang spesifik yang berbeda dari kelas induk, meskipun menggunakan nama metode yang sama.

#### Contoh Overriding Metode

Misalkan kita memiliki kelas `Kendaraan` dengan metode `berbunyi` yang menggambarkan bunyi dari kendaraan secara umum. Lalu, kita memiliki kelas `Mobil` yang merupakan turunan dari `Kendaraan`. Kita ingin `Mobil` memiliki implementasi khusus untuk metode `berbunyi` yang menggambarkan bunyi klakson mobil.

```php
<?php
class Kendaraan {
    public function berbunyi() {
        echo "Kendaraan ini berbunyi: Vroom!";
    }
}

class Mobil extends Kendaraan {

    // method ini suda ada di kelas induknya
    // ini disebut overidding
    public function berbunyi() {
        echo "Mobil ini berbunyi: Telolet!";
    }
}

class Bajay extends Kendaraan {
}

// Menciptakan objek Mobil
$mobil = new Mobil();
$mobil->berbunyi();  // Output: Mobil ini berbunyi: Telolet!

$bajay = new Bajay();
$bajay->berbunyi();  // Output: Mobil ini berbunyi: Vroom!
?>
```

#### Penjelasan

* **Kelas Kendaraan**: Memiliki metode `berbunyi` yang mencetak "Kendaraan ini berbunyi: Vroom!".
* **Kelas Mobil**: Mewarisi `Kendaraan` dan meng-override metode `berbunyi` untuk mencetak "Mobil ini berbunyi: Telolet!" yang lebih spesifik untuk mobil.

Di sini, metode `berbunyi` di kelas `Mobil` menggantikan implementasi yang ada di kelas `Kendaraan`. Ketika objek dari `Mobil` memanggil metode `berbunyi`, PHP menjalankan metode `berbunyi` yang didefinisikan di kelas `Mobil`, bukan yang di kelas `Kendaraan`. Ini adalah inti dari konsep overriding dalam pemrograman berorientasi objek.
