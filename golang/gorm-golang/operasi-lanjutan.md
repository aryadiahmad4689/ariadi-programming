# Operasi Lanjutan

***

**1. Query dengan Relasi:**

Jika Anda memiliki model yang berhubungan, Anda dapat dengan mudah menarik relasi tersebut:

```go
type Profile struct {
	ID     uint
	Name   string
	UserID uint
	User   User
}

db.Preload("User").Find(&profiles)

// Membuat profile untuk user baru
newProfile := Profile{Name: "Alice Wonderland", UserID: newUser.ID}
db.Create(&newProfile)

// Menampilkan semua profil dengan informasi pengguna yang terkait
var profiles []Profile
db.Preload("User").Find(&profiles)

for _, profile := range profiles {
    fmt.Printf("Profile Name: %s, Username: %s, Email: %s\n", profile.Name, profile.User.Username, profile.User.Email)
}
```

* `Preload` memastikan bahwa relasi `User` untuk setiap `Profile` juga dimuat.

***

**2. Pemilihan Kolom Khusus:**

Jika Anda hanya ingin memilih beberapa kolom tertentu:

```go
var usernames []string
db.Model(&User{}).Pluck("username", &usernames)
```

***

**3. Pengurutan dan Limitasi:**

Mengurutkan hasil berdasarkan kolom tertentu dan membatasi jumlah hasil:

```go
var users []User
db.Order("username desc").Limit(5).Find(&users)
```

***

**4. Pengelompokan dan Agregasi:**

Misalkan Anda ingin menghitung jumlah pengguna dengan email domain yang sama:

```go
type Result struct {
	Domain string
	Count  int
}

var results []Result
db.Model(&User{}).Select("SUBSTR(email, INSTR(email, '@') + 1) AS domain, COUNT(*) as count").Group("domain").Scan(&results)
```

***

**5. Menggunakan Raw SQL:**

Jika Anda perlu menulis query SQL kustom:

```go
var users []User
db.Raw("SELECT * FROM users WHERE username = ?", "ariadi").Scan(&users)
```

***

**6. Pengkondisian Lebih Lanjut:**

Untuk kasus-kasus yang lebih kompleks, Anda bisa menggunakan `Where`:

```go
db.Where("username LIKE ? ", "ari%").Find(&users)
```

***

**Kesimpulan:**

GORM memberikan kekuatan penuh dalam mengakses dan memanipulasi database, mulai dari operasi sederhana hingga query lanjutan yang kompleks. Meskipun begitu, selalu pastikan untuk memahami efek dari query yang Anda jalankan, terutama dalam hal kinerja dan keamanan.
