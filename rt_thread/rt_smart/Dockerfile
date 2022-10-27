FROM csplink/ubuntu_ci:22.04

RUN set -x
RUN set

RUN apt update
RUN apt upgrade -y
RUN apt-get install -y scons
RUN apt-get install -y ninja-build
RUN apt-get install -y pkg-config
RUN apt-get install -y libglib2.0-dev
RUN apt-get install -y libpixman-1-dev

RUN mkdir -p /tmp/qemu
RUN curl -s https://download.qemu.org/qemu-7.1.0.tar.xz | tar xJf - -C /tmp/qemu
RUN /tmp/qemu/qemu-7.1.0/configure --target-list=arm-softmmu,aarch64-softmmu,riscv64-softmmu
RUN make -C /tmp/qemu/qemu-7.1.0
RUN make install -C /tmp/qemu/qemu-7.1.0
RUN rm -rf /tmp/qemu

RUN curl -s http://117.143.63.254:9012/www/rt-smart/arm-linux-musleabi_for_x86_64-pc-linux-gnu_latest.tar.bz2 | tar xjf - -C /opt
RUN curl -s http://117.143.63.254:9012/www/rt-smart/aarch64-linux-musleabi_for_x86_64-pc-linux-gnu_latest.tar.bz2 | tar xjf - -C /opt
RUN curl -s http://117.143.63.254:9012/www/rt-smart/riscv64/riscv64-linux-musleabi_for_x86_64-pc-linux-gnu_latest.tar.bz2 | tar xjf - -C /opt

# 清理缓存
RUN apt clean
RUN rm -rf /var/lib/apt/lists/*
RUN mkdir /var/lib/apt/lists/partial

# 结束
RUN cat /etc/issue
RUN python3 -V
RUN scons --version
RUN /opt/arm-linux-musleabi_for_x86_64-pc-linux-gnu/bin/arm-linux-musleabi-gcc -v
RUN /opt/aarch64-linux-musleabi_for_x86_64-pc-linux-gnu/bin/aarch64-linux-musleabi-gcc -v
RUN /opt/riscv64-linux-musleabi_for_x86_64-pc-linux-gnu/bin/riscv64-unknown-linux-musl-gcc -v
RUN qemu-system-aarch64 -version
RUN qemu-system-arm -version
RUN qemu-system-riscv64 -version
