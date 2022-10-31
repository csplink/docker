# docker
csplink中常用的DockerFile

## 构建命令

> 在相应目录下：

```shell
docker build -f ./Dockerfile -t test:tag .
```

## 运行命令

> 无挂载目录

```shell
docker run --name test -p 10000:22 -itd test:tag
```

> 挂载芯片

```shell
docker run --name test -p 10000:22 -v ~:/home/csplink -itd test:tag
```

## 进入终端

```shell
docker exec -it test /bin/bash
```

