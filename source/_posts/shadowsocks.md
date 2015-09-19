title: 使用shadowsocks科学上网
date: 2015-09-19 22:21:07
tags: [shadowsocks, linode, digitalocean]
categories: network
---

> 作为一名开发者，经常需要阅读使用一些国际资源。
> google, gmail, stackoverflow, github, youtube等等。
> 如果你不能访问这些，那基本上就算不上个专业的开发。
> 让我们走进世界的另一端~

## 服务器

> 首先，你需要一台可以访问以上站点的服务器，一般是国外的服务器。

### 选择

* 比较好的服务商是[linode](https://www.linode.com/?r=83525e8ca8c9ce567cb8605e8db95fe6412ad2ba)，虽然贵了点，但速度比[digitalocean](https://www.digitalocean.com/?refcode=f21825cb4d56)之流好上好几倍。

### 购买

* 你需要有信用卡

### 地区

* 新加坡
* 日本
* 一般这两个速度会比较快，可以尝试购买后ping一下对比，再把慢的删了，一般也计费不到0.1$

### 系统

* 本文以ubuntu为例

## [shadowsocks](http://shadowsocks.org)

### 服务端

#### 安装

```shell
apt-get update
apt-get install python-pip
pip install shadowsocks
```

#### 配置

> sss.json

```js
{
    "server":"0.0.0.0",
    "server_port": 1234,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password": "test",
    "timeout": 300,
    "method":"aes-256-cfb",
    "fast_open": false
}
```

#### 启动

```shell
ssserver -c ./sss.json --pid-file ./sss.pid --log-file ./sss.log -d start
```

### 客户端

#### 安装

[各端下载链接](http://shadowsocks.org/en/download/clients.html)

#### 配置

> 比较简单，直接根据服务端的启动配置进行填写

#### 测试

> 启动并打开google, facebook等进行验证是否配置成功
