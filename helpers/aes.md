---
description: Aes Encryption
---

# Aes

```go
package main

import (
   "fmt"
   helper_aes "github.com/langwan/langgo/helpers/crypto/aes"
)

func main() {
   s := "0123456789"
   key := "01234567890123456789012345678901"
   encrypt, err := helper_aes.Encrypt([]byte(key), []byte(s))

   if err != nil {
      panic(err)
   }
   decrypt, err := helper_aes.Decrypt([]byte(key), encrypt)
   if err != nil {
      panic(err)
   }
   fmt.Println(s == string(decrypt))
}
```

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Aes" %}

### Methods

* Encrypt
* Decrypt
