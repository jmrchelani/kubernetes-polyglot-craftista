FROM golang:1.21-alpine as build

WORKDIR /app

COPY go.mod go.sum ./

RUN go mod download

COPY . .

RUN go build -o app .

FROM alpine:latest

WORKDIR /app

COPY --from=build /app/app .
COPY --from=build /app/templates ./templates
COPY --from=build /app/static ./static
COPY --from=build /app/config.json .

EXPOSE 8080

CMD [ "./app" ]