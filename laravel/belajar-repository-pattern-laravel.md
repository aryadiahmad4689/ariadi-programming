# Belajar Repository Pattern Laravel

Halo perkenalkan nama saya ariadi ahmad. kali ini kita punya materi baru di laravel yaitu konsep repository pattern. disini kita akan membahas mengenai bagaimana cara kerja dari repository pattern.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#b9de" id="b9de"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Saya anggap kalian sudah mengenal laravel. jika kalian belum mengenal laravel kalian bisa belajar dulu. baru kita bisa melanjutkan ke konsep ini.

**Pentinya Repository Pattern?**

Konsep repository sendiri adalah bagian dari clean architecture. yaitu memisahkan abstraksi yang berhubungan dengan database dengan bisnis logic. prinsip ini juga sejalan dengan **SOLID Principle yaitu Single Responsibility.** dengan memisahkan bisnis logik dengan database kita bisa mendapatkan banyak manfaat nantinya. seperti code lebih clean dan mudah untuk di testing.

**Yang Sering Di Lakukan !**

Kebiasaan koding diatas sah-sah saja. dan kelihatanya tidak ada masalah. tapi dengan melakukan di atas maka kita sangat tergantung dengan model customer dan jika kita akan merubah maka kita akan mengotak atik controller.

Kita juga mencampur adukkan logic dan query database di controller. sungguh itu sangat tidak clean kan? maka dari itu kita memisahkan hal yang berbau querry database dengan logic bisnis kita.

Step By Step\
Download laravel di website resminya.

Setelah Itu Kita membuat sebuah folder baru di dalam `app/dengan nama Repository`

``![](<../.gitbook/assets/image (81).png>)``

Selanjutnya kita membuat duah buah file di dalam repository .sebagai contoh kita akan membuat `CustomerRepository.php dan CustomerRepositoryImplement.php` contoh kita yaitu menggunakan Customer yaa.

`CustomerRepository.php` kita isikan sebuah contract interface untuk membuat interface yang ingin kita gunakan di repository kita. disini saya mengisikan tiga method sebagai contoh.

```php
<?php
namespace App\Repository;
interface CustomerRepository{ 
    public function save($data); 
    public function findById(int $id); 
    public function findAll();
}
```

Selanjutnya kita akan mengisi `CustomerRepositoryImplement.php` dengan implementasi dari interface yang kita sudah buat di atas.

<figure><img src="../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

Setelah itu kita buat model customer dan controllernya

```
php artisan make:model Customer -m
php artisan make:controller CustomerController -m
```

![](<../.gitbook/assets/image (57).png>)

Untuk isi **`$fillable`** modelnya saya mengisikan dengan (nama,alamat,umur) saja sebagai contoh;

Cara Memakai Repository di controller?

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

1. Memanggi Interface dengan use `App\Repository\CustomerRepository;`
2. Kita passing dengan construct supaya controllernya tau bahwa dia butuh customer repository
3. Kita implement method yang diperlukan seperti contoh di atas.

Selanjutnya kita buatkan ServiceProvider agar kita bisa melakukan Devendency Injection

```
php artisan make:provider RepoServiceProvider
```

![](<../.gitbook/assets/image (74).png>)

Isinya kita cuma binding agar kita bisa pakai nantinya

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

Selanjutnya kita daftarkan provider kita di folder `config/app di bagian provider`

```
// repo providerApp\Providers\RepoServiceProvider::class,
```

Selesai.

**keuntungan?**

1. Misalkan kalian ingin merubah implementasinya. kalian ga perlu lagi mengubah controller cukup di repository
2. jika kalian ingin mengganti **`CustomerRepositoryImplement.php` ** dengan yang baru kalian tinggal ganti dengan meingikuti interface dan kalian bisa ubah behaviornya sesuka kalian
3. dengan begini kita bisa melakukan unit testing hanya pada reponya.
4. Code menjadi lebih clean

**Apakah Cara Diatas Sudah Sempurna?**

Untuk dibilang sempurna ini masih belum bisa di sebut sempurna. yang saya berikan di atas adalah contoh cara implementasi Repository Pattern di laravel. sebenarnya setiap orang beda beda cara implementasinya tapi yang harus kalian pahami bahwa repository pattern mengajak kita untuk memecah kompleksitas querry database dengan logic bisnis.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#b9de" id="b9de"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Cara diatas sebenarnya masih bisa diperbaiki dengan menambahkan yang namanya service. denga service kita memecah lagi logic dengan controller sehingga lebih clean lagi. sehingga controller hanya berisi proses bisnis yang ingin dilakukan.

Sampai disini dulu yaa. **SalamProgrammerMakassar**
