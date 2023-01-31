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
RUN apt-get install -qq libncurses5-dev lib32z1

USER ${user}

RUN mkdir -p ~/tmp \
    && cd ~/tmp \
    && git clone https://github.com/xmake-io/xmake.git \
    && cd ~/tmp/xmake \
    && git checkout tags/v2.7.2 -b v2.7.2-branch \
    && git submodule update --init \
    && make build \
    && ./scripts/get.sh __local__ __install_only__ \
    && /bin/bash -c "source ~/.xmake/profile && xmake --version" \
    && cd ~ \
    && rm -rf ~/tmp

USER root

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
