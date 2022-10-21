# Membuat Validasi Yang Baik Di Laravel

Haloo… perkenalkan nama saya ariadi ahmad, kali ini saya ingin sharing mengenai cara membuat validasi yang baik di laravel. dengan mempelajari ini kita bisa membuat code yang baik di program laravel kita.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#b9de" id="b9de"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Validasi adalah hal yang sangat krusial di dunia pemrogramang. maka dari itu sangat penting bagi kita untuk mengetahui praktik yang baik dalam membuat validasi. di laravel sendiri kita sudah di sediakan package untuk menangani validasi di tersebut.

**Contoh Validasi Yang Biasa Kita Buat**

****![](<../.gitbook/assets/image (73).png>)****

Seperti ini validasi yang biasa kita buat. lalu pertanyaanya apa ada masalah jika kita membuat validasi seperti ini?. sebenarnya ini sah-sah saja tapi dengan membuat seperti ini, kita melanggar pattern single resposibity pattern. yaitu kita melakukan dua action di dalam satu method. yang pertama kita validasi dan kedua kita menyimpan data.

Ada juga misalkan nih kita membuat method baru tapi validasi yang sama. apa yang kita lakukan? yang akan kita lakukan yaitu kita akan copy validasi tersebut dan kita gunakan di method yang kita ingin gunakan. dan ini mengulang pekerjaan yang sama bukan. dan melanggar prinsip DRY.

Kalau begitu ada ga cara membuat validasi yang baik di laravel?

Untungya laravel sudah menyediakan yang namanya **Request.** request sendiri sangat cocok untuk membuat validasi dan memang sangat di rekomendasikan membuat validasi dengan cara seperti ini.

Cara membuat request di laravel?

`php artisan make:request CustomerStoreRequest`

Maka akan di buatkan file di dalam folder request.

![](<../.gitbook/assets/image (56).png>)

<figure><img src="../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

kalian bisa membuat validasi dengan cara di atas dan kalian bisa juga melakukan custom pesan errornya jika kalian tidak ingin menggunakan pesan error defaultnya.

**Cara penggunaan di controller**

****![](<../.gitbook/assets/image (26).png>)****

jangan lupa panggil `use App\Http\Requests\CustomerStoreRequest;`

dengan begini store kalian hanya bertugas melakukan store saja.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#041b" id="041b"></a>

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#b9de" id="b9de"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Jadi sekian cara membuat validasi yang baik di laravel. jika kalian punya saran kalian bisa comment di kolom kementar. **Salam Programmer Makassar**

\
