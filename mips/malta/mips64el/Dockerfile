# Build a Linux kernel for Malta/I6400 following recipe from:
# https://www.mips.com/blog/how-to-run-smp-linux-in-qemu-on-a-mips64-release-6-cpu/
#
# Get resulting vmlinux in 'output_dir' directory with:
# $ run -v output_dir:/mnt IMAGE_ID

FROM debian:stretch-slim

MAINTAINER Philippe Mathieu-Daudé <f4bug@amsat.org>

RUN dpkg --add-architecture mips64el

RUN apt update && \
    DEBIAN_FRONTEND=noninteractive apt install -yy eatmydata && \
    DEBIAN_FRONTEND=noninteractive eatmydata \
    apt install -y --no-install-recommends \
        bc \
        bison \
        build-essential \
        flex \
        gettext \
        gcc-mips64el-linux-gnuabi64 \
        git \
        libncurses5-dev

RUN git clone -j $(getconf _NPROCESSORS_ONLN) \
    --depth 1 \
    --branch v4.7-rc1 \
    git://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git

COPY config-4.7.0-rc1.I6400 linux/.config

RUN ARCH=mips CROSS_COMPILE=mips64el-linux-gnuabi64- \
    make -C linux oldconfig

RUN ARCH=mips CROSS_COMPILE=mips64el-linux-gnuabi64- \
    make -C linux -j $(getconf _NPROCESSORS_ONLN) vmlinux

CMD cp linux/vmlinux /mnt
