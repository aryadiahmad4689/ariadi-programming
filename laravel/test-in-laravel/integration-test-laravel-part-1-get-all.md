# Integration Test Laravel Part 1-Get All

Halo guys kembali lagi kita pada materi testing pada laravel. kali ini kita akan ngetes method index di laravel crud kita yang kemarin . jadi ini kita lanjut aja ya materinya biar ga ngulang dari awal.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawa**h** <a href="#id-9a3c" id="id-9a3c"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Disini kita tidak pure TDD karena kita ga ngetes dlu baru buat tapi kita buat dlu baru ngetes. karena TDD konsepnya kita harus buat dlu testnya baru buat functionnya. oke lansung saja kita masuk ke project laravel kita yang kemarin.

![](<../../.gitbook/assets/image (75).png>)

Disini kita hanya melakan integration testing pada laravel kita. jadi kita test full datanya secara real. walaupun ini sebenarnya mahal dari segi test tapi ini setidaknya kita bisa lihat real aplikasinya kalau berjalan bagaimana. dari semua test saya paling sering saya gunakan adalah test integration, karena saya tidak perlu unit test terlalu banyak karena biasanya sudah tercoverage disini. oke ayo kita mulai.

Kalian ketikkan perintah untuk ngebuat test feature di folder test.

`php artisan make:test CustomerTest`

![](<../../.gitbook/assets/image (29).png>)

Maka akan terbuat sebuah file php dengan nama CustomerTest.php di folder Feature. Sekarang kita tulis test untuk method indexnya.

Jadi yang akan kita test adalah function di bawah dengan menembak lansung routenya.

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

Test Pertama kita buat adalah ngetest test\_index\_success

<figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

```php
$this->withoutExceptionHandling(); ini untuk mengecek jika ada error
$customers = Customer::all();
$response = $this->get(‘customer-index’);
$response->assertViewHas(‘customers’,$customers); melihat datanya apakah sudah sesuai
$response->assertStatus(200); ngecek status codenya
$response->assertSee(“Nama”); ngecek di page ada ga properti ini
```

Setelah Itu Kita Jalankan Testya dengan mengetik perintah

`.vendor/bin/phpunit tests/Feature/CustomerTest.php -v`

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

Disini kita melihat test kita berhasil dengan satu test 3 assertion yang kita masukkan.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawa**h** <a href="#id-9a3c" id="id-9a3c"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Sebenarnya masih banyak lagi yang bisa kita test disini seperti bagaimana kalau gagal test. harusnya kita ngecoverage semua testnya tapi disini saya hanya menunjukkan bagaimana kalau berhasil. berbekal ini saya yakin kalian bisa buat test untuk selanjutnya.

Oke nanti selanjutnya kita akan test Create datanya yaa. jadi di tunggu aja. karena lagi sibuk skripsi dan belajar juga. **Salam Programmer Makassar**

\
