---
description: With GORM
---

# Sqlite

{% code title="main.go" %}
```go
package main

import (
	"fmt"
	"github.com/langwan/langgo"
	"github.com/langwan/langgo/components/sqlite"
)

func main() {
	langgo.Run(&sqlite.Instance{Path: "./database.db"})
	var i int64
	sqlite.Get().Raw("SELECT 1").Scan(&i)
	fmt.Println(i)
}
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Components/Sqlite" %}
