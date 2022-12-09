# Current Working Directory

### Set And Get

{% code title="main.go" %}
```go
package main

import (
	"fmt"
	"github.com/langwan/langgo"
)

func main() {
	langgo.SetWorkDir("./bin")
	workDir := langgo.GetWorkDir()
	fmt.Println(workDir)
}
```
{% endcode %}

{% code title="output" %}
```
./bin
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Basic/Current-Working-Directory" %}
