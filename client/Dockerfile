# STEP 1 build executable binary
FROM golang:alpine as builder
COPY * $GOPATH/src/chat/
WORKDIR $GOPATH/src/chat/
#get dependancies
#you can also use dep
RUN go get -d -v
#build the binary
ENV CGO_ENABLED 0 
ENV GOOS linux 
ENV GOARCH amd64
RUN go build -ldflags="-w -s" -o /go/bin/tcpclient
# STEP 2 build a small image
# start from scratch
FROM scratch
# Copy our static executable
COPY --from=builder /go/bin/tcpclient /go/bin/tcpclient
ENTRYPOINT ["/go/bin/tcpclient"]
