FROM golang:1.8.1-alpine

RUN apk update && apk upgrade && apk add --no-cache bash git

RUN go get github.com/streadway/amqp

ENV SOURCES /go/src/github.com/PacktPublishing/Advanced-Cloud-Native-Go/Communication/RabbitMQ/
COPY . ${SOURCES}

RUN cd ${SOURCES}consumer/ && CGO_ENABLED=0 go build

ENV BROKER_ADDR amqp://guest:guest@localhost:5672/

WORKDIR ${SOURCES}consumer/
CMD ${SOURCES}consumer/consumer
