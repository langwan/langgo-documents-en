# Custom Components

{% code title="file system" %}
```
App (root)
├─ main.go
├─ app.yml
└─ components
   └─ my
      └─ my.go
```
{% endcode %}

{% code title="my.go" %}
```go
package my

type Instance struct {
   Message string `yaml:"message"`
}

const name = "my"

var instance *Instance

func (i *Instance) Run() error {
   instance = i
   return nil
}

func (i *Instance) GetName() string {
   return name
}

func Get() *Instance {
   return instance
}
```
{% endcode %}

{% code title="app.yml" %}
```yaml
my:
  message: my name is langgo
```
{% endcode %}

{% code title="main.go" %}
```go
package main

import (
   "fmt"
   "github.com/langwan/langgo"
   "langwan/langgo-examples/Advanced/Custom-Components/components/my"
)

func main() {
   langgo.Run(&my.Instance{})
   fmt.Println(my.Get().Message)
}
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Advanced/Custom-Components" %}
