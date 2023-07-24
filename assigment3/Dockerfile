FROM golang:alpine AS build-stage
WORKDIR /src/app
COPY ./go-app/go.mod /src/app
COPY ./go-app/main.go /src/app
RUN go install -mod=vendor
RUN go mod tidy
RUN go mod vendor
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -mod=vendor -o ./out/app ./main.go

FROM alpine:latest
COPY --from=build-stage /src/app/out/app /src/app
EXPOSE 8080
ENTRYPOINT [ "./src/app" ]