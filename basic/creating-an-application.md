# Creating An Application

### Application File System

{% code title="file system" %}
```
App (root)
├─ main.go
└─ app.yml
```
{% endcode %}

### Configuration

{% code title="app.yml" %}
```yaml
hello:
    message: "hello langgo"
```
{% endcode %}

### Creating an Application

Create a Langgo application by loading any component using the `langgo.run ()` method.

{% code title="main.go" %}
```go
package main

import (
	"fmt"
	"github.com/langwan/langgo"
	"github.com/langwan/langgo/components/hello"
)

func main() {
	langgo.Run(&hello.Instance{})
	fmt.Println(hello.Get().Message)
}

```
{% endcode %}

{% code title="output" %}
```shell
hello langgo
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Basic/Creating-An-Application" %}
