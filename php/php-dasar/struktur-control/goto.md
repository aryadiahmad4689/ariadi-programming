# Goto

Goto pada PHP adalah suatu perintah yang memungkinkan kita untuk langsung melompat ke bagian tertentu dalam kode program. Misalnya, kita ingin langsung berpindah ke bagian tertentu dalam program tanpa perlu mengeksekusi baris kode di antaranya. Ini mirip dengan melempar diri kita ke suatu tempat dalam kode secara langsung.

Contohnya, kita punya kode seperti ini:

```php
echo "Baris pertama. ";
goto end;
echo "Baris kedua. "; // Baris ini tidak akan dieksekusi jika kita menggunakan goto
end:
echo "Baris terakhir. ";
```

Jika kita menjalankan kode di atas, outputnya akan menjadi:

```
Baris pertama. Baris terakhir.
```

Penting untuk diingat bahwa penggunaan `goto` dalam kode bisa membuatnya sulit untuk dipahami, terutama saat kode menjadi lebih besar. Hal ini dapat mengganggu alur logika program dan menyulitkan untuk memahami bagaimana suatu program berfungsi. Oleh karena itu, sebaiknya hindari penggunaan `goto` kecuali dalam situasi yang sangat spesifik dan diperlukan. Lebih baik gunakan struktur kontrol seperti `if`, `else`, dan `loop` untuk mengatur alur program dengan lebih terstruktur dan mudah dipahami.
