# Return

Return" adalah sebuah perintah dalam PHP yang digunakan untuk mengembalikan nilai dari suatu fungsi. Ketika kita membuat sebuah fungsi di PHP, kita dapat menggunakan "return" untuk mengirimkan nilai kembali ke tempat di mana fungsi itu dipanggil.

1.  Contoh:

    ```php
    function tambah($a, $b) {
        $hasil = $a + $b;
        return $hasil;
    }

    $jumlah = tambah(3, 4); // Panggil fungsi tambah dan simpan hasilnya dalam variabel $jumlah
    echo $jumlah; // Output: 7
    ```

    Pada contoh di atas, fungsi "tambah" menerima dua parameter, menjumlahkannya, dan kemudian mengembalikan hasil penjumlahan tersebut. Nilai yang dikembalikan kemudian disimpan dalam variabel `$jumlah` dan dicetak menggunakan `echo`.

**Informasi tambahan yang penting:**

* "Return" sangat berguna ketika kita ingin menggunakan nilai yang dihasilkan dari sebuah fungsi untuk operasi selanjutnya dalam program kita.
* Kalian harus memperhatikan bahwa setelah perintah "return" dijalankan dalam sebuah fungsi, eksekusi kode di dalam fungsi tersebut berhenti dan nilai yang dikembalikan akan disampaikan ke tempat di mana fungsi itu dipanggil.
* Kalian juga bisa mengembalikan lebih dari satu nilai menggunakan array atau tipe data lain yang dapat menyimpan banyak nilai.
* Pastikan untuk mengembalikan tipe data yang sesuai dengan yang diharapkan oleh kode yang memanggil fungsi tersebut, karena hal ini dapat menghindari kesalahan atau bug dalam program.
