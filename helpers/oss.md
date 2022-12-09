# OSS

{% code title="main.go" %}
```go
package main

import (
   helper_oss "github.com/langwan/langgo/helpers/oss"
   "os"
)

func main() {
   client, err := helper_oss.NewClient("xxxxxx", "xxxxxx", "xxxxxx", "xxxxxx")
   if err != nil {
      panic(err)
   }
   data, err := client.GetObject("Homework - 1028.mp4")
   if err != nil {
      return
   }
   os.WriteFile("./output.mp4", data, 0666)
}
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Components/Upload/Uploading-File-OSS" %}
