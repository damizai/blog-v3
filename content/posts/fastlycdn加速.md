---
title: 使用 FastyCDN 加速 Cloudflare + pages 部署的博客项目
description: 图文详解如何注册并配置 Fastly CDN 服务，绑定华为云 DNS 进行域名解析与 SSL 证书验证，全流程教学，适合初学者快速上手全球加速部署。
date: 2024-10-13 22:28:16
updated: 2024-10-15 00:00:00
image: https://serv.200038.xyz/2024/09/19/993800.webp
categories: [经验分享]
tags: [代码, FastlyCDN, Cloudflare]

recommend: 4
---

### 首先注册 Fastly 账号:

   - **[Fastly注册地址](https://www.fastly.com/signup?tier=free)**

::pic
---
src: https://serv.200038.xyz/2024/12/13/247550.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: Fastly注册地址
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

   - **[华为云国际版注册参考CM喂饭，杨幂的脚大佬](https://blog.cmliussss.com/p/BestWorkers/)**

### 注册好后点击左侧的 `CDN` 找到 右上角 `Cerate service` 点击 按照下图填写后，点击 ACtivate

::pic
---
src: https://serv.200038.xyz/2024/12/13/365969.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: Fastly注册地址
# zoom: false # 是否开启灯箱缩放，默认开启
---
::



### 修改CDN配置

#### 1. 激活配置后，我们需要对`CDN`配置进行一定修改，此处 `Fastly `的操作逻辑对个人用户比较不友好，无法直接修改，必须先将默认创建的配置`Clone一次`，然后创建配置文件 `2`，再进行修改。

::pic
---
src: https://serv.200038.xyz/2024/12/13/119465.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

#### 2. 改好后点击 `Origins` 下面的 `Hosts` 然后点击域名旁边端口的编辑更改配置，改好后点击 `Update`


::pic
---
src: https://serv.200038.xyz/2024/12/13/568835.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

::pic
---
src: https://serv.200038.xyz/2024/12/13/670055.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

::pic
---
src: https://serv.200038.xyz/2024/12/13/408242.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


#### 3. 配置完成会回到页面，点击`Activate`，激活 CDN 配置

::pic
---
src: https://serv.200038.xyz/2024/12/13/587131.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


::pic
---
src: https://serv.200038.xyz/2024/12/13/410656.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


### 配置SSL证书

#### 1. 首先切换到 `Secure`选项卡， `TLS management`下面的 `SubScriptins`，创建一个SSL证书订单。

::pic
---
src: https://serv.200038.xyz/2024/12/13/467371.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

#### 2. 创建好后直接点击 `Submit` 就可以了 


::pic
---
src: https://serv.200038.xyz/2024/12/13/644434.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


#### 3. `SSL证书` 需要 DNS 验证，将验证内容复制下来，打开先前注册好的 `华为云` 添加 DNS 记录

::pic
---
src: https://serv.200038.xyz/2024/12/13/852350.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


::pic
---
src: https://serv.200038.xyz/2024/12/13/676860.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


#### 4. 切换回 `Domains` 选项卡，等待签发成功即可，签发成功后会给出 `CNAME地址` ，将它解析到 `DNS` ，就完成了所有配置内容。


::pic
---
src: https://serv.200038.xyz/2024/12/13/877783.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


#### 5. 看到下图点击 `View/edit` 后 会看到 `fastly`分配的 `cname记录`和 `A 记录`

::pic
---
src: https://serv.200038.xyz/2024/12/13/096721.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

::pic
---
src: https://serv.200038.xyz/2024/12/13/460034.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

#### 6. 在华为云修改 `Fastly` 给出的 `CNAME记录集` 

::pic
---
src: https://serv.200038.xyz/2024/12/13/263158.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


#### 7. 我们再使用[itdog.cn](https://www.itdog.cn/tcping/)的 `tcping` 功能 来检查我们这个域名的 CDN 

::pic
---
src: https://serv.200038.xyz/2024/12/13/887094.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

::pic
---
src: https://serv.200038.xyz/2024/12/13/182319.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


### 至此我们的设置已完成。

--- 

**网络优化** 

**Fastly存在两种节点，anycast节点和固定地域节点，我们可以借助[ipip.net](https://tools.ipip.net/ping.php)的全球ping工具，发现这几种节点，再结合地区，分别选出适合三大运营商的IP地址**。

::pic
---
src: https://serv.200038.xyz/2024/12/13/313448.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: ipip.net
# zoom: false # 是否开启灯箱缩放，默认开启
---
::