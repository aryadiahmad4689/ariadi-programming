# Prototype Pattern Di PHP

Perkenalkan nama saya ariadi ahmad. kali ini kita akan melanjutkan bahasan kita mengenai design pattern. desing pattern yang akan kita bahas adalah Prototype Pattern.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#4596" id="4596"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

**Penjelasan**

Menurut Refactoring guru prototype pattern adalah pola desain kreasi yang memungkinkan Anda menyalin objek yang ada tanpa membuat kode Anda bergantung pada kelasnya.

Gini teman-teman. jadi misalkan kalian punya class Pesawat dan kalian ingin membuat Pesawat yang sama tapi tidak ingin terpengaruh dari class pesawat yang pertama atau class cloninganyaa.

![](<../.gitbook/assets/image (27).png>)

Contoh sederhananya adalah pembelahan sel diatas . mereka masih sama-sama sel tapi sebenarnya mereka adalah sel yang berbeda karena sudah memiliki keperibadian sendiri.

**Implementasi**

Kita buat interface protype yang mempunyai method clone

![](<../.gitbook/assets/image (23).png>)

Sekarang kita buat implementasi concreatenya

![](<../.gitbook/assets/image (84).png>)

Diatas kita membuat class pesawat kita, tapi menyertakan method clone yang mengembalikan dirinya sendiri. jadi nantinya setiap kita memanggil function clone kita bisa copy class pesawat tersebut kedalam objek baru.

Sekarang kita mencoba membuat pesawat kita

![](<../.gitbook/assets/image (35).png>)

Di sini saya telah membuat pesawat saya. pertanyaanya. ada ga sih cara copy isi dari si pesawat1 menjadi pesawat2 dan saya tidak ingin ada saling ketergantungan? jawabanya adalah protype pattern yang kita definisikan di method clone tadi.

Alih-alih kita membuat dan menginialisasi ulang

```
$pesawat2 = new Pesawat;
```

Maka kita bisa melakukan dengan seperti ini

![](<../.gitbook/assets/image (42).png>)

Dengan begini kita bisa bebas copy class pesawat1 tersebut dan mengganti isinya tanpa memengaruhi class pesawat1. lihat di atas kita mengisi class pesawat1 dengan kursi = 40 dan di cloneya kita isi dengan kursi = 200 dengan masih menggunakan mesin yang sama.

Prototype Pattern ini bisa di gunakan misalkan kita ingin copy isi dari sebuah class. tapi kita hanya ingin mengganti beberapa part aja di dalamnya.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#4596" id="4596"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

**Code Full**

```php
<?php

interface Prototype {
    public function clone(): Prototype;
}


class Pesawat implements Prototype{
    private $mesin;
    private $kursi;

    public function setMesin(string $mesin)
    {
        $this->mesin = $mesin;
    }

    public function setKursi(int $kursi)
    {
        $this->kursi =$kursi;
    }

    public function buatPesawat()
    {
        echo $this->mesin." ".$this->kursi;
    }

    public function clone(): Pesawat
    {

        $pesawat = new Pesawat;

        $pesawat->mesin = $this->mesin;
        $pesawat->kursi = $this->kursi;

        return $pesawat;

    }
}


$pesawat1 = new Pesawat;

$pesawat1->setMesin("Kargo");
$pesawat1->setKursi(40);

print_r($pesawat1->buatPesawat());
// output = Kargo 40

$pesawat2 = $pesawat1->clone();
$pesawat2->setKursi(200);

print_r($pesawat2->buatPesawat());
// output = Kargo 200
```

Semoga Mudah dipahami. **Salam Programmer Makassar**
