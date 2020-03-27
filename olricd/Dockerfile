FROM golang:latest as build
RUN go get github.com/buraksezer/olric
WORKDIR /go/src/github.com/buraksezer/olric
RUN CGO_ENABLED=1 go build -ldflags="-s -w" -o /usr/bin/olricd ./cmd/olricd

FROM gcr.io/distroless/base-debian10
COPY --from=build /usr/bin/olricd /usr/bin/olricd
COPY --from=build /go/src/github.com/buraksezer/olric/cmd/olricd/olricd.yaml /etc/olricd.yaml
ENV OLRICD_CONFIG='/etc/olricd.yaml'

EXPOSE 3320 3322
ENTRYPOINT ["/usr/bin/olricd"]
