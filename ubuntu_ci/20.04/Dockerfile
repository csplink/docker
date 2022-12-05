FROM ubuntu:20.04

ARG LOCATION

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
RUN apt install -y lbzip2 bzip2 unzip
RUN apt install -y git
RUN apt install -y xz-utils
RUN apt install -y bash-completion
RUN DEBIAN_FRONTEND="noninteractive" apt -y install tzdata

# set time zone
RUN TZ=Asia/Shanghai && \
    ln -snf /usr/share/zoneinfo/$TZ /etc/localtime

# python
# RUN apt install -y python python-pip
RUN apt install -y python3 python3-pip

# SSH
RUN apt install -y openssh-server

# add user/password
RUN useradd --create-home --no-log-init --shell /bin/bash ${user} \
    && usermod -aG sudo ${user} \
    && echo "${user}:${user}" | chpasswd

# oh-my-posh
RUN wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/posh-linux-amd64 -O /usr/local/bin/oh-my-posh
RUN chmod +x /usr/local/bin/oh-my-posh

USER ${user}
RUN mkdir ~/.poshthemes
RUN wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/themes.zip -O ~/.poshthemes/themes.zip
RUN unzip ~/.poshthemes/themes.zip -d ~/.poshthemes
RUN chmod u+rw ~/.poshthemes/*.omp.*
RUN rm ~/.poshthemes/themes.zip
RUN printf "eval \"\$(oh-my-posh --init --shell bash --config ~/.poshthemes/amro.omp.json)\"" >> ~/.bashrc
USER root

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
# RUN python -V
RUN python3 -V

# expose port
EXPOSE 22 
