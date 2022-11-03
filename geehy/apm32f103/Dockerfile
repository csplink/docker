FROM csplink/ubuntu_ci:22.04

RUN set -x
RUN set

ARG user=csplink

RUN apt update
RUN apt upgrade -y
RUN apt-get install -qq libncurses5-dev lib32z1

USER ${user}

RUN mkdir -p ~/tmp \
    && ~/tmp \
    && git clone https://github.com/xmake-io/xmake.git \
    && ~/tmp/xmake \
    && git checkout tags/v2.7.2 -b v2.7.2-branch \
    && git submodule update --init \
    && make build \
    && ./scripts/get.sh __local__ __install_only__ \
    && /bin/bash -c "source ~/.xmake/profile && xmake --version" \
    && cd ~ \
    && rm -rf ~/tmp

USER root
WORKDIR /

RUN curl -s https://armkeil.blob.core.windows.net/developer/Files/downloads/gnu-rm/10-2020q4/gcc-arm-none-eabi-10-2020-q4-major-x86_64-linux.tar.bz2 | tar xjf - -C /opt

RUN ln -s /lib/x86_64-linux-gnu/libncurses.so.6 /lib/x86_64-linux-gnu/libncurses.so.5
RUN ln -s /lib/x86_64-linux-gnu/libtinfo.so.6 /lib/x86_64-linux-gnu/libtinfo.so.5

# 清理缓存
RUN apt clean
RUN rm -rf /var/lib/apt/lists/*
RUN mkdir /var/lib/apt/lists/partial

# 结束
RUN cat /etc/issue
RUN python3 -V
RUN opt/gcc-arm-none-eabi-10-2020-q4-major/bin/arm-none-eabi-gcc -v
RUN opt/gcc-arm-none-eabi-10-2020-q4-major/bin/arm-none-eabi-gdb -v

USER root
WORKDIR /
