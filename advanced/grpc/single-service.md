# Single Service

{% code title="file system" %}
```
App (root)
├─ client
│  └─ client.go
├─ server
│  ├─ service
│  │  ├─ Hello.go
│  │  └─ server.go
│  └─ server.go
└─ scripts
   ├─ server.proto
   └─ gen.sh
```
{% endcode %}

### client

{% code title="server.proto" %}
```protobuf
syntax = "proto3";

option go_package = ".;pb";

message HelloResponse {
  string msg = 1;
}

message Empty {}

service Server {
  rpc Hello(Empty) returns(HelloResponse);
}
```
{% endcode %}

{% code title="gen.sh" %}
```bash
CLIENT_OUT=../client/pb
protoc \
--go_out=${CLIENT_OUT} \
--go-grpc_out=${CLIENT_OUT} \
--go-grpc_opt=require_unimplemented_servers=false \
server.proto

SERVER_OUT=../server/pb
protoc \
--go_out=${SERVER_OUT} \
--go-grpc_out=${SERVER_OUT} \
--go-grpc_opt=require_unimplemented_servers=false \
server.proto
```
{% endcode %}

{% code title="client.go" %}
```go
package main

import (
   "context"
   "fmt"
   helper_grpc "github.com/langwan/langgo/helpers/grpc"
   "google.golang.org/grpc"
   "langwan/langgo-examples/Advanced/Grpc/Single-Service/client/pb"
   "log"
)

func main() {

   conn, err := helper_grpc.NewClient(nil, "127.0.0.1:8000", grpc.WithInsecure())

   if err != nil {
      fmt.Printf("err: %v", err)
      return
   }

   ServerClient := pb.NewServerClient(conn)

   helloResponse, err := ServerClient.Hello(context.Background(), &pb.Empty{})
   if err != nil {
      fmt.Printf("err: %v", err)
      return
   }

   fmt.Println(helloResponse)
}
```
{% endcode %}

{% code title="output" %}
```
2022/12/08 13:35:56 msg:"hello"
```
{% endcode %}

### server

{% code title="service/server.go" %}
```go
package server

type Server struct {
}
```
{% endcode %}

{% code title="service/Hello.go" %}
```go
package server

import (
   "context"
   "langwan/langgo-examples/Advanced/Grpc/Single-Service/server/pb"
)

func (s Server) Hello(ctx context.Context, request *pb.Empty) (*pb.HelloResponse, error) {
   return &pb.HelloResponse{Msg: "hello"}, nil
}
```
{% endcode %}

{% code title="server.go" %}
```go
package main

import (
   "github.com/langwan/langgo"
   helper_grpc "github.com/langwan/langgo/helpers/grpc"
   "langwan/langgo-examples/Advanced/Grpc/Single-Service/server/pb"
   "langwan/langgo-examples/Advanced/Grpc/Single-Service/server/service/server"
)

const addr = "localhost:8000"

func main() {
   langgo.Run()
   cg := helper_grpc.NewServer(nil)
   cg.Use(helper_grpc.LogUnaryServerInterceptor())
   gs, err := cg.Server()
   if err != nil {
      panic(err)
   }
   pb.RegisterServerServer(gs, server.Server{})
   err = cg.Run(addr)
   if err != nil {
      panic(err)
   }
}
```
{% endcode %}

{% code title="output" %}
```shell
1:35PM INF server ready addr=localhost:8000 tag=run
1:35PM INF req={} resp={"msg":"hello"} runtime=0.03175 tag=run
```
{% endcode %}

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Advanced/Grpc/Single-Service" %}

