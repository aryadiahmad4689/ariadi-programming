# Contoh Inheritance

#### Contoh Sederhana

Misalnya, kita memiliki kelas dasar yang disebut `Hewan` yang memiliki beberapa properti dan metode umum yang digunakan oleh semua jenis hewan.

```php
class Hewan {
    public $nama;
    public $umur;

    public function __construct($nama, $umur) {
        $this->nama = $nama;
        $this->umur = $umur;
    }

    public function makan() {
        echo "{$this->nama} sedang makan.\n";
    }
}
```

Kemudian, kita bisa membuat kelas `Kucing` yang mewarisi kelas `Hewan`. Ini berarti `Kucing` akan memiliki semua properti dan metode yang dimiliki oleh `Hewan`, ditambah dengan apa pun yang khusus untuk `Kucing`.

```php
class Kucing extends Hewan {
    public function suara() {
        echo "{$this->nama} berkata: Meow!\n";
    }
}
```

Dalam penggunaan sehari-hari, kita bisa membuat objek dari kelas `Kucing` dan menggunakan metode yang diwarisi dari `Hewan` serta metode yang spesifik untuk `Kucing`.

```php
$kucing = new Kucing("Tom", 3);
$kucing->makan();   // Output: Tom sedang makan.
$kucing->suara();   // Output: Tom berkata: Meow!
```

Dengan contoh ini, kita dapat melihat bahwa `Kucing` secara otomatis mewarisi fungsi `makan()` dari `Hewan` tanpa perlu mendefinisikan ulang fungsi tersebut di dalam kelas `Kucing`. Ini adalah salah satu keuntungan dari menggunakan inheritance, di mana kita dapat memanfaatkan kode yang sudah ada tanpa duplikasi.
