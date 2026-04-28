FROM golang:1.21-alpine AS builder
WORKDIR /app
COPY static/ ./static/
COPY dispatcher.go .
RUN go build -o dispatcher dispatcher.go

FROM alpine:latest
WORKDIR /app
COPY --from=builder /app/dispatcher .
COPY --from=builder /app/static/ ./static/
EXPOSE 80
CMD ["./dispatcher"]