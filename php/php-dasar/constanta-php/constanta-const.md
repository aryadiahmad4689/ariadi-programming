# Constanta (Const)

Di PHP, kalian bisa pake dua cara buat konstanta: pake `define()` atau pake `const`. Cara kedua ini, pake `const`, jadi lebih baru dan keren. Jadi, kalo kalian mau bikin konstanta pake `const`, kalian bisa kayak gini:

```php
const SITE_NAME = "My Website";
```

Nah, sama kayak sebelumnya, `SITE_NAME` jadi konstanta dan nilainya "My Website". Tapi inget, kalian enggak bisa pake `const` buat ngasih nilai dari variabel atau ekspresi, kaya gini:

```php
const PI = 3.14 * 2; // Ini bakal error, geng
```

Kalian juga bisa akses konstanta ini di mana aja dalam kode kalian, karena dia global. Jadi, enak banget buat ngebawa nilai yang sama di mana-mana dalam program kalian.
