# 使用docker-compose部署Aria2

## 准备环境

* Docker
* Docker-compose
* Ubuntu 18.04

**安装Docker**

```
# Ubuntu
$ curl -fsSL http://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
$ add-apt-repository "deb [arch=amd64] http://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
$ apt install docker-ce -y
$ systemctl enable docker
$ systemctl start docker
```

**安装Docker-compose**

```
$ sudo curl -L "https://wood-bucket.oss-cn-beijing.aliyuncs.com/Linux/Docker/docker-compose-Linux-x86_64-1.25.5" -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
```

---

## 项目说明
本项目通过docker-compose整合了三个容器，分别为`aria2-pro`,`ariang`,`nginx-autoindex`

**容器说明：**

Aria2-pro：下载模块

AriaNG：Web控制面板

Nginx：列出下载的文件

## 部署指南

**克隆项目**

```
$ git clone https://github.com/my6889/aria2
$ cd aria2
```

**修改docker-compose.yaml配置**

```
$ vim docker-compose.yaml
```

第12行：修改RPC_SECRET，也可保持默认，后面会用到

**启动项目**

```
docker-compose up -d 
```

**访问服务**

```
http://宿主机IP:6880    # AriaNG
http://宿主机IP:8888    # Nginx列出的目录
```

**设置AriaNG**
访问`http://宿主机IP:6880`，打开Web页面后
在`系统设置`-`AriaNg设置`-`RPC`中设置Aria2的地址

* 修改`Aria2 RPC地址`为宿主机IP，端口和后缀保持默认
* 修改`Aria2 RPC密钥`为docker-compose.yaml中RPC_SECRET的值

设置后刷新页面生效，如果没有什么问题，左侧栏中的`Aria2状态`会显示为绿色的`已连接`，然后就可以愉快的下载了！