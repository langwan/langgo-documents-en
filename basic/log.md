---
description: Log from zerolog
---

# Log

### Basic

{% code title="main.go" %}
```go
package main

import (
	"github.com/langwan/langgo"
	"github.com/langwan/langgo/components/hello"
)

func main() {
	langgo.Run(&hello.Instance{Message: "hello langgo"})
	langgo.Logger("app", "hello").Info().Str("message", hello.Get().Message).Send()
}
```
{% endcode %}

The `langgo.Logger()` method is output log info, `"app"` is the filename, `"main"` is the tag, other same as [zerolog](https://github.com/rs/zerolog).

{% code title="file system" %}
```
App (root)
└─ logs
   └─ app.log
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Basic/Log/Basic" %}

### Multi Log Files

```go
package main

import (
   "github.com/langwan/langgo"
   "github.com/langwan/langgo/components/hello"
   "github.com/langwan/langgo/components/sqlite"
)

func main() {
   langgo.Run(&hello.Instance{Message: "hello langgo"}, &sqlite.Instance{Path: "./database.db"})
   langgo.Logger("app", "hello").Info().Str("message", hello.Get().Message).Send()
   var i int64
   sqlite.Get().Raw("SELECT 1").Scan(&i)
   langgo.Logger("db", "main").Debug().Int64("i", i).Send()
}
```

{% code title="file system" %}
```
App (root)
└─ logs
   └─ app.log
   └─ db.log
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Basic/Log/Multi-Log-Files" %}

