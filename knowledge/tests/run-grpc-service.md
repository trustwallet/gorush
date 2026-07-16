---
category: tests
confidence: high
documentType: reference
scope: org
contentHash: 4e1b2eca5a92
tags: [test]
source: README.md
verified: 2026-07-16
---

## Run gRPC service

Gorush support [gRPC](https://grpc.io/) service. You can enable the gRPC in `config.yml`, default as disabled. Enable the gRPC server:

```sh
GORUSH_GRPC_ENABLED=true GORUSH_GRPC_PORT=3000 gorush
```

The following example code to send single notification in Go.

[embedmd]:# (rpc/example/go/send/main.go go)
```go
package main

import (
	"context"
	"log"

	"github.com/appleboy/gorush/rpc/proto"

	structpb "github.com/golang/protobuf/ptypes/struct"
	"google.golang.org/grpc"
)

const (
	address = "localhost:9000"
)

func main() {
	// Set up a connection to the server.
	conn, err := grpc.Dial(address, grpc.WithInsecure())
	if err != nil {
		log.Fatalf("did not connect: %v", err)
	}
	defer conn.Close()
	c := proto.NewGorushClient(conn)

	r, err := c.Send(context.Background(), &proto.NotificationRequest{
		Platform: 2,
		Tokens:   []string{"1234567890"},
		Message:  "test message",
		Badge:    1,
		Category: "test",
		Sound:    "test",
		Priority: proto.Priority_High,
		Alert: &proto.Alert{
			Title:    "Test Title",
			Body:     "Test Alert Body",
			Subtitle: "Test Alert Sub Title",
			LocKey:   "Test loc key",
			LocArgs:  []string{"test", "test"},
		},
		Data: &structpb.Struct{
			Fields: map[string]*structpb.Value{
				"key1": {
					Kind: &structpb.Value_StringValue{StringValue: "welcome"},
				},
				"key2": {
					Kind: &structpb.Value_NumberValue{NumberValue: 2},
				},
			},
		},
	})
	if err != nil {
		log.Println("could not greet: ", err)
	}

	if r != nil {
		log.Printf("Success: %t\n", r.Success)
		log.Printf("Count: %d\n", r.Counts)
	}
}
```

See the Node.js example and see more detail frome [README](rpc/example/node/README.md):

[embedmd]:# (rpc/example/node/client.js js)
```js
var messages = require('./gorush_pb');
var services = require('./gorush_grpc_pb');

var grpc = require('grpc');

function main() {
  var client = new services.GorushClient('localhost:9000',
    grpc.credentials.createInsecure());
  var request = new messages.NotificationRequest();
  var alert = new messages.Alert();
  request.setPlatform(2);
  request.setTokensList(["1234567890"]);
  request.setMessage("Hello!!");
  request.setTitle("hello2");
  request.setBadge(2);
  request.setCategory("mycategory");
  request.setSound("sound")
  alert.setTitle("title");
  request.setAlert(alert);
  request.setThreadid("threadID");
  request.setContentavailable(false);
  request.setMutablecontent(false);
  client.send(request, function (err, response) {
    if(err) {
      console.log(err);
    } else {
      console.log("Success:", response.getSuccess());
      console.log("Counts:", response.getCounts());
    }
  });
}

main();
```

GRPC Health Checking example: See [document](https://github.com/grpc/grpc/blob/master/doc/health-checking.md).

[embedmd]:# (rpc/example/go/send/main.go go)
```go
package main

import (
	"context"
	"log"

	"github.com/appleboy/gorush/rpc/proto"

	structpb "github.com/golang/protobuf/ptypes/struct"
	"google.golang.org/grpc"
)

const (
	address = "localhost:9000"
)

func main() {
	// Set up a connection to the server.
	conn, err := grpc.Dial(address, grpc.WithInsecure())
	if err != nil {
		log.Fatalf("did not connect: %v", err)
	}
	defer conn.Close()
	c := proto.NewGorushClient(conn)

	r, err := c.Send(context.Background(), &proto.NotificationRequest{
		Platform: 2,
		Tokens:   []string{"1234567890"},
		Message:  "test message",
		Badge:    1,
		Category: "test",
		Sound:    "test",
		Priority: proto.Priority_High,
		Alert: &proto.Alert{
			Title:    "Test Title",
			Body:     "Test Alert Body",
			Subtitle: "Test Alert Sub Title",
			LocKey:   "Test loc key",
			LocArgs:  []string{"test", "test"},
		},
		Data: &structpb.Struct{
			Fields: map[string]*structpb.Value{
				"key1": {
					Kind: &structpb.Value_StringValue{StringValue: "welcome"},
				},
				"key2": {
					Kind: &structpb.Value_NumberValue{NumberValue: 2},
				},
			},
		},
	})
	if err != nil {
		log.Println("could not greet: ", err)
	}

	if r != nil {
		log.Printf("Success: %t\n", r.Success)
		log.Printf("Count: %d\n", r.Counts)
	}
}
```

## See Also
- [features](../observability/alerting/features.md) <!-- rel:strong -->
- [run gorush web server](../ci/workflows/run-gorush-web-server.md) <!-- rel:strong -->
- [ios example](../security/ios-example.md) <!-- rel:strong -->
- [install from source](../code-conventions/git/install-from-source.md) <!-- rel:related -->
- [request body](../architecture/request-body.md) <!-- rel:related -->
