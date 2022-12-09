# Lru

### Basic

{% code title="main.go" %}
```go
package main

import (
	"fmt"
	helper_lru "github.com/langwan/langgo/helpers/lru"
)

func main() {
	lru := helper_lru.New[string, int](2)
	lru.Set("x", 1)
	lru.Set("y", 2)
	if val, ok := lru.Get("x"); ok {
		fmt.Println("x", val)
	}
	lru.Set("z", 3)
	if val, ok := lru.Get("y"); ok {
		fmt.Println("y", val)
	}
}
```
{% endcode %}

{% code title="output" %}
```shell
x 1
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Lru/Basic" %}

### Peek

{% code title="main.go" %}
```go
package main

import (
   "fmt"
   helper_lru "github.com/langwan/langgo/helpers/lru"
)

func main() {
   lru := helper_lru.New[string, int](2)
   lru.Set("x", 1)
   lru.Set("y", 2)
   if val, ok := lru.Peek("x"); ok {
      fmt.Println("x", val)
   }
   lru.Set("z", 3)
   if val, ok := lru.Peek("x"); ok {
      fmt.Println("x", val)
   }
}
```
{% endcode %}

{% code title="output" %}
```shell
x 1
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Lru/Peek" %}

### Range

{% code title="main.go" %}
```go
package main

import (
   "fmt"
   helper_lru "github.com/langwan/langgo/helpers/lru"
)

func main() {
   lru := helper_lru.New[string, int](2)
   lru.Set("x", 1)
   lru.Set("y", 2)
   lru.Range(func(k, v any) bool {
      fmt.Println(k, v)
      return true
   })
}
```
{% endcode %}

{% code title="output" %}
```shell
x 1
y 2
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Lru/Range" %}

### Mulit Instance

{% code title="main.go" %}
```go
package main

import (
   "fmt"
   helper_lru "github.com/langwan/langgo/helpers/lru"
)

func main() {
   lruAccount := helper_lru.New[string, int](2)
   lruAccount.Set("x", 1)
   lruAccount.Set("y", 2)
   lruAccount.Range(func(k, v any) bool {
      fmt.Println(k, v)
      return true
   })
   lruOrder := helper_lru.New[int, int](2)
   lruOrder.Set(1, 1)
   lruOrder.Set(2, 2)
   lruOrder.Range(func(k, v any) bool {
      fmt.Println(k, v)
      return true
   })
}
```
{% endcode %}

{% code title="output" %}
```shell
y 2
x 1
1 1
2 2
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Lru/Multi" %}

