FROM csplink/ubuntu_ci:22.04

RUN set -x
RUN set

# 换源, github 用国外源会快很多
RUN /bin/cp -rf /etc/apt/sources.list.bak /etc/apt/sources.list

RUN apt update
RUN apt upgrade -y
RUN apt-get install -y scons
RUN apt-get install -y qemu
RUN apt-get install -y qemu-system-aarch64 qemu-system-arm qemu-system-riscv64

RUN curl -s http://117.143.63.254:9012/www/rt-smart/arm-linux-musleabi_for_x86_64-pc-linux-gnu_latest.tar.bz2 | tar xjf - -C /opt
RUN curl -s http://117.143.63.254:9012/www/rt-smart/aarch64-linux-musleabi_for_x86_64-pc-linux-gnu_latest.tar.bz2 | tar xjf - -C /opt
RUN curl -s http://117.143.63.254:9012/www/rt-smart/riscv64/riscv64-linux-musleabi_for_x86_64-pc-linux-gnu_latest.tar.bz2 | tar xjf - -C /opt

# 清理缓存
RUN apt clean
RUN rm -rf /var/lib/apt/lists/*
RUN mkdir /var/lib/apt/lists/partial

# 换源
# RUN sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list; 
# RUN sed -i 's/security.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list; 
RUN sed -i 's/archive.ubuntu.com/repo.huaweicloud.com/g' /etc/apt/sources.list; 
RUN sed -i 's/security.ubuntu.com/repo.huaweicloud.com/g' /etc/apt/sources.list; 

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
