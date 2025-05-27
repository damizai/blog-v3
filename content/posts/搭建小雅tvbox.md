---
title: 安装小雅Alist - TVbox
description: 如果你想要快速搭建一个可用于阿里云盘等云存储资源管理的工具，并希望在自己的 VPS 上部署一个高效、稳定的服务，那么 小雅 Alist是一个不错的选择。通过 Docker 环境，我们可以轻松部署 小雅 Alist，并结合多种功能，使其成为强大的资源管理工具。    
date: 2024-07-11 20:49:52
updated: 2024-10-08 00:00:00
image: https://serv.200038.xyz/2024/09/19/578021.webp
categories: [经验分享]
tags: [代码, 小雅Alist, TVbox, VPS]
# tags:
_path: /posts/21c2

recommend: 2
---


- **小雅项目地址**             https://github.com/monlor/docker-xiaoya
- **小雅全家桶项目地址**       https://github.com/DDS-Derek/xiaoya-alist   
- **X-UI项目地址**             https://github.com/FranzKafkaYu/x-ui
- **3X-UI项目地址**            https://github.com/MHSanaei/3x-ui
- **勇哥X-UI项目地址**         https://github.com/yonggekkk/x-ui-yg
- **Alpine系统X-UI项目地址**   https://github.com/Lynn-Becky/Alpine-x-ui
---
## 要准备的资源如下：

###  VPS

推荐使用甲骨文云服务器，或者以下备用选项：
- **10.99美元/年 VPS**
  - 1核1G/15G SSD硬盘
  - [网址链接](https://my.racknerd.com/aff.php?aff=11188&pid=838)
  
- **16.88美元/年 VPS (洛杉矶DC-02)**
  - 1核1.5G/25G SSD硬盘
  - [网址链接](https://my.racknerd.com/aff.php?aff=11188&pid=839)

- **23.88美元/年 VPS (洛杉矶DC-02)**
  - 2核2.5G/38G SSD硬盘
  - [网址链接](https://my.racknerd.com/aff.php?aff=11188&pid=840)

- **Haxipv6免费鸡 缺点就是五天续费**
  - [网址链接](https://hax.co.id/)

###  域名

- **顶级数字域名，可以使用支付宝付款**
  - [网址链接](https://www.namesilo.com/)


- **顶级数字域名，价格约为0.67美元/年.需要信用卡贝宝支付**
  - [网址链接](https://www.spaceship.com/)

###  软件工具

- **XSHELL/XFTP**
  - 免费正版: [下载链接](https://www.xshell.com/zh/free-for-home-school/)

- **FINSHELL**
  - 免费正版: [下载链接](https://www.hostbuf.com/t/988.html)

- **WindTermL**
  - 免费正版: [下载链接](https://windterm.org/)
 
### 登入SSH面板安装docker

``` SHELL
apt update && apt install docker.io -y
curl -fsSL https://get.docker.com | sh
```
### 安装casaos

``` SHELL
wget -qO- https://get.casaos.io | bash
```

### docker常用命令

``` SHELL
systemctl status docker #验证docker是否安装成功
docker version #查看版本
docker restart xiaoya-tvbox #重启xiaoya容器
docker stop xiaoya #停止指定容器
docker ps #列出所有容器
docker rm #容器ID 删除指定容器
docker images #查看所有镜像
docker rmi #镜像ID 删除指定镜像
```

### 在VPS上部署小雅Alist

---
##  1. 获取token等三个链接

###  mytoken.txt的token获取链接（二选一）

  - [网址链接](https://aliyuntoken.vercel.app/)
  - [网址链接](https://alist.nn.ci/zh/guide/drivers/aliyundrive.html/)

###   myopentoken.txt的token获取链接

  - [网址链接](https://alist.nn.ci/zh/guide/drivers/aliyundrive_open.html)

##  2. temp_transfer_folder_id.txt的阿里云盘转存目录ID获取链接

 -  实测在阿里云资源盘的资源库里新建一个文件夹复制浏览器的URL最后一个/后面的一串代码就行了，比如
 -  https://www.aliyundrive.com/drive/file/resource/640xxxxxxxxxxxxxxxxxxxca8a 最后一串就是- - - -            640xxxxxxxxxxxxxxxxxxxca8a，记得这个目录不要删，里面的内容可以定期删除

##  3. 最新版小雅alist安装脚本

 -  用SSH工具登陆到你要安装小雅alist的主机终端，复制下面两行代码之中的一个，到命令行粘贴执行即可，必须提前部署好docker运行环境。

###  安装脚本1——bridge网络模式

``` bash
bash -c "$(curl http://docker.xiaoya.pro/update_new.sh)“
```

###  安装脚本2——host网络模式（小雅官网推荐）

``` bash
bash -c "$(curl http://docker.xiaoya.pro/update_new.sh)" -s host
```

###  小雅全家桶安装脚本

``` bash
bash -c "$(curl --insecure -fsSL https://ddsrem.com/xiaoya_install.sh)"
```

###  4. 定时清理阿里云盘转存目录的脚本

``` bash
bash -c "$(curl -s https://xiaoyahelper.zngle.cf/aliyun_clear.sh | tail -n +2)" -s 3 -tg
bash -c "$(curl -s https://xiaoyahelper.zngle.cf/aliyun_clear.sh | tail -n +2)" -s 5 -tg
```
注：上面这个命令后缀-tg可以删除，这个是电报机器人接收通知，-3是定时和更新，-5是实时清理。

###  5. 登录小雅Alist

 -  浏览器输入登录地址比如IPV4：http://74.58.158.23:5678
 -  浏览器输入登录地址比如IPV6：http://[2a01:4f8:211:2312:1234:4321:1711:1]:5678               

###  6. 用域名解析网址登录小雅Alist

 -  先去cloudflare 添加DNS解析记录 然后再用域名和端口号登录比如：http://xiaoya.xxx.com:5678
 -  Cloudflare  - [网址链接](https://dash.cloudflare.com/)         

###  7. 完善安全设置，添加强制的登录和密码

 -  用记事本分别建立两个文件，guestlogin.txt (空文件即可)和 guestpass.txt（里面写您自定的登录密码）,

###  8. 登录账号自己设置

 -  登录账号名：dav
 -  密码：自己设置
 -  设置强制登入，和自定义密码
 -  把密码保存到 /etc/xiaoya/guestpass.txt （不过不要设置稀奇古怪的符号，例如；&#“~@（）*$ 之类的）
 -  如果你的xiaoya放在公网，为了防止别人蹭网，可以设置强制登入，新增 /etc/xiaoya/guestlogin.txt 这个文件，重启即
 -  可，文件有没有内容无所谓，如果取消强制登入就删除这个文件。强制登入的账号为 dav，密码使用
 -  /etc/xiaoya/guestpass.txt 里设置的，同时webdav连接使用 dav 这个用户
 -  上述2个功能设置好后需要重启docker才会生效。
 -  docker restart xiaoya


### 9. 最后你就可以愉快的观看小雅Alist啦啦啦。