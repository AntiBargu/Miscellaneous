#### 环境

腾讯云lighthouse入门版。

```shell
运算组件：2核CPU、2GB内存 (入门型Linux-2核2G-40G-0.5T)
系统盘：40GB SSD云硬盘 (入门型Linux-2核2G-40G-0.5T)
流量包：0.5TB 月流量包 (入门型Linux-2核2G-40G-0.5T)
地域：东京
镜像：OpenCloudOS 8.6
```

#### 配置

开箱配置，仅仅安装了docker（OpenCloudOS/CentOS 目前默认的容器管理工具是podman，从使用上两者差不多）。



#### 问题描述

无法拉取mirrors.tencent.com的容器镜像

##### 问题命令

```shell
docker pull mirrors.tencent.com/tlinux/tlinux3.2:latest
```

##### 错误信息

```shell
Emulate Docker CLI using podman. Create /etc/containers/nodocker to quiet msg.
Trying to pull mirrors.tencent.com/tlinux/tlinux3.2:latest...
Error: initializing source docker://mirrors.tencent.com/tlinux/tlinux3.2:latest: pinging container registry mirrors.tencent.com: invalid status code from registry 404 (Not Found)
```

##### 显示debug级日志

```shell
docker --log-level=debug pull mirrors.tencent.com/tlinux/tlinux3.2:latest
```

##### debug级日志描述如下

```shell
INFO[0000] /usr/bin/podman filtering at log level debug
DEBU[0000] Called pull.PersistentPreRunE(/usr/bin/podman --log-level=debug pull mirrors.tencent.com/tlinux/tlinux3.2:latest)
DEBU[0000] Merged system config "/usr/share/containers/containers.conf"
DEBU[0000] Using conmon: "/usr/bin/conmon"
DEBU[0000] Initializing boltdb state at /var/lib/containers/storage/libpod/bolt_state.db
DEBU[0000] Using graph driver overlay
DEBU[0000] Using graph root /var/lib/containers/storage
DEBU[0000] Using run root /run/containers/storage
DEBU[0000] Using static dir /var/lib/containers/storage/libpod
DEBU[0000] Using tmp dir /run/libpod
DEBU[0000] Using volume path /var/lib/containers/storage/volumes
DEBU[0000] Set libpod namespace to ""
DEBU[0000] [graphdriver] trying provided driver "overlay"
DEBU[0000] Cached value indicated that overlay is supported
DEBU[0000] Cached value indicated that overlay is supported
DEBU[0000] Cached value indicated that metacopy is being used
DEBU[0000] Cached value indicated that native-diff is not being used
INFO[0000] Not using native diff for overlay, this may cause degraded performance for building images: kernel has CONFIG_OVERLAY_FS_REDIRECT_DIR enabled
DEBU[0000] backingFs=extfs, projectQuotaSupported=false, useNativeDiff=false, usingMetacopy=true
DEBU[0000] Initializing event backend file
DEBU[0000] Configured OCI runtime crun initialization failed: no valid executable found for OCI runtime crun: invalid argument
DEBU[0000] Configured OCI runtime runj initialization failed: no valid executable found for OCI runtime runj: invalid argument
DEBU[0000] Configured OCI runtime kata initialization failed: no valid executable found for OCI runtime kata: invalid argument
DEBU[0000] Configured OCI runtime runsc initialization failed: no valid executable found for OCI runtime runsc: invalid argument
DEBU[0000] Configured OCI runtime krun initialization failed: no valid executable found for OCI runtime krun: invalid argument
DEBU[0000] Using OCI runtime "/usr/bin/runc"
INFO[0000] Setting parallel job count to 7
DEBU[0000] Pulling image mirrors.tencent.com/tlinux/tlinux3.2:latest (policy: always)
DEBU[0000] Looking up image "mirrors.tencent.com/tlinux/tlinux3.2:latest" in local containers storage
DEBU[0000] Normalized platform linux/amd64 to {amd64 linux  [] }
DEBU[0000] Trying "mirrors.tencent.com/tlinux/tlinux3.2:latest" ...
DEBU[0000] Trying "mirrors.tencent.com/tlinux/tlinux3.2:latest" ...
DEBU[0000] Trying "mirrors.tencent.com/tlinux/tlinux3.2:latest" ...
DEBU[0000] Loading registries configuration "/etc/containers/registries.conf"
DEBU[0000] Loading registries configuration "/etc/containers/registries.conf.d/000-shortnames.conf"
DEBU[0000] Loading registries configuration "/etc/containers/registries.conf.d/001-rhel-shortnames.conf"
DEBU[0000] Loading registries configuration "/etc/containers/registries.conf.d/002-rhel-shortnames-overrides.conf"
DEBU[0000] Normalized platform linux/amd64 to {amd64 linux  [] }
DEBU[0000] Attempting to pull candidate mirrors.tencent.com/tlinux/tlinux3.2:latest for mirrors.tencent.com/tlinux/tlinux3.2:latest
DEBU[0000] parsed reference into "[overlay@/var/lib/containers/storage+/run/containers/storage:overlay.mountopt=nodev,metacopy=on]mirrors.tencent.com/tlinux/tlinux3.2:latest"
Trying to pull mirrors.tencent.com/tlinux/tlinux3.2:latest...
DEBU[0000] Copying source image //mirrors.tencent.com/tlinux/tlinux3.2:latest to destination image [overlay@/var/lib/containers/storage+/run/containers/storage:overlay.mountopt=nodev,metacopy=on]mirrors.tencent.com/tlinux/tlinux3.2:latest
DEBU[0000] Using registries.d directory /etc/containers/registries.d
DEBU[0000] Trying to access "mirrors.tencent.com/tlinux/tlinux3.2:latest"
DEBU[0000] No credentials matching mirrors.tencent.com/tlinux/tlinux3.2 found in /run/user/0/containers/auth.json
DEBU[0000] No credentials matching mirrors.tencent.com/tlinux/tlinux3.2 found in /root/.config/containers/auth.json
DEBU[0000] No credentials matching mirrors.tencent.com/tlinux/tlinux3.2 found in /root/.docker/config.json
DEBU[0000] No credentials matching mirrors.tencent.com/tlinux/tlinux3.2 found in /root/.dockercfg
DEBU[0000] No credentials for mirrors.tencent.com/tlinux/tlinux3.2 found
DEBU[0000]  No signature storage configuration found for mirrors.tencent.com/tlinux/tlinux3.2:latest, using built-in default file:///var/lib/containers/sigstore
DEBU[0000] Looking for TLS certificates and private keys in /etc/docker/certs.d/mirrors.tencent.com
DEBU[0000] GET https://mirrors.tencent.com/v2/
DEBU[0000] Ping https://mirrors.tencent.com/v2/ status 404
DEBU[0000] GET https://mirrors.tencent.com/v1/_ping
DEBU[0001] Ping https://mirrors.tencent.com/v1/_ping status 404
DEBU[0001] Accessing "mirrors.tencent.com/tlinux/tlinux3.2:latest" failed: pinging container registry mirrors.tencent.com: invalid status code from registry 404 (Not Found)
DEBU[0001] Error pulling candidate mirrors.tencent.com/tlinux/tlinux3.2:latest: initializing source docker://mirrors.tencent.com/tlinux/tlinux3.2:latest: pinging container registry mirrors.tencent.com: invalid status code from registry 404 (Not Found)
Error: initializing source docker://mirrors.tencent.com/tlinux/tlinux3.2:latest: pinging container registry mirrors.tencent.com: invalid status code from registry 404 (Not Found)
```

##### 关键日志（个人认为）

```shell
DEBU[0000] Using registries.d directory /etc/containers/registries.d
DEBU[0000] Trying to access "mirrors.tencent.com/tlinux/tlinux3.2:latest"
DEBU[0000] No credentials matching mirrors.tencent.com/tlinux/tlinux3.2 found in /run/user/0/containers/auth.json
DEBU[0000] No credentials matching mirrors.tencent.com/tlinux/tlinux3.2 found in /root/.config/containers/auth.json
DEBU[0000] No credentials matching mirrors.tencent.com/tlinux/tlinux3.2 found in /root/.docker/config.json
DEBU[0000] No credentials matching mirrors.tencent.com/tlinux/tlinux3.2 found in /root/.dockercfg
DEBU[0000] No credentials for mirrors.tencent.com/tlinux/tlinux3.2 found
DEBU[0000]  No signature storage configuration found for mirrors.tencent.com/tlinux/tlinux3.2:latest, using built-in default file:///var/lib/containers/sigstore
DEBU[0000] Looking for TLS certificates and private keys in /etc/docker/certs.d/mirrors.tencent.com
```

##### 个人分析

本地的docker客户端缺少mirrors.tencent.com的证书，从而无法建立安全的TLS连接导致镜像拉取失败。



#### 解决问题的尝试

##### 1. 排除个别镜像拉取失败的情况

在github上搜索”FROM mirrors.tencent.com language:Dockerfile“，搜索到其他以mirrors.tencent.com的镜像为base image的dockerfile，如下：

###### case 1

```dockerfile
FROM mirrors.tencent.com/rpf_detectronv2/rpf_detectronv2_oym:version1.0
RUN pip3 install shapely,Levenshtein
RUN python3 -m pip install 'git+https://github.com/facebookresearch/detectron2.git'
RUN python3 -m pip install 'git+https://github.com/Megvii-BaseDetection/cvpods.git'
```

镜像拉取失败且错误信息与tlinux的case一致

```shell
docker --log-level=debug pull mirrors.tencent.com/rpf_detectronv2/rpf_detectronv2_oym:version1.0
```

###### case 2

```dockerfile
FROM mirrors.tencent.com/ruitaoyuan/mongo-shell:0.0.1
LABEL maintainer="blueking"
COPY ./ /data/workspace/
RUN chmod +x /data/workspace/init-mongodb.sh
```

镜像拉取失败且错误信息与tlinux的case一致

```shell
docker --log-level=debug pull mirrors.tencent.com/ruitaoyuan/mongo-shell:0.0.1
```

###### case 3

```dockerfile
FROM mirrors.tencent.com/sccmsp/golang:1.16
MAINTAINER tencent
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo "Asia/Shanghai" > /etc/timezone
ADD privservice /
RUN mkdir /conf
```

镜像拉取失败且错误信息与tlinux的case一致

```shell
docker --log-level=debug pull mirrors.tencent.com/sccmsp/golang:1.16
```



##### 2. 排除拉取方式不正确的情况

docker/podman pull的使用规则还是很简单的

```shell
docker/podman pull $REPOSITORY $TAG
```

在github上搜索引用非官方镜像的dockerfile，并执行拉取。

微软镜像市场主页：https://mcr.microsoft.com/en-us/

```shell
# 拉取微软的ruby镜像
docker pull mcr.microsoft.com/devcontainers/ruby:3

# 拉取阿里云的镜像
docker pull registry.cn-hongkong.aliyuncs.com/graphscope/manylinux2014:2021-10-14-14ac00e-arm64
```



##### 3. 排除源配置问题

https://mirrors.tencent.com/的文档中描述了在云服务器上使用腾讯云Docker软件源的规则，由于当前环境使用podman容器管理工具，故在配置文件/etc/containers/registries.conf中做出如下修改，其中insecure是HTTPS的配置项，当insecure为true时，允许使用不安全的HTTP协议以及TLS连接。

```shell
[[registry]]
perfix = "mirrors.tencent.com/*"
location = "mirror.ccs.tencentyun.com"
insecure = true
#insecure = false
```



#### 另类的解决方案

##### 方法

使用wget下载打包的镜像，利用docker load子命令解压下载的镜像

###### case 1

```shell
# 在mirrors.tencent.com镜像站找到的tlinux镜像
wget https://mirrors.cloud.tencent.com/tlinux/3.1/images/x86_64/tlinux-64bit-v3.1.20200928.tar

# 看命名...没想到可以正常load....
docker load < tlinux-64bit-v3.1.20200928.tar

# 镜像存在
docker images

# 测试是否可用，可用...
docker run -it localhost/tlinux-64bit-v3.1.20200928.sqfs bash
```

进入容器后，查看操作系统版本：

```shell
[root@bce64ca94309 /]# cat /etc/os-release
NAME="TencentOS Linux"
VERSION="3.1 (Final)"
ID="tencentos"
ID_LIKE="rhel fedora centos"
VERSION_ID="3.1"
PLATFORM_ID="platform:el8.2"
PRETTY_NAME="TencentOS Linux 3.1 (Final)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:tencentos:tencentos:3"
HOME_URL="https://tlinux.qq.com/"
BUG_REPORT_URL="https://tlinux.qq.com/"

CENTOS_MANTISBT_PROJECT="CentOS-8"
CENTOS_MANTISBT_PROJECT_VERSION="8"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="8"
```

###### case 2

```shell
wget https://mirrors.opencloudos.tech/opencloudos/9.0/images/x86_64/opencloudos-9.0-minimal-x86_64.tar

docker load < opencloudos-9.0-minimal-x86_64.tar

docker run -it localhost/opencloudos/opencloudos:9.0 bash
```

进入容器后，查看操作系统版本：

```shell
bash-5.1# cat /etc/os-release
NAME="OpenCloudOS"
VERSION="9.0"
ID="opencloudos"
ID_LIKE="opencloudos"
VERSION_ID="9.0"
PLATFORM_ID="platform:oc9.0"
PRETTY_NAME="OpenCloudOS 9.0"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:opencloudos:opencloudos:9.0"
HOME_URL="https://www.opencloudos.org/"
BUG_REPORT_URL="https://bugs.opencloudos.tech/"
bash-5.1#
```

##### 缺点

在使用dockerfile制作镜像时，没有办法通过FROM命令引用这些基础镜像。当然，也可以先push到dockerhub上，再FROM（涉及安全风险）。



#### 问题汇总

##### 1. 无法拉取mirrors.tencent.com的容器镜像？是否是证书问题？如果是，那么如何安装？

##### 2. tencent是否有类似dockerhub和微软一样的镜像市场？如果有，在哪里看？如果没有，有没有镜像仓库内的镜像列表，如何获取？



#### 回答

```shell
OpenCloud OS和TLinux 在dockerhub上已经发布。
mirrors.tencent.com/*是公司内部的镜像仓库，暂不对外开放权限。
```

[OpenCloud OS](https://hub.docker.com/r/opencloudos/opencloudos)

[TencentOS Server 3.1](https://hub.docker.com/r/tencentos/tencentos_server31)
