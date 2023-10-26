# Install And Connet

Install And Connect

install library gorm

```
go get -u gorm.io/gorm
```

install driver sqlite

```
go get -u gorm.io/driver/sqlite
```

Create Connection Golang

```go
package main

import (
	"fmt"
	"gorm.io/driver/sqlite"
	"gorm.io/gorm"
)

var db *gorm.DB
var err error

func initializeDatabase() (*gorm.DB, error) {
	// Membuat koneksi ke database SQLite
	db, err := gorm.Open(sqlite.Open("test.db"), &gorm.Config{})
	if err != nil {
		return nil, fmt.Errorf("failed to connect database: %v", err)
	}
	return db, nil
}

func main() {
	db, err = initializeDatabase()
	if err != nil {
		panic(err)
	}

    // Lanjutkan dengan operasi database menggunakan variabel `db`
}

```
