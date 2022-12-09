---
description: Transcoding and generating thumbnails using FFmpeg.
---

# FFmpeg

### Transcoding

Transcoding to h264 mp4 file.

{% code title="app.yml" %}
```yaml
ffmpeg:
  ffmpeg: /opt/homebrew/bin/ffmpeg
  ffprobe: /opt/homebrew/bin/ffprobe
  command_timeout: 1h
```
{% endcode %}

{% code title="main.go" %}
```
package main

import (
	"github.com/langwan/langgo"
	"github.com/langwan/langgo/components/ffmpeg"
)

func main() {
	langgo.Run(&ffmpeg.Instance{})
	ffmpeg.Get().Transcoding("../../../samples/sample.mov", "./output.mp4", true)
}
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Components/FFmpeg/Transcoding" %}

### Generate thumbnails

{% code title="app.yml" %}
```yaml
ffmpeg:
  ffmpeg: /opt/homebrew/bin/ffmpeg
  ffprobe: /opt/homebrew/bin/ffprobe
  command_timeout: 1h
```
{% endcode %}

{% code title="main.go" %}
```go
package main

import (
   "github.com/langwan/langgo"
   "github.com/langwan/langgo/components/ffmpeg"
   "time"
)

func main() {
   langgo.Run(&ffmpeg.Instance{})
   ffmpeg.Get().Thumbnail("../../../samples/sample.mov", "./output.jpg", time.Second, true)
}
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Components/FFmpeg/Generate-Thumbnails" %}

### Gets Video Duration

{% code title="main.go" %}
```
package main

import (
   "fmt"
   "github.com/langwan/langgo"
   "github.com/langwan/langgo/components/ffmpeg"
)

func main() {
   langgo.Run(&ffmpeg.Instance{})
   duration, err := ffmpeg.Get().Duration("../../../samples/sample.mov")
   if err != nil {
      return
   }
   fmt.Println(duration)
}
```
{% endcode %}

{% code title="output" %}
```
12.96s
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Components/FFmpeg/Gets-Video-Duration" %}
