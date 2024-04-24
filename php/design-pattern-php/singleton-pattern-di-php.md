# Singleton Pattern Di PHP

Halo nama saya ariadi ahmad. kali ini kita akan membahas desing pattern lagi yaitu singleton pattern.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#4596" id="4596"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Penjelasan

Menurut refactoring guru singleton adalah pola desain kreasi yang memungkinkan Anda memastikan bahwa kelas hanya memiliki satu instance, sambil memberikan titik akses global ke instance ini.

Jadi intinya begini teman-teman. pattern singleton ini mengajak kita untuk setiap kali kita ingin membuat sebuah instance ke sebuah kelas dan jika kelas itu sama harusnya hanya ada satu instance aja.

Contoh

```
$instance1 = new Instance;
```

Jika kita melakukan hal diatas berarti kita menyimpan sebuah memori untuk variable diatas dan isinya adalah `new Instance` tadi. jadi ketika kita ingin memanggil class instance diatas harus ada mekanisme yang mengetahui bahwa instance tersebut sudah ada di memory jadi ketika kita melakukan inisiasi ke kelas yang sama kita tidak perlu membuat baru lagi cukup pakai yang sudah ada. begitulah penjelasanya kira-kira.

**Implementasi**

```php
<?php
class Database {    
   private static $instance = null;     
   public static function getInstance()    {        
       if (self::$instance == null) {            
       self::$instance = new Database();        
        }         
       return self::$instance;   
   }    
   public function query($sql)    {        
    echo "Mengeksekusi \"{$sql}\" ..<br/>";    
   }
 
}
```

Apa yang di lakukan diatas.

1. Membuat Sebuah Class Database
2. Membuat Sebuah Method getInstance()
3. Melakukan pengecekan di dalam method. jika class ini belum di buat maka saya ingin class ini melakukan instansiasi baru. tapi jika sudah ada kembalikan saja nilainya.

Cara penggunaanya

`$database = Database::getInstance()`

`$database->query("select * from customer");`

Dengan begini kita memastikan bahwa kita hanya melakukan satu kali instansiasi class.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#4596" id="4596"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

**Noted**

_Tidak semua class butuh satu kali instasisasi ada beberapa kasus tertentu kita ingin classnya itu membuat alamat memori baru._

Semoga Mudah di pahami. **Salam Programmer Makassar**
