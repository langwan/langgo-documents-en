---
description: Json Web Token
---

# Jwt

{% code title="main.go" %}
```go
package main

import (
	"fmt"
	"github.com/langwan/langgo"
	"github.com/langwan/langgo/components/jwt"
)

func main() {
	langgo.Run(&jwt.Instance{Secret: "123456"})
	payload := struct {
		Name string
	}{Name: "langwan"}
	sign, err := jwt.Sign(payload)
	if err != nil {
		panic(err)
	}
	err = jwt.Verify(sign)
	if err != nil {
		panic(err)
	} else {
		fmt.Println("verify ok")
	}
}
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Components/Jwt" %}

### Methods

* Sign
* Verify
