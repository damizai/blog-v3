---
title: YxVm博客申请的方式和赞助更改
description: 想加入 YxVm 的赞助计划？只要你博客够优秀、数据够实在、内容够干净，那就大胆申请吧！从 UV 到 GitHub Star，从APP下载量到频道关注数，只要你有料，YxVm就能给你稳稳的服务器支持
date: 2025-04-08 21:55:31
updated: 2025-04-08 22:55:31
image: https://serv.200038.xyz/2025/04/05/688458.webp
categories: [经验分享]
tags: [VPS, YxVm]
# tags:
_path: /posts/96a0

recommend: 11
---


📝 记得：

- 准备好 UV 图、网站信息、开源项目等证明材料

- 登录 NodeSupport 填好资料

- 发 Issue 到 GitHub

- 嵌入赞助 iframe，到位！

---

## YxVmvps申请流程

**温馨提示需要申请前提要有[nodeseek](https://www.nodeseek.com/)的论坛账号**

## 首先看你的博客浏览量UV，以下是参考方案及审批门槛概览

|  | 配置A | 配置B | 配置C | 配置D |
| --- | --- | --- | --- | --- |
| 网站 | 300 uv/月 | 500 uv/月 | 1k uv/月 | 2k uv/月 |
| 频道 | 1k 关注 | 3k 关注 | 6k 关注 | 10k关注 |
| 开源项目 | 200 star | 500 star | 2k star | 5k star |
| APP | 500 下载 | 1k 下载 | 3k 下载 | 10k下载 |

## 目前的配置对应关系

- 配置A: YxVM | HKECO-Basic (1Cpu/767MB RAM)
- 配置B: YxVM | HKECO-Standard (1Cpu/1G RAM)
- 配置C: YxVM | HKECO-Advanced (2Cpu/2G RAM)
- 配置D: YxVM | HKECO-Luxury (4Cpu/4G RAM)

## 网站类申请具体要求

- 网站需要尽量填写日访问量曲线和月访问量曲线截图
- 尽量提供基于js的统计结果（如Umami、宝塔、1panel、百度统计、谷歌统计），准确度比cf统计更高
- 域名成立时间需要在半年以上，免费二级域名网站根据质量限定门槛
- 要求在面板上验证通过后，先在申请资助的网站上添加赞助说明[iframe](https://support.nodeget.com/page/promotion?id={your_id})组件，以降低审核成本
- 网站主要面向的是博客类型的内容站，其他类型根据影响力和质量综合评定，拒绝涉政和黄赌毒网站

## 打开[NodeSupport](https://support.nodeseek.com/)这个网址使用Nodeseek登录后填写资料

- 申请类型我是博客选择的博客,申请依据填写你的博客链接,申请描述填写你的用途，证明资料填写你的博客UV统计图床链接
- 下一步是选择你博客UV浏览的机器，按照你的UV来选择，期望时长是永久
- 然后把生成的Issue 模板填入到 [Gitub](https://github.com/NodeSeekDev/NodeSupport/issues)这里。点击NewIssue申请 
- 最后的 Issue ID 填写你 Gitub 申请#号后面的ID就可以了。

## 然后在网站上添加赞助说明[iframe](https://support.nodeget.com/page/promotion?id={your_id})组件。`your_id`填写你Github申请的ID 这里我添加到右下角了。分享一下

------

**在_souece/_date/目录下新建 `widget.yml`复制以下代码即可**

``` yml
top:
  - class_name: card-sponsor
    id_name: sidebarSponsor
    name: YxVm
    icon: fa-solid fa-heart
    html: |
     <div class="sponsor-card animated-fadein">
      <iframe 
        src="https://support.nodeseek.com/page/promotion?id={你的申请ID}" 
        style="border-radius: 8px; width: 100%; height: 200px; border: none;">
      </iframe>
     </div>
```

## 就是这么简单。嘿嘿嘿