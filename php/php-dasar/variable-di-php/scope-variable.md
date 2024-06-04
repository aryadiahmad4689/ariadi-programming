# Scope Variable

Di PHP, cakupan variabel (variable scope) menentukan di mana variabel bisa diakses dalam kode. Ada beberapa jenis cakupan variabel yang perlu kita pahami:

1. **Lokal**: Variabel yang didefinisikan di dalam fungsi hanya tersedia di dalam fungsi tersebut dan tidak bisa diakses dari luar fungsi.
2. **Global**: Variabel yang didefinisikan di luar semua fungsi memiliki cakupan global dan bisa diakses dari mana saja dalam skrip kecuali dari dalam fungsi, kecuali jika variabel tersebut secara eksplisit dinyatakan sebagai global di dalam fungsi tersebut.
3. **Static**: Variabel statis di dalam fungsi mempertahankan nilai mereka antar pemanggilan fungsi dan hanya hilang ketika eksekusi skrip berakhir. Ini berguna ketika kita perlu menyimpan informasi antar pemanggilan fungsi tanpa menggunakan variabel global.

#### Contoh:

Untuk memahami variabel lokal, global, dan statis, kita bisa melihat contoh berikut:

```php
$x = 5; // variabel global

function tesLokal() {
    $y = 10; // variabel lokal
    echo $y;
}

function tesGlobal() {
    global $x;
    echo $x;
}

function tesStatic() {
    static $count = 0; // variabel statis
    $count++;
    echo $count;
}

tesLokal();   // Output akan 10
tesGlobal();  // Output akan 5
tesStatic();  // Output akan 1
tesStatic();  // Output akan 2
```

Di contoh di atas, variabel `$y` adalah lokal untuk fungsi `tesLokal` dan tidak bisa diakses dari luar fungsi tersebut. Variabel `$x` adalah global dan diakses di dalam `tesGlobal` dengan kata kunci `global`. Variabel `$count` adalah statis yang menyimpan nilai antara pemanggilan fungsi.

#### Informasi Tambahan:

* Menggunakan variabel global secara berlebihan bisa membuat kode susah untuk diikuti dan dikelola. Lebih baik gunakan parameter fungsi untuk mengirimkan variabel ke fungsi.
* Variabel statis berguna tetapi harus digunakan dengan hati-hati karena mereka mempertahankan nilai antara pemanggilan fungsi dan bisa menyebabkan perilaku yang tidak terduga jika tidak dimanage dengan baik.

