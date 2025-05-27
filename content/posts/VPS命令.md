---
title: VPS命令及Hexo的基本命令
description: 这篇文章提供了多种命令与脚本的集合，主要面向VPS用户、Linux用户和Hexo博客管理者，帮助他们在不同环境下进行系统维护、工具安装以及配置管理。
date: 2024-07-06 21:55:31
updated: 2024-11-28 00:00:00
image: https://biu.biuxin.com/2025/05/04/903004.webp
categories: [经验分享]
tags: [代码, VPS工具箱]
recommend: 100
---

>小姐姐视频
<details>
<summary><code><strong>小姐姐视频</strong></code></summary>
<iframe width="100%" height="600" src="https://api.kuleu.com/api/MP4_xiaojiejie?type" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"></iframe>
</details>

>自用影视站观看
<details>
<summary><code><strong>自用影视站观看</strong></code></summary>
<iframe width="100%" height="630" src="https://video.biuxin.com/" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"></iframe>
</details>

>哔哩哔哩观看
<details>
<summary><code><strong>哔哩哔哩观看</strong></code></summary>
<iframe width="100%" height="800" src="//www.bilibili.com/bangumi/play/ss47836?from_spmid=666.4.hotlist.1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"></iframe>
</details>

### Windows电脑卸载`CFTunnels`命令

``` shell
cloudflared service uninstall
```

### debian/Ubuntu 基础组件

``` shell
apt update -y  && apt install -y curl
```

### CentOS 基础组件

``` shell
yum update && yum install -y curl
```

### Alpine Linux 基础组件

``` shell
apk update && apk add curl
```

### VPS 更新命令

``` shell
apt update && apt upgrade -y
```

### 安装必要环境

``` shell
apt update -y && apt install -y curl socat wget sudo
```

### 如果你是V6鸡,需要先装一个Warp

``` shell
wget -N https://gitlab.com/fscarmen/warp/-/raw/main/menu.sh && bash menu.sh [option] [lisence/url/token]
```

### 科技loon工具箱脚本

``` shellL
bash <(curl -sL kejilion.sh)
```

``` shell
curl -sS -O https://kejilion.pro/kejilion.sh && chmod +x kejilion.sh && ./kejilion.sh
```

### GitHub版 部分小伙伴会遇到官网版出现大段乱码！就用GitHub版本吧！

``` shell
curl -sS -O https://raw.githubusercontent.com/kejilion/sh/main/kejilion.sh && chmod +x kejilion.sh && ./kejilion.sh
```

### 国内服务器版

``` shell
curl -sS -O https://raw.gitmirror.com/kejilion/sh/main/cn/kejilion.sh && chmod +x kejilion.sh && ./kejilion.sh
```

### Mr.Wnang工具箱脚本

``` shell
curl -fsSL https://raw.githubusercontent.com/eooce/ssh_tool/main/ssh_tool.sh -o ssh_tool.sh && chmod +x ssh_tool.sh && ./ssh_tool.sh
```

##  在VPS上安装X-UI面板

### 原版X-UI 

``` shell
bash <(curl -Ls https://raw.githubusercontent.com/FranzKafkaYu/x-ui/master/install.sh)
```
### 勇哥魔改版 X-UI

``` shell
bash <(curl -Ls https://raw.githubusercontent.com/yonggekkk/x-ui-yg/main/install.sh)
```

### 3X-ui 

``` shell
bash <(curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh)
```

### VPS Alpine 系统安装哪吒命令  

``` shell
apk add curl 
apk add sudo
```

### VPS 检测流媒体 

``` shell
bash <(curl -Ls IP.Check.Place)
```

### VPS 出口IP

``` shell
curl ipinfo.io/ip
```

### Hexo 插件卸载命令

``` bash
npm uninstall 插件名
```
### Hexo 哔哩番剧更新命令

``` bash
hexo bangumi -u
```
### Hexo 友链更新命令

``` bash
node link.js
```