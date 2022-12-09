---
description: service discovery for GRPC
---

# ETCD And GRPC



{% code title="shell" %}
```shell
docker pull bitnami/etcd
```
{% endcode %}

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

### GRPC Proto File

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

### client

{% code title="client.go" %}
```go
package main

import (
   "context"
   "fmt"
   helper_grpc "github.com/langwan/langgo/helpers/grpc"
   "langwan/langgo-examples/Advanced/Grpc/ETCD-And-GRPC/client/pb"

   clientv3 "go.etcd.io/etcd/client/v3"
   "go.etcd.io/etcd/client/v3/naming/resolver"
   "google.golang.org/grpc"
   "google.golang.org/grpc/balancer/roundrobin"
   "google.golang.org/grpc/credentials/insecure"
   "log"
   "time"
)

const etcdHost = "http://localhost:2379"
const serviceName = "langgo/server"

func main() {

   etcdClient, err := clientv3.NewFromURL(etcdHost)
   if err != nil {
      panic(err)
   }
   etcdResolver, err := resolver.NewBuilder(etcdClient)

   conn, err := helper_grpc.NewClient(nil, fmt.Sprintf("etcd:///%s", serviceName), grpc.WithResolvers(etcdResolver), grpc.WithTransportCredentials(insecure.NewCredentials()), grpc.WithDefaultServiceConfig(fmt.Sprintf(`{"LoadBalancingPolicy": "%s"}`, roundrobin.Name)))
   if err != nil {
      panic(err)

   }

   ServerClient := pb.NewServerClient(conn)

   for {
      helloRespone, err := ServerClient.Hello(context.Background(), &pb.Empty{})
      if err != nil {
         fmt.Printf("err: %v", err)
         return
      }

      log.Println(helloRespone, err)
      time.Sleep(500 * time.Millisecond)
   }

}
```
{% endcode %}

### server

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

{% code title="service/server.go" %}
```go
package server

type Server struct {
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

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Advanced/Grpc/ETCD-And-GRPC" %}
