# Model Dan Migrasi



## Create Model

```go
type User struct {
	ID       uint   `gorm:"primaryKey"`
	Username string `gorm:"uniqueIndex"`
	Email    string
	Password string
}
```

Referensi: [https://gorm.io/docs/models.html](https://gorm.io/docs/models.html)

## Migrasi

```go
// Pastikan database sudah diinisialisasi
db, err := initializeDatabase()
if err != nil {
	panic(err)
}

// Melakukan migrasi untuk model User
db.AutoMigrate(&User{})
```

Referensi : [https://gorm.io/docs/migration.html](https://gorm.io/docs/migration.html)
