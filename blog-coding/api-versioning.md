# Api Versioning

Mengapa Menggunakan Versi API?&#x20;

Bayangkan kita memiliki API untuk prakiraan cuaca. Ribuan situs web menggunakannya untuk membuat dasbor dan aplikasi lainnya.

Katakanlah kita ingin mengubah kontrak data objek respons kita. Hal ini dapat melibatkan penggantian nama bidang, penambahan bidang baru, atau perubahan seluruh kontrak data. Jika kita mengubah nama bidang yang ada, aplikasi pengguna kita mungkin berhenti bekerja atau mulai menimbulkan kesalahan

![](<../.gitbook/assets/image (91).png>)\
\


<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Untuk memperbaikinya, kita harus meminta semua pengguna kita untuk memperbarui aplikasi mereka agar dapat bekerja dengan perubahan terbaru Kita. Jika ini sering terjadi, pengguna akan frustrasi. \
\
Pembuatan versi dapat memecahkan masalah ini. karena dengan pembuatan versi, client dapat memilih kapan dia ingin menggunakan versi terbarunya dan kapan dia tidak ingin.

Itu sebabnya merancang perubahan sangat penting untuk API. Kita harus menggunakan pembuatan versi untuk memberikan perubahan kepada pengguna dengan cara yang jelas, konsisten, dan terdokumentasi dengan baik.\
\
**Kapan Membuat Versi API?**

Pembuatan versi tidak boleh dilakukan terlalu sering, karena dapat mengganggu dan mengharuskan pengembang untuk sering memperbarui kode mereka.&#x20;

Berikut beberapa skenario ketika versi API baru diperlukan:

**Perubahan yang dapat menyebabkan kerusakan:** Saat kita melakukan perubahan yang berpotensi merusak perangkat lunak. Misalnya, memperkenalkan kolom wajib baru di payload atau menghapus parameter yang tidak lagi valid dalam panggilan API.&#x20;

**Fitur Baru:** Saat menambahkan fitur atau fungsi baru ke API sambil memastikan kompatibilitas dengan pengguna yang sudah ada.

**Perbaikan Bug:** Saat mengatasi bug atau masalah di API, penting untuk menerapkan perbaikan tanpa menimbulkan gangguan pada konsumen yang sudah ada.

**Peningkatan Kinerja:** Saat menerapkan peningkatan atau pengoptimalan kinerja yang dapat mengubah cara pengguna berinteraksi dengan API.

### Strategi Versi

Sejauh ini, kita telah membahas pembuatan versi API dan mengapa kita membutuhkannya. Sekarang, mari kita jelajahi beberapa pendekatan untuk pembuatan versi.&#x20;

* Strategi perubahan aditif
* Strategi versi eksplisit

#### Strategi perubahan aditif

Dalam pendekatan ini, Kita menambahkan fitur atau kolom baru ke API  tanpa mengubah yang sudah ada. Setiap pembaruan pada API harus kompatibel dengan versi sebelumnya.&#x20;

Namun, beberapa operasi tidak diperbolehkan dalam strategi perubahan aditif. Tabel di bawah menunjukkan beberapa operasi tersebut.&#x20;

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

Di sisi lain, ada beberapa hal yang boleh di lakukan.&#x20;

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Poin terakhir dalam tabel operasi yang diizinkan mungkin tampak bertentangan, namun sebenarnya tidak. Ide utamanya adalah untuk menghindari perubahan yang merusak. Selama pengguna dapat ikut serta.

Misalnya, kita memiliki respons berikut di API cuaca fiktif seperti yang ditunjukkan di bawah ini.

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

**Catatan:** _Dalam strategi perubahan aditif, menambahkan perubahan baru tidak dianggap sebagai perubahan yang dapat menghentikan. Namun, ada pengecualian terhadap aturan ini. Misalnya, kita tidak dapat menambahkan parameter kueri yang diperlukan. Dalam contoh di atas, kita tidak bisa menjadikan parameter kueri_ **“ **_**exclude\_pressure=true”** wajib._ \
\
**Strategi pembuatan versi eksplisit**

Dalam pendekatan ini, kita menyimpan beberapa versi API. Saat kita ingin melakukan perubahan pada API, kita merilisnya sebagai versi baru. Hal ini berbeda dengan strategi perubahan aditif, yang tidak memperbolehkan perubahan yang dapat dihentikan. Strategi pembuatan versi eksplisit memungkinkan kita melakukan perubahan apa pun, dan itulah perbedaan utamanya.\
\
**Uri Component**\
![](<../.gitbook/assets/image (4).png>)\
\
**Keunggulan**\
![](<../.gitbook/assets/image (5).png>)

**Http Header Versioning**\
![](<../.gitbook/assets/image (6).png>)

**Keunggulan**\
![](<../.gitbook/assets/image (8).png>)

**Minta pembuatan versi parameter**\
![](<../.gitbook/assets/image (9).png>)

**Keunggulan**

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>
