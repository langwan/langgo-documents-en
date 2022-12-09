# Downloading Http File

{% code title="app.yml" %}
```
download:
  workers: 5
  part_size: 5m
  buf_size: 200k
```
{% endcode %}

{% code title="main.go" %}
```go
package main

import (
   "context"
   "fmt"
   "github.com/langwan/langgo"
   "github.com/langwan/langgo/components/download"
   helper_progress "github.com/langwan/langgo/helpers/progress"
)

type MyListener struct {
}

func (l MyListener) ProgressChanged(event *helper_progress.ProgressEvent) {
   fmt.Println(event)
}

func main() {
   addr := "https://file-examples.com/storage/fe352586866388d59a8918d/2017/04/file_example_MP4_1280_10MG.mp4"
   langgo.Run(&download.Instance{})
   reader := download.HttpReader{
      Url: addr,
   }
   download.Download(context.Background(), "./output.mp4", &reader, &MyListener{})
}
```
{% endcode %}

{% code title="file system" %}
```
App (root)
├─ main.go
├─ app.yml
└─ output.mp4
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Components/Download/Downloading-Http-File" %}
