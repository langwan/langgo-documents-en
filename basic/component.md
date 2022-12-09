---
description: A unique persistent instance of a component
---

# Component

There are several ways to load components.

### Initialized&#x20;

Components are loading when the app is initialized.

#### From Configuration

{% code title="app.yml" %}
```yaml
hello:
    message: "hello"
```
{% endcode %}

{% code title="main.go" %}
```go
package main

import (
	"github.com/langwan/langgo"
	"github.com/langwan/langgo/components/hello"
)

func main() {
	langgo.Run(&hello.Instance{})
	fmt.Println(hello.Get().Message)
}
```
{% endcode %}

{% code title="outout" %}
```shell
hello
```
{% endcode %}

Get `hello.Get().Message` from "app.yml".

{% hint style="info" %}
`hello.Get()` Get a unique persistent instance of a component.
{% endhint %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Component/Configuration" %}

#### From  Parameters

{% code title="main.go" %}
```go
package main

import (
	"github.com/langwan/langgo"
	"github.com/langwan/langgo/components/hello"
)

func main() {
	langgo.Run(&hello.Instance{Message: "hello"})
	fmt.Println(hello.Get().Message)
}
```
{% endcode %}

{% code title="output" %}
```shell
hello
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Component/Parameters" %}

#### Loading Components

{% code title="app.yml" %}
```
hello:
  message: "hello langgo"
sqlite:
  path: database.db
```
{% endcode %}

{% code title="main.go" %}
```go
package main

import (
	"fmt"
	"github.com/langwan/langgo"
	"github.com/langwan/langgo/components/hello"
	"github.com/langwan/langgo/components/sqlite"
)

func main() {
	langgo.Run(&hello.Instance{}, &sqlite.Instance{Path: "./database.db"})
	fmt.Println(hello.Get().Message)
	var i int64
	sqlite.Get().Raw("SELECT 1").Scan(&i)
	fmt.Println(i)
}
```
{% endcode %}

{% code title="output" %}
```
hello
1
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Component/Loading-Components" %}

### Runtime

Components are loading at runtime. using `langgo.LoadComponents()` method.

{% code title="main.go" %}
```go
package main

import (
	"fmt"
	"github.com/langwan/langgo"
	"github.com/langwan/langgo/components/hello"
	"github.com/langwan/langgo/components/sqlite"
)

func main() {
	langgo.Run(&sqlite.Instance{Path: "./database.db"})
	langgo.LoadComponents(&hello.Instance{Message: "hello langgo"})
	fmt.Println(hello.Get().Message)
}
```
{% endcode %}

{% code title="output" %}
```
hello
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Component/Runtime" %}
