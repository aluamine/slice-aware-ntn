FROM golang:1.14 AS builder

RUN git clone https://github.com/shynuu/trunks
WORKDIR /go/trunks
RUN go get -d github.com/shynuu/trunks
RUN go install github.com/shynuu/trunks

FROM debian:buster-slim
RUN apt-get update && DEBIAN_FRONTEND=non-interactive apt-get install -qy --no-install-recommends --no-install-suggests \
    iproute2 iptables procps tcpdump iputils-ping \
    && rm -rf /var/lib/apt/lists/*
COPY --from=builder /go/bin/trunks /usr/local/sbin/trunks
