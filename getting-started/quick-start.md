# Quick Start

### Installation

```shell
go get -u github.com/langwan/langgo
```

### Creating an Application

Create a Langgo application by loading any component using the `langgo.run ()` method.

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
hello langgo
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Basic/Creating-An-Application" %}
