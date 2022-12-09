# Cutting Log

{% code title="main.go" %}
```go
package main

import (
   "fmt"
   "github.com/langwan/langgo"
   "github.com/langwan/langgo/core/log"
   "os"
   "syscall"
   "time"
)

func main() {
   langgo.Run()
   log.SetCuttingSignal(syscall.SIGUSR1)
   fmt.Printf("pid = %d\n", os.Getpid())
   langgo.SignalNotify()
   for {
      log.Logger("app", "main").Info().Timestamp().Send()
      time.Sleep(time.Second)
   }
}
```
{% endcode %}

{% code title="output" %}
```
pid = 27354
12:05PM INF tag=main
12:05PM INF tag=main
12:05PM INF tag=main
... ...
```
{% endcode %}

{% code title="cut.sh" %}
```bash
#!/usr/bin/env bash
mv logs/app.log logs/app.log.bk
kill -USR1 27354
```
{% endcode %}

{% code title="file system" %}
```
App (root)
├─ main.go
├─ cut.sh
└─ logs
   └─ app.log
   └─ app.log.bk
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Advanced/Cutting-Log" %}
