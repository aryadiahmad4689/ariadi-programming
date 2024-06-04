# Operator Perbandingan

Operator perbandingan dalam PHP digunakan untuk membandingkan dua nilai dan mengevaluasi kondisi menjadi benar (TRUE) atau salah (FALSE).

```php
<!-- 1. **Sama dengan (`==`):** Memeriksa apakah dua nilai memiliki nilai yang sama. -->
   <?php
   if (5 == 5) {
       echo "Benar"; // Output: Benar
   }
   ?>

<!-- 2. **Identik (`===`):** Memeriksa apakah dua nilai memiliki nilai yang sama dan tipe data yang sama. -->
   <?php
   if (5 === "5") {
       echo "Benar";
   } else {
       echo "Salah"; // Output: Salah
   }
   ?>

<!-- 3. **Tidak sama dengan (`!=` atau `<>`):** Memeriksa apakah dua nilai tidak sama. -->
   <?php
   if (5 != 10) {
       echo "Benar"; // Output: Benar
   }
   ?>

<!-- 4. **Tidak identik (`!==`):** Memeriksa apakah dua nilai tidak sama atau tidak memiliki tipe data yang sama. -->
   <?php
   if (5 !== "5") {
       echo "Benar"; // Output: Benar
   }
   ?>

<!-- 5. **Lebih besar dari (`>`):** Memeriksa apakah nilai di sebelah kiri lebih besar dari nilai di sebelah kanan. -->
   <?php
   if (10 > 5) {
       echo "Benar"; // Output: Benar
   }
   ?>

<!-- 6. **Lebih kecil dari (`<`):** Memeriksa apakah nilai di sebelah kiri lebih kecil dari nilai di sebelah kanan. -->
   <?php
   if (5 < 10) {
       echo "Benar"; // Output: Benar
   }
   ?>

<!-- 7. **Lebih besar atau sama dengan (`>=`):** Memeriksa apakah nilai di sebelah kiri lebih besar dari atau sama dengan nilai di sebelah kanan. -->
   <?php
   if (5 >= 5) {
       echo "Benar"; // Output: Benar
   }
   ?>

<!-- 8. **Lebih kecil atau sama dengan (`<=`):** Memeriksa apakah nilai di sebelah kiri lebih kecil dari atau sama dengan nilai di sebelah kanan. -->
   <?php
   if (5 <= 10) {
       echo "Benar"; // Output: Benar
   }
   ?>
```
