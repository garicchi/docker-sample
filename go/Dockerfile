FROM golang:1.11.0-alpine

RUN apk add --update git gcc build-base
RUN go get -u github.com/golang/dep/cmd/dep

ENV GOROOT /usr/local/go/
ENV GOPATH /go/

# 先に依存パッケージを記述したファイルだけCOPYする
COPY ./src/app/Gopkg.toml /go/src/app/Gopkg.toml
COPY ./src/app/Gopkg.lock /go/src/app/Gopkg.lock

WORKDIR /go/src/app

# tomlからパッケージをインストール
RUN dep ensure -v -vendor-only=true

# ソースコードのCOPY
# もしソースコードに変更があってもパッケージのインストールはcacheされる
COPY ./src/app /go/src/app

WORKDIR /go

RUN go build -o /go/bin/app app

ENTRYPOINT /go/bin/app
