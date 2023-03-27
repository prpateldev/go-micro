# Micro Services in Go

This repository is an example of micro services written in go programming language. The examples implemented in different approaches, e.g. it contains example of http services, RabbitMQ for managing queues, RPC and gRPC, mostly these examples can be seen in **Logger Service and Broker Service**.

**Tools needed for GRPC**

Run this in projects/
```bash
go install google.golang.org/protobuf/cmd/protoc-gen-go@v1.27
go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@v1.2
```

Later install protoc tool for generating gRPC code from .proto files.
```bash  
brew install protobuf
protoc --version
```

And make sure that your go path is added in $PATH, check .zshrc or .bashrc
```bash
export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin
```

**Command to generate code**
```bash
protoc --go_out=. --go_opt=paths=source_relative --go-grpc_out=. --go-grpc_opt=paths=source_relative logs.proto
```
Note: To run above command you must be in the same directory where .proto file is located.
