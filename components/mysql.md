---
description: With GORM
---

# MySQL

### Single Instance

{% code title="app.yml" %}
```yaml
mysql:
  items:
    main:
      conn_max_lifetime: 1h
      dsn: root:123456@tcp(localhost:3306)/sample?charset=utf8mb4&parseTime=True&loc=Local
      max_idle_conns: 1
      max_open_conns: 10
```
{% endcode %}

Parameters

* `conn_max_lifetime`: maximum lifetime of a connection.
* `dsn`: dsn string.
* `max_idle_conns`: maximum number of idle connections.
* `max_open_conns`: maximum number of open connections.

{% code title="main.go" %}
```go
package main

import (
	"fmt"
	"github.com/langwan/langgo"
	"github.com/langwan/langgo/components/mysql"
)

func main() {
	langgo.Run(&mysql.Instance{})
	var i int64
	mysql.Main().Raw("SELECT 1").Scan(&i)
	fmt.Println(i)
}
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Components/Mysql/Single-Instance" %}

### Multi Instances

{% code title="app.yml" %}
```yaml
mysql:
  items:
    main:
      conn_max_lifetime: 1h
      dsn: root:123456@tcp(localhost:3306)/sample?charset=utf8mb4&parseTime=True&loc=Local
      max_idle_conns: 1
      max_open_conns: 10
    slave:
      conn_max_lifetime: 1h
      dsn: slave:123456@tcp(localhost:3306)/sample?charset=utf8mb4&parseTime=True&loc=Local
      max_idle_conns: 1
      max_open_conns: 10
```
{% endcode %}

{% code title="main.go" %}
```go
package main

import (
   "fmt"
   "github.com/langwan/langgo"
   "github.com/langwan/langgo/components/mysql"
)

func main() {
   langgo.Run(&mysql.Instance{})
   var i int64
   mysql.Main().Raw("SELECT 1").Scan(&i)
   fmt.Println(i)
   mysql.Get("slave").Raw("SELECT 2").Scan(&i)
   fmt.Println(i)
}
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Components/Mysql/Multi-Instances" %}
