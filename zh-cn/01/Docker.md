# 第三方 DockerHub 镜像服务

**注意:**

- 以下内容仅做镜像服务的整理与搜集，未做任何安全性检测和验证。
- 使用前请自行斟酌，并根据实际需求进行必要的安全审查。
- 本列表中的任何服务都不做任何形式的安全承诺或保证。

| DockerHub 镜像仓库                                           | 镜像加地址                        |
| ------------------------------------------------------------ | --------------------------------- |
| [bestcfipas镜像服务](https://t.me/bestcfipas/1900)           | `https://docker.registry.cyou`    |
|                                                              | `https://docker-cf.registry.cyou` |
| [zero_free镜像服务](https://t.me/zero_free/80)               | `https://docker.jsdelivr.fyi`     |
|                                                              | `https://dockercf.jsdelivr.fyi`   |
|                                                              | `https://dockertest.jsdelivr.fyi` |
| [docker proxy](https://dockerpull.com/)                      | `https://dockerpull.com`          |
| [docker proxy](https://dockerproxy.cn/)                      | `https://dockerproxy.cn`          |
| [Docker镜像加速站](https://hub.uuuadc.top/)                  | `https://hub.uuuadc.top`          |
|                                                              | `https://docker.1panel.live`      |
|                                                              | `https://hub.rat.dev`             |
| [DockerHub 镜像加速代理](https://docker.anyhub.us.kg/)       | `https://docker.anyhub.us.kg`     |
|                                                              | `https://docker.chenby.cn`        |
|                                                              | `https://dockerhub.jobcher.com`   |
| [镜像使用说明](https://dockerhub.icu/)                       | `https://dockerhub.icu`           |
| [Docker镜像加速站](https://docker.ckyl.me/)                  | `https://docker.ckyl.me`          |
| [镜像使用说明](https://docker.awsl9527.cn/)                  | `https://docker.awsl9527.cn`      |
| [镜像使用说明](https://docker.hpcloud.cloud/)                | `https://docker.hpcloud.cloud`    |
| [DaoCloud 镜像站](https://github.com/DaoCloud/public-image-mirror) | `https://docker.m.daocloud.io`    |
| [AtomHub 可信镜像仓库平台](https://atomhub.openatom.cn/) (只包含基础镜像，共336个) | `https://atomhub.openatom.cn`     |

------

<iframe width="560" height="315" src="https://www.youtube.com/embed/l2jwq9CagNQ?si=ZCklhAtR-NfN2Aeb" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen="" style="box-sizing: border-box; top: 0px; left: 0px; margin: 0px 0px 20px; width: 970px; height: 545.625px; border-radius: 12px;"></iframe>

# [CF-Workers-docker.io：Docker仓库镜像代理工具](https://github.com/cmliu/CF-Workers-docker.io)

https://github.com/cmliu/CF-Workers-docker.io

本项目是一个基于 Cloudflare Workers 的 Docker 镜像代理工具，旨在中转对 Docker 官方镜像仓库的请求，解决访问限制并加速访问。

## 为什么需要这个工具？

[![神秘原因](https://img.090227.xyz/file/dcdbd209203846c6b8fdf.png)](https://img.090227.xyz/file/dcdbd209203846c6b8fdf.png)
由于**神秘原因**，国内用户逐渐无法访问Docker Hub仓库。这对于开发者来说是个不小的难题。

而我的解决方案是通过**赛博菩萨**中转请求，解决访问限制并加速访问。

注意：**不推荐使用该项目搭建公共服务**。使用你自己的域名搭建公共服务有可能会遭受**污染和反诈**，推荐小规模自用即可。

------

## 部署方式

访问[CF-Workers-docker.io：Docker仓库镜像代理工具](https://github.com/cmliu/CF-Workers-docker.io)项目页面

- **Workers** 部署：复制 [_worker.js](https://github.com/cmliu/CF-Workers-docker.io/blob/main/_worker.js) 代码，`保存并部署`即可
- **Pages** 部署：`Fork` 后 `连接GitHub` 一键部署即可

------

## 如何使用？

例如您的Workers项目域名为：`docker.fxxk.dedyn.io`；

### 1.官方镜像路径前面加域名

```
SHELL
docker pull docker.fxxk.dedyn.io/stilleshan/frpc:latest
SHELL
docker pull docker.fxxk.dedyn.io/library/nginx:stable-alpine3.19-perl
```

### 2.一键设置镜像加速

修改文件 `/etc/docker/daemon.json`（如果不存在则创建）

```
SHELL
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://docker.fxxk.dedyn.io"]  # 请替换为您自己的Worker自定义域名
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

------

## 变量说明

| 变量名 | 示例                   | 必填 | 备注                                       |
| ------ | ---------------------- | ---- | ------------------------------------------ |
| URL302 | https://t.me/CMLiussss | ❌    | 主页302跳转                                |
| URL    | https://www.baidu.com/ | ❌    | 主页伪装(设为`nginx`则伪装为nginx默认页面) |



## [GitHub项目地址](https://github.com/cmliu/CF-Workers-docker.io)

