# Licensed under the Apache License, Version 2.0 (the "License");
# You may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# Copyright (C) 2022-2023 xqyjlj<xqyjlj@126.com>
#
# @author      xqyjlj
# @file        Dockerfile
#
# Change Logs:
# Date           Author       Notes
# ------------   ----------   -----------------------------------------------
# 2023-01-31     xqyjlj       initial version
#

FROM csplink/ubuntu_ci:22.04

RUN set -x
RUN set

ARG user=csplink

RUN apt update
RUN apt upgrade -y
RUN apt-get install -y scons
RUN apt-get install -y ninja-build
RUN apt-get install -y pkg-config
RUN apt-get install -y libglib2.0-dev
RUN apt-get install -y libpixman-1-dev
RUN apt-get install -y -qq libncurses5-dev lib32z1

RUN mkdir -p /tmp \
    && cd /tmp \
    && curl -s https://download.qemu.org/qemu-7.1.0.tar.xz | tar xJf - -C /tmp \
    && cd /tmp/qemu-7.1.0 \
    && ./configure --target-list=arm-softmmu,aarch64-softmmu,riscv64-softmmu \
    && make -j$(nproc) \
    && make install \
    && cd / \
    && rm -rf /tmp/qemu-7.1.0

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
RUN opt/arm-linux-musleabi_for_x86_64-pc-linux-gnu/bin/arm-linux-musleabi-gcc -v
RUN opt/aarch64-linux-musleabi_for_x86_64-pc-linux-gnu/bin/aarch64-linux-musleabi-gcc -v
RUN opt/riscv64-linux-musleabi_for_x86_64-pc-linux-gnu/bin/riscv64-unknown-linux-musl-gcc -v
RUN qemu-system-aarch64 -version
RUN qemu-system-arm -version
RUN qemu-system-riscv64 -version
