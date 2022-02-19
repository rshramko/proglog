# proglog

This repository contains an example project from the book "Distributed Services with Go".

## What is possible to do right now

You can start server which exposes API on port 8080 to access a prototype of Log

### How to start server

Go to _cmd/server_ folder and do:

```
$ go run .
```

### How to play with the API

Open another terminal and first post some data (_httpie_ is used in the example):

```
$ http POST http://localhost:8080 record:='{"value": "TGV0J3MgR28gIzEK"}'
HTTP/1.1 200 OK
Content-Length: 13
Content-Type: text/plain; charset=utf-8
Date: Wed, 16 Feb 2022 20:22:24 GMT

{
    "offset": 0
}
```

Repeat the same POST request with the values _TGV0J3MgR28gIzEK_ and _TGV0J3MgR28gIzMK_.

Now query the data back:

```
$ http GET http://localhost:8080 offset:=0
HTTP/1.1 200 OK
Content-Length: 51
Content-Type: text/plain; charset=utf-8
Date: Wed, 16 Feb 2022 20:23:46 GMT

{
    "record": {
        "offset": 0,
        "value": "TGV0J3MgR28gIzEK"
    }
}
```

## How to compile proto files

First, you need to install protobuf runtime to be used. Please follow the official guide [Compiling your protocol buffers](https://developers.google.com/protocol-buffers/docs/gotutorial#compiling-your-protocol-buffers).

In short:

1. Install the _protoc_ compiler itself (e.g., in Arch Linux you can install _extra/protobuf_ package).
2. Install runtime `go install google.golang.org/protobuf/cmd/protoc-gen-go@latest`.
3. Install grpc runtime `go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest`.

Having compiler installed, do from the root of the repo:

```
$ protoc api/v1/*.proto \
    --go_out=. \
    --go-grpc_out=. \
    --go_opt=paths=source_relative \
    --go-grpc_opt=paths=source_relative \
    --proto_path=.
```
