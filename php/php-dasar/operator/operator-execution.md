# Operator Execution

Di dalam PHP, ada satu operator eksekusi: backticks (\`\`). Perhatikan bahwa ini bukan tanda kutip tunggal! PHP akan mencoba menjalankan isi dari backticks sebagai perintah shell; hasilnya akan dikembalikan (artinya, tidak hanya ditampilkan pada output; dapat ditugaskan ke dalam variabel). Penggunaan operator backtick identik dengan fungsi shell\_exec().

```php
<?php
$output = `ls -al`;
echo "<pre>$output</pre>";
?>
```

Catatan:

* Operator backtick dinonaktifkan ketika fungsi shell\_exec() dinonaktifkan.

Catatan:

* Berbeda dengan beberapa bahasa pemrograman lainnya, backticks tidak memiliki arti khusus dalam string yang diapit oleh tanda kutip ganda.

Informasi tambahan: Penting untuk diketahui bahwa operator backtick dapat membantu dalam menjalankan perintah shell dari dalam skrip PHP. Namun, perlu diingat bahwa penggunaan ini dapat meningkatkan risiko keamanan jika tidak digunakan dengan hati-hati, terutama jika data yang diterima dari pengguna diintegrasikan ke dalam perintah shell tersebut tanpa validasi atau sanitasi yang memadai. Selain itu, pastikan bahwa penggunaan shell\_exec() dan operator backtick tidak dinonaktifkan dalam pengaturan PHP yang berlaku.
