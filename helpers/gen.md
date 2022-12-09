---
description: Generate Int, String, Uuid
---

# Gen

### Random Int

{% code title="main.go" %}
```go
package main

import (
	"fmt"
	helper_gen "github.com/langwan/langgo/helpers/gen"
)

func main() {
	for i := 0; i < 10; i++ {
		ri := helper_gen.RandInt(10, 100)
		fmt.Printf("%d ", ri)
	}
}
```
{% endcode %}

{% code title="output" %}
```
20 19 85 58 20 73 51 18 41 16
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Gen/Random-Int" %}

### Random String(All Characters)

{% code title="main.go" %}
```go
package main

import (
   "fmt"
   helper_gen "github.com/langwan/langgo/helpers/gen"
)

func main() {
   rs, err := helper_gen.RandString(10)
   if err != nil {
      panic(err)
   }
   fmt.Println(rs)
}
```
{% endcode %}

{% code title="output" %}
```
2u`EU$=Py&
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Gen/Random-String-All-Characters" %}

### Random String(The Specified Characters)

{% code title="main.go" %}
```go
package main

import (
   "fmt"
   helper_gen "github.com/langwan/langgo/helpers/gen"
)

func main() {
   rs, err := helper_gen.RandString(10, helper_gen.LettersNumberNoZero, helper_gen.LettersUpperCaseLetter)
   if err != nil {
      panic(err)
   }
   fmt.Println(rs)
}
```
{% endcode %}

{% code title="output" %}
```
G8NXIH4CYE
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Gen/Rand-String-The-Specified-Characters" %}

### Generate Uuid

{% code title="main.go" %}
```go
package main

import (
   "fmt"
   helper_gen "github.com/langwan/langgo/helpers/gen"
)

func main() {
   uuid := helper_gen.Uuid()
   fmt.Println(uuid)
   uuid = helper_gen.UuidNoSeparator()
   fmt.Println(uuid)
   uuid = helper_gen.UuidShort()
   fmt.Println(uuid)
}
```
{% endcode %}

{% code title="output" %}
```
5654ddca-e6ce-473f-b15b-a24cdf19c8d9
03531299ddde4c07a401f4fec80717c5
CuasqfGZahmyDuzfYuuArd
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Gen/Generate-Uuid" %}
