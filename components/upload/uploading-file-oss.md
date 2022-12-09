# Uploading File OSS

{% code title="app.yml" %}
```yaml
upload:
  workers: 5
  part_size: 5m
```
{% endcode %}

{% code title="main.go" %}
```go
package main

import (
	"context"
	"fmt"
	"github.com/langwan/langgo"
	"github.com/langwan/langgo/components/upload"
	helper_oss "github.com/langwan/langgo/helpers/oss"
	helper_progress "github.com/langwan/langgo/helpers/progress"
)

type MyPartList struct {
	uploadId string
	parts    []*upload.Part
}

func (m *MyPartList) RomoveParts() error {
	return nil
}

func (m *MyPartList) Load() ([]*upload.Part, error) {
	return nil, nil
}

func (m *MyPartList) SetList(parts []*upload.Part) {
	m.parts = parts
}

func (m *MyPartList) GetList() []*upload.Part {
	return m.parts
}

func (m *MyPartList) SavePart(part *upload.Part) error {
	return nil
}

func (m *MyPartList) GetUploadId() string {
	return m.uploadId
}

func (m *MyPartList) SetUploadId(uploadId string) error {
	m.uploadId = uploadId
	return nil
}

type Listener struct {
}

func (l Listener) ProgressChanged(event *helper_progress.ProgressEvent) {
	fmt.Println(event)
}

func main() {
	langgo.Run(&upload.Instance{})
	ossClient, err := helper_oss.NewClient("xxxxxx", "xxxxxx", "xxxxxx", "xxxxxx")
	if err != nil {
		panic(err)
	}
	writer := upload.OssWriter{
		Client: ossClient,
	}

	partList := MyPartList{}

	upload.UploadFile(context.Background(), "../../../samples/sample.mov", "upload_oss_test.mov", &partList, &writer, &Listener{})
}

```
{% endcode %}

{% code title="output" %}
```
&{2018345 22989865 2018345 2}
&{7261225 22989865 7261225 2}
&{12504105 22989865 12504105 2}
&{17746985 22989865 17746985 2}
&{22989865 22989865 22989865 2}
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Components/Upload/Uploading-File-OSS" %}
