FROM golang:1.24-alpine3.22

# upgrading packages
RUN apk update && \
    apk upgrade --available && \
    apk add --no-cache \
    curl

WORKDIR /app/logger
COPY ./configuration-exporter/configuration-exporter/logger/go.mod ./
COPY ./configuration-exporter/configuration-exporter/logger/go.sum ./
RUN go mod download

WORKDIR /app
COPY ./configuration-exporter/configuration-exporter/go.mod ./
COPY ./configuration-exporter/configuration-exporter/go.sum ./
RUN go mod download

# go build and exec
COPY configuration-exporter/configuration-exporter .
RUN go build -o /configuration-exporter
CMD [ "/configuration-exporter" ]
