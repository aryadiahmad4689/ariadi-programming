# Abstract Pattern Di PHP

Halo perkenalkan nama saya ariadi ahmad. kali ini kita akan membahas desing pattern lagi yaitu abstract pattern.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#id-4596" id="id-4596"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Apa Itu Abstract Pattern

Menurut refactorin guru abstract pattern adala pola desain kreasi yang memungkinkan Anda menghasilkan family objek terkait tanpa menentukan kelas konkretnya. mungkin agak bingun ya dengan penjelasan di atas. intinya ketika kalian ingin membuat sebuah kelas dan punya family atau kelompok. maka kalian bisa menggunakan design pattern ini.

Contoh

![](<../../.gitbook/assets/image (46).png>)

Seperti diatas kita punya banyak variant seperti Art,Victorian,Modern. dengan product familinya

**Time To Implement**

Pertama untuk mengimplementasikan seperti di atas. maka yang pertama yang kita harus buat adalah Buat productnyaa dengan menggunakan factory yang sudah kita pelajarin pada tulisan sebelumnya.

![](<../../.gitbook/assets/image (17).png>)

Oke kita telah membuat dua product. selanjutnya kita buat concreate class Varianya yang mengimplementasikan produknya.

![](<../../.gitbook/assets/image (18).png>)

Selanjutnya Kita Buat Abstract Factory Untuk Membuat Productnya

![](<../../.gitbook/assets/image (52).png>)

Kita membuat sebuah abstract factory untuk membuat furniture. karena meja dan kursi kita anggap dia masuk sebagai family furniture.

Selanjutnya Kita Buat Concreate Class Variantnya.

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

dengan begini kita telah mengimplementasikan abstract factory.

How To Use?

<figure><img src="../../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>

Apa Kelebihanya?

Misalkan nih. kita pengen buat meja dan kursi dengan variant baru contoh Minimalist. is easy.

![](<../../.gitbook/assets/image (87).png>)

Lihat kita sudah menambah kode kita tapi tidak merubah kode yang lama. dengan begini kita bisa membuat banyak variant tanpa merusak kode yang lama.

<figure><img src="../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#id-4596" id="id-4596"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Code Full

```php
<?php

interface Kursi
{
    public function execute();
}

interface Meja
{
    public function execute();
}

interface Lemari 
{
    public function execute();
}


class MinimalistMeja implements Meja
{
    public function execute()
    {
        echo "Sedang Membuat Minimalist Meja";
    }  
}

class MinimalistKursi implements Kursi
{
    public function execute()
    {
        echo "Sedang Membuat Minimalist Kursi";
    }
}


class ModerenKursi implements Kursi
{
    public function execute()
    {
        echo "Sedang Membuat Kursi Moderen";
    }
}

class KlasikKursi implements Kursi
{
    public function execute()
    {
        echo "Sedang Membuat Kursi Klasik";
    }
}

class ModerenMeja implements Meja
{
    public function execute()
    {
        echo "Sedang Membuat Meja Moderen";
    }
}

class KlasikMeja implements Meja
{
    public function execute()
    {
        echo "Sedang Membuar Meja Klasik";
    }
}

// 
interface AbstractFurnitureFactory 
{
    public function createMeja(): Meja;
    public function createKursi() : Kursi;
}

class FurnitureModeren implements AbstractFurnitureFactory
{
    public function createMeja(): Meja
    {
        return new ModerenMeja;
    }

    public function createKursi(): Kursi
    {
        return new ModerenKursi;
    }
    
}

class FurnitureKlasik implements AbstractFurnitureFactory
{
    public function createMeja(): Meja
    {
        return new KlasikMeja;
    }

    public function createKursi(): Kursi
    {
        return new KlasikKursi;
    }
}

class FurnitureMinimalist implements AbstractFurnitureFactory
{
    public function createMeja(): Meja
    {
        return new MinimalistMeja;
    }

    public function createKursi(): Kursi
    {
        return new MinimalistKursi;
    }
}


// ariadi sedang pesan meja Moderen Dan Kursi Moderen

$AriadiPesanFurnitureModeren = new  FurnitureModeren;

$AriadiPesanFurnitureModeren->createMeja()->execute();
// Sedang Membuat Meja Moderen
$AriadiPesanFurnitureModeren->createKursi()->execute();
// Sedang Membuat Kursi Moderen

$AriadiPesanFurnitureMinimalist  = new FurnitureMinimalist;
$AriadiPesanFurnitureMinimalist->createMeja()->execute();
// Sedang Membuat Meja Minimalist
$AriadiPesanFurnitureMinimalist->createKursi()->execute();
// Sedang Membuat Kursi Minimalisth
```



Semoga Mudah Di Pahami. **Salam Programmer Makassar**

\
