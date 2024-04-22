# Belajar Service Layer Pattern Laravel

Halo perkenalkan nama saya ariadi ahmad. kali ini kita akan melanjutkan pembahasan kita mengenai laravel. pada tulisan kali ini kita mencoba menambahkan sebuah abstraksi layer baru bernama service. service nantinya ini berguna untuk menampung abstraksi Logic bisnis pada aplikasi kita.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#b9de" id="b9de"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Service Layer adalah sebuah design architecture untuk memisahkan logic dengan proses bisnis pada sebuah aplikasi. misalkan kalian punya proses bisnis mencari kota berdasarkan namanya. proses bisnisnya yaudah cuma masukkan nama lalu muncul kotanya. sedangkan logic bisnis yang ngurus bagaimana logicnya sebelum dapat kota yang di maksud. seperti itu gambaran besarnya.

**Step By Step**

Buka Project Laravel Kita Sebelumnya Tentang Repository Pattern.

Buatlah sebuah folder didalam `app` dengan nama `Service`

![](<../.gitbook/assets/image (41).png>)

Buatlah dua bua file `CustomerService.php dan CustomerServiceImplement.php`

Customer Service berguna untuk membuat contract pada aplikasi kita yang akan di implementasikan oleh `CustomerServiceImplement.php` .

Pada controller kita akan ada perubahan sedikit. kita yang awalnya melakukan dependency injection lansung ke repository sekarang kita inject dia ke service yang kita buat

```
protected $customerRepo;public function __construct(CustomerRepository $customerRepo){$this->customerRepo = $customerRepo;}
```

sekarang

<figure><img src="../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

kita mengganti semua methodnya berdasarkan yang kita buat di service

Selanjutnya kita buat `CustomerService.php` seperti ini.

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

Kemudian `CustomerServiceImplement.php` seperti ini

<figure><img src="../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

Waktu belajar repository kita awalnya nge inject repository lansung ke Controller sekarang kita inject dia lansung ke Servicenya. jadi intinya Dari `Repo->Service->Controller.` seperti inilah gambarang high levelnya.

Selanjutnya kita binding servicenya ke service provider. disini saya menggunakan `RepoServiceProvider.php` sebagai contoh. kalian bisa membuat service provider sendiri jika kalian mau.

<figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

Selanjutnya kit test aplikasinya menggunakan Test/Feature karena kita juga sudah belajar test pada tulisan sebelumnya. testnya sederhana kita cuma pengen tau dia berhasil tambah data.

<figure><img src="../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

test

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

Kita suddah berhasil membuat service pattern.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#b9de" id="b9de"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Reponya Bisa Kalian Kunjungi di [https://github.com/aryadiahmad4689/belajar-clean-architecture-laravel](https://github.com/aryadiahmad4689/belajar-clean-architecture-laravel)

Terimah Kasih. **Salam Programmer Makassar**
