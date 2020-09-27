FROM ubuntu:16.04

RUN apt update && \
    DEBIAN_FRONTEND=noninteractive apt install -yy eatmydata && \
    DEBIAN_FRONTEND=noninteractive eatmydata \
    apt install -y --no-install-recommends \
        bc \
        build-essential \
        ca-certificates \
        cpio \
        gettext \
        git \
        libncurses5-dev \
        pkg-config \
        python \
        rsync \
        unzip \
        wget

RUN wget -O - https://buildroot.org/downloads/buildroot-2014.11.tar.bz2 | \
    tar -xajf -

COPY buildroot-2014.11/.config buildroot-2014.11/.config

RUN make -C buildroot-2014.11 oldconfig

RUN make -C buildroot-2014.11 toolchain

CMD make -C /buildroot-2014.11
