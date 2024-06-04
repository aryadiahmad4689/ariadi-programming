# NULL

Tipe data NULL adalah tipe khusus dalam PHP yang hanya memiliki satu nilai, yaitu `null`. Ini artinya, saat kalian menetapkan variabel dengan nilai `null`, itu berarti variabel tersebut tidak memiliki nilai atau tidak menunjuk ke apa pun. Tipe data NULL sering digunakan untuk mewakili ketiadaan nilai atau sebagai hasil dari operasi yang tidak mengembalikan nilai.

Misalnya, bayangkan kita memiliki sebuah variabel yang menyimpan alamat email pengguna yang belum ditentukan. Pada awalnya, variabel tersebut bisa diinisialisasi dengan `null` untuk menunjukkan bahwa alamat email belum ada:

```php
$email = NULL;
```

Ini berarti pada saat itu, variabel `$email` tidak memiliki nilai dan belum ditetapkan ke alamat email manapun.

Contoh lain adalah ketika kalian menghapus nilai dari suatu variabel:

```php
$deletedData = null;
```

Di sini, kita menetapkan variabel `$deletedData` ke `null` untuk menunjukkan bahwa data telah dihapus dan variabelnya kini tidak menunjuk ke data apapun.

Dalam penggunaan praktis, tipe data NULL sering digunakan sebagai inisialisasi default untuk variabel yang kemungkinan nilainya belum diketahui atau belum ditentukan, atau sebagai indikasi bahwa data sudah tidak lagi relevan atau telah dihapus. Ini membantu dalam mengelola data dengan lebih fleksibel dalam aplikasi PHP.
