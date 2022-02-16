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

Open another terminal and first post some data (_httpie_ is used as an example):

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
