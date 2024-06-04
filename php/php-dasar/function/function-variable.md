# Function Variable

Variable Function adalah kemampuan dalam PHP untuk menyimpan nama fungsi ke dalam sebuah variabel dan kemudian memanggil fungsi tersebut menggunakan variabel tersebut.

1.  **Contoh**:

    ```php
    <?php
    function greet() {
        echo "Halo, dunia!";
    }

    $funcName = "greet";
    $funcName(); // Output: Halo, dunia!
    ?>
    ```

    Pada contoh di atas, kita mendefinisikan fungsi `greet()`, kemudian menyimpan nama fungsi tersebut ke dalam variabel `$funcName`. Setelah itu, kita memanggil fungsi tersebut menggunakan variabel `$funcName`.
2. **Informasi Penting**:
   * Dalam PHP, menggunakan Variable Function memungkinkan kalian untuk membuat kode yang lebih dinamis, karena kalian dapat menentukan fungsi mana yang ingin dipanggil berdasarkan kondisi atau input tertentu.
   * Penting untuk memastikan bahwa nama fungsi yang disimpan dalam variabel sudah terdefinisi sebelumnya, atau akan menyebabkan kesalahan (error) saat mencoba memanggilnya.
   * Variable Function dapat digunakan untuk mengimplementasikan pola desain tertentu seperti Strategi atau Pemetaan Nama (Name Mapping).
