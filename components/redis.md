---
description: Redis Component
---

# Redis

### Single Instance

{% code title="app.yml" %}
```yaml
redis:
  items:
    main:
      dsn: redis://default:redispw@localhost:55000/0
```
{% endcode %}

{% code title="main.go" %}
```go
package main

import (
   "fmt"
   "github.com/langwan/langgo"
   "github.com/langwan/langgo/components/redis"
   "time"
)

func main() {
   langgo.Run(&redis.Instance{})
   redis.Main().Set("key", "langgo", 10*time.Second)
   val := redis.Main().Get("key")
   fmt.Println(val)
}
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Components/Redis/Single-Instance" %}

### Multi Instances

{% code title="app.yml" %}
```yaml
redis:
  items:
    main:
      dsn: redis://default:redispw@localhost:55000/0
    slave:
      dsn: redis://default:redispw@localhost:55000/0
```
{% endcode %}

{% code title="main.go" %}
```go
package main

import (
   "fmt"
   "github.com/langwan/langgo"
   "github.com/langwan/langgo/components/redis"
   "time"
)

func main() {
   langgo.Run(&redis.Instance{})
   redis.Main().Set("key", "langgo", 10*time.Second)
   val := redis.Main().Get("key")
   fmt.Println(val)

   redis.Get("slave").Set("key", "slave", 10*time.Second)
   val = redis.Get("slave").Get("key")
   fmt.Println(val)
}
```
{% endcode %}

{% code title="output" %}
```
get key: langgo
get key: slave
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Components/Redis/Multi-Instances" %}
