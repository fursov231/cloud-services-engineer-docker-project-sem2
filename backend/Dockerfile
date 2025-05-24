FROM golang:1.24.3-alpine3.21 AS builder

WORKDIR /app

COPY go.mod go.sum ./

RUN go mod download

COPY . .

RUN go build -o myapp ./cmd/api && rm -rf /var/cache/*

FROM alpine:3.21.3

RUN addgroup -S appgroup && adduser -S appuser -G appgroup

WORKDIR /app

COPY --from=builder --chown=appuser:appgroup /app/myapp ./

USER appuser

EXPOSE 8081

CMD ["./myapp"]