FROM golang:1.18-alpine AS builder

WORKDIR /app

COPY go.mod .
COPY go.sum .
RUN go mod download

COPY . .

RUN go build -o /hello-2 main.go

FROM alpine:latest

COPY --from=builder /hello-2 /hello-2

EXPOSE 8000

CMD ["/hello-2"]
