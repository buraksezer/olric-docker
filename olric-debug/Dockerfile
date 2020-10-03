FROM golang:alpine as build
RUN apk add build-base
RUN GO111MODULE=on go get -ldflags="-s -w" github.com/buraksezer/olric/cmd/olric-cli@v0.3.0-beta.4
RUN GO111MODULE=on go get -ldflags="-s -w" github.com/buraksezer/olric/cmd/olric-stats@v0.3.0-beta.4
RUN GO111MODULE=on go get -ldflags="-s -w" github.com/buraksezer/olric/cmd/olric-load@v0.3.0-beta.4