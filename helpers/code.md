# Code

Call Struct Function

```go
package main

import (
   "context"
   "encoding/json"
   "fmt"
   helper_code "github.com/langwan/langgo/helpers/code"
)

type MyStruct struct {
}

type FooRequest struct {
   Name string `json:"name"`
}

func (my *MyStruct) Foo(ctx context.Context, request *FooRequest) (string, error) {
   return fmt.Sprintf("my name is %s", request.Name), nil
}

func main() {
   myStruct := MyStruct{}
   request := FooRequest{Name: "langgo"}
   marshal, err := json.Marshal(&request)
   if err != nil {
      panic(err)
   }
   response, code, err := helper_code.Call(context.Background(), &myStruct, "Foo", string(marshal))
   if err != nil {
      panic(err)
   }
   fmt.Printf("code = %v\n", code)
   fmt.Printf("response = %v\n", response)
}
```

{% embed url="https://github.com/langwan/langgo-examples/tree/main/0.5.x/Helpers/Code/Call-Struct-Function" %}
