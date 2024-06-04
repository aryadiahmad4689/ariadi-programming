# Praktek Pelajaran PHP Dasar

```php
<?php
// Struktur dasar skrip PHP

// Variabel dan tipe data
$angka = array(20, 30, 25, 35, 40); // Array indeks untuk menyimpan angka
$total = 0; // Integer untuk menyimpan total
$nilaiRataRata = 0.0; // Float untuk menyimpan nilai rata-rata

// Menghitung total menggunakan perulangan
foreach ($angka as $nilai) {
    $total += $nilai; // Menggunakan operator penugasan
}

// Menghitung nilai rata-rata
$jumlahAngka = count($angka); // Menghitung jumlah elemen dalam array
if ($jumlahAngka > 0) { // Pengkondisian
    $nilaiRataRata = $total / $jumlahAngka; // Menggunakan operator aritmatika
}

function klasifikasiNilai($nilai) {
    if ($nilai >= 35) {
        return "Tinggi";
    } elseif ($nilai >= 25) {
        return "Sedang";
    } else {
        return "Rendah";
    }
}

// Menentukan tipe nilai rata-rata
$tipeNilai = is_int($nilaiRataRata) ? "Bilangan Bulat" : "Pecahan";

// Mengklasifikasikan nilai rata-rata
$klasifikasi = klasifikasiNilai($nilaiRataRata);

// Menampilkan hasil
echo "Total: $total ";
echo "Nilai Rata-Rata: $nilaiRataRata - Tipe: $tipeNilai ";
echo "Klasifikasi: $klasifikasi ";
?>
```
