---
description: Multiple goroutines download files. Support Http, OSS, S3.
---

# Download

### Configuration

```
download:
  workers: 5
  part_size: 5m
  buf_size: 200k
```

* workers: number of goroutines.
* part\_size: part size
* buf\_size: download buffer size

### Reader

* **HttpReader**\
  Http Request Reader
* **OssReader**\
  Aliyun Oss Reader
* **S3Reader**\
  Amazon s3 Reader

### Download Files

{% content-ref url="downloading-http-file.md" %}
[downloading-http-file.md](downloading-http-file.md)
{% endcontent-ref %}

{% content-ref url="downloading-oss-file.md" %}
[downloading-oss-file.md](downloading-oss-file.md)
{% endcontent-ref %}

{% content-ref url="downloading-s3-file.md" %}
[downloading-s3-file.md](downloading-s3-file.md)
{% endcontent-ref %}

### Tune Workers

```go
func main() {
    langgo.Run(&download.Instance{})
    download.Get().Tune(10)
}
```

