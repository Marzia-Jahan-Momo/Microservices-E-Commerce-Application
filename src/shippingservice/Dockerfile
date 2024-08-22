FROM golang:1.22.5-alpine as builder
WORKDIR /src

# restore dependencies
COPY go.mod go.sum ./

RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -o /go/bin/shippingservice .

# Final stage
FROM scratch

WORKDIR /src

COPY --from=builder /go/bin/shippingservice /src/shippingservice

ENV APP_PORT=50051

ENV GOTRACEBACK=single

EXPOSE 50051
ENTRYPOINT ["/src/shippingservice"]
