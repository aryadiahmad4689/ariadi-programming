# Properti dan Method

#### Properti

Properti adalah variabel yang terdapat di dalam kelas. Properti digunakan untuk menyimpan data atau informasi yang berkaitan dengan objek.&#x20;

**Contoh**: Misalkan kita memiliki kelas `Buku` yang menyimpan informasi tentang buku. Properti dalam kelas ini bisa mencakup `judul`, `penulis`, dan `tahun_terbit`.

```php
class Buku {
    public $judul;
    public $penulis;
    public $tahun_terbit;
}
```

Bisa kita katakan properti adalah bentuk data dari sebuah class. seperti diatas biasanya buku itu memiliki judul, penulis dan tahun terbit. maka dari itu bisa disebut representasi asli dari dunia nyata.

#### Method

Method adalah fungsi yang terdapat dalam kelas. Metode ini mendefinisikan perilaku atau fungsi yang dapat dilakukan objek. Seperti properti, metode juga memiliki tingkat akses yang mengontrol di mana metode tersebut dapat dipanggil.

Contoh

```php
class Buku {
    public $judul;
    public $penulis;
    public $tahun_terbit;

    // Method untuk mendapatkan deskripsi buku
    public function getDeskripsi() {
        return "{$this->judul} ditulis oleh {$this->penulis} dan diterbitkan pada tahun {$this->tahun_terbit}.";
    }
}

```

Menggunakan Properti Dan Method

```php
// Membuat objek dari kelas Buku
$buku1 = new Buku();
$buku1->judul = "Belajar PHP";
$buku1->penulis = "John Doe";
$buku1->tahun_terbit = 2021;

// Memanggil metode getDeskripsi
echo $buku1->getDeskripsi();  // Output: Belajar PHP ditulis oleh John Doe dan diterbitkan pada tahun 2021.

```
