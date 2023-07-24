FROM golang:alpine
WORKDIR /app
COPY ./go-app/go.mod /app
COPY ./go-app/main.go /app
RUN go install -mod=vendor
RUN go mod tidy
RUN go mod vendor
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -mod=vendor -o ./out/app ./main.go
ENTRYPOINT [ "./out/app" ] 