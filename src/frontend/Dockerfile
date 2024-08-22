FROM golang:1.22.5-alpine as builder
WORKDIR /src

COPY go.mod go.sum ./

RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -o /go/bin/frontend .


# Final stage
FROM scratch

WORKDIR /src

COPY --from=builder /go/bin/frontend /src/server

COPY ./templates ./templates

COPY ./static ./static

ENV GOTRACEBACK=single

EXPOSE 8080
ENTRYPOINT ["/src/server"]
