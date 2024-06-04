# Abstraction Class

#### Apa Itu Abstraction?

Dalam konteks pemrograman berorientasi objek (OOP), _abstraction_ adalah prinsip untuk menyembunyikan kompleksitas detail dari implementasi dan hanya menampilkan fungsionalitas yang penting ke pengguna. Abstraction memungkinkan programmer untuk bekerja pada tingkat yang lebih abstrak saat berinteraksi dengan objek, tanpa perlu memahami detail yang rumit dari operasi internal objek tersebut.

#### Tujuan dari Abstraction

Tujuan utama dari abstraction adalah untuk mengisolasi dampak perubahan dalam kode. Misalnya, dengan menggunakan abstraction, seorang developer dapat mengubah cara kerja sebuah metode di dalam kelas tanpa mengganggu kode yang menggunakan kelas tersebut. Abstraction juga membantu dalam meningkatkan modularitas dan memudahkan pengelolaan sistem yang kompleks.

**Kenapa Menggunakan Abstraction Class**

Kita menggunakan kelas abstrak untuk membangun kerangka dasar dalam pemrograman berorientasi objek. Kelas abstrak memungkinkan kita menentukan metode-metode yang harus diimplementasikan oleh kelas turunannya, sehingga memastikan bahwa semua kelas turunan memiliki fungsionalitas yang konsisten dan sesuai. Ini berguna terutama ketika beberapa kelas berbagi struktur dan perilaku yang sama tetapi masing-masing memiliki implementasi yang spesifik dan berbeda. Melalui kelas abstrak, kita dapat mengurangi duplikasi kode dan meningkatkan modularitas serta pemeliharaan kode.

**Contoh**

```php
<?php
// Membuat abstract class Vehicle
abstract class Vehicle {
    // Property umum untuk semua kendaraan
    protected $brand;

    // Constructor untuk set brand
    public function __construct($brand) {
        $this->brand = $brand;
    }

    // Abstract function start
    abstract protected function start();

    // Abstract function stop
    abstract protected function stop();

    // Function umum untuk mendapatkan brand
    public function getBrand() {
        return $this->brand;
    }
}

// Membuat class Car yang mewarisi Vehicle
class Car extends Vehicle {
    // Implementasi dari abstract function start
    public function start() {
        return "Car " . $this->brand . " started";
    }

    // Implementasi dari abstract function stop
    public function stop() {
        return "Car " . $this->brand . " stopped";
    }
}

class Truktor extends Vehicle {
    // Implementasi dari abstract function start
    public function start() {
        return "Truktor " . $this->brand . " started";
    }

    // Implementasi dari abstract function stop
    public function stop() {
        return "Truktor " . $this->brand . " stopped";
    }
}

// Membuat objek dari class Car
$myCar = new Car("Toyota");
echo $myCar->start();  // Output: Car Toyota started
echo "<br>";
echo $myCar->stop();   // Output: Car Toyota stopped
?>

```

Dengan menggunakan abstraction class maka kita memaksa setiap class turunanya untuk mengikuti implementasi yang ada. dalam contoh kasus ini adalah function `start` dan `stop` . tapi untuk detailnya itu tergantung dari masing masing class. dengan begini maka ini memungkinkan setiap class turunan mempuyai implementasi yang sama.
