# SingleFlight Di Golang

Halo teman2 semua. kali ini saya akan membahas mengenai singleflight. karena saya beberapa hari ini research dan banyak baca artikel akhirnya ketemu feature di golang dengan nama single flight. singleflight sendiri adalah sebuah metode sharing information yang di akses secara terus menerus dan merupakan data yang sama. jadi intinya alih alih kita melakukan request yang banyak ke sebuah function maka kita bisa memotong itu dengan sharing data/informationya saja. jadi satu kali akses saja dan ini akan membuat proses data kita semakin cepat.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah <a href="#45af" id="45af"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Contoh kode saya ambil dari [https://gist.githubusercontent.com/bagusandrian/7c5982a652545f50dd29818480fce85c/raw/351fe39fd8f4e4a58409dcfae60b70c4746f0dc3/main.go](https://gist.githubusercontent.com/bagusandrian/7c5982a652545f50dd29818480fce85c/raw/351fe39fd8f4e4a58409dcfae60b70c4746f0dc3/main.go)

saya modifikasi sedikit karena github ngeblock ip saya karena terlalu banyak request ke apinya.

```go
package main

import (
	"fmt"
	"log"
	"net/http"
	"time"

	"golang.org/x/sync/singleflight"
)

func main() {
	var requestGroup singleflight.Group // localhost:8080/normal
	http.HandleFunc("/normal", func(w http.ResponseWriter, r *http.Request) {
		start := time.Now() // call function githubStatus()
		status, err := googleStatus()
		if err != nil {
			http.Error(w, err.Error(), http.StatusInternalServerError)
			return
		}
		// print processing time and status
		log.Printf("/google handler requst: processing time: %+v | status %q", time.Since(start), status)
		fmt.Fprintf(w, "Google Status: %q", status)
	})
	http.HandleFunc("/singleflight", func(w http.ResponseWriter, r *http.Request) {
		start := time.Now()
		v, err, shared := requestGroup.Do("github", func() (interface{}, error) { // call function goofleStatus()
			return googleStatus()
		}) // Check the error, as before.
		if err != nil {
			http.Error(w, err.Error(), http.StatusInternalServerError)
			return
		}
		status := v.(string) // print processing time and status
		log.Printf("/github handler requst: processing time: %+v | status %q | shared: %t", time.Since(start), status, shared)
		fmt.Fprintf(w, "GitHub Status: %q", status)
	})
	log.Println("running server on port :8080")
	http.ListenAndServe("127.0.0.1:8080", nil)
}
func googleStatus() (string, error) {
	time.Sleep(1 * time.Second)
	log.Println("call googleStatus")
	resp, err := http.Get("https://google.com")
	if err != nil {
		return "", err
	}
	defer resp.Body.Close()
	if resp.StatusCode != http.StatusOK {
		return "", fmt.Errorf("goggle response: %s", resp.Status)
	}
	return resp.Status, err
}

```

Di atas ada dua function yang pertama

Pemanggilan request tanpa singleflight dan hasilnya seperti ini

![](<../.gitbook/assets/image (63).png>)

lihat hasilnya setiap kali request kita memanggil terus function google status dan process timenya di atas 1 second.

Kita lihat ketika menggunakan singleflight

![](<../.gitbook/assets/image (25).png>)

lihat perbedaanya dia hanya sekali manggil google status dan melakukan sharing data dan lihat response timenya 50 persenya ada yang di bawah 1 second

## **Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawah** <a href="#39ec" id="39ec"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

### **Note** <a href="#00ac" id="00ac"></a>

* implementasi perlu diperhatikan dengan baik
* sebaiknya tidak digunakan untuk proses insert, update, delete karena rawan terjadi racecondition
* sebaiknya di pakai untuk proses load yang massive dalam waktu bersamaan
* sebaiknya gunakan untuk data yang tidak terlalu realtime tapi pengaksesanya sangat sering
* sebaiknya di gunakan untuk data yang perubahanya tidak terlalu sering

itulah gu**ys** sedikit tentang singleflight di golang semoga bermanfaat.

\
