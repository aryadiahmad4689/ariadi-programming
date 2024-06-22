# Rate Limiter Http Di Golang

Halo Semua, kali ini saya akan sharing tentang rate limiter di golang. rate limiter sendiri adalah sebuah metode untuk membatalkan request dari pengguna yang terlalu banyak dalam waktu bersamaan.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawa**h** <a href="#id-9a3c" id="id-9a3c"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

**Implementasi**

Kita membuat sebuah folder bernama `middleware` dan di dalamnya buat sebuah file bernama `limiter.go`

```go
package middleware

import (
	"log"
	"net"
	"net/http"
	"sync"
	"time"

	"golang.org/x/time/rate"
)

// getVisitor
type visitor struct {
	limiter  *rate.Limiter
	lastSeen time.Time
}

var visitors = make(map[string]*visitor)
var mu sync.Mutex

// menjalankan di belakang clean up visitor
func init() {
	go cleanupVisitors()
}

// membersihkan map visitor ketika sudah tiga menit
func cleanupVisitors() {
	for {
		time.Sleep(time.Minute)

		mu.Lock()
		for ip, v := range visitors {
			if time.Since(v.lastSeen) > 3*time.Minute {
				delete(visitors, ip)
			}
		}
		mu.Unlock()
	}
}

// menangkap semua pengunjung berdasarkan ip yang melakukan request
func getVisitor(ip string) *rate.Limiter {
	mu.Lock()
	defer mu.Unlock()
	v, exists := visitors[ip]
	// mengecheck apakah ip ini ada
	// jika tidak ada daftarkan ipnya di map
	if !exists {
		// setiap satu detik hanya ada 15 request yang diperbolahkan
		limiter := rate.NewLimiter(1, 15)

		// menyimpan ip dan menetapkan limiter
		visitors[ip] = &visitor{limiter, time.Now()}
		return limiter
	}
	// ketika ip ditemukan jalankan limiter dari ip itu
	// Update waktu terakhir dia request
	v.lastSeen = time.Now()
	return v.limiter
}

// ini bisa di gunakan nanti sebagai middleware
func Limiter(h http.Handler) http.Handler {
	return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		var host, _, err = net.SplitHostPort(r.RemoteAddr)
		if err != nil {
			log.Print(err.Error())
			http.Error(w, "Internal Server Error", http.StatusInternalServerError)
			return
		}

		// check visitor
		var limiter = getVisitor(host)
		// jika limit penuh return error to many request
		if !limiter.Allow() {
			http.Error(w, http.StatusText(http.StatusTooManyRequests), http.StatusTooManyRequests)
			return
		}

		h.ServeHTTP(w, r)
	})
}

```

Kita membuat sebuah function public bernama limiter yang melewati http handler. function ini digunakan untuk menangkap semua request yang masuk berdasarkan ip dan di validasi oleh get visitor. untuk penjelasan silahkan lihat komentar di codenya.\
\
**Coba Kita Test**\
kita membuat sebuah folder bernama server dialamnya ada file bernama server.go\
\
![](<../../.gitbook/assets/image (6) (1) (1).png>)

isikan dengan

```go
package main

import (
	"log"
	"net/http"

	limit "github.com/aryadiahmad4689/rate-limit-go/middleware"
)

func okHandler(w http.ResponseWriter, r *http.Request) {
	w.Write([]byte("OK"))
}

func main() {
	mux := http.NewServeMux()
	mux.HandleFunc("/", okHandler)
	// Wrap the servemux with the limit middleware.
	log.Print("Listening on :4000...")
	http.ListenAndServe(":4000", limit.Limiter(mux))
}
```

untuk di root main.go isikan dengan\
foldenya sekarang seperti\
![](<../../.gitbook/assets/image (19).png>)

```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
	"time"
)

func test() {
	c := http.Client{Timeout: time.Duration(1) * time.Second}
	resp, err := c.Get("http://localhost:4000")
	if err != nil {
		fmt.Printf("Error %s", err)
		return
	}
	defer resp.Body.Close()
	body, err := ioutil.ReadAll(resp.Body)
	fmt.Printf("Body : %s", body)
}
func main() {
	var i int
	for i = 0; i < 20; i++ {
		test()
		fmt.Println(i)

	}
}

```

jalankan server terlebih dahulu baru jalankan root main.go dan hasilnya\


<figure><img src="../../.gitbook/assets/image (5) (2).png" alt=""><figcaption></figcaption></figure>

lihat hasilnya ketika request ke lima belas dia akan mengembalikan error bahwa request terlalu banyak.

Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawa**h**

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)\
\
\
Itulah teman teman tentang rate-limiter di golang. semoga membantu
