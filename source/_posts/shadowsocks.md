---
title: Shadowsock 配置指南
---



### Centos 7

---

#### 1. 安装

```shell
curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
python get-pip.py
pip install --upgrade pip
pip install shadowsocks
```

#### 2. 配置

###### 编辑配置文件

```shell
vim /etc/shadowsocks.json
```

###### 配置文件内容

```json
{
    "server":"服务器IP地址",
    "server_port":8080,
    "local_port":1080,
    "password":"password",
    "timeout":60,
    "method":"aes-256-cfb"
}
```

###### 编辑自启动文件

``` /etc/systemd/system/shadowsocks.service ```

###### 自启动文件内容

``` shell
[Unit]
Description=Shadowsocks

[Service]
TimeoutStartSec=0
ExecStart=/usr/bin/ssserver -c /etc/shadowsocks.json

[Install]
WantedBy=multi-user.target
```

#### 3.  启动

```shell
systemctl enable shadowsocks
systemctl start shadowsocks
```

#### 4. 查看服务状态

```shell
systemctl status shadowsocks -l
```

#### 5. 配置防火墙

```shell
firewall-cmd --permanent --add-port=8080/tcp
firewall-cmd --reload
```





### Debian 9 (Stretch)

---

#### 1. 安装

``` shell
   sh -c 'printf "deb http://deb.debian.org/debian stretch-backports main" > /etc/apt/sources.list.d/stretch-backports.list'
   apt-get update
   apt -t stretch-backports install shadowsocks-libev -y
```

#### 2. 配置

###### 编辑配置文件

```shell
vim /etc/shadowsocks-libev/config.json
```

###### 配置文件内容

```json
{
    "server":"服务器IP地址",
    "server_port":8080,
    "local_port":1080,
    "password":"password",
    "timeout":60,
    "method":"aes-256-cfb"
}
```

#### 3. 启动

```shell
/etc/init.d/shadowsocks-libev start
```