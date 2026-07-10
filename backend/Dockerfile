FROM dhi.io/golang:1-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN CGO_ENABLED=0 go build -o /tmp/devboard-backend .

FROM dhi.io/golang:1-alpine

WORKDIR /app

COPY --from=builder /tmp/devboard-backend ./devboard-backend

RUN chmod +x ./devboard-backend

EXPOSE 8080

ENTRYPOINT ["./devboard-backend"]
