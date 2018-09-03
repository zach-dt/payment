FROM ubuntu:16.04

# Install GO
RUN apt-get update -y && apt-get install --no-install-recommends -y -q curl build-essential ca-certificates git mercurial bzr
RUN mkdir /go && curl https://storage.googleapis.com/golang/go1.7.3.linux-amd64.tar.gz | tar xvzf - -C /go --strip-components=1
RUN mkdir /gopath

ENV GOROOT /go
ENV GOPATH /gopath
ENV PATH $PATH:$GOROOT/bin:$GOPATH/bin

# Build app
RUN mkdir /app
COPY payment/ /go/src/github.com/microservices-demo/payment

RUN go get -u github.com/FiloSottile/gvt
RUN cd /go/src/github.com/microservices-demo/payment/ && gvt restore
RUN ls -lsa /go/src/github.com/microservices-demo/payment

RUN GOOS=linux go build -a -ldflags -linkmode=external -installsuffix cgo -o /app/main github.com/microservices-demo/payment/cmd/paymentsvc

CMD ["/app/main", "-port=8080"]

#EXPOSE 80
