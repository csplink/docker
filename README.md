<div align="center">
    <a href="https://csplink.top">
        <img width="160" heigth="160" src="https://raw.githubusercontent.com/csplink/csp/master/Apps/CSP.Apps.Dev/Resources/Images/logo.svg" alt="logo" />
    </a>
    <h1>DOCKER</h1>
    <div>
        <a href="https://github.com/csplink/docker/actions?query=workflow%F0%9F%93%9D%20context">
            <img src="https://img.shields.io/github/actions/workflow/status/csplink/docker/context.yml?style=flat&label=context" alt="github-ci" />
        </a>
        <a href="https://github.com/csplink/docker/actions?query=workflow%3A%F0%9F%92%95mirror">
            <img src="https://img.shields.io/github/actions/workflow/status/csplink/docker/mirror.yml?style=flat&label=mirror" alt="github-ci" />
        </a>
        <a href="https://github.com/csplink/docker/actions?query=workflow%3A%F0%9F%91%B7geehy-apm32f103">
            <img src="https://img.shields.io/github/actions/workflow/status/csplink/docker/geehy-apm32f103.yml?style=flat&label=geek:apm32f103" alt="github-ci" />
        </a>
        <a href="https://github.com/csplink/docker/actions?query=workflow%3A%F0%9F%91%B7rt_thread-rt_smart">
            <img src="https://img.shields.io/github/actions/workflow/status/csplink/docker/rt_thread-rt_smart.yml?style=flat&label=rt_thread:rt_smart" alt="github-ci" />
        </a>
        <a href="https://github.com/csplink/docker/actions?query=workflow%3A%F0%9F%91%B7ubuntu_ci-16.04">
            <img src="https://img.shields.io/github/actions/workflow/status/csplink/docker/ubuntu_ci-16.04.yml?style=flat&label=ubuntu_ci:16.04" alt="github-ci" />
        </a>
        <a href="https://github.com/csplink/docker/actions?query=workflow%3A%F0%9F%91%B7ubuntu_ci-18.04">
            <img src="https://img.shields.io/github/actions/workflow/status/csplink/docker/ubuntu_ci-18.04.yml?style=flat&label=ubuntu_ci:18.04" alt="github-ci" />
        </a>
        <a href="https://github.com/csplink/docker/actions?query=workflow%3A%F0%9F%91%B7ubuntu_ci-20.04">
            <img src="https://img.shields.io/github/actions/workflow/status/csplink/docker/ubuntu_ci-20.04.yml?style=flat&label=ubuntu_ci:20.04" alt="github-ci" />
        </a>
        <a href="https://github.com/csplink/docker/actions?query=workflow%3A%F0%9F%91%B7ubuntu_ci-22.04">
            <img src="https://img.shields.io/github/actions/workflow/status/csplink/docker/ubuntu_ci-22.04.yml?style=flat&label=ubuntu_ci:22.04" alt="github-ci" />
        </a>
    </div>
    <div>
        <a href="https://github.com/csplink/docker/pulls">
            <img src="https://img.shields.io/github/issues-pr/csplink/docker.svg" alt="pulls" />
        </a>
        <a href="https://github.com/csplink/docker/issues">
            <img src="https://img.shields.io/github/issues/csplink/docker.svg" alt="pulls" />
        </a>
    </div>
    <div>
        <a href="https://github.com/csplink/docker/blob/master/LICENSE">
            <img src="https://img.shields.io/github/license/csplink/docker.svg?colorB=f48041&style=flat" alt="license" />
        </a>
        <a href="https://csplink.top">
            <img src="https://img.shields.io/badge/wiki-document-blue?style=flat" alt="document" />
        </a>
        <a href="https://gitter.im/csplink/community">
            <img src="https://badges.gitter.im/csplink/csp.svg" alt="gitter" />
        </a>
        <a href="https://jq.qq.com/?_wv=1027&k=CWt7TZln">
            <img src="https://img.shields.io/badge/chat-on%20QQ-ff69b4.svg?style=flat" alt="qq" />
        </a>
        <a href="https://space.bilibili.com/24969427/">
            <img src="https://img.shields.io/badge/video-bilibili-FB7299?style=flat" alt="bilibili" />
        </a>
    </div>
    <b>CSP: Tools for flexible configuration of chips and boards.</b><br/>
    <i>DockerFile commonly used in csplink</i><br/>
</div>

**English** | [中文](README-zh_CN.md)

## ✨ Features

- 👷 CI builds automatically
- ☁️ Sync to DockerHub

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
