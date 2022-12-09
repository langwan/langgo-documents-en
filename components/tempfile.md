---
description: Generate and manage temporary files
---

# TempFile

### Basic

{% code title="main.go" %}
```go
package main

import (
	"fmt"
	"github.com/langwan/langgo"
	"github.com/langwan/langgo/components/tempfile"
)

func main() {
	langgo.Run(&tempfile.Instance{Base: "tmp"})
	filename, err := tempfile.Get().CreateFile([]byte("langgo"), 0644)
	if err != nil {
		panic(err)
		return
	}
	defer tempfile.Get().RemoveFile(filename)
	data, err := tempfile.Get().ReadFile(filename, false)
	if err != nil {
		panic(err)
		return
	}
	fmt.Println(string(data))
}
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Components/TempFile/Simple" %}

### Read And Remove

{% code title="main.go" %}
```go
package main

import (
   "fmt"
   "github.com/langwan/langgo"
   "github.com/langwan/langgo/components/tempfile"
)

func main() {
   langgo.Run(&tempfile.Instance{Base: "tmp"})
   filename, err := tempfile.Get().CreateFile([]byte("langgo"), 0644)
   if err != nil {
      panic(err)
      return
   }

   data, err := tempfile.Get().ReadFile(filename, true)
   if err != nil {
      panic(err)
      return
   }
   fmt.Println(string(data))
}
```
{% endcode %}

if `ReadFile()` method parameter `remove` is true read and remove file.

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Components/TempFile/Read-And-Remove" %}

