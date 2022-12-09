---
description: Password hash
---

# Password

{% code title="app.yml" %}
```yaml
password:
  salt: langgo
```
{% endcode %}

{% code title="main.go" %}
```go
package main

import (
   "fmt"
   "github.com/langwan/langgo"
   "github.com/langwan/langgo/components/password"
)

func main() {
   langgo.Run(&password.Instance{})
   hash := password.Hash("123456")
   fmt.Println(hash)
}
```
{% endcode %}

{% code title="output" %}
```
61a61b0cb05d57199243b49f59769f7b6508a9a2
```
{% endcode %}
