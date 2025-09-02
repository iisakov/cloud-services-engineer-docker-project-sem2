FROM golang:1.17-alpine AS builder

WORKDIR /app

COPY . .

RUN go build -o api ./cmd/api

FROM alpine:3.21

RUN adduser -D -u 1001 appuser
USER appuser

WORKDIR /app

EXPOSE 80

COPY --from=builder /app/api .
CMD ["/app/api"]