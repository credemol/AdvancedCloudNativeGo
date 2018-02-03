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

$ go get github.com/credemol/AdvancedCloudNativeGo

$ mkdir -p ${GOPATH}/src/github.com/your-github-username/AdvancedCloudNativeGo
$ cd ${GOPATH}/src/github.com/your-github-username/AdvancedCloudNativeGo
```

> In this case, your-github-username means your username registered on github.com.

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

##### Download and Install gin
[gin/gonic/gin](https://github.com/gin-gonic/gin)

```sh
$ go get github.com/gin-gonic/gin
```

##### Create main.go file
```sh
$ cd ${GOPATH}/src/github.com/credemol/AdvancedCloudNativeGo

$ mkdir -p Frameworks/Gin-Web && cd "$_"
$ vi main.go
```

---
#### main.go template

```go
package main

import (
	"net/http"
	"os"

	"github.com/gin-gonic/gin"
)

func main() {

}

func port() string {
	port := os.Getenv("PORT")
	if len(port) == 0 {
		port = "8080"
	}
	return ":" + port
}
```
@[3-8](import libraries)
@[10-12](main function)
@[14-20](get port value saved as an environment variable or 8080 by default)

---
#### main.go - main() function

```go
func main() {
	engine := gin.Default()

	engine.GET("/ping", func(c *gin.Context) {
		c.String(http.StatusOK, "pong")
  })
  


	engine.Run(port())
}
```

---
#### run and test

```sh
$ go build 
$ ./Gin-Web

$ curl http://localhost:8080/ping
```

---
#### main.go - add more endpoits

```go
func main() {
	engine := gin.Default()

	engine.GET("/ping", func(c *gin.Context) {
		c.String(http.StatusOK, "pong")
	})

	engine.GET("/hello", func(c *gin.Context) {
		c.JSON(http.StatusOK, gin.H{"message": "Hello Gin Framework."})
	})

	engine.Run(port())
}
```
@[7-9](JSON Response Data)

---
#### build and run again

```sh
$ Ctrl-C
$ go build
$ ./Gin-Web

$ curl http://localhost:8080/hello
```

---
#### book.go 

```go
package main

// Book type with Name, Author and ISBN
type Book struct {
	Title       string `json:"title"`
	Author      string `json:"author"`
	ISBN        string `json:"isbn"`
	Description string `json:"description,omitempty"`
}

var books = map[string]Book{
	"0345391802": Book{Title: "The Hitchhiker's Guide to the Galaxy", Author: "Douglas Adams", ISBN: "0345391802"},
	"0000000000": Book{Title: "Advanced Cloud Native Go", Author: "M.-Leander Reimer", ISBN: "0000000000"},
}

// AllBooks returns a slice of all books
func AllBooks() []Book {
	values := make([]Book, len(books))
	idx := 0
	for _, book := range books {
		values[idx] = book
		idx++
	}
	return values
}

// GetBook returns the book for a given ISBN
func GetBook(isbn string) (Book, bool) {
	book, found := books[isbn]
	return book, found
}

// CreateBook creates a new Book if it does not exist
func CreateBook(book Book) (string, bool) {
	_, exists := books[book.ISBN]
	if exists {
		return "", false
	}
	books[book.ISBN] = book
	return book.ISBN, true
}

// UpdateBook updates an existing book
func UpdateBook(isbn string, book Book) bool {
	_, exists := books[isbn]
	if exists {
		books[isbn] = book
	}
	return exists
}

// DeleteBook removes a book from the map by ISBN key
func DeleteBook(isbn string) {
	delete(books, isbn)
}
```
@[1](package main)
@[4-9](Book Data struct and JSON property names)
@[11-13](Initialize data source using map)
@[17-25](get all books)
@[28-31](get a book with isbn)
@[34-41](create a book)
@[44-50](update a book)
@[53-55](delete a book)

---
#### main.go - main function

```go
func main() {
	engine := gin.Default()

	engine.GET("/ping", func(c *gin.Context) {
		c.String(http.StatusOK, "pong")
	})

	engine.GET("/hello", func(c *gin.Context) {
		c.JSON(http.StatusOK, gin.H{"message": "Hello Gin Framework."})
	})

	engine.GET("/api/books", func(c *gin.Context) {
		c.JSON(http.StatusOK, AllBooks())
	})

	engine.POST("/api/books", func(c *gin.Context) {
		var book Book
		if c.BindJSON(&book) == nil {
			isbn, created := CreateBook(book)
			if created {
				c.Header("Location", "/api/books/"+isbn)
				c.Status(http.StatusCreated)
			} else {
				c.Status(http.StatusConflict)
			}
		}
	})

	engine.GET("/api/books/:isbn", func(c *gin.Context) {
		isbn := c.Params.ByName("isbn")
		book, found := GetBook(isbn)

		if found {
			c.JSON(http.StatusOK, book)
		} else {
			c.AbortWithStatus(http.StatusNotFound)
		}
	})

	engine.PUT("/api/books/:isbn", func(c *gin.Context) {
		isbn := c.Params.ByName("isbn")

		var book Book

		if c.BindJSON(&book) == nil {
			exists := UpdateBook(isbn, book)
			if exists {
				c.Status(http.StatusOK)
			} else {
				c.AbortWithStatus(http.StatusNotFound)
			}
		}
	})

	engine.DELETE("api/books/:isbn", func(c *gin.Context) {
		isbn := c.Params.ByName("isbn")
		DeleteBook(isbn)
		c.Status(http.StatusOK)
	})

	engine.Run(port())
}
```
@[12-14](get all books)
@[16-27](create a book)
@[29-38](get a book with isbn)
@[40-53](update a book with isbn)
@[55-59](delete a book with isbn)

---
#### run and test api

```sh
$ go build
$ ./Gin-Web

[GIN] 2018/01/23 - 14:42:23 | 200 |     168.202µs |             ::1 | GET      /api/books
[GIN] 2018/01/23 - 14:44:09 | 201 |     270.462µs |             ::1 | POST     /api/books
[GIN] 2018/01/23 - 14:45:12 | 200 |      70.793µs |             ::1 | GET      /api/books/1234567890
[GIN] 2018/01/23 - 14:46:05 | 200 |      46.466µs |             ::1 | PUT      /api/books/1234567890
[GIN] 2018/01/23 - 14:46:33 | 200 |      40.716µs |             ::1 | GET      /api/books
[GIN] 2018/01/23 - 14:47:07 | 200 |       3.584µs |             ::1 | DELETE   /api/books/1234567890

```
> Test these endpoint with Postman test

---
#### Gin-Web Template in main() function before engine.Run(port())

```go
	engine.LoadHTMLGlob("./templates/*.html")
	engine.StaticFile("/favicon.ico", "./favicon.ico")

	engine.GET("/", func(c *gin.Context) {
		c.HTML(http.StatusOK, "index.html", gin.H{
			"title": "Advanced Cloud Native Go with Gin Framework",
		})
	})
```

---
#### templates/index.html

```html
{{ define "index.html" }}
<html>

<head>
    <title>{{ .title }}</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
    <script type="text/JavaScript">
        $(document).ready(function(){
            $.getJSON( "/hello", function( data ) {
                $("#message").html(data.message)
             });
         });
    </script>
</head>

<body>
    <div id="message"></div>
</body>

</html>
{{ end }}
```

---
#### Run & Test

```sh
$ Ctrl-C
$ go build
$ ./Gin-Web

$ curl http://localhost:8080/
```

---
### 1.4 Containerization and Composition with Docker

- Writing a Dockerfile for the advanced Go microservice
- Building and running Docker image using Docker Compose
- Tagging and pushing Docker image to remote registry

--- 
#### Frameworks/Gin-Web/Dockerfile

```dockerfile
FROM golang:1.8.1-alpine

RUN apk update && apk upgrade && apk add --no-cache bash git
RUN go get github.com/gin-gonic/gin

ENV SOURCES /go/src/github.com/PacktPublishing/Advanced-Cloud-Native-Go/Frameworks/Gin-Web/
COPY . ${SOURCES}

RUN cd ${SOURCES}  && CGO_ENABLED=0 go build

WORKDIR ${SOURCES}
CMD ${SOURCES}Gin-Web
EXPOSE 8080
```

---
#### Frameworks/Gin-Web/docker-compose.yml

```yaml
version: '2'

services:
  gin-web:
    build: .
    image: gin-web:1.0.1
    environment:
    - PORT=8080
    ports:
    - "8080:8080"
```

---
#### build docker image and run

```sh
$ docker version
$ docker images

$ docker-compose build
$ docker-compose up

$ Ctrl-C
$ docker-compose up -d
$ docker ps
$ docker-compose stop
$ docker ps

```

---
#### tag docker image & push it

```sh
$ docker image ls | grep gin-web

$ docker tag gin-web:1.0.1 credemol/gin-web:1.0.1
$ docker image ls | grep gin-web

$ docker push credemol/gin-web:1.0.1
```

---
### 1.5 Microservice orchestration with Kubernetes

- Describing and creating a Kubernetes deployment data vectors
- Describing and creating a Kubernetes service directory and files
- Deploying and running deployment and service in Kubernetes locally

---
#### Frameworks/Gin-Web/kubernetes/k8s-deployment.yml

```yaml
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: gin-web
  labels:
    app: gin-web
spec:
  replicas: 3
  template:
    metadata:
      labels: 
        app: gin-web
        tier: service
    spec:
      containers:
      - name: gin-web
        image: gin-web:1.0.1
        ports:
        - containerPort: 9090
        env:
        - name: PORT
          value: "9090"
        
        resources:
          requests:
            memory: "64Mi"
            cpu: "125m"
          limits:
            memory: "128Mi"
            cpU: "250m"

        readinessProbe:
          httpGet:
            path: /ping
            port: 9090
          initialDelaySeconds: 5
          timeoutSeconds: 5
        livenessProbe:
          httpGet:
            path: /ping
            port: 9090
          initialDelaySeconds: 5
          timeoutSeconds: 5
```
@[1-6](deployment)
@[7-13](replicaset)
@[14-22](pod)
@[24-30](resource limitation)
@[32-43](readiness probe & liveness probe)

---
#### Frameworks/Gin-Web/kubernetes/k8s-service.yml

```yaml
apiVersion: v1
kind: Service
metadata: 
  name: gin-web
  labels:
    app: gin-web
    tier: service
spec:
  type: NodePort
  ports:
  - port: 9090
  selector:
    app: gin-web
```

---
#### Frameworks/Gin-Web/kubernetes/k8s-ingress.yml

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: gin-web
  labels:
    app: gin-web
    tier: frontend
spec:
  backend:
    serviceName: gin-web
    servicePort: 9090
```

---
#### run the app on the kubernetes

```sh
$ minikube version
$ minikube ip
$ kubectl cluster-info
$ minikube dashboard


$ kubectl apply -f kubernetes/

$ kubectl get deployments
# make sure that pods are not running
$ kubectl get pods

```

---
#### minikube docker-env

```sh
$ kubectl delete all -l app=gin-web

$ minikube docker-env
$ eval $(minikube docker-env)

$ docker image ls | grep gin-web
$ docker-compose build 
$ docker image ls | grep gin-web

$ kubectl apply -f kubernetes/
$ kubectl get all -l app=gin-web
$ kubectl get pods -l app=gin-web

$ kubectl log one-of-pod-names
```

---
#### minikube service

```sh
$ kubectl get services
$ kubectl get svc

$ minikube service gin-web
$ minikube service gin-web --url

$ curl "$(minikube service gin-web --url)/hello"

$ kubectl scale deployment gin-web --replicas=8
$ kubectl get pods
```

---
## 2. Service Discovery and Configuration

- Introduction and using Consul for service discovery
- Performing service endpoint registration using Consul
- Implementing microservice discovery
- Configuring with Kubernetes only
- Introducing and using Consul as central configuration server
- Performing service lookup in a client using Consul

---
### Install Consule

```sh
$ go get github.com/hashicorp/consul
$ ls ${GOPATH}/bin
```
Ignore below!!

It is not necessary to install Consul to complete this section.
[Consul Installation Guide](https://www.consul.io/docs/install/index.html)

```sh
# on Mac OS
$ brew install consul

# on Windows OS, Open CMD as Administrator
$ choco install consul
```

---
### 2.1 Using Consul for Microservice Discovery

- Starting and running Consul using Docker compose
- Registering services with Consul using REST API
- Lookup services using the Consul UI and REST API

```sh
$ exit
$ mkdir -p Discovery/Consul && cd "$_"
```

---
#### Disvoery/Consul/docker-compose.yml

```yaml
version: '2'

services:
  consul:
    image: consul:0.8.3
    ports:
      - "8300:8300"
      - "8400:8400"
      - "8500:8500"
    links:
      - gin-web-01
      - gin-web-02
    networks:
      - sky-net

  gin-web-01:
    image: gin-web:1.0.1
    environment:
      - PORT=8080
    ports:
      - "8080:8080"
    networks:
      - sky-net

  gin-web-02:
    image: gin-web:1.0.1
    environment:
      - PORT=9090
    ports:
      - "9090:9090"
    networks:
      - sky-net

networks:
  sky-net:
    driver: bridge  
```
@[4-13](consule service)
@[16-23](gin-web-01 service)
@[25-32](gin-web-02 service)
@[34-36](networks)

---
#### Run Consul

```sh
$ cd 
$ docker container stop $(docker container ls -q)
$ docker container rm $(docker container ls -aq)
$ docker-compose up
$ open http://localhost:8500/ui
```

- [Get Consul Catalog Services](http://localhost:8500/v1/catalog/services)
- [Get Consul Agent Services](http://localhost:8500/v1/agent/services)


#### Register Consul (Gin-Web-01)

- URL: [http://localhost:8500/v1/agent/service/register](http://localhost:8500/v1/agent/service/register)
- HTTP Method: PUT
- Header: Content-Type: application/json

```json
{
	"ID": "gin-web-01",
	"Name": "gin-web",
	"Tags": [
		"cloud-native-go",
		"v1"
	],
	"Address": "gin-web-01",
	"Port": 8080,
	"EnableTagOverride": false,
	"check": {
		"id": "ping", 
		"name": "HTTP API on port 8080",
		"http": "http://gin-web-01:8080/ping",
		"interval": "5s",
		"timeout": "1s"
	}
}
```

---
#### Register Consul (Gin-Web-01)

- URL: [http://localhost:8500/v1/agent/service/register](http://localhost:8500/v1/agent/service/register)
- HTTP Method: PUT
- Header: Content-Type: application/json

```json
{
	"ID": "gin-web-02",
	"Name": "gin-web",
	"Tags": [
		"cloud-native-go",
		"v1"
	],
	"Address": "gin-web-02",
	"Port": 9090,
	"EnableTagOverride": false,
	"check": {
		"id": "ping", 
		"name": "HTTP API on port 9090",
		"http": "http://gin-web-02:9090/ping",
		"interval": "5s",
		"timeout": "1s"
	}
}
```

---
#### Stop gin-web-02 service and see how Consul works

```sh
$ docker container ls
$ docker container stop consul_gin-web-02_1
```

Send requests below
1. Get Consul Health Gin-Web All
1. Get Consul Health Gin-Web Passing
1. Get Consul Critical Health Checks

```sh
$ docker-compose down
```
---
### 2.2 Using Consul for Central Microservice Configuration

- Starting and running Consul using Docker compose
- Creating configuration values using the Consul UI and REST API
- Retrieving configuration values using the Consul REST API

```sh
$ exit

$ mkdir -p Configuration/Consul && cd "$_"
```

---
#### Configuration/Consul/docker-compose.yml

```yaml
version: '2'

services:
  consul:
    image: consul:0.8.3
    ports:
      - "8300:8300"
      - "8400:8400"
      - "8500:8500"
    networks:
      - sky-net

networks:
  sky-net:
    driver: bridge
```

---
#### Run Consule

```sh
$ docker-compose up

# open new terminal
$ open http://localhost:8500/ui
```

---
#### Configuration

1. Click KEY/VALUE menu
1. Key: path1/path2
1. Value: The value

```sh
$ consul kv get path1/path2
$ consul kv put foo bar
$ consul kv get foo
```

---
#### Consul REST API for Configuration

1. Get Gin Web All Keys
1. Create Gin Web Message Key
1. Get Gin Web All Keys (Again)
1. Get Gin Web All Configs
1. Get Gin Web Message Config(Raw)
1. Create Gin Web Message Key(Update)
1. Get Gin Web Message Config(Raw)
1. Delete Gin Web Configs

---
### 2.3 Implement Go microservice registration with Consul

- Implementing service endpoint registration with Consul for Go microservice
- Implementing and registering health check endpoint
- Running microservice and Consul using Docker compose

```sh
$ mkdir -p Discovery/Simple/server && cd "$_"
```

---
#### Discovery/Simple/server/simple-server.go

```go
package main

import (
	"fmt"
	"net/http"
	"os"
)

func main() {
	registerServiceWithConsul()

	fmt.Println("Starting Simple Server.")
	http.HandleFunc("/info", info)
	http.ListenAndServe(port(), nil)
}

func registerServiceWithConsul() {
	// TODO implement me
}

func info(w http.ResponseWriter, r *http.Request) {
	fmt.Println("The /info endpoint is being called...")
	w.WriteHeader(http.StatusOK)
	fmt.Fprintf(w, "Hello Consul Discovery")
}

func port(): string {
	port := os.Getenv("PORT")

	if len(port) == 0 {
		port = "8080"
	}
	return ":" + port
}

func hostname() string {
	hostname, _ := os.Hostname()
	return hostname
}
```
@[1-7](package and import)
@[9-15](main function)
@[17-19](registerServiceWithConsul function)
@[21-25](/info handler function)
@[27-34](get port)
@[36-39](get hostname)

---
#### registerServiceWithConsul() 

```go
import (
	"fmt"
	"net/http"
	"os"
	"strconv"

	consulapi "github.com/hashicorp/consul/api"
)

func registerServiceWithConsul() {
	config := consulapi.DefaultConfig()
	consul, err := consulapi.NewClient(config)
	if err != nil {
		fmt.Println(err)
	}

	var registration = new(consulapi.AgentServiceRegistration)

	registration.ID = "simple-server"
	registration.Name = "simple-server"

	address := hostname()
	registration.Address = address
	port, _ := strconv.Atoi(port()[1:len(port())])
	registration.Port = port

	registration.Check = new(consulapi.AgentServiceCheck)
	registration.Check.HTTP = fmt.Sprintf("http://%s:%v/info", address, port)
	registration.Check.Interval = "5s"
	registration.Check.Timeout = "3s"

	consul.Agent().ServiceRegister(registration)
}
```
@[7-7](import consul/api)
@[10-33](registerServiceWithConsul function)
@[11-15](config)
@[17-32](registration)

---
#### Discovery/Simple/server/Dockerfile

```dockerfile
FROM golang:1.8.1-alpine

RUN apk update && apk upgrade && apk add --no-cache bash git

RUN go get github.com/hashicorp/consul/api

ENV SOURCES /go/src/github.com/PacktPublishing/Advanced-Cloud-Native-Go/Discovery/Simple/
COPY . ${SOURCES}

RUN cd ${SOURCES}server/ && CGO_ENABLED=0 go build

ENV CONSUL_HTTP_ADDR localhost:8500

WORKDIR ${SOURCES}server/
CMD ${SOURCES}server/server
```

---
#### Discovery/Simple/docker-compose.yml

```yaml
version: '2'

services:
  consul:
    image: consul:0.8.3
    ports:
      - "8300:8300"
      - "8400:8400"
      - "8500:8500"
    networks:
      - sky-net
  
  simple-server:
    build:
      context: .
      dockerfile: server/Dockerfile
    image: simple-server:1.0.1
    environment:
      - CONSUL_HTTP_ADDR=consul:8500
    depends_on:
      - consul
    networks:
      - sky-net
      
networks:
  sky-net:
    driver: bridge
```
@[3-11](consul service)
@[13-23](simple-server service)
@[25-27](networks configuration)

---
#### Run services

```sh
$ cd Discovery/Simple
$ docker-compose up

# Run following commands in a new terminal
$ open http://localhost:8500/ui
$ docker ps
$ docker stop simple_simple-server_1
# And then refresh SERVICES from Consul UI
```

---
### 2.4 Implement Go Microservice Lookup with Consul

- Implementing a simple service client application
- Implementing a service endpoint lookup via Consul
- Running Consul, microservice, and client using Docker compose

```sh
$ mkdir -p Discovery/Simple/client && cd "$_"

```

#### Discovery/Simple/client/simple-client.go

```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
	"time"

	consulapi "github.com/hashicorp/consul/api"	
)

var url string

func main() {
	lookupServiceWithConsul()

	fmt.Println("Starting Simple Client")
	var client = &http.Client{
		Timeout: time.Second * 10,
	}

	callHelloEvery(5*time.Second, client)
}

func lookupServiceWithConsul() {

}

func hello(t time.Time, client *http.Client) {
	response, err := client.Get(url)

	if err != nil {
		fmt.Println(err)
		return
	}

	body, _ := ioutil.ReadAll(response.Body)
	fmt.Printf("%s. Time is %v\n", body, t)
}

func callHelloEvery(d time.Duration, client *http.Client) {
	for x := range time.Tick(d) {
		hello(x, client)
	}
}
```
@[1-1](main package)
@[3-10](import packages)
@[14-23](main function)
@[25-27](lookupServiceWithConsul function)
@[29-39](hello function)
@[41-45](callHelloEvery function)

---
#### lookupServiceWithConsul() function

```go
func lookupServiceWithConsul() {
	config := consulapi.DefaultConfig()
	consul, error := consulapi.NewClient(config)
	if error != nil {
		fmt.Println(error)
		return
	}

	services, error := consul.Agent().Services()
	if error != nil {
		fmt.Println(error)
		return
	}

	service := services["simple-server"]
	address := service.Address
	port := service.Port

	url = fmt.Sprintf("http://%s:%v/info", address, port)
}
```

---
#### Discovery/Simple/client/Dockerfile

```dockerfile
FROM golang:1.8.1-alpine

RUN apk update && apk upgrade && apk add --no-cache bash git

RUN go get github.com/hashicorp/consul/api

ENV SOURCES /go/src/github.com/PacktPublishing/Advanced-Cloud-Native-Go/Discovery/Simple/
COPY . ${SOURCES}

RUN cd ${SOURCES}client/ && CGO_ENABLED=0 go build

ENV CONSUL_HTTP_ADDR localhost:8500

WORKDIR ${SOURCES}client/
CMD ${SOURCES}client/client
```

---
#### Discovery/Simple/docker-compose.yml

```yaml
version: '2'

services:
  consul:
    image: consul:0.8.3
    ports:
      - "8300:8300"
      - "8400:8400"
      - "8500:8500"
    networks:
      - sky-net
  
  simple-server:
    build:
      context: .
      dockerfile: server/Dockerfile
    image: simple-server:1.0.1
    environment:
      - CONSUL_HTTP_ADDR=consul:8500
    depends_on:
      - consul
    networks:
      - sky-net

  simple-client:
    build:
      context: .
      dockerfile: client/Dockerfile
    image: simple-client:1.0.1
    environment:
      - CONSUL_HTTP_ADDR=consul:8500
    depends_on:
      - consul
      - simple-server
    networks:
      - sky-net      
      
networks:
  sky-net:
    driver: bridge
    
```
@[25-36](simple-client service)


---
#### Build images and Run them

```sh
$ cd Discovery/Simple
$ docker-compose build
$ docker-compose up

# Run these commands in a new terminal
$ open http://localhost:8500/ui
$ docker container ls
$ docker container logs simple_simple-client_1
```

---
### 3.5 Implement service discovery and configuration with Kubernetes

- Describing deploying Kubernetes service, and config map definitions
- Implementing Go microservice client configuration using the config map
- Running Go microservice client and service with Kubernetes

---

![important-k8s-concepts](https://user-images.githubusercontent.com/5771924/35316925-87b4b728-0117-11e8-9a73-a978fa5f5cb4.png)

---?image=https://user-images.githubusercontent.com/5771924/35316925-87b4b728-0117-11e8-9a73-a978fa5f5cb4.png&size=auto 100%

---
#### Initialize

```sh
$ mkdir -p Discovery/Kubernetes/server 
$ mkdir -p Discovery/Kubernetes/client

$ cd Discovery/Kubernetes
```

---
#### Discovery/Kubernetes/server/simple-k8s-server.go

```go
package main

import (
	"fmt"
	"net/http"
	"os"
)

func main() {
	http.HandleFunc("/info", info)
	http.ListenAndServe(port(), nil)
}

func info(w http.ResponseWriter, r *http.Request) {
	fmt.Println("The /info endpoint is being called...")
	w.WriteHeader(http.StatusOK)
	fmt.Fprintf(w, "Hello Kubernetes Discovery & Configuration")
}

func port() string {
	port := os.Getenv("PORT")
	if len(port) == 0 {
		port = "8080"
	}
	return ":" + port
}
```
@[1-1](main package)
@[3-7](import packages)
@[9-12](main function)
@[14-18](info function)
@[20-26](port function)

---
### Discovery/Kubernetes/server/Dockerfile

```dockerfile
FROM golang:1.8.1-alpine

ENV SOURCES /go/src/github.com/PacktPublishing/Advanced-Cloud-Native-Go/Discovery/Kubernetes/
COPY . ${SOURCES}

RUN cd ${SOURCES}server/ && CGO_ENABLED=0 go build

WORKDIR ${SOURCES}server/
CMD ${SOURCES}server/server
```

---
#### Discovery/Kubernetes/client/simple-k8s-client.go

```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
	"os"
	"time"
)

var url string

func main() {
	initServiceURL()

	var client = &http.Client{
		Timeout: time.Second * 10,
	}

	callHelloEvery(5*time.Second, client)
}

func initServiceURL() {
	url = os.Getenv("SERVICE_URL")
	fmt.Printf("(ENV) SERVICE_URL: %s", url)
	if len(url) == 0 {
		url = "http://simple-k8s-server:8080/info"
	}
}

func hello(t time.Time, client *http.Client) {
	// Call the greeter
	response, err := client.Get(url)

	if err != nil {
		fmt.Println(err)
		return
	}

	// print response
	body, _ := ioutil.ReadAll(response.Body)
	fmt.Printf("%s. Time is %v\n", body, t)
}

func callHelloEvery(d time.Duration, client *http.Client) {
	for x := range time.Tick(d) {
		hello(x, client)
	}
}
```
@[1-1](main package)
@[3-9](import packages)
@[11](url variable)
@[13-21](main function)
@[23-29](initServiceURL function)
@[31-43](hello function)
@[45-49](callHelloEvery function)

---
#### Discovery/Kubernetes/client/Dockerfile

```dockerfile
FROM golang:1.8.1-alpine

ENV SOURCES /go/src/github.com/PacktPublishing/Advanced-Cloud-Native-Go/Discovery/Kubernetes/
COPY . ${SOURCES}

RUN cd ${SOURCES}client/ && CGO_ENABLED=0 go build

WORKDIR ${SOURCES}client/
CMD ${SOURCES}client/client
```

---
#### Discovery/Kubernetes/docker-compose.yml

```yaml
version: '2'

services: 
  simple-k8s-server:
    build:
      context: .
      dockerfile: server/Dockerfile
    image: simple-k8s-server:1.0.1
    environment: 
    - PORT=9090
    ports: 
    - "9090:9090"

  simple-k8s-client:
    build:
      context: .
      dockerfile: client/Dockerfile
    image: simple-k8s-client:1.0.1      
    depends_on:
    - simple-k8s-server
    environment: 
    - SERVICE_URL=http://simple-k8s-server:9090/info
```
@[1-12](simple-k8s-server service)
@[14-22](simple-k8s-client service)

---
#### Build Docker Images

```sh
$ cd Discovery/Kubernetes

$ env | grep DOCKER
$ minikube docker-env 
$ eval $(minikube docker-env)
$ env | grep DOCKER

$ docker-compose build
$ docker image ls | grep simple-k8s

```

---
#### Discovery/Kubernetes/simple-k8s-server-deployment.yaml (Deprecated)

```yaml
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: simple-k8s-server
spec:
  replicas: 2
  template:
    metadata:
      labels:
        io.kompose.service: simple-k8s-server
    spec:
      containers:
      - name: simple-k8s-server
        image: "simple-k8s-server:1.0.1"
        ports:
        - containerPort: 9090
        env:
        - name: PORT
          value: "9090"

        readinessProbe:
          httpGet:
            path: /info
            port: 9090
          initialDelaySeconds: 5
          timeoutSeconds: 5
        livenessProbe:
          httpGet:
            path: /info
            port: 9090
          initialDelaySeconds: 10
          timeoutSeconds: 5
```
@[6](replicas)
@[11-19](simple-k8s-server pods)
@[21-32](readinessProbe and livenessProbe)

---
#### Kubernetes + Compose = Kompose
[http://kompose.io/](http://kompose.io/)
[https://developers.redhat.com/blog/2017/08/02/getting-started-with-kompose/](https://developers.redhat.com/blog/2017/08/02/getting-started-with-kompose/)

Installation
```sh
$ brew install kompose
$ cd Discovery/Kubernetes

```

---
#### Discovery/Kubernetes/docker-compose.yml

```yaml
version: '3'

services: 
  simple-k8s-server:
    build:
      context: .
      dockerfile: server/Dockerfile
    image: simple-k8s-server:1.0.1
    environment: 
    - PORT=9090
    ports: 
    - "9090:9090"
    labels:
      kompose.service.type: NodePort
    deploy:
      replicas: 2

  simple-k8s-client:
    build:
      context: .
      dockerfile: client/Dockerfile
    image: simple-k8s-client:1.0.1      
    depends_on:
    - simple-k8s-server
    environment: 
    - SERVICE_URL=http://simple-k8s-server:9090/info
```
@[1](set version as 3)
@[13-16](kompose uses these properties. set service type as NodePort rather than ClusterIP which is default value)

---
#### Generate Kubernetes file

```sh
$ kompose convert

INFO Kubernetes file "simple-k8s-client-service.yaml" created 
INFO Kubernetes file "simple-k8s-server-service.yaml" created 
INFO Kubernetes file "simple-k8s-client-deployment.yaml" created 
INFO Kubernetes file "simple-k8s-server-deployment.yaml" created 
```

---
#### simple-k8s-server-deployment.yaml

```yaml
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  annotations:
    kompose.cmd: kompose convert
    kompose.service.type: NodePort
    kompose.version: 1.7.0 ()
  creationTimestamp: null
  labels:
    io.kompose.service: simple-k8s-server
  name: simple-k8s-server
spec:
  replicas: 2
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        io.kompose.service: simple-k8s-server
    spec:
      containers:
      - env:
        - name: PORT
          value: "9090"
        image: simple-k8s-server:1.0.1
        name: simple-k8s-server
        ports:
        - containerPort: 9090
        resources: {}
        
        readinessProbe:
          httpGet:
            path: /info
            port: 9090
          initialDelaySeconds: 5
          timeoutSeconds: 5
        livenessProbe:
          httpGet:
            path: /info
            port: 9090
          initialDelaySeconds: 10
          timeoutSeconds: 5

      restartPolicy: Always
status: {}

```
@[12](set the value of replicas as 2)
@[31-42](readinessProbe and livenessProbe)

---
#### Run simple-k8s-server

```sh
$ kubectl apply -f simple-k8s-server-deployment.yaml
$ kubectl apply -f simple-k8s-server-service.yaml
$ kubectl get pods

```

---
#### simple-k8s-configmap.yaml

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: simple-k8s-config
  namespace: default
data:
  service.url: "http://simple-k8s-server:9090/info"
```

---
#### apply simple-k8s-config

```sh
$ kubectl apply -f simple-k8s-configmap.yaml
$ kubectl get configmaps
$ kubectl describe configmap simple-k8s-config

```

---
#### simple-k8s-client-deployment.yaml

```yaml
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  annotations:
    kompose.cmd: kompose convert
    kompose.version: 1.7.0 ()
  creationTimestamp: null
  labels:
    io.kompose.service: simple-k8s-client
  name: simple-k8s-client
spec:
  replicas: 1
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        io.kompose.service: simple-k8s-client
    spec:
      containers:
      - env:
        - name: SERVICE_URL
          valueFrom: 
            configMapKeyRef:
              name: simple-k8s-config
              key: service.url
        image: simple-k8s-client:1.0.1
        name: simple-k8s-client
        resources: {}
      restartPolicy: Always
status: {}

```
@[23-26](read service.url from ConfigMap named simple-k8s-config)

---
#### apply simple-k8s-client

```sh
$ kubectl apply -f simple-k8s-client-deployment.yaml
$ kubectl apply -f simple-k8s-client-service.yaml

$ minikube dashboard
```

---
## 3. Microservice Communication

- Challenges involved with different microservice communication patterns
- Guarding synchronous calls by using a circuit breaker
- Implementing topic based async publish-subscribe communication with Kafka
- implementing RPC with a binary protocol like ProtoBuf
- Implementing async messaging with work queues and RabbitMQ

---
### 3.1 Microservice Communication Patterns: Sync and Async

- Pros and cons of synchronous microservice communication
- Pros and cons of asynchronous microservice communication
- Pros and cons of different message payload encoding

---
#### A General Internet Communication Model

![communication-model](https://user-images.githubusercontent.com/5771924/35365459-0c751fde-01b8-11e8-86dc-a8f0c90d0f10.png)

---
#### Classification of Communication Systems: 
##### Message Receiver Cardinality

![message-receiver-cardinality](https://user-images.githubusercontent.com/5771924/35366121-295b5b74-01bb-11e8-91bf-bdd0624ee845.png)

---
#### Classification of Communication Systems:
##### Who Begins the Communication?

![who-brings-communication](https://user-images.githubusercontent.com/5771924/35366129-317b995e-01bb-11e8-9668-bbe4a224d548.png)

---
#### Messaging Is a Flexible, Asynchronous Yet Reliable
##### Communication Pattern

![communication-pattern](https://user-images.githubusercontent.com/5771924/35366789-80a3eb32-01be-11e8-8421-d939e15350a7.png)

---
#### Popular Message Payload Formats and Encodings

- XML
- JSON
- Binary (For example, grpc)

---
### 3.2 Implement Sync RPC calls with Binary Protocols

- Writing service definition and generate code
- Writing server side implementation and microservice
- Writing client side code and call service remotely

--- 
#### Initialize 

```sh
$ mkdir -p Communication/Go-Micro/proto && cd "$_"
```

---
#### Protocol Buffers
Protocol Buffers are a language-neutral, platform-neutral extensible mechanism for serializing structured data.

[https://developers.google.com/protocol-buffers/](https://developers.google.com/protocol-buffers/)
[https://github.com/grpc/grpc-go](https://github.com/grpc/grpc-go)

```sh
#$ go get -u github.com/golang/protobuf/protoc-gen-go
#$ go get -u github.com/golang/protobuf/{proto,protoc-gen-go}
$ go get github.com/micro/protobuf/{proto,protoc-gen-go}
$ go get -u google.golang.org/grpc
# make sure that protoc-gen-go has been installed.
# It must be in your $PATH for the protocol compiler protoc to find it.
$ ls ${GOPATH}/bin
```

---
#### Install Protocol Compiler

[http://google.github.io/proto-lens/installing-protoc.html](http://google.github.io/proto-lens/installing-protoc.html)

```sh
$ brew install protobuf

# or brew upgrade protobuf

$ protoc --help
$ protoc --version
```

---
#### Communication/Go-Micro/proto/greeter.proto

```proto
syntax = "proto3";

service Greeter {
    rpc Hello(HelloRequest) returns (HelloResponse) {}
}

message HelloRequest {
    string name = 1;
}

message HelloResponse {
    string name = 2;
}
```

---
#### generate go source file

> protoc -I=$SRC_DIR --go_out=$DST_DIR $SRC_DIR/addressbook.proto
[https://github.com/micro/go-micro](https://github.com/micro/go-micro)
```sh
#$ protoc --go_out=plugins=grpc:. greeter.proto
$ cd Communication/Go-Micro/proto
#$ protoc --go_out=plugins=micro:. greeter.proto
$ go get github.com/micro/protobuf/{proto,protoc-gen-go}
$ protoc -I ./proto/ ./proto/greeter.proto --go_out=plugins=micro:proto
$ 
$ ls -l
$ cat greeter.pb.go
```

---
#### Install go-micro

```sh
$ go get github.com/micro/go-micro
```

---
#### Communication/Go-Micro/server/main.go

```go

package main

import (
	"fmt"

	proto "github.com/credemol/AdvancedCloudNativeGo/Communication/Go-Micro/proto"
	micro "github.com/micro/go-micro"
	"golang.org/x/net/context"
)

type Greeter struct{}

func (g *Greeter) Hello(ctx context.Context, req *proto.HelloRequest, rsp *proto.HelloResponse) error {
	rsp.Greeting = "Hello " + req.Name

	fmt.Printf("Responding with %s\n", rsp.Greeting)
	return nil
}

func main() {
	service := micro.NewService(
		micro.Name("greeter"),
		micro.Version("1.0.1"),
		micro.Metadata(map[string]string{
			"type": "helloworld",
		}),
	)

	service.Init()

	proto.RegisterGreeterHandler(service.Server(), new(Greeter))

	if err := service.Run(); err != nil {
		fmt.Println(err)
	}
}

```

---
#### Communication/Go-Micro/server/Dockerfile

```dockerfile
FROM golang:1.8.1-alpine

RUN apk update && apk upgrade && apk add --no-cache bash git

RUN go get -u github.com/micro/micro && \
    go get github.com/micro/protobuf/proto && \
    go get -u github.com/micro/protobuf/protoc-gen-go

ENV SOURCES /go/src/github.com/credemol/AdvancedCloudNativeGo/Communication/Go-Micro/
COPY . ${SOURCES}

RUN cd ${SOURCES}server/ && CGO_ENABLED=0 go build

ENV CONSUL_HTTP_ADDR localhost:8500

WORKDIR ${SOURCES}server/
CMD ${SOURCES}server/server
```

---
#### Communication/Go-Micro/client/main.go

```go
package main

import (
	"fmt"
	"time"

	proto "github.com/credemol/AdvancedCloudNativeGo/Communication/Go-Micro/proto"
	micro "github.com/micro/go-micro"
	"golang.org/x/net/context"
)

func main() {
	service := micro.NewService(
		micro.Name("greeter"),
		micro.Version("latest"),
		micro.Metadata(map[string]string{
			"type": "helloworld",
		}),
	)

	service.Init()

	greeter := proto.NewGreeterClient("greeter", service.Client())
	callEvery(3*time.Second, greeter, hello)
}

func hello(t time.Time, greeter proto.GreeterClient) {
	rsp, err := greeter.Hello(context.TODO(), &proto.HelloRequest{Name: "Nick, calling at " + t.String()})

	if err != nil {
		fmt.Println(err.Error())
		return
	}
	fmt.Printf("%s\n", rsp.Greeting)
}

func callEvery(d time.Duration, greeter proto.GreeterClient, f func(time.Time, proto.GreeterClient)) {
	for x := range time.Tick(d) {
		f(x, greeter)
	}
}

```

---
#### Communication/Go-Micro/client/Dockerfile

```dockerfile
FROM golang:1.8.1-alpine

RUN apk update && apk upgrade && apk add --no-cache bash git

RUN go get -u github.com/micro/micro && \
    go get github.com/micro/protobuf/proto && \
    go get -u github.com/micro/protobuf/protoc-gen-go && \
    go get github.com/micro/go-plugins/wrapper/breaker/hystrix && \
    go get github.com/afex/hystrix-go/hystrix

ENV SOURCES /go/src/github.com/credemol/AdvancedCloudNativeGo/Communication/Go-Micro/
COPY . ${SOURCES}

RUN cd ${SOURCES}client/ && CGO_ENABLED=0 go build

ENV CONSUL_HTTP_ADDR localhost:8500

WORKDIR ${SOURCES}client/
CMD ${SOURCES}client/client
```


---
#### Communication/Go-Micro/docker-compose.yml

```yaml
version: '2'

services: 
  consul:
    image: consul:0.8.3
    ports:
      - "8300:8300"
      - "8400:8400"
      - "8500:8500"
    networks:
      - sky-net

  go-micro-server:
    build:
      context: .
      dockerfile: server/Dockerfile
    image: go-micro-server:1.0.1
    environment: 
    - CONSUL_HTTP_ADDR=consul:8500
    depends_on:
      - consul
    networks:
      - sky-net

  go-micro-client:
    build:
      context: .
      dockerfile: client/Dockerfile
    image: go-micro-client:1.0.1     
    environment: 
    - CONSUL_HTTP_ADDR=consul:8500 
    depends_on:
      - consul
      - go-micro-server
    networks:
      - sky-net

networks:
  sky-net:
    driver: bridge
  
```

---
#### build

```sh
$ docker-compose build
$ docker-compose up
/*
$ cd proto
$ go install
$ cd ../server
$ go build
$ cd ../client
$ go build
$ cd ..
*/
```

---
### 3.3 Using circuit breakers for resilient communication

- Implementing synchronous call using a circuit breaker
- Defining fallback behavior in case of service errors
- Configuring circuit breaker and adding monitoring dashboard

---
#### Histrix Hot it works
![Hystrix](https://www.slideshare.net/ufried/resilience-with-hystrix)

---
#### Communication/Go-Micro/client/main.go

```go
package main

import (
	"fmt"
	"net"
	"net/http"
	"time"

	hystrix "github.com/afex/hystrix-go/hystrix"
	proto "github.com/credemol/AdvancedCloudNativeGo/Communication/Go-Micro/proto"
	micro "github.com/micro/go-micro"
	breaker "github.com/micro/go-plugins/wrapper/breaker/hystrix"
	"golang.org/x/net/context"
)

func main() {
	service := micro.NewService(
		micro.Name("greeter"),
		micro.Version("latest"),
		micro.Metadata(map[string]string{
			"type": "helloworld",
		}),
	)

	service.Init(
		micro.WrapClient(breaker.NewClientWrapper()),
	)

	hystrix.DefaultVolumeThreshold = 3
	hystrix.DefaultErrorPercentThreshold = 75
	hystrix.DefaultTimeout = 500
	hystrix.DefaultSleepWindow = 3500

	hystrixStreamHandler := hystrix.NewStreamHandler()
	hystrixStreamHandler.Start()
	go http.ListenAndServe(net.JoinHostPort("", "8081"), hystrixStreamHandler)

	greeter := proto.NewGreeterClient("greeter", service.Client())
	callEvery(3*time.Second, greeter, hello)
}

func hello(t time.Time, greeter proto.GreeterClient) {
	rsp, err := greeter.Hello(context.TODO(), &proto.HelloRequest{Name: "Nick, calling at " + t.String()})

	if err != nil {
		if err.Error() == "hystrix: timeout" {
			fmt.Printf("%s. Insert fallback logic here.\n", err.Error())
		} else {
			fmt.Println(err.Error())
		}

		return
	}
	fmt.Printf("%s\n", rsp.Greeting)
}

func callEvery(d time.Duration, greeter proto.GreeterClient, f func(time.Time, proto.GreeterClient)) {
	for x := range time.Tick(d) {
		f(x, greeter)
	}
}
```


---
#### Communication/Go-Micro/server/main.go

```go
package main

import (
	"fmt"
	"time"

	proto "github.com/credemol/AdvancedCloudNativeGo/Communication/Go-Micro/proto"
	micro "github.com/micro/go-micro"
	"golang.org/x/net/context"
)

type Greeter struct{}

var counter int

func (g *Greeter) Hello(ctx context.Context, req *proto.HelloRequest, rsp *proto.HelloResponse) error {
	counter++
	if counter > 7 && counter < 15 {
		time.Sleep(1000 * time.Millisecond)
	} else {
		time.Sleep(100 * time.Millisecond)
	}
	rsp.Greeting = "Hello " + req.Name

	fmt.Printf("Responding with %s\n", rsp.Greeting)
	return nil
}

func main() {
	service := micro.NewService(
		micro.Name("greeter"),
		micro.Version("1.0.1"),
		micro.Metadata(map[string]string{
			"type": "helloworld",
		}),
	)

	service.Init()

	proto.RegisterGreeterHandler(service.Server(), new(Greeter))

	if err := service.Run(); err != nil {
		fmt.Println(err)
	}
}

```

---
#### docker-compose.yml

```yaml
version: '2'

services: 
  consul:
    image: consul:0.8.3
    ports:
      - "8300:8300"
      - "8400:8400"
      - "8500:8500"
    networks:
      - sky-net

  go-micro-server:
    build:
      context: .
      dockerfile: server/Dockerfile
    image: go-micro-server:1.0.1
    environment: 
    - CONSUL_HTTP_ADDR=consul:8500
    depends_on:
      - consul
    networks:
      - sky-net

  go-micro-client:
    build:
      context: .
      dockerfile: client/Dockerfile
    image: go-micro-client:1.0.1     
    environment: 
    - CONSUL_HTTP_ADDR=consul:8500 
    depends_on:
      - consul
      - go-micro-server
    networks:
      - sky-net

  hystrix-dashboard:
    image: mlabouardy/hystrix-dashboard:latest
    ports:
      - "9002:9002"
    networks:
      - sky-net

networks:
  sky-net:
    driver: bridge
  
```

---
#### hystrix dashboard


---
### 3.4 Implement Message Queuing with RabbitMQ

- Implementing message producer for RabbitMQ
- Implementing message consumer and processing logic
- Running the mesage queue, and consumer with Docker compose

---
#### Initialize Project

```sh
$ mkdir -p Communication/RabbitMQ/consumer
$ mkdir -p Communication/RabbitMQ/producer && cd "$_"
```

---
#### Communication/RabbitMQ/producer/producer.go

```go
package main

import (
	"fmt"
	"log"
	"os"
	"time"

	"github.com/streadway/amqp"
)

func main() {
	fmt.Println("Starting RabbitMQ producer...")
	time.Sleep(7 * time.Second)

	conn, err := amqp.Dial(brokerAddr())
	failOnError(err, "Failed to connect to RabbitMQ")
	defer conn.Close()

	ch, err := conn.Channel()
	failOnError(err, "Failed to open a channel")
	defer ch.Close()

	q, err := ch.QueueDeclare(
		queue(), // name
		true,    // durable
		false,   // delete when unused
		false,   // exclusive
		false,   // no-wait
		nil,     // arguments
	)
	failOnError(err, "Failed to declare a queue")

	msgCount := 0

	// Get signal for finish
	doneCh := make(chan struct{})

	go func() {
		for {
			msgCount++
			body := fmt.Sprintf("Hello RabbitMQ message %v", msgCount)

			err = ch.Publish(
				"",     // exchange
				q.Name, // routing key
				false,  // mandatory
				false,  // immediate
				amqp.Publishing{
					ContentType: "text/plain",
					Body:        []byte(body),
				})
			log.Printf(" [x] Sent %s", body)
			failOnError(err, "Failed to publish a message")

			time.Sleep(5 * time.Second)
		}
	}()

	<-doneCh
}

func brokerAddr() string {
	brokerAddr := os.Getenv("BROKER_ADDR")
	if len(brokerAddr) == 0 {
		brokerAddr = "amqp://guest:guest@localhost:5672/"
	}
	return brokerAddr
}

func queue() string {
	queue := os.Getenv("QUEUE")
	if len(queue) == 0 {
		queue = "default-queue"
	}
	return queue
}

func failOnError(err error, msg string) {
	if err != nil {
		log.Fatalf("%s: %s", msg, err)
	}
}

```

---
#### Communication/RabbitMQ/producer/Dockerfile

```Dockerfile
FROM golang:1.8.1-alpine

RUN apk update && apk upgrade && apk add --no-cache bash git

RUN go get github.com/streadway/amqp

ENV SOURCES /go/src/github.com/PacktPublishing/Advanced-Cloud-Native-Go/Communication/RabbitMQ/
COPY . ${SOURCES}

RUN cd ${SOURCES}producer/ && CGO_ENABLED=0 go build

ENV BROKER_ADDR amqp://guest:guest@localhost:5672/

WORKDIR ${SOURCES}producer/
CMD ${SOURCES}producer/producer
```

---
#### Communication/RabbitMQ/consumer/consumer.go

```go
package main

import (
	"fmt"
	"log"
	"os"
	"time"

	"github.com/streadway/amqp"
)

func main() {
	fmt.Println("Starting RabbitMQ consumer...")
	time.Sleep(7 * time.Second)

	conn, err := amqp.Dial(brokerAddr())
	failOnError(err, "Failed to connect to RabbitMQ")
	defer conn.Close()

	ch, err := conn.Channel()
	failOnError(err, "Failed to open a channel")
	defer ch.Close()

	q, err := ch.QueueDeclare(
		queue(), // name
		true,    // durable
		false,   // delete when unused
		false,   // exclusive
		false,   // no-wait
		nil,     // arguments
	)
	failOnError(err, "Failed to declare a queue")

	msgs, err := ch.Consume(
		q.Name, // queue
		"",     // consumer
		true,   // auto-ack
		false,  // exclusive
		false,  // no-local
		false,  // no-wait
		nil,    // args
	)
	failOnError(err, "Failed to register a consumer")

	forever := make(chan bool)

	go func() {
		for d := range msgs {
			log.Printf("Received a message: %s", d.Body)
		}
	}()

	log.Printf(" [*] Waiting for messages. To exit press CTRL+C")
	<-forever
}

func brokerAddr() string {
	brokerAddr := os.Getenv("BROKER_ADDR")
	if len(brokerAddr) == 0 {
		brokerAddr = "amqp://guest:guest@localhost:5672/"
	}
	return brokerAddr
}

func queue() string {
	queue := os.Getenv("QUEUE")
	if len(queue) == 0 {
		queue = "default-queue"
	}
	return queue
}

func failOnError(err error, msg string) {
	if err != nil {
		log.Fatalf("%s: %s", msg, err)
	}
}

```

---
#### Communication/RabbitMQ/consumer/Dockerfile

```dockerfile
FROM golang:1.8.1-alpine

RUN apk update && apk upgrade && apk add --no-cache bash git

RUN go get github.com/streadway/amqp

ENV SOURCES /go/src/github.com/PacktPublishing/Advanced-Cloud-Native-Go/Communication/RabbitMQ/
COPY . ${SOURCES}

RUN cd ${SOURCES}consumer/ && CGO_ENABLED=0 go build

ENV BROKER_ADDR amqp://guest:guest@localhost:5672/

WORKDIR ${SOURCES}consumer/
CMD ${SOURCES}consumer/consumer

```

---
#### Communication/RabbitMQ/docker-compose.yml

```yaml
version: '2'

services: 
  rabbitmq:
    image: rabbitmq:3.6.9-management-alpine
    ports:
      - "4369:4369"
      - "5671:5671"
      - "5672:5672"
      - "15671:15671"
      - "15672:15672"
      - "25672:25672"
    environment: 
      - RABBITMQ_DEFAULT_USER=guest
      - RABBITMQ_DEFAULT_PASS=guest
    networks:
      - sky-net

  rabbitmq-producer:
    build:
      context: .
      dockerfile: producer/Dockerfile
    image: rabbitmq-producer:1.0.1
    environment: 
      - BROKER_ADDR=amqp://guest:guest@rabbitmq:5672/
      - QUEUE=test-queue
    depends_on:
      - rabbitmq
    links:
      - rabbitmq
    networks:
      - sky-net

  rabbitmq-consumer:
    build:
      context: .
      dockerfile: consumer/Dockerfile
    image: rabbitmq-consumer:1.0.1     
    environment: 
      - BROKER_ADDR=amqp://guest:guest@rabbitmq:5672/
      - QUEUE=test-queue
    depends_on:
      - rabbitmq
    links:
      - rabbitmq
    networks:
      - sky-net

networks:
  sky-net:
    driver: bridge
```

---
#### Build and Run

```sh
$ docker-compose build
$ docker-compose up
```

---
#### RabbitMQ Management

[http://localhost:15672](http://localhost:15672)

Username: guest
Password: guest

```sh
$ docker container ls
$ docker container stop rabbitmq_rabbitmq-consumer_1
$ docker container start rabbitmq_rabbitmq-consumer_1

```

---
### 3.5 Implement Publish/Subscribe with Apache Kafka

- Implementing message publishing to Apache Kafka
- Implementing topic subscription and processing logic
- Run Apache Kafca, publisher, and subscriber with Docker compose

---
#### Initialize Project

```sh
$ mkdir -p Communication/Kafka/subscriber
$ mkdir -p Communication/Kafka/producer && cd "$_"
```

---
#### Communication/Kafka/producer/producer.go

```go
package main

import (
	"fmt"
	"os"

	"time"

	"github.com/Shopify/sarama"
)

func main() {
	fmt.Println("Starting synchronous Kafka producer...")
	time.Sleep(5 * time.Second)

	config := sarama.NewConfig()
	config.Producer.Return.Successes = true
	config.Producer.Return.Errors = true
	config.Producer.RequiredAcks = sarama.WaitForAll
	config.Producer.Retry.Max = 5

	brokers := []string{brokerAddr()}
	producer, err := sarama.NewSyncProducer(brokers, config)
	if err != nil {
		panic(err)
	}

	defer func() {
		if err := producer.Close(); err != nil {
			panic(err)
		}
	}()

	topic := topic()
	msgCount := 0

	// Get signal for finish
	doneCh := make(chan struct{})

	go func() {
		for {
			msgCount++

			msg := &sarama.ProducerMessage{
				Topic: topic,
				Value: sarama.StringEncoder(fmt.Sprintf("Hello Kafka %v", msgCount)),
			}

			partition, offset, err := producer.SendMessage(msg)
			if err != nil {
				panic(err)
			}

			fmt.Printf("Message is stored in topic(%s)/partition(%d)/offset(%d)\n", topic, partition, offset)
			time.Sleep(5 * time.Second)
		}
	}()

	<-doneCh
}

func brokerAddr() string {
	brokerAddr := os.Getenv("BROKER_ADDR")
	if len(brokerAddr) == 0 {
		brokerAddr = "localhost:9092"
	}
	return brokerAddr
}

func topic() string {
	topic := os.Getenv("TOPIC")
	if len(topic) == 0 {
		topic = "default-topic"
	}
	return topic
}

```

---
#### Communication/Kafka/producer/Dockerfile

```dockerfile
FROM golang:1.8.1-alpine

RUN apk update && apk upgrade && apk add --no-cache bash git

RUN go get github.com/Shopify/sarama

ENV SOURCES /go/src/github.com/PacktPublishing/Advanced-Cloud-Native-Go/Communication/Kafka/
COPY . ${SOURCES}

RUN cd ${SOURCES}producer/ && CGO_ENABLED=0 go build

ENV BROKER_ADDR localhost:9092

WORKDIR ${SOURCES}producer/
CMD ${SOURCES}producer/producer

```

---
#### Communication/Kafka/subscriber/subscriber.go

```go
package main

import (
	"fmt"
	"os"
	"os/signal"
	"time"

	"github.com/Shopify/sarama"
)

func main() {
	fmt.Println("Starting synchronous Kafka subscriber...")
	time.Sleep(5 * time.Second)

	config := sarama.NewConfig()
	config.Consumer.Offsets.Initial = sarama.OffsetOldest
	config.Consumer.Offsets.CommitInterval = 5 * time.Second
	config.Consumer.Return.Errors = true

	// Create new consumer
	brokers := []string{brokerAddr()}
	master, err := sarama.NewConsumer(brokers, config)
	if err != nil {
		panic(err)
	}

	defer func() {
		if err := master.Close(); err != nil {
			panic(err)
		}
	}()

	topic := topic()

	// decide about the offset here: literal value, sarama.OffsetOldest, sarama.OffsetNewest
	// this is important in case of reconnection
	consumer, err := master.ConsumePartition(topic, 0, sarama.OffsetOldest)
	if err != nil {
		panic(err)
	}

	signals := make(chan os.Signal, 1)
	signal.Notify(signals, os.Interrupt)

	// Count how many message processed
	msgCount := 0

	// Get signal for finish
	doneCh := make(chan struct{})
	go func() {
		for {
			select {
			case err := <-consumer.Errors():
				fmt.Println(err)
			case msg := <-consumer.Messages():
				msgCount++
				fmt.Println("Received messages", string(msg.Key), string(msg.Value))
			case <-signals:
				fmt.Println("Interrupt is detected")
				doneCh <- struct{}{}
			}
		}
	}()

	<-doneCh
	fmt.Println("Processed", msgCount, "messages")
}

func brokerAddr() string {
	brokerAddr := os.Getenv("BROKER_ADDR")
	if len(brokerAddr) == 0 {
		brokerAddr = "localhost:9092"
	}
	return brokerAddr
}

func topic() string {
	topic := os.Getenv("TOPIC")
	if len(topic) == 0 {
		topic = "default-topic"
	}
	return topic
}

```

---
#### Communication/Kafka/subscriber/Dockerfile

```dockerfile
FROM golang:1.8.1-alpine

RUN apk update && apk upgrade && apk add --no-cache bash git

RUN go get github.com/Shopify/sarama

ENV SOURCES /go/src/github.com/PacktPublishing/Advanced-Cloud-Native-Go/Communication/Kafka/
COPY . ${SOURCES}

RUN cd ${SOURCES}subscriber/ && CGO_ENABLED=0 go build

ENV BROKER_ADDR localhost:9092

WORKDIR ${SOURCES}subscriber/
CMD ${SOURCES}subscriber/subscriber

```

---
#### Communication/Kafka/docker-compose.yml

```yaml
version: '2'

services: 
  zookeeper:
    image: dockerkafka/zookeeper
    ports:
      - "2181:2181"
      - "2888:2888"
      - "3888:3888"
      - "5000:5000"
    networks:
      - sky-net

  kafka:
    image: dockerkafka/kafka
    ports:
      - "9092:9092"
    depends_on:
      - zookeeper
    links:
      - zookeeper
    networks:
      - sky-net

  kafka-producer:
    build:
      context: .
      dockerfile: producer/Dockerfile
    image: kafka-producer:1.0.1
    environment: 
      - BROKER_ADDR=kafka:9092
    depends_on:
      - zookeeper
      - kafka
    links:
      - kafka
    networks:
      - sky-net

  kafka-subscriber:
    build:
      context: .
      dockerfile: subscriber/Dockerfile
    image: kafka-subscriber:1.0.1     
    environment: 
      - BROKER_ADDR=kafka:9092 
    depends_on:
      - zookeeper
      - kafka
    links:
      - kafka
    networks:
      - sky-net

networks:
  sky-net:
    driver: bridge
  
```

---
#### Build & Run

```sh
$ docker-compose build
```

--- 
# Q & A