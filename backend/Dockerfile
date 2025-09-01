FROM golang:1.17-alpine AS builder

WORKDIR /app

COPY . .

RUN go build -o api ./cmd/api

FROM alpine:3.21

WORKDIR /app

COPY --from=builder /app/api .
CMD ["/app/api"]