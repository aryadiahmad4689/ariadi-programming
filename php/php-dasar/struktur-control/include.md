# Include

`include` adalah sebuah perintah yang digunakan untuk menyisipkan (mengimpor) isi dari satu file ke dalam file PHP lainnya. Ini memungkinkan kita untuk menggunakan kode yang sama di berbagai file PHP tanpa harus menuliskannya ulang di setiap file

bayangkan kita memiliki beberapa file PHP yang memerlukan bagian-bagian yang sama, seperti header, footer, atau fungsi-fungsi tertentu. Daripada menyalin dan menempelkan kode yang sama di setiap file, kita bisa membuat file terpisah untuk bagian-bagian itu dan menggunakan `include` untuk memasukkannya ke dalam file-file PHP yang lain.

Contohnya, jika kita memiliki file `header.php` yang berisi kode untuk membuat bagian atas halaman web, dan kita ingin menggunakannya di beberapa file PHP lainnya, kita bisa menggunakan `include` seperti ini:

Tentu, mari berikan contoh yang lebih nyata dengan kasus penggunaan `include` dalam PHP.

Bayangkan kita memiliki sebuah situs web sederhana yang terdiri dari beberapa halaman seperti `index.php`, `about.php`, dan `contact.php`. Setiap halaman tersebut memiliki struktur yang sama untuk bagian header dan footer, tetapi kontennya berbeda.

Pertama, kita akan membuat file untuk bagian header dan footer, misalnya `header.php` dan `footer.php`. Berikut adalah contoh isi dari kedua file tersebut:

**header.php:**

```php
<!DOCTYPE html>
<html>
<head>
    <title>Contoh Situs Web</title>
    <link rel="stylesheet" type="text/css" href="style.css">
</head>
<body>
    <header>
        <h1>Selamat Datang di Contoh Situs Web</h1>
        <nav>
            <ul>
                <li><a href="index.php">Home</a></li>
                <li><a href="about.php">Tentang Kami</a></li>
                <li><a href="contact.php">Hubungi Kami</a></li>
            </ul>
        </nav>
    </header>
```

**footer.php:**

```php
    <footer>
        <p>Hak Cipta &copy; 2024 Contoh Situs Web</p>
    </footer>
</body>
</html>
```

Sekarang, mari kita lihat contoh bagaimana kita menggunakan `include` untuk menyertakan header dan footer ini di dalam halaman-halaman PHP lainnya, seperti `index.php`:

**index.php:**

```php
<?php
// Menyisipkan (include) bagian header
include 'header.php';
?>

<main>
    <h2>Selamat Datang di Halaman Utama</h2>
    <p>Ini adalah halaman utama situs kami.</p>
</main>

<?php
// Menyisipkan (include) bagian footer
include 'footer.php';
?>
```

Dengan cara ini, kita tidak perlu menuliskan kode header dan footer di setiap halaman. Kita hanya perlu menggunakan `include` untuk memasukkan kode tersebut di setiap halaman yang kita butuhkan. Ini membuat kode kita lebih mudah dipelihara dan mengurangi duplikasi kode yang tidak perlu.
