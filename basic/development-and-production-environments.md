# Development And Production Environments

### From App Startup

{% code title="run.sh" %}
```shell
#!/usr/bin/env bash

## development
langgo_env=development go run .
## production
langgo_env=production go run .
```
{% endcode %}

{% code title="main.go" %}
```go
package main

import (
	"fmt"
	"github.com/langwan/langgo"
	"github.com/langwan/langgo/core"
)

func main() {
	langgo.Run()
	fmt.Printf("mode = %s\n", core.EnvName)
}
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Basic/Development-And-Production-Environments/From-App-Startup" %}

### From Code

{% code title="main.go" %}
```go
package main

import (
	"fmt"
	"github.com/langwan/langgo"
	"github.com/langwan/langgo/core"
)

func main() {
	langgo.SetEnvName(core.Development)
	langgo.Run()
	fmt.Printf("mode = %s\n", langgo.GetEnvName())
}
```
{% endcode %}

{% code title="output" %}
```shell
mode = development
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Basic/Development-And-Production-Environments/From-Code" %}

