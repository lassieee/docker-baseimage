FROM arm32v6/alpine:3.11
MAINTAINER Erik de Vries <docker@erikdevries.nl>

# qemu arm static binary
COPY tmp/qemu-arm-static /usr/bin/qemu-arm-static

# root filesystem
COPY rootfs /

# base image packages
RUN apk -U update && \
    apk -U upgrade && \
    apk -U add --no-cache \
        bash \
        coreutils \
        ca-certificates \
        shadow \
        curl

# s6 overlay
RUN curl -L https://github.com/just-containers/s6-overlay/releases/download/v2.0.0.1/s6-overlay-armhf.tar.gz \
    | tar -xzC /

# create default user / group and folders
RUN groupadd -g 1000 abc && \
    useradd -u 1000 -g abc -d /app -s /bin/false abc && \
    mkdir -p \
	    /app \
	    /config

ENTRYPOINT ["/init"]