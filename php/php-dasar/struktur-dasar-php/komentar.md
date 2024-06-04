# Komentar

Pada PHP, komentar digunakan untuk memberikan penjelasan tentang kode yang tidak dijalankan oleh mesin. Ada tiga jenis komentar:

1.  **Komentar Satu Baris** menggunakan `//` atau `#`. Contoh:

    ```php
    // Ini komentar satu baris
    # Ini juga komentar satu baris
    ```

    Komentar ini berhenti di akhir baris atau blok kode PHP, mana yang lebih dulu.
2.  **Komentar Multi-Baris** menggunakan `/* */`. Contoh:

    ```php
    /* Ini adalah komentar
       yang melintasi beberapa baris */
    ```

    Komentar jenis ini berakhir saat menemukan `*/` dan tidak boleh bersarang dalam komentar lain.
3. **Penggunaan Spesial** pada PHP 8, komentar satu baris yang dimulai dengan `#[` memiliki arti khusus sebagai "atribut.\
   `<?php #[~~my super cool comment~~~] ?>`

Komentar tidak mempengaruhi kinerja karena tidak diproses oleh PHP.

Untuk penjelasan lebih mendetail, Anda bisa mengunjungi [dokumentasi PHP tentang komentar](https://www.php.net/manual/en/language.basic-syntax.comments.php).
