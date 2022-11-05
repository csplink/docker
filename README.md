# docker
DockerFile commonly used in csplink

## Build

> in the corresponding directory:

```shell
docker build -f ./Dockerfile -t test:tag .
```
## Run

### no mounted directory

```shell
docker run --name test -p 10000:22 -itd test:tag
```
### mounted directory

```shell
docker run --name test -p 10000:22 -v ~:/home/csplink -itd test:tag
```
## Exec

```shell
docker exec -it test /bin/bash
```
### Mirror
> sometimes we need to switch to the mirror of the local service

#### huaweicloud

```shell
sed -i 's/archive.ubuntu.com/repo.huaweicloud.com/g' /etc/apt/sources.list; 
sed -i 's/security.ubuntu.com/repo.huaweicloud.com/g' /etc/apt/sources.list; 
```
#### aliyun

```shell
sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list; 
sed -i 's/security.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list; 
```
