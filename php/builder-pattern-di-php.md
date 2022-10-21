# Builder Pattern Di PHP

Halo perkenalkan nama saya ariadi ahmad. kali ini kita akan membahas desain pattern lagi yaitu builder pattern.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#4596" id="4596"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Penjelasan

Builder Pattern menurut refactoring guru adalah pola desain kreasi yang memungkinkan Anda membuat objek kompleks selangkah demi selangkah. Pola memungkinkan Anda untuk menghasilkan berbagai jenis dan representasi objek menggunakan kode konstruksi yang sama.

Jadi analoginya begini teman-teman. jika kalian ingin bangun rumah, kalian harus membuat properti lain di bangun secara independent. seperti Pintu,Jendela,Kamar harus terpisah dari rumah itu sendiri seperti di dunia nyata. hal ini memungkinkan kita untuk membongkar pasang properti di rumah tersebut.

![](<../.gitbook/assets/image (71).png>)

Seperti terlihat di atas. semuanya masih rumah cuma properti dari rumah tersebut yang berbeda.

**Implementasi**

Pertama Kita Buat Builder Rumah Kita

![](<../.gitbook/assets/image (80).png>)

disini kita mendifinikan kontrak untuk builder rumah kita. jadi siapapun mau bangun rumah harus punya properti diatas.

kita buat implementasi concreatenya

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

Dengan begini kita bebas membuat rumah kita sesuai dengan keinginan.

lihat di rumah kayu ada yang mempunyai tangga tapi tidak punya kolam renang sedangkan rumah kaca punya kolam renang tapi tidak punya tangga.

Dengan Begini kta bebas kreasi ruma kita.

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

Dengan begini kita tidak tergantung pada apapun. rumah kayu itu sebenarnya punya properti tangga tapi saya tidak mau memasangya dan tidak terjadi error sama sekali. jadi kita bisa bebas mau memakainya atu tidak sama sekali.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#4596" id="4596"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Code Full

```php
<?php

interface BuilderRumah{
    public function setJendela(int $jendela);
    public function setAtap(string $atap);
    public function setPintu(string $pintu);
    public function build();
}

class RumahKayu implements BuilderRumah{

    private $jendela;
    private $atap;
    private $pintu;
    private $tangga;
    public function setJendela(int $jendela)
    {
        $this->jendela =$jendela;
        return $this;
    }
    public function setAtap( string $atap)
    {
        $this->atap = $atap;
        return $this;
    }
    public function setPintu(string $pintu)
    {
        $this->pintu = $pintu;
        return $this;
    }

    public function settTangga(bool $tangga)
    {
        $this->tangga = $tangga;
        return $this;
    }

    public function build()
    {
        echo $this->jendela.$this->atap.$this->pintu.$this->tangga;
    }
}

class RumahKaca implements BuilderRumah{

    private $jendela;
    private $atap;
    private $pintu;
    private $kolam;

    public function setJendela(int $jendela)
    {
        $this->jendela =$jendela;
        return $this;
    }
    public function setAtap( string $atap)
    {
        $this->atap = $atap;
        return $this;
    }
    public function setPintu(string $pintu)
    {
        $this->pintu = $pintu;
        return $this;
    }

    public function kolamRenang(bool $kolam)
    {
        $this->kolam = $kolam;
        return $this;
    }

    public function build()
    {
        echo $this->jendela.$this->atap.$this->pintu.$this->kolam;
    }
}



class ClientCode{
    
    private $buildRumah;
    public function __construct(BuilderRumah $builderRumah)
    {
        $this->buildRumah = $builderRumah;
    }

    public function BangunRumah()
    {
        $this->buildRumah->build();
    }
}



$rumahKayu = new RumahKayu();

$rumahKayu->setJendela(2)->setAtap("semen")->setPintu("kayu");

$clicentCode = new ClientCode($rumahKayu);

$clicentCode->BangunRumah();
```

Semoga Mudah Dipahami Ya. **Salam Programmer Makassar**

\
