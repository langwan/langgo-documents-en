---
description: Os Library enhancements
---

# Os

### Copying File

Allows copying file across drives

{% code title="main.go" %}
```
package main

import (
   "fmt"
   helper_os "github.com/langwan/langgo/helpers/os"
)

func main() {
   wn, err := helper_os.CopyFile("./ls.bk", "/bin/ls")
   if err != nil {
      panic(err)
   }
   fmt.Printf("copy file %d bytes\n", wn)
}
```
{% endcode %}

{% code title="output" %}
```
copy file 187040 bytes
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Os/CopyFile" %}

### Moving File

Allows moving file across drives

{% code title="main.go" %}
```go
package main

import (
	"fmt"
	helper_os "github.com/langwan/langgo/helpers/os"
)

func main() {
	wn, err := helper_os.MoveFile("./ls.bk2", "./ls.bk")

	if err != nil {
		panic(err)
	}
	fmt.Printf("move file %d bytes\n", wn)
}
```
{% endcode %}

{% code title="output" %}
```
move file 187040 bytes
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Os/MoveFile" %}

### Copying File Watcher

Observing file copies

```go
package main

import (
   "fmt"
   helper_os "github.com/langwan/langgo/helpers/os"
)

type Listener struct{}

func (l *Listener) ProgressChanged(event *helper_os.ProgressEvent) {
   fmt.Printf("event = %d, %d / %d\n", event.EventType, event.ConsumedBytes, event.TotalBytes)
}

func main() {
   _, err := helper_os.CopyFileWatcher("./ls.bk", "/bin/ls", nil, &Listener{})
   if err != nil {
      panic(err)
   }
}
```

{% code title="output" %}
```
event = 1, 0 / 187040
event = 2, 32768 / 187040
event = 2, 65536 / 187040
event = 2, 98304 / 187040
event = 2, 131072 / 187040
event = 2, 163840 / 187040
event = 2, 187040 / 187040
event = 3, 187040 / 187040
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Os/CopyFile-Watcher" %}

### Creating An Folder

{% code title="main.go" %}
```go
package main

import (
   "fmt"
   helper_os "github.com/langwan/langgo/helpers/os"
)

func main() {
   err := helper_os.CreateFolder("./newfolder", true)
   if err != nil {
      panic(err)
   }
   err = helper_os.CreateFolder("./newfolder", true)
   if err != nil {
      panic(err)
   }
   fmt.Println("create newfolder ok")

   err = helper_os.CreateFolder("./newfolder2", false)
   if err != nil {
      fmt.Println("create newfolder2 failed")
      return
   }
   err = helper_os.CreateFolder("./newfolder2", false)
   if err != nil {
      fmt.Println("create newfolder2 failed")
      return
   }
   fmt.Println("create newfolder2 ok")
}
```
{% endcode %}

{% code title="output" %}
```
create newfolder ok
create newfolder2 failed
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Os/CreateFolder" %}

### Reading File From Offset

{% code title="main.go" %}
```go
package main

import (
   "fmt"
   helper_os "github.com/langwan/langgo/helpers/os"
)

func main() {
   data, err := helper_os.ReadFileAt("/usr/share/man/man1/open.1", 50, 20)
   if err != nil {
      panic(err)
   }
   fmt.Println(data)
}
```
{% endcode %}

{% code title="output" %}
```
[108 108 32 82 105 103 104 116 115 32 82 101 115 101 114 118 101 100 46 10]
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Os/Reading-File-From-Offset" %}

### Generate Unique Filename

{% code title="main.go" %}
```go
package main

import (
   "fmt"
   helper_gen "github.com/langwan/langgo/helpers/gen"
   helper_os "github.com/langwan/langgo/helpers/os"
)

func main() {
   filename, err := helper_os.GenUniqueFilename("/bin/ls", 10, nil)
   if err != nil {
      panic(err)
   }
   fmt.Println(filename)
   for i := 0; i < 3; i++ {
      filename, err = helper_os.GenUniqueFilename("/bin/ls", 10, func(name string) string {
         return name + "_" + helper_gen.UuidShort()
      })
      if err != nil {
         panic(err)
      }
      fmt.Println(filename)
   }
}
```
{% endcode %}

{% code title="output" %}
```
/bin/ls1
/bin/ls_YooP5EELJjhjPsdjCvRUmd
/bin/ls_szWLxpoBiPhLQwuZnbQo9f
/bin/ls_y4nEcbfoged4FHyfDoncJk
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Os/Generate-Unique-Filename" %}

### Gets Goroutine Id

{% code title="main.go" %}
```go
package main

import (
   "fmt"
   helper_os "github.com/langwan/langgo/helpers/os"
   "sync"
)

func main() {
   wg := sync.WaitGroup{}
   for i := 0; i < 3; i++ {
      wg.Add(1)
      go func() {
         id := helper_os.GetGoroutineId()
         fmt.Printf("goroutine %d\n", id)
         wg.Done()
      }()
   }
   wg.Wait()
}
```
{% endcode %}

{% code title="output" %}
```
goroutine 18
goroutine 20
goroutine 19
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Os/Gets-Goroutine-Id" %}

### Gets the filename without the extension

```go
package main

import (
   "fmt"
   helper_os "github.com/langwan/langgo/helpers/os"
)

func main() {
   filename := helper_os.FileNameWithoutExt("/foo/langgo.jpg")
   fmt.Println(filename)
}
```

```
/foo/langgo
```

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Os/Gets-The-Filename-Without-The-Extension" %}

### Gets File Info

{% code title="main.go" %}
```go
package main

import (
   "fmt"
   helper_os "github.com/langwan/langgo/helpers/os"
)

func main() {
   info, err := helper_os.GetFileInfo("/bin/ls")
   if err != nil {
      panic(err)
   }
   fmt.Printf("%+v", info)
}
```
{% endcode %}

{% code title="output" overflow="wrap" %}
```
&{Name:ls Path:/bin/ls Mime:{MIME:{Type:application Subtype:x-mach-binary Value:application/x-mach-binary} Extension:macho} Head:[202 254 186 190 0 0 0 2 1 0 0 7 0 0 0 3 0 0 64 0 0 1 28 96 0 0 0 14 1 0 0 12 128 0 0 2 0 1 128 0 0 1 90 160 0 0 0 14 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0] Width:0 Height:0 Stat:0x1400009a820}
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Os/Gets-File-Info" %}

### Touching File

{% code title="main.go" %}
```go
package main

import helper_os "github.com/langwan/langgo/helpers/os"

func main() {
   helper_os.TouchFile("./langgo", true, false)
   helper_os.TouchFile("./foo/foo", true, true)
}
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Os/TouchFile" %}

### Reading Directory

```go
package main

import (
	"fmt"
	helper_os "github.com/langwan/langgo/helpers/os"
)

func main() {
	files, err := helper_os.ReadDir("../", true)
	if err != nil {
		return
	}
	for _, file := range files {
		fmt.Println(file.Name())
	}
}
```

{% code title="output" %}
```
CopyFile
CopyFile-Watcher
CreateFolder
Generate-Unique-Filename
Gets-File-Info
Gets-Goroutine-Id
Gets-The-Filename-Without-The-Extension
MoveFile
Reading-Directory
Reading-File-From-Offset
TouchFile
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Os/Reading-Directory" %}

### File And Folder Exists

{% code title="main.go" %}
```go
package main

import (
   "fmt"
   helper_os "github.com/langwan/langgo/helpers/os"
)

func main() {
   ok := helper_os.FileExists("/bin/ls")
   fmt.Println(ok)

   ok = helper_os.FileExists("/bin")
   fmt.Println(ok)

   ok = helper_os.FolderExists("/bin/ls")
   fmt.Println(ok)

   ok = helper_os.FolderExists("/bin")
   fmt.Println(ok)
}
```
{% endcode %}

{% code title="outout" %}
```
true
true
false
true
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Os/File-And-Folder-Exists" %}
