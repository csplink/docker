FROM ubuntu:18.04

ARG LOCATION

RUN set -x
RUN set

ARG user=csplink

# 换源
# RUN sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list; 
# RUN sed -i 's/security.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list; 
RUN sed -i 's/archive.ubuntu.com/repo.huaweicloud.com/g' /etc/apt/sources.list; 
RUN sed -i 's/security.ubuntu.com/repo.huaweicloud.com/g' /etc/apt/sources.list; 

# 安装基础软件
RUN apt update
RUN apt upgrade -y
RUN apt install -y sudo vim
RUN apt install -y net-tools inetutils-ping
RUN apt install -y wget curl
RUN apt install -y tree
RUN apt install -y lbzip2 bzip2
RUN apt install -y git
RUN apt install -y xz-utils
RUN DEBIAN_FRONTEND="noninteractive" apt -y install tzdata

# 设置时区
RUN TZ=Asia/Shanghai && \
    ln -snf /usr/share/zoneinfo/$TZ /etc/localtime

# python相关
RUN apt install -y python python-pip
RUN apt install -y python3 python3-pip

# pip源
RUN mkdir -p /root/.pip/
COPY ./conf/pip.conf /root/.pip/pip.conf
COPY ./conf/pydistutils.cfg /root/.pydistutils.cfg

# SSH
RUN apt install -y openssh-server

# 添加用户/密码
RUN useradd --create-home --no-log-init --shell /bin/bash ${user} \
    && usermod -aG sudo ${user} \
    && echo "${user}:${user}" | chpasswd

# 清理缓存
RUN apt clean
RUN rm -rf /var/lib/apt/lists/*
RUN mkdir /var/lib/apt/lists/partial

# 自启动ssh
COPY ./start_ssh.sh /root/start_ssh.sh
RUN chmod +x /root/start_ssh.sh
RUN printf "\n# startup run\n" >> /root/.bashrc
RUN printf "if [ -f /root/start_ssh.sh ]; then\n" >> /root/.bashrc
RUN printf "    ./root/start_ssh.sh\n" >> /root/.bashrc
RUN printf "fi\n" >> /root/.bashrc

# 结束
RUN cat /etc/issue
RUN python -V
RUN python3 -V

# 暴露端口
EXPOSE 22 
