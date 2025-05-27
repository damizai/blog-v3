---
title: 搭建一个 PixPro 若梦图床 + 接入Cloudflare R2
description: 这是一个基于 Serv00 服务器和 PixPro 图床系统的完整安装和部署教程。通过这个项目，用户可以搭建一个图床系统，并支持接入 Cloudflare R2 存储，便捷地上传和管理图片。项目为用户提供了一个简单易用的界面，并且支持个性化封面的生成与管理。
date: 2024-09-10 12:00:57
updated: 2024-09-19 00:00:00
image: https://serv.200038.xyz/2024/09/19/052317.webp
categories: [经验分享]
tags: [代码, 前端, 图床, Serv00]
# tags:
_path: /posts/55f0

recommend: 9
---

##  Serv00上搭建一个PixPro图床,内存太小,我们可以接入到CFR2 足够个人使用。自己有VPS的也可在宝塔上面部署
---

### 面板页

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/976547.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 面板页
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

### 后台页

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/960882.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 后台页
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


### 安装前准备

**[Serv00账号注册](https://www.serv00.com/)**

::link-card
---
title: Github,PixPro项目地址
description: 若梦图床
icon: https://biu.biuxin.com/2025/05/09/717977.webp
link: https://github.com/JLinMr/PixPro
---
::


## 安装步骤

1. 注册好Serv00账号打开网页进入到面板端添加域名或者用自己的域名都行，这里我用别的网站注册的二级域名。如下图添加

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/112850.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: Serv00
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


2. 把里面的A记录解析你托管到CF的域名或者别的地方申请的

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/029835.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: A记录解析
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/582959.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: A记录解析
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


3. 按照下图打开域名的权限

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/207768.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 域名权限
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/501489.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 域名权限
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


**点击Save等待成功**

4. 创建MySQL数据库（保存账号及地址）

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/932094.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: MySQL数据库
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/685608.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: MySQL数据库
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


5. [下载ZIP文件](https://github.com/JLinMr/PixPro/archive/refs/tags/v1.7.6.zip)

6. 上传安装包并解压进入文件管理器

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/454695.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 上传安装包并解压
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

7. 进入public_html文件夹删除其下所有文件

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/294142.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 进入public_html文件夹删除其下所有文件
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


8. 上传安装包到你添加的域名或者Serv00自带域名下

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/188599.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: Serv00自带域名下
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/433766.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: Serv00自带域名下
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

9. 选择你们下载文件的路径上传好如下图

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/877759.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 路径上传
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/406831.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 路径上传
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/228408.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 路径上传
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

### 和上一步一样

10. 进去后如下图所以我们`Shift`建一直按着然后点击鼠标左键全选

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/605036.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 全选
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


11. 移动到我们开始创建域名目录下的`public_html`

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/156152.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 移动到public_html
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


12. 修改PHP版本 在域名目录下创建一个文本，名为：`.htaccess`  

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/025935.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 修改PHP版本
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/837480.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 修改PHP版本
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


13. 添加PHP版本

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/880712.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 添加PHP版本
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


**选择`Text Editor` 添加以下代码**

``` php
AddType application/x-httpd-php81 .php
```

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/397539.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 添加PHP版本代码
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


14. 访问你的域名开始安装系统，管理员账户和密码自己设置 ，如果要接入`CFR2`我们存储选择 `S3` 下面我会写`S3`安装方式

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/805964.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 安装系统
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

::pic
---
src: ttps://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/039522.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 安装系统
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/119364.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 安装系统
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

15. 点击回到首页就可以上传图片了

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/808160.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 上传图片
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

---
### 接入R2 前提 已开通 Cloudflare R2

### 进入到 Cloudflare 面板 找到 R2 右边有一个管理 R2API 令牌点击创建 API令牌 ，创建好后里面有我们需要的访问密钥和机密访问密钥


::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/551368.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 创建 API令牌
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


### 1. 进入到 Cloudflare 面板 找到 R2 点击创建存储桶

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/628918.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 创建存储桶
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

   
### 2. 进入后名称随便写。位置选择亚太地区后点击创建存储桶

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/201182.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 位置选择
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


### 3. 创建好后点击设置拉到下面看到 R2.dev 子域点击后面的允许访问 ， 连接域需要添加你托管到CF上面域名

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/312754.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: R2.dev 子域
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


### 4. 14 步我们安装选择`S3`后看到下图 

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/427281.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 安装选择`S3`
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

| 参数 | 值 |
| --- | --- |
| S3 Region | auto |
| S3 Bucket | 你的存储桶名称 |
| S3 Endpoint | 你的S3API 后面不要加你的存储桶名称 |
| S3 Access Key ID | R2API令牌访问密钥 |
| S3 Access Key Secret | R2API令牌机密访问密钥 |
| S3 自定义域名 | R2.dev 添加的自定义域 或 R2 分配的域名 |

### 5. 点击完成安装即可。这是我们上传好的图片 我下面的域名就是我们 R2 分配的域名 

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/247691.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: R2分配的域名
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

### 6. 我们回到 Cloudflare R2 就会看到刚刚上传的图片

::pic
---
src: https://cdn.jsdelivr.net/gh/niceao/img/2024/12/13/058878.web
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 上传的图片
# zoom: false # 是否开启灯箱缩放，默认开启
---
::

> 在给大家推荐一个的在线生成封面网站，专为博客、短视频、社交媒体等生成个性化封面.[GitHub,项目地址](https://github.com/JLinMr/Mini-Cover).这个封面可以和图床结合。 封面做好后我们不用去上传到图床直接点击封面网站的外链即可,前提已部署`PixPro` 图床

### 感谢作者[梦爱吃鱼](https://blog.bsgun.cn/)，欢迎大家去预览、哈哈哈