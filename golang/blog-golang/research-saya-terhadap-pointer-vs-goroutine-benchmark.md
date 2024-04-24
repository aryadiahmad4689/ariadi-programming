# Research Saya Terhadap Pointer Vs Goroutine (Benchmark)

Halo semua kali ini saya akan membahas sedikit research saya mengenai gourotine dan pointer di golang. kenapa saya melakukan ini. karena di kantor tempat saya bekerja sekarang terjadi perubahan code yang sangat besar yaitu mengganti semuanya kedalam pointer dan terbukti itu sangat cepat dan luar biasa. akhirnya timbullah ide di dalam pikiran saya bagaimana kalau pointer di bandingkan dengan goroutine dalam read and write sebuah data, manakah yang akan lebih cepat? disclaimer terlebih dahulu. saya tidak tau apakah yang saya lakukan dalam menulis code ini sudah benar benar best practicenya jadi mungkin ini akan mempengaruhi hasil dari bench nya.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#id-8f78" id="id-8f78"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)



**Gouroutine**

goroutine mirip dengan thread, tapi sebenarnya bukan. Sebuah _native thread_ bisa berisikan sangat banyak goroutine. Mungkin lebih pas kalau goroutine disebut sebagai **mini thread**. Goroutine sangat ringan, hanya dibutuhkan sekitar **2kB** memori saja untuk satu buah goroutine. Eksekusi goroutine bersifat _asynchronous_, menjadikannya tidak saling tunggu dengan goroutine lain.

> _Karena goroutine sangat ringan, maka eksekusi banyak goroutine bukan masalah. Akan tetapi jika jumlah goroutine sangat banyak sekali (contoh 1 juta goroutine dijalankan pada komputer dengan RAM terbatas), memang proses akan jauh lebih cepat selesai, tapi memory/RAM pasti bengkak._
>
> Goroutine merupakan salah satu bagian paling penting dalam _concurrent programming_ di Go. Salah satu yang membuat goroutine sangat istimewa adalah eksekusi-nya dijalankan di multi core processor. Kita bisa tentukan berapa banyak core yang aktif, makin banyak akan makin cepat. (novalagung.com)

**Pointer**

_adalah reference_ atau alamat memori. Variabel pointer berarti variabel yang berisi alamat memori suatu nilai. Sebagai contoh sebuah variabel bertipe integer memiliki nilai **4**, maka yang dimaksud pointer adalah **alamat memori di mana nilai 4 disimpan**, bukan nilai 4 itu sendiri.

> Variabel-variabel yang memiliki _reference_ atau alamat pointer yang sama, saling berhubungan satu sama lain dan nilainya pasti sama. Ketika ada perubahan nilai, maka akan memberikan efek kepada variabel lain (yang referensi-nya sama) yaitu nilainya ikut berubah.(novalagung.com)

1. **Menulis Code Dengan Pointer**

Saya namai testnya dengan`BenchmarChange1`

![](<../../.gitbook/assets/image (67).png>)

dia atas adalah contoh codingan dengan menggunakan pointer

2\. Menulis Code Dengan Goroutine

Saya namai testnya dengan`BenchmarChange`

![](<../../.gitbook/assets/image (50).png>)

dia atas adalah contoh codingan dengan menggunakan goroutine

Ketika saya coba melakukan bencmark ternyata hasilnya menggunakan pointer jauh lebih cepat

![](<../../.gitbook/assets/image (19) (1).png>)

dari hasilnya kita bisa melihat yang menggunakan pointer hanya butuh waktu `0.0000009ns` saja dalam melakukan proses data berbeda jauh dengan menggunakan goroutine yang butuh waktu `0.0000050ns` untuk melakukan proses data. bahkan saya mengulang tiga kali tetap saja hasilnya pointer jauh lebih cepat dalam memproses sebuah data. saya tidak tau apakah saya sudah menggunakan best practice dalam menulis coding goroutine. mungkin ada saran?

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#id-8f78" id="id-8f78"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Jadi itulah hasil researchnya yaa. mungkin teman2 bisa memberikan masukan.

