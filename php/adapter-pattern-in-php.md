# Adapter Pattern In PHP

Halo, perkenalkan nama saya ariadi ahmad. kali ini kita masuk ke pembahasan yang baru mengenai pattern. sekarang kita akan masuk ke structural pattern dan fokusnya kita akan membahas mengenai adapter pattern.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#d45d" id="d45d"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)



**Apa itu adapter patttern?**

Adapter Pattern menurut refactoring guru adalah pola desain struktural yang memungkinkan objek dengan antarmuka yang tidak kompatibel untuk berkolaborasi.

**Penjelasan.**

Jadi gini teman-teman. kita analogikan dengan colokan. kita tau colokan di indonesia itu mempunyai dua lubang tapi di luar indonesia itu berbeda lubang colokanya. maka untuk memakai colokan dari luar indonesia agar bisa compatible dengan colokan di indonesia maka kita butuh yang namanya adapter untu menyesuaikan dengan colokan yang ada di indonesia. jadi begitulah sekiranya penjelasan singkatnya.

**Implementasi**

misalkan kita punya perusahaan bernama writely yang perusahaanya bertujuan untuk melakukan penulisan document.

kita buat dlu interfacenya

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

buat implementasinya

<figure><img src="../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

sampai disini tidak ada masalah. sampai pada suatu waktu kita ingin mengganti teknologi ke google doc. dan ternyata google doc kita tidak sesuai dengan codingan yang kita buat. maka dari itu kita bisa membuat implementasi yang sesuai dengan menggunakan adapter

<figure><img src="../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>

Dengan begini kita berhasil mengganti teknologi kita. tanpa merusak kode inti di codingan kita. lihat di atas. kita masih mengimplementasikan interface yang sama. tapi kita sudah mengganti teknologi kita sesuai dengan kebutuhan yang kita inginkan.

Full Code

```php
<?php

// kita membuat interface autenticate
interface DocManager
{
public function authenticate($user, $pwd);
public function getDocuments($folderid);
public function getDocumentsByType($folderid, $type);
public function getFolders($folderid=null);
public function saveDocument($document);
}


class Writely implements DocManager
{
    public function authenticate($user, $pwd)
    {
    //authenticate using Writely authentication scheme
    }
    public function getDocuments($folderid)
    {
    //get documents available in a folder
    }
    public function getDocumentsByType($folderid, $type)
    {
    //get documents of specific type from a folder
    }
    public function getFolders($folderid=null)
    {
    //get all folders under a specific folder
    }

    public function saveDocument($document)
    {
    //save the document
    }
}


class GoogleDocsAdapter implements DocManager
{
    private $manager;

    public function __construct()
    {
    $this->manager = new GoogleDocs();
    }

    public function authenticate($user, $pwd)
    {
    $this->manager->setUser($user);
    $this->manager->setPwd($pwd);
    $this->manager->authenticateByClientLogin();
    }

    public function getDocuments($folderid)
    {
    return $this->manager->getAllDocuments();
    }
    
    public function getDocumentsByType($folderid, $type)
    {
    //get documents using GoogleDocs object and return only
    //which match the type
    }
    public function getFolders($folderid=null)
    {
    //for example there is no folder in GoogleDocs, so
    //return anything.
    }
    public function saveDocument($document)
    {
    //save the document using GoogleDocs object
    }
}
```

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#d45d" id="d45d"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Semoga mudah dipahami. **Salam Programmer Makassar**
