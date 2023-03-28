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

**Build Docker Image**

```bash
docker build -f logger-service.dockerfile -t prpateldev/logger-service:1.0.0 .
```

Push docker image to docker hub
```bash
docker push prpateldev/logger-service:1.0.0
```

If you are not logged in use 
```bash 
docker login
```


**Docker swarm commands**
To init docker swarm
```bash
docker swarm init
```

To get worker token
```bash
docker swarm join-token worker
```

To get manager token
```bash
docker swarm join-token manager
```

To deploy docker swarm
```bash
docker stack deploy -c swarm.yml myapp
```


To list all running services
```bash
docker service ls
```

To scale service
```bash
docker service scale myapp_listener-service=3
```

To update a service
- Build docker image with tag (-t) and updated version e.g. 1.0.1 etc.
- Push the image to docker hub.
- Always update service when there are atleast 2 replicas are running, to prevent down time. (or scale a service before update if there is only 1 replica).
- Finally run the docker service update command.


To update a service
```bash
docker service update --image prpateldev/logger-service:1.0.1 myapp_logger-service
```

To stop running all docker swarm services
```bash
docker stack rm myapp
```

To remove docker swarm e.g. myapp
use --force for manager
```bash
docker swarm leave --force
```

