# Berkenalan Dengan Test Di Laravel

Halo semua kali ini kita akan masuk ke topik baru di laravel yaitu testing. testing sangat penting bagi development karena akan mempermudah kita mengetahui letak error atau masalah pada aplikasi website kita. di sini kita akan melanjutkan belajar laravel kita dengan topik baru yaitu testing pada laravel.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawa**h** <a href="#id-9a3c" id="id-9a3c"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Sebelum lanjut kalian bisa belajar terlebih dahulu mengenai apa itu\
— Unit testing\
— Integration testing\
— N2N testing

Mengenai topik di atas kalian bisa mencari referensinya di google

Oke pertama, kalian harus mendownload laravel jika kalian belum punya laravel atau menggunakan project laravel sebelumnya saat membuat Crud di laravel.

kalian bisa menuju kebawah dan cari folder tests di laravel kalian

![](<../../.gitbook/assets/image (48).png>)

di dalam folder ini terdapat dua folder yaitu folder yaitu unit dan feature

**Feature :** adalah sebuah folder untuk membuat test mengenai feature-feature yang ada di laravel. biasanya isi dari folder ini adalah test mengenai integration testing pada laravel\
**Unit :** Adalah sebuah folder untuk membuat test mengenai unit terkecil pada laravel. biasaya isinya adalah function2 dari sebuah kelas.

**Cara Membuat Test Di folder Feature?**\
kalian bisa mengetikkan perintah ini di terminal kalian\
`php artisan make:test CustomerTest`

![](<../../.gitbook/assets/image (24).png>)

**Cara menjalankan test di feature ?**\
`vendor/bin/phpunit — testsuite=Feature or php artisan test — testsuite=Feature`

<figure><img src="../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

Disini kita mendapatkan 2 test passed karena kita punya 2 test dan 2 assertion

**Cara membuat tets di folder unit ?**\
kalian bisa mengetikkan perintah ini di terminal kalian\
`php artisan make:test CustomerTest --unit`

![](<../../.gitbook/assets/image (82).png>)

**Cara menjalankan test di unit?**

`vendor/bin/phpunit tests/Unit or php artisan test tests/Unit`

<figure><img src="../../.gitbook/assets/image (6) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawa**h** <a href="#id-9a3c" id="id-9a3c"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Itulah sedikit perkenalan mengenai testing di laravel bagi kalian yang ingin mencoba sendiri lebih dalam lagi tentang testing di laravel jadi kalian bisa ikuti panduan di laravel resminya atau nonton youtube untuk beberapa chanel yang membahas mengenai laravel testing. untuk praktik yang lainya mungkin kita bisa melanjutkan dengan membuat test untuk crud yang sudah kita buat sebelumnya. sebenarnya saya lagi sibuk skripsian dan belajar juga jadi jarang posting article lagi.

\
