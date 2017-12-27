---
title: cenots7下修改Docker的默认镜像存储位置
menu:
  side:
    parent: linux
    weight: 3
---

## cenots7下修改Docker的默认镜像存储位置


### 方式一

修改配置`/usr/lib/systemd/system/docker.service`

使用 --graph参数指定存储位置

```bash
ExecStart=/usr/bin/dockerd --graph=/data/docker/data
```

### 方式二

目前不存在则创建目录

```bash
mkdir -p /etc/systemd/system/docker.service.d
```

修改配置 `/etc/systemd/system/docker.service.d/docker.conf`

```bash
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd --graph=/data/docker/data
```

重启docker

```bash
systemctl daemon-reload
systemctl restart docker
```

查看docker信息`docker info`


```bash
Containers: 0
 Running: 0
 Paused: 0
 Stopped: 0
Images: 0
Server Version: 17.03.2-ce
Storage Driver: overlay
 Backing Filesystem: xfs
 Supports d_type: true
Logging Driver: json-file
Cgroup Driver: cgroupfs
Plugins:
 Volume: local
 Network: bridge host macvlan null overlay
Swarm: inactive
Runtimes: runc
Default Runtime: runc
Init Binary: docker-init
containerd version: 4ab9917febca54791c5f071a9d1f404867857fcc
runc version: 54296cf40ad8143b62dbcaa1d90e520a2136ddfe
init version: 949e6fa
Security Options:
 seccomp
  Profile: default
Kernel Version: 3.10.0-693.el7.x86_64
Operating System: CentOS Linux 7 (Core)
OSType: linux
Architecture: x86_64
CPUs: 1
Total Memory: 3.702 GiB
Name: centos7
ID: OGCE:NPGO:YXTT:WQJ6:FOGI:N5TG:I6G3:ZZVU:FRVV:SWUI:ASSQ:QCAA
Docker Root Dir: /home/dockerdata
Debug Mode (client): false
Debug Mode (server): false
Registry: https://index.docker.io/v1/
Experimental: false
Insecure Registries:
 127.0.0.0/8
```
