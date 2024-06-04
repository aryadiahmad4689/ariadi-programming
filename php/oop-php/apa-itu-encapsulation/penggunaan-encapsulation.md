# Penggunaan Encapsulation

#### 1. Public

Modifier `public` membuat properti atau metode dapat diakses dari mana saja, baik di dalam kelas itu sendiri, dari kelas turunan, maupun dari luar kelas.

**Contoh:**

```php
class Mobil {
    public $warna = "Merah";

    public function tampilkanWarna() {
        echo $this->warna;
    }
}

$mobil = new Mobil();
$mobil->tampilkanWarna();  // Output: Merah
```

#### 2. Private

Modifier `private` membatasi akses hanya ke dalam kelas di mana properti atau metode tersebut didefinisikan. Artinya, kelas lain, termasuk kelas turunan, tidak dapat mengakses properti atau metode tersebut.

**Contoh:**

```php
class Mobil {
    private $warna = "Merah";

    public function tampilkanWarna() {
        echo $this->warna;
    }
}

$mobil = new Mobil();
$mobil->tampilkanWarna();  // Output: Merah
$mobil->warna;  // Error: Tidak bisa diakses dari luar kelas
```

#### 3. Protected

Modifier `protected` membuat properti atau metode dapat diakses oleh kelas di mana mereka didefinisikan, serta oleh kelas-kelas turunan (subclass).

**Contoh:**

```php
class Kendaraan {
    protected $warna = "Biru";
}

// ini adalah pewarisan sifat
class Mobil extends Kendaraan {
    public function tampilkanWarna(){
        echo $this->warna;
    }
}
$mobil = new Mobil();
$mobil->tampilkanWarna();  // Output: Biru
$mobil->warna;  // Error: Tidak bisa diakses secara langsung dari luar kelas atau subkelas
```

Penggunaan modifier ini membantu mengatur arsitektur program dengan mengendalikan akses ke data dan metode, serta meningkatkan keamanan dan integritas data dalam pengembangan perangkat lunak.

Encapsulation Juga bisa dilakukan pada sebuah method contoh

```php
class Account {
    private $balance = 1000; // Properti 'balance' bersifat private

    // Metode publik untuk menambahkan uang ke saldo
    public function deposit($amount) {
        if ($amount > 0) {
            $this->balance += $amount;
            return "Deposit berhasil. Saldo saat ini: $this->balance";
        }
        return "Masukkan jumlah yang valid.";
    }

    // Metode publik untuk mengambil uang dari saldo
    public function withdraw($amount) {
        if ($amount > 0 && $amount <= $this->balance) {
            $this->balance -= $amount;
            return "Penarikan berhasil. Saldo saat ini: $this->balance";
        }
        return "Penarikan gagal. Jumlah tidak valid atau saldo tidak cukup.";
    }

    // Metode private untuk mendapatkan saldo saat ini
    private function getBalance() {
        return $this->balance;
    }

    // Metode publik untuk mengecek saldo (menggunakan metode private getBalance)
    public function checkBalance() {
        return "Saldo saat ini: " . $this->getBalance();
    }
}

$myAccount = new Account();
echo $myAccount->deposit(500);  // Output: Deposit berhasil. Saldo saat ini: 1500
echo $myAccount->withdraw(200); // Output: Penarikan berhasil. Saldo saat ini: 1300
echo $myAccount->checkBalance(); // Output: Saldo saat ini: 1300

```
