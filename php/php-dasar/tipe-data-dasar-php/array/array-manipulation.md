# Array Manipulation

Fungsi manipulasi array dalam PHP sangat berguna untuk mengolah data dalam array.

```php
<!-- ### 1. `array_push()`
- **Deskripsi**: Menambahkan satu atau lebih elemen ke akhir array.
- **Contoh**: -->
<?php
  $arr = [1, 2, 3];
  array_push($arr, 4, 5);
  print_r($arr); // Output: Array ( [0] => 1 [1] => 2 [2] => 3 [3] => 4 [4] => 5 )
?>

<!-- ### 2. `array_pop()`
- **Deskripsi**: Menghapus elemen terakhir dari array dan mengembalikannya.
- **Contoh**: -->
<?php
  $arr = [1, 2, 3, 4];
  $lastElement = array_pop($arr);
  echo $lastElement; // Output: 4
  print_r($arr); // Output: Array ( [0] => 1 [1] => 2 [2] => 3 )
?>

<!-- ### 3. `array_shift()`
- **Deskripsi**: Menghapus elemen pertama dari array dan mengembalikannya, menggeser semua elemen lain ke bawah.
- **Contoh**: -->
<?php
  $arr = ['a', 'b', 'c'];
  $firstElement = array_shift($arr);
  echo $firstElement; // Output: a
  print_r($arr); // Output: Array ( [0] => b [1] => c )
?>

<!-- ### 4. `array_unshift()`
- **Deskripsi**: Menambahkan satu atau lebih elemen ke awal array.
- **Contoh**: -->
<?php
  $arr = ['b', 'c'];
  array_unshift($arr, 'a');
  print_r($arr); // Output: Array ( [0] => a [1] => b [2] => c )
?>

<!-- ### 5. `array_slice()`
- **Deskripsi**: Mengembalikan potongan array.
- **Contoh**: -->
<?php
  $arr = [1, 2, 3, 4, 5];
  $slice = array_slice($arr, 1, 3);
  print_r($slice); // Output: Array ( [0] => 2 [1] => 3 [2] => 4 )
?>

<!-- ### 6. `array_merge()`
- **Deskripsi**: Menggabungkan satu atau lebih array.
- **Contoh**: -->
<?php
  $array1 = [1, 2, 3];
  $array2 = [4, 5, 6];
  $result = array_merge($array1, $array2);
  print_r($result); // Output: Array ( [0] => 1 [1] => 2 [2] => 3 [3] => 4 [4] => 5 [5] => 6 )
?>

<!-- ### 7. `sort()`
- **Deskripsi**: Mengurutkan array.
- **Contoh**: -->
<?php
  $arr = [3, 1, 2];
  sort($arr);
  print_r($arr); // Output: Array ( [0] => 1 [1] => 2 [2] => 3 )
?>
```
