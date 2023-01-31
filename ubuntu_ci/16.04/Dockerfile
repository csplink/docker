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

FROM ubuntu:16.04

RUN set -x
RUN set

ARG user=csplink

# install basic
RUN apt update
RUN apt upgrade -y
RUN apt install -y sudo vim
RUN apt install -y net-tools inetutils-ping
RUN apt install -y wget curl
RUN apt install -y tree
RUN apt install -y lbzip2 bzip2
RUN apt install -y git
RUN apt install -y xz-utils
RUN apt install -y bash-completion
RUN DEBIAN_FRONTEND="noninteractive" apt -y install tzdata

# set time zone
RUN TZ=Asia/Shanghai && \
    ln -snf /usr/share/zoneinfo/$TZ /etc/localtime

# python
RUN apt install -y python python-pip
RUN apt install -y python3 python3-pip

# SSH
RUN apt install -y openssh-server

# add user/password
RUN useradd --create-home --no-log-init --shell /bin/bash ${user} \
    && usermod -aG sudo ${user} \
    && echo "${user}:${user}" | chpasswd

# clean cache
RUN apt clean
RUN rm -rf /var/lib/apt/lists/*
RUN mkdir /var/lib/apt/lists/partial

# auto start ssh
COPY ./start_ssh.sh /root/start_ssh.sh
RUN chmod +x /root/start_ssh.sh
RUN printf "\nsource /usr/share/bash-completion/bash_completion\n" >> /root/.bashrc
RUN printf "\n# startup run\n" >> /root/.bashrc
RUN printf "if [ -f /root/start_ssh.sh ]; then\n" >> /root/.bashrc
RUN printf "    ./root/start_ssh.sh\n" >> /root/.bashrc
RUN printf "fi\n" >> /root/.bashrc

# end
RUN cat /etc/issue
RUN python -V
RUN python3 -V

# expose port
EXPOSE 22 
