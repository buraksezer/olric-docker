FROM golang:latest as build

RUN go get -u github.com/buraksezer/olric-consul-plugin
WORKDIR /go/src/github.com/buraksezer/olric-consul-plugin
RUN CGO_ENABLED=1 go build -ldflags="-s -w" -buildmode=plugin -o /usr/lib/olric-consul-plugin.so

FROM olricio/olricd:latest
COPY --from=build /usr/lib/olric-consul-plugin.so /usr/lib/olric-consul-plugin.so