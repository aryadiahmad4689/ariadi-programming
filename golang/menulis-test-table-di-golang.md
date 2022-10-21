# Menulis Test Table Di Golang

Halo semua**.** kali ini saya akan membagikan cara menulist test table di golang. test table sendiri adalah jenis test yang dilakukan menggunakan perulangan untuk mempermudah kita dalam menulis case yang terus berulang agar code kita tidak redundant.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawa**h** <a href="#9a3c" id="9a3c"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Lansung Saja Prakteknya

disini saya membuat sebuah file bernama `main_test.go`

`Didalamnya saya menulis sebuah struct dan method sederhana`

```go
package mocktestgo

import (
	"errors"
	"fmt"
	"testing"
)

type Person struct {
	Nama string
	Umur int
}

type User struct {
}

func (u *User) GetPerson(param Person) (Person, error) {
	// jika nama kosong kembalikan error
	if param.Nama == "" {
		return param, errors.New("harap isi nama")
	}
	// jika umur kosong kembalikan error
	if param.Umur < 1 {
		return param, errors.New("harap isi umur")
	}
	return Person{Nama: param.Nama, Umur: param.Umur}, nil
}

```

diatas saya membuat sebuah method getPerson sederhana yang fungsinya hanya untuk mengembalikan nilai dari person itu sendiri. saya memberikan sebuah percabangan sederhana untuk mengecek nama atau umur tidak diisi.

#### **Test Tanpa Test Table**

```go
func TestGetPerson(t *testing.T) {
	t.Run("nama cannot null", func(t *testing.T) {
		var user = &User{}
		var person = Person{Umur: 10}
		var errName = errors.New("harap isi nama anda")
		var result, err = user.GetPerson(Person{Nama: "", Umur: 10})

		if err.Error() != errName.Error() {
			t.Errorf("error get person %v != %v", err, errName)
		}
		if person != result {
			t.Errorf("error get person %v != %v", person, result)
		}
	})
}
```

ini adalah contoh menulis test yang biasanya kita lakukan. misalkan kita ingin menambah test untuk `check umur cannot null` maka kita akan menuliskan testnya lagi  seperti ini

```go
t.Run("umur cannot null", func(t *testing.T) {
		var user = &User{}
		var person = Person{Nama: "ariadi"}
		var errUmur = errors.New("harap isi umur")
		var result, err = user.GetPerson(person)

		if err.Error() != errUmur.Error() {
			t.Errorf("error get person %v != %v", err, errUmur)
		}
		if person != result {
			t.Errorf("error get person %v != %v", person, result)
		}
	})
```

lihat kita mengulangi proses yang sama hanya untuk case yang berbeda tentu ini memakan waktu dalam menulisnya kan. coba kita lihat dengan menggunakan test table

#### Test Dengan Test Table

```go
	type args struct {
		param Person
	}
	tests := []struct {
		name    string
		u       *User
		args    args
		want    Person
		wantErr bool
	}{
		{
			name: "nama cannot be null", // nama testnya
			u:    &User{},
			args: args{param: Person{
				Nama: "",
				Umur: 10,
			}},
			want:    Person{Umur: 10},
			wantErr: true, // kita ingin errornya sama denga true kan karena dia error
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			got, err := tt.u.GetPerson(tt.args.param)
			if (err != nil) != tt.wantErr {
				t.Errorf("User.GetPerson() error = %v, wantErr %v", err, tt.wantErr)
				return
			}
			if !reflect.DeepEqual(got, tt.want) {
				t.Errorf("User.GetPerson() = %v, want %v", got, tt.want)
			}
		})
	}
```

mungkin terlihat lebih panjang ya. tapi misalkan kita ingin menambah case baru kita hanya perlu menambahkan casenya di dalam array test seperti

```go
type args struct {
		param Person
	}
	tests := []struct {
		name    string
		u       *User
		args    args
		want    Person
		wantErr bool
	}{
		{
			name: "nama cannot be null", // nama testnya
			u:    &User{},
			args: args{param: Person{
				Nama: "",
				Umur: 10,
			}},
			want:    Person{Umur: 10},
			wantErr: true, // kita ingin errornya sama denga true kan karena dia error
		},
		{
			name: "umur cannot be null", // nama testnya
			u:    &User{},
			args: args{param: Person{
				Nama: "",
				Umur: 10,
			}},
			want:    Person{Umur: 10},
			wantErr: true, // kita ingin errornya sama denga true kan karena dia error
		},
		{
			name: "get person success", // nama testnya
			u:    &User{},
			args: args{param: Person{
				Nama: "ariadi",
				Umur: 10,
			}},
			want:    Person{Nama: "ariadi", Umur: 10},
			wantErr: false, // kita ingin errornya sama dengan false karena ga error
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			got, err := tt.u.GetPerson(tt.args.param)
			if (err != nil) != tt.wantErr {
				t.Errorf("User.GetPerson() error = %v, wantErr %v", err, tt.wantErr)
				return
			}
			if !reflect.DeepEqual(got, tt.want) {
				t.Errorf("User.GetPerson() = %v, want %v", got, tt.want)
			}
		})
	}
```

lihatkan code dibawahnya tidak berubah hanya casenya yang ditambah.



Cara diatas bukan berarti cara test yang paling benar yaa. ini adalah jenis test yang bisa kita  lakukan di golang dan di beberapa bahasa lain juga. kalian tergantung bisa melakukan cara test yang kalian suka yang penting testnya tidak menyusahkan kalian dan berjalan dengan baik. kalau untuk saya sendiri saya lebih suka jenis test table wlaupun di kantor di pakai kedua duanya.

## Yang Ingin Membantu Saya Untuk Terus Berkontribusi Boleh Banget Klik Dibawa**h** <a href="#9a3c" id="9a3c"></a>

[![Trakteer Saya](https://cdn.trakteer.id/images/embed/trbtn-red-5.png)](https://trakteer.id/ariadi-ahmad-28xqo/tip)

Code Lenkap If You Want

```go
package mocktestgo

import (
	"errors"
	"reflect"
	"testing"
)

type Person struct {
	Nama string
	Umur int
}

type User struct {
}

func (u *User) GetPerson(param Person) (Person, error) {
	if param.Nama == "" {
		return param, errors.New("harap isi nama anda")
	}
	if param.Umur < 1 {
		return param, errors.New("harap isi umur")
	}
	return Person{Nama: param.Nama, Umur: param.Umur}, nil
}

func TestGetPerson(t *testing.T) {
	t.Run("nama cannot null", func(t *testing.T) {
		var user = &User{}
		var person = Person{Umur: 10}
		var errName = errors.New("harap isi nama anda")
		var result, err = user.GetPerson(Person{Nama: "", Umur: 10})

		if err.Error() != errName.Error() {
			t.Errorf("error get person %v != %v", err, errName)
		}
		if person != result {
			t.Errorf("error get person %v != %v", person, result)
		}
	})

	t.Run("umur cannot null", func(t *testing.T) {
		var user = &User{}
		var person = Person{Nama: "ariadi"}
		var errUmur = errors.New("harap isi umur")
		var result, err = user.GetPerson(person)

		if err.Error() != errUmur.Error() {
			t.Errorf("error get person %v != %v", err, errUmur)
		}
		if person != result {
			t.Errorf("error get person %v != %v", person, result)
		}
	})
}

func TestUser_GetPerson(t *testing.T) {
	type args struct {
		param Person
	}
	tests := []struct {
		name    string
		u       *User
		args    args
		want    Person
		wantErr bool
	}{
		{
			name: "nama cannot be null", // nama testnya
			u:    &User{},
			args: args{param: Person{
				Nama: "",
				Umur: 10,
			}},
			want:    Person{Umur: 10},
			wantErr: true, // kita ingin errornya sama denga true kan karena dia error
		},
		{
			name: "umur cannot be null", // nama testnya
			u:    &User{},
			args: args{param: Person{
				Nama: "",
				Umur: 10,
			}},
			want:    Person{Umur: 10},
			wantErr: true, // kita ingin errornya sama denga true kan karena dia error
		},
		{
			name: "get person success", // nama testnya
			u:    &User{},
			args: args{param: Person{
				Nama: "ariadi",
				Umur: 10,
			}},
			want:    Person{Nama: "ariadi", Umur: 10},
			wantErr: false, // kita ingin errornya sama dengan false karena ga error
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			got, err := tt.u.GetPerson(tt.args.param)
			if (err != nil) != tt.wantErr {
				t.Errorf("User.GetPerson() error = %v, wantErr %v", err, tt.wantErr)
				return
			}
			if !reflect.DeepEqual(got, tt.want) {
				t.Errorf("User.GetPerson() = %v, want %v", got, tt.want)
			}
		})
	}
}
```

Terimah Kasih Salam Programmer Makassar
