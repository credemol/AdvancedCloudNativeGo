# Advanced Cloud Native Go


--- 
## Resources

- [Advanced Cloud Native Go](https://www.packtpub.com/application-development/advanced-cloud-native-go-video)
---
## Agenda

1. Go Microservice Frameworks
1. Service Discovery and Configuration
1. Microservice Communication


---
## 1. Go Microservice Frameworks

1. The course overview
1. Anatomy of a cloud native application platform
1. Overview of Go microservice frameworks and libraries
1. Advanced Go microservice implementation
1. Containerization and composition with Docker

---
## 2. Service Discovery and Configuration

1. Using consul for microserivce discovery
1. Using Consul for central microservice configuration
1. Implement Go microservice registration with Consul
1. Implement Go microservice lookup with Consul
1. Implement service discovery and configuration with Kubernetes

---
## 3. Microservice Communication

1. Microservice communication patterns:
  - Sync and Async
1. Implement sync RCP calls with binary protocols
1. Using circuit breakers for resilient communication
1. Implement message queuing with Rabbitmq
1. Implement publish/subscribe with Apache Kafka
---
## Configuration

```sh
$ export GOPATH=~/go

$ mkdir -p ${GOPATH}/src/AdvancedCloudNativeGo
$ cd ${GOPATH}/src/AdvancedCloudNativeGo
```


---
### The course overview

--- 
#### What we will learn
![what-we-will-learn](https://user-images.githubusercontent.com/5771924/35202385-c728d00a-ff65-11e7-9aa9-c7794162eb78.png)
####


---
#### Pre-Requisites

- Basic programming skills and Go knowledge
- Any modern operating system (Windows 10, mac OS, Linux)
- Working Go language installation, see https://golang.org/
- IDE with Go support (for example: Visual Studio Code or Gogland)
- Docker toolbox or Docker native installation
- Local Kubernetes installation
- See https://github.com/kubernetes/minikube

---
## Go Microservice Frameworks

- Cloud native app platforms, Go microservice frameworks
- Writing Docker file for the advanced Go microservice
- Deployment, service, and edge server in Kubernetes
- Advanced REST service using the Gin web framework
- Using Docker compose to build and run microservice locally

---
### 1.1 Anatomy of a Cloud Native Application Platform

- Understanding the building blocks of a cloud native application platform
- Understanding the key functions of such a platform
- Knowing key technologies from the cloud native landspace

---
#### Building Blocks and Functions of a Cloud Native Application Platform

![cloud-native-app-platform](https://user-images.githubusercontent.com/5771924/35207815-639418a6-ff88-11e7-8f97-0db352b692f4.png)


---?image=https://2.bp.blogspot.com/-4c7UAsVGTnw/WVmhDkAG0FI/AAAAAAAANXI/UpBW9hxHxVkyP9DUWyNJfQuz6AnRLbq5QCLcBGAs/s640/bb-cna.jpg&size=auto 100%

---?image=https://4.bp.blogspot.com/-kdEZZoaBhJQ/WVmhDjQiX2I/AAAAAAAANXM/qC1AiUTiJ3I3njICaBqBvn6djcBvINjrACLcBGAs/s640/bb-cna1.jpg&size=auto 100%


---
![https://github.com/cncf/landscape](https://raw.githubusercontent.com/cncf/landscape/master/landscape/CloudNativeLandscape_latest.png)

---
### 1.2 Overview of Go Microservice Frameworks and Libraries

- Overviewing individual libraries and its examples
- Overviewing individual service frameworks and its examples
- Overviewing individual web frameworks and its examples

---
#### Overview of Go Microservice Frameworks and Libraries

Individual Libraries   | Service Frameworks    | Web Frameworks
-----------------------|-----------------------|-------------------
<ul><li>afex/hystrix-go</li><li>armon/go-metrics</li><li>Sirupsen/logrus</li><li>grpc/grps-go</li><li>spacemonkeygo/ monkit</li></ul>|<ul><li>Gizmo</li><li>Go Micro</li></li>Go Kit</li><li>Kite</li></ul>|<ul><li>Gin Gonic</li><li>Gorilla</li><li>Goji</li><li>Go Martini</li></ul>

---
#### Individual Libraries

- [grpc/grpc-go](https://github.com/grpc/grpc-go)
- [apex/hystrix-go](https://github.com/afex/hystrix-go)
- [go-metrics](https://github.com/armon/go-metrics)
- [spacemonkeygo/monkit](https://github.com/spacemonkeygo/monkit)
- [sirupsen/logrus](https://github.com/Sirupsen/logrus)

---
#### Service Frameworks

- [go-kit/kit](https://github.com/go-kit/kit)
- [micro/go-micro](https://github.com/micro/go-micro)
- [NYTimes/gizmo](https://github.com/nytimes/gizmo)

---
#### Web Frameworks

- [Gorilla web toolkit](http://www.gorillatoolkit.org)
- [gin/gonic/gin](https://github.com/gin-gonic/gin)

----
### 1.3 Advanced Go microservice implementation

- Implement basic HTTP microservice server with Configurable port
- Implement basic routing logic for different paths and verbs
- Implement JSON request and response processing

---
#### main.go

```sh
$ cd ${GOPATH}/src/AdvancedCloudNativeGo
$ vi main.go
```

---
####

```go

```


--- 
# Q & A