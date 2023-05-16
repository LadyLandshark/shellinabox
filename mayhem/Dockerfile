# Build Stage:
FROM --platform=linux/amd64 ubuntu:18.04 as builder

## Install build dependencies.
ARG DEBIAN_FRONTEND=noninteractive
ENV TZ="America/New York"
RUN apt-get update && apt-get install -y make build-essential git libpam0g-dev zlib1g-dev dh-autoreconf libssl1.0-dev

## Add Source Code
ADD * /
ADD shellinabox /shellinabox
ADD logging /logging
ADD debian /debian
ADD demo /demo
ADD libhttp /libhttp
ADD m4 /m4
ADD misc /misc

## Build Step
RUN  autoreconf -i && ./configure && make

# Package Stage
FROM --platform=linux/amd64 ubuntu:20.04
COPY --from=builder /shellinaboxd /
#RUN apt-get update && apt install -y libsdl2-2.0-0 libpcap0.8 libasound2 libx11-6 libglib2.0-0
