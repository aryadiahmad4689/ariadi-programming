# Crud

Create

```go
func createUser(username, email, password string) (*User, error) {
	user := &User{Username: username, Email: email, Password: password}
	result := db.Create(user)
	return user, result.Error
}
```

Get Data

```go
func getUserByID(id uint) (*User, error) {
	var user User
	result := db.First(&user, id)
	return &user, result.Error
}
```

Update

```go
func updateUserEmail(id uint, newEmail string) (*User, error) {
	user, err := getUserByID(id)
	if err != nil {
		return nil, err
	}
	user.Email = newEmail
	result := db.Save(user)
	return user, result.Error
}
```

Delete

```go
func deleteUser(id uint) error {
	user, err := getUserByID(id)
	if err != nil {
		return err
	}
	result := db.Delete(user)
	return result.Error
}
```
