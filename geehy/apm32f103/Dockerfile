FROM csplink/ubuntu_ci:22.04

RUN set -x
RUN set

ARG user=csplink

RUN apt update
RUN apt upgrade -y
RUN apt-get install -qq libncurses5-dev lib32z1

USER ${user}

RUN mkdir -p ~/tmp
WORKDIR /home/${user}/tmp
RUN git clone https://github.com/xmake-io/xmake.git
WORKDIR /home/${user}/tmp/xmake
RUN git checkout tags/v2.7.2 -b v2.7.2-branch
RUN git submodule update --init
RUN make build
RUN ./scripts/get.sh __local__ __install_only__
RUN /bin/bash -c "source ~/.xmake/profile"
RUN rm -rf ~/tmp

RUN mkdir -p ~/.csplink/toolchains
RUN curl -s https://armkeil.blob.core.windows.net/developer/Files/downloads/gnu-rm/10-2020q4/gcc-arm-none-eabi-10-2020-q4-major-x86_64-linux.tar.bz2 | tar xjf - -C ~/.csplink/toolchains

RUN echo ${user} | sudo -S ln -s /lib/x86_64-linux-gnu/libncurses.so.6 /lib/x86_64-linux-gnu/libncurses.so.5
RUN echo ${user} | sudo -S ln -s /lib/x86_64-linux-gnu/libtinfo.so.6 /lib/x86_64-linux-gnu/libtinfo.so.5

# 清理缓存
RUN echo ${user} | sudo -S apt clean
RUN echo ${user} | sudo -S rm -rf /var/lib/apt/lists/*
RUN echo ${user} | sudo -S mkdir /var/lib/apt/lists/partial

# 结束
RUN cat /etc/issue
RUN python3 -V
RUN /bin/bash -c "source ~/.xmake/profile && xmake --version"
RUN ~/.csplink/toolchains/gcc-arm-none-eabi-10-2020-q4-major/bin/arm-none-eabi-gcc -v
RUN ~/.csplink/toolchains/gcc-arm-none-eabi-10-2020-q4-major/bin/arm-none-eabi-gdb -v

USER root
WORKDIR /
