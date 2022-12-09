---
description: Generate Snowflake Id
---

# Snowflake

{% code title="main.go" %}
```go
package main

import (
	"fmt"
	"github.com/langwan/langgo"
	"github.com/langwan/langgo/components/snowflake"
)

func main() {
	langgo.Run(&snowflake.Instance{MachineID: 1})
	id := snowflake.Gen()
	fmt.Printf("Int64  ID: %d\n", id)
	id = snowflake.Gen()
	fmt.Printf("Int64  ID: %d\n", id)
	id = snowflake.Gen()
	fmt.Printf("Int64  ID: %d\n", id)
}
```
{% endcode %}

{% code title="output" %}
```shell
Int64  ID: 123128837511843840
Int64  ID: 123128837511843841
Int64  ID: 123128837511843842
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Components/Snowflake" %}

### Methods

* Gen
