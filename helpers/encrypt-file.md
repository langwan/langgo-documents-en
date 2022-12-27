---
description: The aes256 algorithm was used to encrypt and decrypt the file
---

# Encrypt File

### ReadFile And WriteFile

When the file size is small, readfile and writefile are used directly to read and write the encrypted file.

{% code title="file system" %}
```
.
├── icon.jpg
└── main.go

```
{% endcode %}

{% code title="main.go" %}
```go
package main

import (
	helper_crypto_file "github.com/langwan/langgo/helpers/crypto/file"
	"os"
)

func main() {
	key := []byte("01234567890123456789012345678901")
	data, err := os.ReadFile("./icon.jpg")
	if err != nil {
		return
	}
	helper_crypto_file.WriteFile(key, "./dst.jpg.en", data, 0666)

	de, err := helper_crypto_file.ReadFile(key, "./dst.jpg.en")
	if err != nil {
		return
	}
	os.WriteFile("./dst.jpg", de, 0666)
}

```
{% endcode %}

{% code title="file system (output)" %}
```
.
├── dst.jpg
├── dst.jpg.en
├── icon.jpg
└── main.go
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/CryptoFile/ReadFile" %}

### Read And Write File By Buffer

When the file size is large, you can use the cache to read and write encrypted files.

{% code title="main.go" %}
```go
package main

import (
	"fmt"
	helper_crypto_file "github.com/langwan/langgo/helpers/crypto/file"
	"io"
	"os"
	"time"
)

func main() {
	encryptedFile("01234567890123456789012345678901", "./icon.jpg", "./dst.jpg", "./dst.jpg.en")
}

func encryptedFile(key string, src string, dst string, en string) {

	st := time.Now()

	defer func() {
		fmt.Println("runtime", time.Since(st))
	}()

	os.Remove(en)
	os.Remove(dst)

	cf := helper_crypto_file.File{
		Secret: []byte(key),
	}
	fd, err := os.Open(src)
	defer fd.Close()
	if err != nil {
		panic(err)
	}
	err = cf.Create(en)
	if err != nil {
		panic(err)
	}
	buf := make([]byte, helper_crypto_file.DefaultBufferSize)
	rn := 0
	wn := 0
	i := 0
	for {
		n, err := fd.ReadAt(buf, int64(rn))

		i++
		rn += n
		if n == 0 {
			break
		} else if err != nil && err != io.EOF {

			panic(err)
		}
		n, err = cf.WriteAt(buf[:n], int64(wn))

		if err != nil {
			panic(err)
		}
		wn += n
	}

	cf.Close()

	cf = helper_crypto_file.File{
		Secret: []byte("01234567890123456789012345678901"),
	}
	cf.Open(en)
	defer cf.Close()

	fd, err = os.Create(dst)
	if err != nil {
		panic(err)
	}
	defer fd.Close()
	buf = make([]byte, helper_crypto_file.DefaultBlockSize)
	rn = 0
	wn = 0

	i = 0
	for {
		de, n, err := cf.ReadAt(buf, int64(rn))

		i++
		rn += n
		if n == 0 {
			break
		} else if err != nil && err != io.EOF {

			panic(err)
		}
		n, err = fd.WriteAt(de, int64(wn))

		if err != nil {
			panic(err)
		}
		wn += n
	}
}

```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/CryptoFile/Buffer" %}
