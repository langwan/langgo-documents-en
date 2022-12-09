# Signal Processing

{% code title="main.go" %}
```go
package main

import (
   "fmt"
   "github.com/langwan/langgo"
   "os"
   "syscall"
)

func main() {
   langgo.Run()
   done := make(chan struct{})
   langgo.SignalHandlers(func(sig os.Signal) {
      fmt.Printf("receive sig is %s\n", sig.String())
   }, syscall.SIGHUP, syscall.SIGUSR1)
   langgo.SignalNotify()
   fmt.Printf("pid = %d\n", os.Getpid())
   <-done
}
```
{% endcode %}

```
pid = 78602
receive sig is user defined signal 1
receive sig is hangup
```

{% code title="send.sh" %}
```bash
#!/usr/bin/env bash
kill -USR1 78602
sleep 1
kill -HUP 78602
```
{% endcode %}

{% hint style="info" %}
78602 is `os.Getpid() output`value
{% endhint %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Advanced/Signal-Processing" %}
