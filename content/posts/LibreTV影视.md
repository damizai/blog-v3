---
title: LibreTV 是一个轻量级、免费的在线视频搜索与观看平台
description: LibreTV是一个轻量级、免费的在线视频搜索与观看平台，提供来自多个视频源的内容搜索与播放服务。无需注册，即开即用，支持多种设备访问。项目结合了前端技术和后端代理功能，可部署在支持服务端功能的各类网站托管服务上。
date: 2025-04-18 16:00:00
updated: 2025-04-20 16:00:00
image: https://serv.200038.xyz/2025/04/25/453673.webp
categories: [经验分享]
tags: [LibreTV, 影视分享, 网页前端]
# tags:
_path: /posts/4109

recommend: 3
---

## LibreTV - 免费在线视频搜索与观看平台

<div align="center">
  <img src="https://images.icon-icons.com/38/PNG/512/retrotv_5520.png" alt="LibreTV Logo" width="120">
  <br>
  <p><strong>自由观影，畅享精彩</strong></p>
</div>

## 📺 项目简介

LibreTV 是一个轻量级、免费的在线视频搜索与观看平台，提供来自多个视频源的内容搜索与播放服务。无需注册，即开即用，支持多种设备访问。项目结合了前端技术和后端代理功能，可部署在支持服务端功能的各类网站托管服务上。


::link-card
---
title: LibreTV-Github
description: LibreTV-Github
icon: https://biu.biuxin.com/2025/05/09/717977.webp
link: https://github.com/LibreSpark/LibreTV
---
::

## 站点密码是 `BiuXin`

::link-banner
---
banner: https://biu.biuxin.com/2025/05/09/362563.webp
title: 演示站点LibreTV
description: BiuXinLibreTV
link: https://video.biuxin.com
---
::

## 项目截图

::pic
---
src: https://serv.200038.xyz/2025/04/25/107520.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 项目截图
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


## 应用特点

- 🎬 多个API资源。
- 📦 支持CFpages静态部署，vercel部署。

## 🚀 快速部署

选择以下任一平台，点击一键部署按钮，即可快速创建自己的 LibreTV 实例：

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2FLibreSpark%2FLibreTV) [![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/LibreSpark/LibreTV)

## 📋 详细部署指南

### Cloudflare Pages

1. Fork 或克隆本仓库到您的 GitHub 账户
2. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com/)，进入 Pages 服务
3. 点击"创建项目"，连接您的 GitHub 仓库
4. 使用以下设置：
   - 构建命令：留空（无需构建）
   - 输出目录：留空（默认为根目录）
5. 点击"保存并部署"
6. 可选：在"设置" > "环境变量"中配置密码保护

### Vercel

1. Fork 或克隆本仓库到您的 GitHub/GitLab 账户
2. 登录 [Vercel](https://vercel.com/)，点击"New Project"
3. 导入您的仓库，使用默认设置
4. 点击"Deploy"
5. 可选：在"Settings" > "Environment Variables"中配置密码保护

### Netlify

1. Fork 或克隆本仓库到您的 GitHub 账户
2. 登录 [Netlify](https://app.netlify.com/)
3. 点击"New site from Git"，选择您的仓库
4. 构建设置保持默认
5. 点击"Deploy site"
6. 可选：在"Site settings" > "Build & deploy" > "Environment"中配置密码保护



## 🔧 自定义配置

### 密码保护

要为您的 LibreTV 实例添加密码保护，可以在部署平台上设置环境变量：

**环境变量名**: `PASSWORD` 
**值**: 您想设置的密码

各平台设置方法：

- **Cloudflare Pages**: Dashboard > 您的项目 > 设置 > 环境变量
- **Vercel**: Dashboard > 您的项目 > Settings > Environment Variables
- **Netlify**: Dashboard > 您的项目 > Site settings > Build & deploy > Environment


### API兼容性

LibreTV 支持标准的苹果 CMS V10 API 格式。添加自定义 API 时需遵循以下格式：
- 搜索接口: `https://example.com/api.php/provide/vod/?ac=videolist&wd=关键词`
- 详情接口: `https://example.com/api.php/provide/vod/?ac=detail&ids=视频ID`

**添加 CMS 源**:
1. 在设置面板中选择"自定义接口"
2. 接口地址只需填写到域名部分: `https://example.com`（不要包含`/api.php/provide/vod`部分）


## ⚠️ 免责声明

LibreTV 仅作为视频搜索工具，不存储、上传或分发任何视频内容。所有视频均来自第三方 API 接口提供的搜索结果。如有侵权内容，请联系相应的内容提供方。

本项目开发者不对使用本项目产生的任何后果负责。使用本项目时，您必须遵守当地的法律法规。