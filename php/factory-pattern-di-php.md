# Factory Pattern Di PHP

Halo perkenalkan nama saya ariadi ahmad. kali ini kita akan membahas salah satu design pattern yitu Factory Pattern. Menurut Refactorin Guru Factory Pattern adalah pola desain kreasi yang menyediakan antarmuka untuk membuat objek di superclass, tetapi memungkinkan subclass untuk mengubah jenis objek yang akan dibuat.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#4596" id="4596"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

**Penjelasan**

Kalau dari penjelasan seperti di atas mungkin kurang mengerti yaa. saya juga sebenarnya kurang mengerti dari penjelasan itu. tapi saya akan mencoba menjelaskan secara sederhana. Seperti namanya factory, atau bahasa indonesianya adalah pabrik. maka factory pattern ini berfungsi sebagai pabrik, misalkan kita punya `class Baju Jeans` `Class Baju biasa`. karena semuanya samaa-sama baju maka kita bisa membuat class yang bertugas sebagai pabriknya. jadi terlepas nanti misalkan ada tambahan `class baju robek`, `baju pincang`, `baju lengan pendek`. hehehe. kita ga peduli karena kita sudah punya pabrik yang nama`classnya baju`.

**Implementasi**

Pertama kita buat pabriknya dengan nama classnya Baju dan punya method namanya buatBaju

![](<../.gitbook/assets/image (1) (1).png>)

Selanjutnya kita buat concreate classnya. berdasarkan jenis baju yang ingin kita buat. contoh disini **`bajuLenganPanjang dan bajuLenganPendek`**

**``**![](<../.gitbook/assets/image (22).png>)**``**

kita sudah membuat baju dengan mengimplementasikan pabriknya.

Sebenarnya factory pattern sudah selesai sampai disini. tapi saya ingin menambahkan sedikit agar terlihat lebih nyata. misalkan kita ingin punya class PembuatBaju. pembuat baju ini nantinya ada banyak juga. jadi setiap orang bedah baju yang di buat untuk mempercepat produksi begitu.

Cara Implementasi

![](<../.gitbook/assets/image (88).png>)

Sederhana banget sih. kita buat sebuah abstraksi untuk si pembuatnya. jadi misalkan satu orang nangani satu produksi aja atau bisa lebih sebenarnya tergantung kebutuhan. tapi disini saya hanya menuliskan satu aja biar mudah.

**Penjelasanya**

1. Kita ingin Herman menangani produksi pembuatan baju lengan panjang
2. Kita Ingin Adi Menangani produksi Baju Lengan Pendek

Kita Lihat Hasilnya

![](<../.gitbook/assets/image (49).png>)

Dengan Begini kita bisa dengan mudah mengganti implementasinya. misalkan nih kita punya produksi baju yang lain lagi. contoh BajuJeans. gampang aja. kita buat aja **`bajuJeans`** yang implement pabrik baju.

![](<../.gitbook/assets/image (83).png>)

lalu Kita ganti misalkan si Herman pindah naganin `bajuJeans`

``![](<../.gitbook/assets/image (45).png>)``

![](<../.gitbook/assets/image (4) (1).png>)

lihat code di client kita tidak berubah walaupun Herman udah berubah pekerjaanya Ke **`Baju Jeans`**

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#4596" id="4596"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

**Code Full**

```php
<?php

interface Baju{
   public function buatBaju();
}

class BajuLenganPanjang implements Baju{

    public function buatBaju()
    {
        echo "Baju Lengan Panjang";
    }
}

class BajuJeans implements Baju{

    public function buatBaju()
    {
        echo "Baju Jeans";
    }
}

class BajuLenganPendek implements Baju{

    public function buatBaju()
    {
        echo "Baju Lengan Pendek";
    }
}


abstract class PembuatBaju 
{
    abstract function produksi() : Baju;
}

class Adi extends PembuatBaju
{
    public function produksi(): Baju
    {
        return new BajuLenganPendek;
    }
}

class Herman extends PembuatBaju
{
    public function produksi(): Baju
    {
        return new BajuJeans;
    }
}



$herman = new Herman();
$herman->produksi()->buatBaju();

// output = Baju Jeans
echo"<br>";
$adi = new Adi();
$adi->produksi()->buatBaju();

// output = Baju Lengan Pendek
```

Sekian yaa. semoga mudah di pahami. **Salam Programmer Makassar**
