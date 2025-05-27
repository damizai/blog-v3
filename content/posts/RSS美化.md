---
title: 美化你的博客RSS订阅地址
description: 这篇文章介绍了RSS的基本概念、结构、优势以及如何通过XSLT技术美化RSS订阅地址。RSS是一种基于XML的内容分发格式，允许用户通过RSS阅读器自动获取网站的最新更新
date: 2025-05-03 16:00:00
updated: 2025-05-03 16:00:00
image: https://biu.200038.xyz/2025/04/26/660779.webp
categories: [经验分享]
tags: [代码, 前端, RSS美化]
# tags:
_path: /posts/47bc

recommend: 5
---

## 介绍 

### 1. 什么是RSS

RSS（全称为 Really Simple Syndication 或 Rich Site Summary）是一种基于 XML 的内容分发格式，主要用于网站内容的自动订阅与聚合。它的设计目标是：让用户无需逐个访问网站，即可通过 RSS 阅读器自动获取网站的最新更新。

RSS 最初被广泛应用于博客、新闻网站、论坛等内容频繁更新的平台，目前依然是信息分发与聚合的重要工具。

### 2. RSS 的基本结构

一个标准的 RSS 文档是一个 XML 文件，包含如下几个核心元素：

``` xml
<rss version="2.0">
  <channel>
    <title>站点名称</title>
    <link>https://example.com</link>
    <description>站点简介</description>
    <item>
      <title>文章标题</title>
      <link>https://example.com/post/1</link>
      <description>文章摘要</description>
      <pubDate>Fri, 12 Apr 2025 14:00:00 +0800</pubDate>
    </item>
    <!-- 可有多个 item -->
  </channel>
</rss>
```

- <rss> 是文档的根节点，version="2.0" 表示使用 RSS 2.0 标准；
- <channel> 包含了整个订阅源的信息；
- <item> 表示一篇文章或一条内容更新记录；
- 每个 <item> 可包含标题、链接、发布时间、摘要等字段

### 3. 优势

RSS提供了一种完全不需要平台中介的内容获取方式，使用户可以主动订阅感兴趣的源，集中管理、阅读多个站点的更新内容。与社交媒体推荐流不同，RSS完全由用户控制，无广告干扰、无算法推荐。同时，RSS格式标准统一，适合程序处理和自动化集成，常用于信息聚合、数据采集和内容推送等场景。

### 4. RSS阅读器

目前也有很多优秀的RSS阅读器，这里我推荐一下我的Friend-Circle-Lite，完全依赖免费服务运行，使用github action定时运行，理论上可以配合结果json插入所有的站点，地址如下，欢迎品尝！

::link-card
---
title: Github项目地址
description: Github
icon: https://biu.biuxin.com/2025/05/09/717977.webp
link: https://github.com/willow-god/Friend-Circle-Lite
---
::

### 5. RSS美化原理

首先展示一下最终的美化效果：

![RSS美化](https://biu.biuxin.com/2025/05/04/410953.webp)


### 大家可以打开这个网址可以看一下我们美化过的效果


::link-banner
---
banner: https://biu.200038.xyz/2025/05/09/602522.webp
title: RSS美化站点网页预览地址
description: RSS美化站点
link: https://rss.biuxin.com
---
::


`RSS`是一种基于`XML`的内容分发格式，默认在浏览器中呈现为结构化但缺乏样式的纯文本。为了提升其可读性与视觉效果，可以通过引入 `XSLT（Extensible Stylesheet Language Transformations）` 技术，对`XML`结构进行转换，使其在浏览器中以`HTML`的形式展示。


RSS 美化的核心原理是：使用 `XSL` 样式表对`RSS`的`XML`数据进行转换，并生成结构化的`HTML`页面。浏览器在解析`XML`时，会根据声明的 `XSL` 文件渲染页面内容。

在`RSS`文件头部添加如下声明，即可引用本地的 `XSL` 文件：


``` xml
<?xml-stylesheet type="text/xsl" href="rss-style.xsl"?>
```

### 6. XSL文件

`XSL` 是一种专门用于转换 `XML` 文档结构的样式语言。借助 `XSL`，可以将原始的RSS数据（如 `<item>` 列表）转换为`HTML`结构，搭配`CSS`实现样式美化，从而达到`“美化RSS”`的目的，同时因为在真正的源码中，`XSL`的引入只是一行小小的类似于注释的声明，所以完全不会影响到`RSS`的整体接口，也不会影响`RSS`的抓取。


::pic
---
src: https://biu.biuxin.com/2025/05/04/582848.webp
# mirror: # 是否借助第三方图片加载服务，见源代码
caption: 源代码展示
# zoom: false # 是否开启灯箱缩放，默认开启
---
::


下面是一个简单的`XSL`文件示例，可以将`RSS`的`XML`结构转为一个简洁的`html`界面

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="1.0"
  xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:output method="html" encoding="UTF-8" indent="yes"/>
  <xsl:template match="/">
    <html>
      <head>
        <title><xsl:value-of select="rss/channel/title"/></title>
        <style>
          body { font-family: sans-serif; padding: 2em; background: #f8f8f8; }
          .item { margin-bottom: 1.5em; padding: 1em; background: #fff; border-radius: 6px; }
          .title { font-size: 1.2em; font-weight: bold; color: #333; }
          .date { font-size: 0.9em; color: #888; margin-top: 0.3em; }
        </style>
      </head>
      <body>
        <h1><xsl:value-of select="rss/channel/title"/></h1>
        <xsl:for-each select="rss/channel/item">
          <div class="item">
            <div class="title">
              <a href="{link}" target="_blank"><xsl:value-of select="title"/></a>
            </div>
            <div class="date">
              <xsl:value-of select="pubDate"/>
            </div>
            <div class="description">
              <xsl:value-of select="description" disable-output-escaping="yes"/>
            </div>
          </div>
        </xsl:for-each>
      </body>
    </html>
  </xsl:template>
</xsl:stylesheet>
```

### 7. 限制

出于安全限制，大多数现代浏览器`默认禁止加载跨域的 XSL 样式表`。也就是说，如果你在 RSS 文件中通过远程地址引用 XSL：

``` xml
<?xml-stylesheet type="text/xsl" href="https://example.com/rss-style.xsl"?>
```

实测`Chrome`是无法加载的，其他浏览器暂时没有测试，但是建议使用相对路径。

### 8. 实现美化

上面是原理部分，所有`xml`的美化都是基于这个原理，而我个人使用的是`Hexo`，为了更加简单的进行美化，我实现了一个`Hexo插件`，插件地址如下：


::link-card
---
title: Github项目地址
description: Github
icon: https://biu.biuxin.com/2025/05/09/717977.webp
link: https://github.com/willow-god/hexo-pretty-feed
---
::


该插件完全基于原插件 [hexo-generator-feed](https://github.com/hexojs/hexo-generator-feed)，仅仅添加了在Atom顶部插入XSL文件的功能，为了方便个人进行美化，同时，所有的XSL需要放在本地，所以甚至没有添加内置的美化文件，下面简单讲解一下使用方式。

### 9. 安装插件

由于两个插件共用一个配置，可能会造成冲突，所以请卸载掉原插件并安装新插件：

``` bash
npm uninstall hexo-generator-feed --save
npm install hexo-pretty-feed --save
```


该插件和原始插件配置完全兼容，如果你不愿意添加美化，可以删掉参数`pretty_atom_file`和`pretty_rss2_file`，功能和原版保持完全一致。


### 10. 添加文件

下面就添加美化文件，在`source`文件夹下任意位置创建文件`atom.xsl`或者`rss2.xsl`，具体选哪个需要看你个人的`rss`需求，当然也可以两个都加上

其中，`atom.xsl`文件写入以下内容：复制的时候注意上面的空格

``` xml
<?xml version="1.0" encoding="utf-8"?><xsl:stylesheet version="3.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:atom="http://www.w3.org/2005/Atom"><xsl:output method="html" version="1.0" encoding="UTF-8" indent="yes"/><xsl:template match="/"><xsl:variable name="title"><xsl:value-of select="/atom:feed/atom:title"/></xsl:variable><xsl:variable name="description"><xsl:value-of select="/atom:feed/atom:subtitle"/></xsl:variable><xsl:variable name="link"><xsl:value-of select="/atom:feed/atom:link[@rel='alternate']/@href | /atom:feed/atom:link[not(@rel)]/@href"/></xsl:variable><html class="dark scroll-smooth"><head><meta charset="utf-8"/><meta name="viewport" content="width=device-width, initial-scale=1"/><meta name="referrer" content="unsafe-url"/><title><xsl:value-of select="$title"/></title><style>*,:after,:before{--tw-border-spacing-x:0;--tw-border-spacing-y:0;--tw-translate-x:0;--tw-translate-y:0;--tw-rotate:0;--tw-skew-x:0;--tw-skew-y:0;--tw-scale-x:1;--tw-scale-y:1;--tw-pan-x: ;--tw-pan-y: ;--tw-pinch-zoom: ;--tw-scroll-snap-strictness:proximity;--tw-gradient-from-position: ;--tw-gradient-via-position: ;--tw-gradient-to-position: ;--tw-ordinal: ;--tw-slashed-zero: ;--tw-numeric-figure: ;--tw-numeric-spacing: ;--tw-numeric-fraction: ;--tw-ring-inset: ;--tw-ring-offset-width:0px;--tw-ring-offset-color:#fff;--tw-ring-color:rgba(59,130,246,.5);--tw-ring-offset-shadow:0 0 #0000;--tw-ring-shadow:0 0 #0000;--tw-shadow:0 0 #0000;--tw-shadow-colored:0 0 #0000;--tw-blur: ;--tw-brightness: ;--tw-contrast: ;--tw-grayscale: ;--tw-hue-rotate: ;--tw-invert: ;--tw-saturate: ;--tw-sepia: ;--tw-drop-shadow: ;--tw-backdrop-blur: ;--tw-backdrop-brightness: ;--tw-backdrop-contrast: ;--tw-backdrop-grayscale: ;--tw-backdrop-hue-rotate: ;--tw-backdrop-invert: ;--tw-backdrop-opacity: ;--tw-backdrop-saturate: ;--tw-backdrop-sepia: ;--tw-contain-size: ;--tw-contain-layout: ;--tw-contain-paint: ;--tw-contain-style: }::backdrop{--tw-border-spacing-x:0;--tw-border-spacing-y:0;--tw-translate-x:0;--tw-translate-y:0;--tw-rotate:0;--tw-skew-x:0;--tw-skew-y:0;--tw-scale-x:1;--tw-scale-y:1;--tw-pan-x: ;--tw-pan-y: ;--tw-pinch-zoom: ;--tw-scroll-snap-strictness:proximity;--tw-gradient-from-position: ;--tw-gradient-via-position: ;--tw-gradient-to-position: ;--tw-ordinal: ;--tw-slashed-zero: ;--tw-numeric-figure: ;--tw-numeric-spacing: ;--tw-numeric-fraction: ;--tw-ring-inset: ;--tw-ring-offset-width:0px;--tw-ring-offset-color:#fff;--tw-ring-color:rgba(59,130,246,.5);--tw-ring-offset-shadow:0 0 #0000;--tw-ring-shadow:0 0 #0000;--tw-shadow:0 0 #0000;--tw-shadow-colored:0 0 #0000;--tw-blur: ;--tw-brightness: ;--tw-contrast: ;--tw-grayscale: ;--tw-hue-rotate: ;--tw-invert: ;--tw-saturate: ;--tw-sepia: ;--tw-drop-shadow: ;--tw-backdrop-blur: ;--tw-backdrop-brightness: ;--tw-backdrop-contrast: ;--tw-backdrop-grayscale: ;--tw-backdrop-hue-rotate: ;--tw-backdrop-invert: ;--tw-backdrop-opacity: ;--tw-backdrop-saturate: ;--tw-backdrop-sepia: ;--tw-contain-size: ;--tw-contain-layout: ;--tw-contain-paint: ;--tw-contain-style: }
        
        /*! tailwindcss v3.4.17 | MIT License | https://tailwindcss.com*/*,:after,:before{box-sizing:border-box;border:0 solid #e7e7f0}:after,:before{--tw-content:""}:host,html{line-height:1.5;-webkit-text-size-adjust:100%;-moz-tab-size:4;-o-tab-size:4;tab-size:4;font-family:ui-sans-serif,system-ui,sans-serif,Apple Color Emoji,Segoe UI Emoji,Segoe UI Symbol,Noto Color Emoji;font-feature-settings:normal;font-variation-settings:normal;-webkit-tap-highlight-color:transparent}body{margin:0;line-height:inherit}hr{height:0;color:inherit;border-top-width:1px}abbr:where([title]){-webkit-text-decoration:underline dotted;text-decoration:underline dotted}h1,h2,h3,h4,h5,h6{font-size:inherit;font-weight:inherit}a{color:inherit;text-decoration:inherit}b,strong{font-weight:bolder}code,kbd,pre,samp{font-family:ui-monospace,SFMono-Regular,Menlo,Monaco,Consolas,Liberation Mono,Courier New,monospace;font-feature-settings:normal;font-variation-settings:normal;font-size:1em}small{font-size:80%}sub,sup{font-size:75%;line-height:0;position:relative;vertical-align:baseline}sub{bottom:-.25em}sup{top:-.5em}table{text-indent:0;border-color:inherit;border-collapse:collapse}button,input,optgroup,select,textarea{font-family:inherit;font-feature-settings:inherit;font-variation-settings:inherit;font-size:100%;font-weight:inherit;line-height:inherit;letter-spacing:inherit;color:inherit;margin:0;padding:0}button,select{text-transform:none}button,input:where([type=button]),input:where([type=reset]),input:where([type=submit]){-webkit-appearance:button;background-color:transparent;background-image:none}:-moz-focusring{outline:auto}:-moz-ui-invalid{box-shadow:none}progress{vertical-align:baseline}::-webkit-inner-spin-button,::-webkit-outer-spin-button{height:auto}[type=search]{-webkit-appearance:textfield;outline-offset:-2px}::-webkit-search-decoration{-webkit-appearance:none}::-webkit-file-upload-button{-webkit-appearance:button;font:inherit}summary{display:list-item}blockquote,dd,dl,figure,h1,h2,h3,h4,h5,h6,hr,p,pre{margin:0}fieldset{margin:0}fieldset,legend{padding:0}menu,ol,ul{list-style:none;margin:0;padding:0}dialog{padding:0}textarea{resize:vertical}input::-moz-placeholder,textarea::-moz-placeholder{opacity:1;color:#a8a8b8}input::placeholder,textarea::placeholder{opacity:1;color:#a8a8b8}[role=button],button{cursor:pointer}:disabled{cursor:default}audio,canvas,embed,iframe,img,object,svg,video{display:block;vertical-align:middle}img,video{max-width:100%;height:auto}[hidden]:where(:not([hidden=until-found])){display:none}:root{--card-radius:0.75rem;--btn-radius:var(--card-radius);--badge-radius:var(--btn-radius);--input-radius:var(--btn-radius);--avatar-radius:9999px;--annonce-radius:var(--avatar-radius);--ui-border-color:#1f1f31;--btn-border:#1f1f31;--badge-border:var(--btn-border);--input-border:var(--ui-border-color);--ui-disabled-border:#121220;--ui-error-border:#e11d48;--ui-success-border:#65a30d;--input-outline:#4f46e5;--ui-bg:rgb(18 18 32/var(--ui-bg-opacity));--ui-soft-bg:#1f1f31;--overlay-bg:rgba(2,2,13,.25);--input-bg:var(--ui-soft-bg);--ui-disabled-bg:#121220;--card-padding:1.5rem;--display-text-color:#fff;--title-text-color:var(--display-text-color);--body-text-color:#d6d6e1;--caption-text-color:#6e6e81;--placeholder-text-color:#4d4d5f;--ui-bg-opacity:1;color:var(--body-text-color)}*,.border{border-color:var(--ui-border-color)}button:disabled{border:none!important;background:var(--ui-disabled-bg)!important;background-image:none!important;box-shadow:none!important;color:var(--placeholder-text-color)!important;pointer-events:none!important}button:disabled:before{content:var(--tw-content);display:none}a:focus-visible,button:focus-visible{outline-width:2px;outline-offset:2px;outline-color:#4f46e5}a:focus-visible:focus-visible,button:focus-visible:focus-visible{outline-style:solid}input:user-invalid,select:user-invalid,textarea:user-invalid{--input-border:var(--ui-error-border);--ui-border-color:var(--ui-error-border);--input-outline:var(--ui-error-border);--title-text-color:#fb7185}[data-rounded=none]{--card-radius:0px;--avatar-radius:0px}[data-rounded=default]{--card-radius:0.25rem}[data-rounded=small]{--card-radius:0.125rem}[data-rounded=medium]{--card-radius:0.375rem}[data-rounded=large]{--card-radius:0.5rem}[data-rounded=xlarge]{--card-radius:0.75rem}[data-rounded="2xlarge"]{--card-radius:1rem;--input-radius:0.75rem}[data-rounded="3xlarge"]{--card-radius:1.5rem;--input-radius:0.75rem}[data-rounded=full]{--card-radius:1.5rem;--btn-radius:9999px;--input-radius:1rem}[data-shade=glassy]{--ui-bd-blur:40px;--ui-bg-opacity:0.75;--ui-bg:rgb(58 58 75/var(--ui-bg-opacity));--ui-border-color:rgba(250,250,254,.1);--ui-soft-bg:rgba(77,77,95,.5)}[data-shade="800"]{--ui-border-color:#3a3a4b;--ui-bg:#1f1f31;--ui-soft-bg:#121220}[data-shade="900"]{--ui-border-color:#1f1f31;--ui-bg:#121220;--ui-soft-bg:#1f1f31}[data-shade="950"]{--ui-border-color:#1f1f31;--ui-bg:#02020d;--ui-soft-bg:#1f1f31}.container{width:100%}@media (min-width:640px){.container{max-width:640px}}@media (min-width:768px){.container{max-width:768px}}@media (min-width:1024px){.container{max-width:1024px}}@media (min-width:1280px){.container{max-width:1280px}}@media (min-width:1536px){.container{max-width:1536px}}.icon-\[tabler--rss\]{display:inline-block;width:1em;height:1em;background-color:currentColor;-webkit-mask-image:var(--svg);mask-image:var(--svg);-webkit-mask-repeat:no-repeat;mask-repeat:no-repeat;-webkit-mask-size:100% 100%;mask-size:100% 100%;--svg:url("data:image/svg+xml;charset=utf-8,%3Csvg xmlns='http://www.w3.org/2000/svg' width='24' height='24'%3E%3Cpath fill='none' stroke='%23000' stroke-linecap='round' stroke-linejoin='round' stroke-width='2' d='M4 19a1 1 0 1 0 2 0 1 1 0 1 0-2 0M4 4a16 16 0 0 1 16 16M4 11a9 9 0 0 1 9 9'/%3E%3C/svg%3E")}.link{--tw-text-opacity:1;color:rgb(129 140 248/var(--tw-text-opacity,1));transition-property:color,background-color,border-color,text-decoration-color,fill,stroke,opacity,box-shadow,transform,filter,-webkit-backdrop-filter;transition-property:color,background-color,border-color,text-decoration-color,fill,stroke,opacity,box-shadow,transform,filter,backdrop-filter;transition-property:color,background-color,border-color,text-decoration-color,fill,stroke,opacity,box-shadow,transform,filter,backdrop-filter,-webkit-backdrop-filter;transition-timing-function:cubic-bezier(.4,0,.2,1);transition-duration:.15s}.link.variant-ghost:hover,.link.variant-underlined{text-decoration-line:underline}.link.variant-animated{position:relative}.link.variant-animated:before{position:absolute;left:0;right:0;bottom:0;height:1px;transform-origin:right;--tw-scale-x:0;transform:translate(var(--tw-translate-x),var(--tw-translate-y)) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y));transition-property:color,background-color,border-color,text-decoration-color,fill,stroke,opacity,box-shadow,transform,filter,-webkit-backdrop-filter;transition-property:color,background-color,border-color,text-decoration-color,fill,stroke,opacity,box-shadow,transform,filter,backdrop-filter;transition-property:color,background-color,border-color,text-decoration-color,fill,stroke,opacity,box-shadow,transform,filter,backdrop-filter,-webkit-backdrop-filter;transition-timing-function:cubic-bezier(.4,0,.2,1);content:var(--tw-content);transition-duration:.2s}.link.variant-animated:hover:before{transform-origin:left;content:var(--tw-content);--tw-scale-x:1;transform:translate(var(--tw-translate-x),var(--tw-translate-y)) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y))}.link.intent-info{--tw-text-opacity:1;color:rgb(96 165 250/var(--tw-text-opacity,1))}.link.intent-neutral{--tw-text-opacity:1;color:rgb(255 255 255/var(--tw-text-opacity,1))}.link.variant-animated.intent-neutral:before{content:var(--tw-content);background-color:hsla(0,0%,100%,.5)}.link.variant-animated.intent-info:before{content:var(--tw-content);--tw-bg-opacity:1;background-color:rgb(37 99 235/var(--tw-bg-opacity,1))}.link.variant-animated.intent-primary:before{content:var(--tw-content);--tw-bg-opacity:1;background-color:rgb(79 70 229/var(--tw-bg-opacity,1))}.link.variant-ghost.intent-neutral,.link.variant-underlined.intent-neutral{text-decoration-color:hsla(0,0%,100%,.5)}.mx-auto{margin-left:auto;margin-right:auto}.my-2{margin-top:.5rem;margin-bottom:.5rem}.my-6{margin-top:1.5rem;margin-bottom:1.5rem}.-mt-5{margin-top:-1.25rem}.ml-4{margin-left:1rem}.mr-1{margin-right:.25rem}.mr-2{margin-right:.5rem}.mt-1{margin-top:.25rem}.block{display:block}.inline-block{display:inline-block}.inline{display:inline}.flex{display:flex}.hidden{display:none}.h-8{height:2rem}.min-h-screen{min-height:100vh}.min-h-svh{min-height:100svh}.w-24{width:6rem}.w-8{width:2rem}.max-w-full{max-width:100%}.max-w-screen-lg{max-width:1024px}.flex-1{flex:1 1 0%}.grow{flex-grow:1}.cursor-pointer{cursor:pointer}.flex-col{flex-direction:column}.flex-wrap{flex-wrap:wrap}.items-start{align-items:flex-start}.justify-center{justify-content:center}.justify-between{justify-content:space-between}.gap-1{gap:.25rem}.gap-2{gap:.5rem}.gap-x-4{-moz-column-gap:1rem;column-gap:1rem}.gap-y-2{row-gap:.5rem}.space-y-2>:not([hidden])~:not([hidden]){--tw-space-y-reverse:0;margin-top:calc(.5rem*(1 - var(--tw-space-y-reverse)));margin-bottom:calc(.5rem*var(--tw-space-y-reverse))}.space-y-4>:not([hidden])~:not([hidden]){--tw-space-y-reverse:0;margin-top:calc(1rem*(1 - var(--tw-space-y-reverse)));margin-bottom:calc(1rem*var(--tw-space-y-reverse))}.space-y-6>:not([hidden])~:not([hidden]){--tw-space-y-reverse:0;margin-top:calc(1.5rem*(1 - var(--tw-space-y-reverse)));margin-bottom:calc(1.5rem*var(--tw-space-y-reverse))}.overflow-hidden{overflow:hidden}.scroll-smooth{scroll-behavior:smooth}.truncate{overflow:hidden;text-overflow:ellipsis;white-space:nowrap}.bg-gray-925{--tw-bg-opacity:1;background-color:rgb(9 9 21/var(--tw-bg-opacity,1))}.bg-gradient-to-r{background-image:linear-gradient(to right,var(--tw-gradient-stops))}.from-primary-600{--tw-gradient-from:#4f46e5 var(--tw-gradient-from-position);--tw-gradient-to:rgba(79,70,229,0) var(--tw-gradient-to-position);--tw-gradient-stops:var(--tw-gradient-from),var(--tw-gradient-to)}.to-accent-400{--tw-gradient-to:#e879f9 var(--tw-gradient-to-position)}.bg-clip-text{-webkit-background-clip:text;background-clip:text}.p-1{padding:.25rem}.px-4{padding-left:1rem;padding-right:1rem}.py-2{padding-top:.5rem;padding-bottom:.5rem}.py-4{padding-top:1rem;padding-bottom:1rem}.py-6{padding-top:1.5rem;padding-bottom:1.5rem}.pb-2{padding-bottom:.5rem}.pt-2{padding-top:.5rem}.text-center{text-align:center}.font-sans{font-family:ui-sans-serif,system-ui,sans-serif,Apple Color Emoji,Segoe UI Emoji,Segoe UI Symbol,Noto Color Emoji}.text-2xl{font-size:1.5rem;line-height:2rem}.text-lg{font-size:1.125rem;line-height:1.75rem}.text-sm{font-size:.875rem;line-height:1.25rem}.font-bold{font-weight:700}.font-medium{font-weight:500}.font-semibold{font-weight:600}.leading-normal{line-height:1.5}.text-transparent{color:transparent}.antialiased{-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale}.text-title{color:var(--title-text-color)}.text-body{color:var(--body-text-color)}.\!text-caption{color:var(--caption-text-color)!important}.text-caption{color:var(--caption-text-color)}.dark{--display-text-color:#fff;--title-text-color:var(--display-text-color);--caption-text-color:#6e6e81;--body-text-color:#d6d6e1;--placeholder-text-color:#4d4d5f;--ui-border-color:#232323}[data-shade="900"]:where(.dark,.dark *),[data-shade="925"]:where(.dark,.dark *),[data-shade="950"]:where(.dark,.dark *){--ui-border-color:#383838}@media (min-width:640px){.sm\:gap-1{gap:.25rem}}@media (min-width:768px){.md\:flex-row{flex-direction:row}.md\:space-y-0>:not([hidden])~:not([hidden]){--tw-space-y-reverse:0;margin-top:calc(0px*(1 - var(--tw-space-y-reverse)));margin-bottom:calc(0px*var(--tw-space-y-reverse))}.md\:p-4{padding:1rem}.md\:px-6{padding-left:1.5rem;padding-right:1.5rem}.md\:pt-6{padding-top:1.5rem}}@media (min-width:1024px){.lg\:dark\:bg-gray-900:is(.dark *){--tw-bg-opacity:1;background-color:rgb(18 18 32/var(--tw-bg-opacity,1))}}</style></head><body class="bg-gray-925 min-h-screen min-h-svh font-sans leading-normal antialiased lg:dark:bg-gray-900"><main class="min-w-screen container mx-auto flex min-h-screen max-w-screen-lg flex-col px-4 py-6 md:px-6"><header class="space-y-2 pt-2 md:pt-6"><a title="{$title}" href="{$link}" target="_blank" rel="noopener noreferrer"><h1 class="flex text-2xl"><span class="icon-[tabler--rss] mr-2 h-8 w-8"/><span class="lg2:text-3xl from-primary-600 to-accent-400 inline-block bg-gradient-to-r bg-clip-text font-bold text-transparent"><xsl:value-of select="$title" disable-output-escaping="yes"/></span></h1></a><p class="text-body pt-2 text-lg py-4"><xsl:value-of select="$description" disable-output-escaping="yes"/></p><p class="text-caption text-sm">
              This RSS feed for the
              <a class="link intent-neutral variant-animated !text-caption font-bold" title="{$title}" href="{$link}" target="_blank" rel="noopener noreferrer"><xsl:value-of select="$title"/></a>
              website.
            </p><p class="text-body text-sm hidden" id="subscribe-links">
              You can subscribe this RSS feed by
              <a class="link intent-neutral variant-animated font-bold" title="Feedly" data-href="https://feedly.com/i/subscription/feed/" target="_blank" rel="noopener noreferrer">Feedly</a>,
              <a class="link intent-neutral variant-animated font-bold" title="Inoreader" data-href="https://www.inoreader.com/feed/" target="_blank" rel="noopener noreferrer">Inoreader</a>,
              <a class="link intent-neutral variant-animated font-bold" title="Newsblur" data-href="https://www.newsblur.com/?url=" target="_blank" rel="noopener noreferrer">Newsblur</a>,
              <a class="link intent-neutral variant-animated font-bold" title="Follow" data-href="follow://add?url=" rel="noopener noreferrer">Follow</a>,
              <a class="link intent-neutral variant-animated font-bold" title="RSS Reader" data-href="feed:" data-raw="true" rel="noopener noreferrer">RSS Reader</a>
              or
              <a class="link intent-neutral variant-animated font-bold" title="{$title} 's feed source" data-href="" data-raw="true" rel="noopener noreferrer">View Source</a>.
            </p><script>
              document.addEventListener('DOMContentLoaded', function () {
                document.querySelectorAll('a[data-href]').forEach(function (a) {
                  const url = new URL(location.href)
                  const feed = url.searchParams.get('url') || location.href
                  const raw = a.getAttribute('data-raw')
                  if (raw) {
                    a.href = a.getAttribute('data-href') + feed
                  } else {
                    a.href = a.getAttribute('data-href') + encodeURIComponent(feed)
                  }
                })
                document.getElementById('subscribe-links').classList.remove('hidden')
              })
            </script></header><hr class="my-6"/><section class="flex-1 space-y-6 p-1 md:p-4"><xsl:choose><xsl:when test="/rss/channel/item"><xsl:for-each select="/rss/channel/item"><article class="space-y-2"><details><summary class="max-w-full truncate"><xsl:if test="title"><h2 class="text-title inline cursor-pointer text-lg font-semibold"><xsl:value-of select="title" disable-output-escaping="yes"/></h2></xsl:if><xsl:if test="pubDate"><time class="text-caption ml-4 mt-1 block text-sm"><xsl:value-of select="pubDate"/></time></xsl:if></summary><div class="text-body px-4 py-2"><p class="my-2"><xsl:choose><xsl:when test="description"><xsl:value-of select="description" disable-output-escaping="yes"/></xsl:when></xsl:choose></p><xsl:if test="link"><a class="link variant-animated intent-neutral font-bold" href="{link}" target="_blank" rel="noopener noreferrer">
                            Read More
                          </a></xsl:if></div></details></article></xsl:for-each></xsl:when><xsl:when test="/atom:feed/atom:entry"><xsl:for-each select="/atom:feed/atom:entry"><article class="space-y-2"><details><summary class="max-w-full truncate"><xsl:if test="atom:title"><h2 class="text-title inline cursor-pointer text-lg font-semibold"><xsl:value-of select="atom:title" disable-output-escaping="yes"/></h2></xsl:if><xsl:if test="atom:updated"><time class="text-caption ml-4 mt-1 block text-sm"><xsl:value-of select="atom:updated"/></time></xsl:if></summary><div class="text-body px-4 py-2"><p class="my-2"><xsl:choose><xsl:when test="atom:summary"><xsl:value-of select="atom:summary" disable-output-escaping="yes"/></xsl:when><xsl:when test="atom:content"><xsl:value-of select="atom:content" disable-output-escaping="yes"/></xsl:when></xsl:choose></p><xsl:if test="atom:link/@href"><a class="link variant-animated intent-neutral font-bold" href="{atom:link/@href}" target="_blank" rel="noopener noreferrer">
                            Read More
                          </a></xsl:if></div></details></article></xsl:for-each></xsl:when></xsl:choose></section><hr class="my-6"/><footer><div class="flex flex-col justify-between space-y-4 md:flex-row md:space-y-0"><div class="space-y-4"><a class="flex text-2xl font-bold" href="https://rss.beauty" title="RSS.Beauty"><span class="text-title icon-[tabler--rss] mr-1 h-8 w-8"/><span class="text-title">RSS</span>.
                  <span class="from-primary-600 to-accent-400 bg-gradient-to-r bg-clip-text text-transparent">Beauty</span></a><div class="text-caption">Make Your RSS Beautiful</div></div><div class="space-y-4"><div class="flex flex-wrap gap-x-4 gap-y-2"><a class="link intent-neutral variant-animated" target="_blank" title="GitHub" href="https://github.com/ccbikai/RSS.Beauty">GitHub</a><a class="link intent-neutral variant-animated" target="_blank" title="X/Twitter" href="https://404.li/kai">X/Twitter</a></div><div class="text-title flex gap-1 overflow-hidden font-medium">
                  Made with ❤️‍🔥 By
                  <div class="flex items-start justify-center gap-2 text-center font-semibold sm:gap-1"><div class="block"><a href="https://html.zone" target="_blank" title="HTML.ZONE" class="block pb-2">HTML.ZONE</a><div class="-mt-5 grow overflow-hidden"><svg class="w-24" aria-hidden="true" height="22" viewBox="0 0 283 22" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M1.24715 19.3744C72.4051 10.3594 228.122 -4.71194 281.724 7.12332" stroke="url(#paint0_linear_pl)" stroke-width="4"/><defs><linearGradient id="paint0_linear_pl" x1="282" y1="5.49999" x2="40" y2="13" gradientUnits="userSpaceOnUse"><stop stop-color="#facc15"/><stop offset="1" stop-color="#a855f7"/></linearGradient></defs></svg></div></div></div></div></div></div></footer></main></body></html></xsl:template></xsl:stylesheet>
```
`rss2.xsl`文件写入以下内容：

``` xml
<?xml version="1.0" encoding="utf-8"?><xsl:stylesheet version="3.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:atom="http://www.w3.org/2005/Atom"><xsl:output method="html" version="1.0" encoding="UTF-8" indent="yes"/><xsl:template match="/"><xsl:variable name="title"><xsl:value-of select="/rss/channel/title"/></xsl:variable><xsl:variable name="description"><xsl:value-of select="/rss/channel/description"/></xsl:variable><xsl:variable name="link"><xsl:value-of select="/rss/channel/link"/></xsl:variable><html class="dark scroll-smooth"><head><meta charset="utf-8"/><meta name="viewport" content="width=device-width, initial-scale=1"/><meta name="referrer" content="unsafe-url"/><title><xsl:value-of select="$title"/></title><style>*,:after,:before{--tw-border-spacing-x:0;--tw-border-spacing-y:0;--tw-translate-x:0;--tw-translate-y:0;--tw-rotate:0;--tw-skew-x:0;--tw-skew-y:0;--tw-scale-x:1;--tw-scale-y:1;--tw-pan-x: ;--tw-pan-y: ;--tw-pinch-zoom: ;--tw-scroll-snap-strictness:proximity;--tw-gradient-from-position: ;--tw-gradient-via-position: ;--tw-gradient-to-position: ;--tw-ordinal: ;--tw-slashed-zero: ;--tw-numeric-figure: ;--tw-numeric-spacing: ;--tw-numeric-fraction: ;--tw-ring-inset: ;--tw-ring-offset-width:0px;--tw-ring-offset-color:#fff;--tw-ring-color:rgba(59,130,246,.5);--tw-ring-offset-shadow:0 0 #0000;--tw-ring-shadow:0 0 #0000;--tw-shadow:0 0 #0000;--tw-shadow-colored:0 0 #0000;--tw-blur: ;--tw-brightness: ;--tw-contrast: ;--tw-grayscale: ;--tw-hue-rotate: ;--tw-invert: ;--tw-saturate: ;--tw-sepia: ;--tw-drop-shadow: ;--tw-backdrop-blur: ;--tw-backdrop-brightness: ;--tw-backdrop-contrast: ;--tw-backdrop-grayscale: ;--tw-backdrop-hue-rotate: ;--tw-backdrop-invert: ;--tw-backdrop-opacity: ;--tw-backdrop-saturate: ;--tw-backdrop-sepia: ;--tw-contain-size: ;--tw-contain-layout: ;--tw-contain-paint: ;--tw-contain-style: }::backdrop{--tw-border-spacing-x:0;--tw-border-spacing-y:0;--tw-translate-x:0;--tw-translate-y:0;--tw-rotate:0;--tw-skew-x:0;--tw-skew-y:0;--tw-scale-x:1;--tw-scale-y:1;--tw-pan-x: ;--tw-pan-y: ;--tw-pinch-zoom: ;--tw-scroll-snap-strictness:proximity;--tw-gradient-from-position: ;--tw-gradient-via-position: ;--tw-gradient-to-position: ;--tw-ordinal: ;--tw-slashed-zero: ;--tw-numeric-figure: ;--tw-numeric-spacing: ;--tw-numeric-fraction: ;--tw-ring-inset: ;--tw-ring-offset-width:0px;--tw-ring-offset-color:#fff;--tw-ring-color:rgba(59,130,246,.5);--tw-ring-offset-shadow:0 0 #0000;--tw-ring-shadow:0 0 #0000;--tw-shadow:0 0 #0000;--tw-shadow-colored:0 0 #0000;--tw-blur: ;--tw-brightness: ;--tw-contrast: ;--tw-grayscale: ;--tw-hue-rotate: ;--tw-invert: ;--tw-saturate: ;--tw-sepia: ;--tw-drop-shadow: ;--tw-backdrop-blur: ;--tw-backdrop-brightness: ;--tw-backdrop-contrast: ;--tw-backdrop-grayscale: ;--tw-backdrop-hue-rotate: ;--tw-backdrop-invert: ;--tw-backdrop-opacity: ;--tw-backdrop-saturate: ;--tw-backdrop-sepia: ;--tw-contain-size: ;--tw-contain-layout: ;--tw-contain-paint: ;--tw-contain-style: }
        
        /*! tailwindcss v3.4.17 | MIT License | https://tailwindcss.com*/*,:after,:before{box-sizing:border-box;border:0 solid #e7e7f0}:after,:before{--tw-content:""}:host,html{line-height:1.5;-webkit-text-size-adjust:100%;-moz-tab-size:4;-o-tab-size:4;tab-size:4;font-family:ui-sans-serif,system-ui,sans-serif,Apple Color Emoji,Segoe UI Emoji,Segoe UI Symbol,Noto Color Emoji;font-feature-settings:normal;font-variation-settings:normal;-webkit-tap-highlight-color:transparent}body{margin:0;line-height:inherit}hr{height:0;color:inherit;border-top-width:1px}abbr:where([title]){-webkit-text-decoration:underline dotted;text-decoration:underline dotted}h1,h2,h3,h4,h5,h6{font-size:inherit;font-weight:inherit}a{color:inherit;text-decoration:inherit}b,strong{font-weight:bolder}code,kbd,pre,samp{font-family:ui-monospace,SFMono-Regular,Menlo,Monaco,Consolas,Liberation Mono,Courier New,monospace;font-feature-settings:normal;font-variation-settings:normal;font-size:1em}small{font-size:80%}sub,sup{font-size:75%;line-height:0;position:relative;vertical-align:baseline}sub{bottom:-.25em}sup{top:-.5em}table{text-indent:0;border-color:inherit;border-collapse:collapse}button,input,optgroup,select,textarea{font-family:inherit;font-feature-settings:inherit;font-variation-settings:inherit;font-size:100%;font-weight:inherit;line-height:inherit;letter-spacing:inherit;color:inherit;margin:0;padding:0}button,select{text-transform:none}button,input:where([type=button]),input:where([type=reset]),input:where([type=submit]){-webkit-appearance:button;background-color:transparent;background-image:none}:-moz-focusring{outline:auto}:-moz-ui-invalid{box-shadow:none}progress{vertical-align:baseline}::-webkit-inner-spin-button,::-webkit-outer-spin-button{height:auto}[type=search]{-webkit-appearance:textfield;outline-offset:-2px}::-webkit-search-decoration{-webkit-appearance:none}::-webkit-file-upload-button{-webkit-appearance:button;font:inherit}summary{display:list-item}blockquote,dd,dl,figure,h1,h2,h3,h4,h5,h6,hr,p,pre{margin:0}fieldset{margin:0}fieldset,legend{padding:0}menu,ol,ul{list-style:none;margin:0;padding:0}dialog{padding:0}textarea{resize:vertical}input::-moz-placeholder,textarea::-moz-placeholder{opacity:1;color:#a8a8b8}input::placeholder,textarea::placeholder{opacity:1;color:#a8a8b8}[role=button],button{cursor:pointer}:disabled{cursor:default}audio,canvas,embed,iframe,img,object,svg,video{display:block;vertical-align:middle}img,video{max-width:100%;height:auto}[hidden]:where(:not([hidden=until-found])){display:none}:root{--card-radius:0.75rem;--btn-radius:var(--card-radius);--badge-radius:var(--btn-radius);--input-radius:var(--btn-radius);--avatar-radius:9999px;--annonce-radius:var(--avatar-radius);--ui-border-color:#1f1f31;--btn-border:#1f1f31;--badge-border:var(--btn-border);--input-border:var(--ui-border-color);--ui-disabled-border:#121220;--ui-error-border:#e11d48;--ui-success-border:#65a30d;--input-outline:#4f46e5;--ui-bg:rgb(18 18 32/var(--ui-bg-opacity));--ui-soft-bg:#1f1f31;--overlay-bg:rgba(2,2,13,.25);--input-bg:var(--ui-soft-bg);--ui-disabled-bg:#121220;--card-padding:1.5rem;--display-text-color:#fff;--title-text-color:var(--display-text-color);--body-text-color:#d6d6e1;--caption-text-color:#6e6e81;--placeholder-text-color:#4d4d5f;--ui-bg-opacity:1;color:var(--body-text-color)}*,.border{border-color:var(--ui-border-color)}button:disabled{border:none!important;background:var(--ui-disabled-bg)!important;background-image:none!important;box-shadow:none!important;color:var(--placeholder-text-color)!important;pointer-events:none!important}button:disabled:before{content:var(--tw-content);display:none}a:focus-visible,button:focus-visible{outline-width:2px;outline-offset:2px;outline-color:#4f46e5}a:focus-visible:focus-visible,button:focus-visible:focus-visible{outline-style:solid}input:user-invalid,select:user-invalid,textarea:user-invalid{--input-border:var(--ui-error-border);--ui-border-color:var(--ui-error-border);--input-outline:var(--ui-error-border);--title-text-color:#fb7185}[data-rounded=none]{--card-radius:0px;--avatar-radius:0px}[data-rounded=default]{--card-radius:0.25rem}[data-rounded=small]{--card-radius:0.125rem}[data-rounded=medium]{--card-radius:0.375rem}[data-rounded=large]{--card-radius:0.5rem}[data-rounded=xlarge]{--card-radius:0.75rem}[data-rounded="2xlarge"]{--card-radius:1rem;--input-radius:0.75rem}[data-rounded="3xlarge"]{--card-radius:1.5rem;--input-radius:0.75rem}[data-rounded=full]{--card-radius:1.5rem;--btn-radius:9999px;--input-radius:1rem}[data-shade=glassy]{--ui-bd-blur:40px;--ui-bg-opacity:0.75;--ui-bg:rgb(58 58 75/var(--ui-bg-opacity));--ui-border-color:rgba(250,250,254,.1);--ui-soft-bg:rgba(77,77,95,.5)}[data-shade="800"]{--ui-border-color:#3a3a4b;--ui-bg:#1f1f31;--ui-soft-bg:#121220}[data-shade="900"]{--ui-border-color:#1f1f31;--ui-bg:#121220;--ui-soft-bg:#1f1f31}[data-shade="950"]{--ui-border-color:#1f1f31;--ui-bg:#02020d;--ui-soft-bg:#1f1f31}.container{width:100%}@media (min-width:640px){.container{max-width:640px}}@media (min-width:768px){.container{max-width:768px}}@media (min-width:1024px){.container{max-width:1024px}}@media (min-width:1280px){.container{max-width:1280px}}@media (min-width:1536px){.container{max-width:1536px}}.icon-\[tabler--rss\]{display:inline-block;width:1em;height:1em;background-color:currentColor;-webkit-mask-image:var(--svg);mask-image:var(--svg);-webkit-mask-repeat:no-repeat;mask-repeat:no-repeat;-webkit-mask-size:100% 100%;mask-size:100% 100%;--svg:url("data:image/svg+xml;charset=utf-8,%3Csvg xmlns='http://www.w3.org/2000/svg' width='24' height='24'%3E%3Cpath fill='none' stroke='%23000' stroke-linecap='round' stroke-linejoin='round' stroke-width='2' d='M4 19a1 1 0 1 0 2 0 1 1 0 1 0-2 0M4 4a16 16 0 0 1 16 16M4 11a9 9 0 0 1 9 9'/%3E%3C/svg%3E")}.link{--tw-text-opacity:1;color:rgb(129 140 248/var(--tw-text-opacity,1));transition-property:color,background-color,border-color,text-decoration-color,fill,stroke,opacity,box-shadow,transform,filter,-webkit-backdrop-filter;transition-property:color,background-color,border-color,text-decoration-color,fill,stroke,opacity,box-shadow,transform,filter,backdrop-filter;transition-property:color,background-color,border-color,text-decoration-color,fill,stroke,opacity,box-shadow,transform,filter,backdrop-filter,-webkit-backdrop-filter;transition-timing-function:cubic-bezier(.4,0,.2,1);transition-duration:.15s}.link.variant-ghost:hover,.link.variant-underlined{text-decoration-line:underline}.link.variant-animated{position:relative}.link.variant-animated:before{position:absolute;left:0;right:0;bottom:0;height:1px;transform-origin:right;--tw-scale-x:0;transform:translate(var(--tw-translate-x),var(--tw-translate-y)) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y));transition-property:color,background-color,border-color,text-decoration-color,fill,stroke,opacity,box-shadow,transform,filter,-webkit-backdrop-filter;transition-property:color,background-color,border-color,text-decoration-color,fill,stroke,opacity,box-shadow,transform,filter,backdrop-filter;transition-property:color,background-color,border-color,text-decoration-color,fill,stroke,opacity,box-shadow,transform,filter,backdrop-filter,-webkit-backdrop-filter;transition-timing-function:cubic-bezier(.4,0,.2,1);content:var(--tw-content);transition-duration:.2s}.link.variant-animated:hover:before{transform-origin:left;content:var(--tw-content);--tw-scale-x:1;transform:translate(var(--tw-translate-x),var(--tw-translate-y)) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y))}.link.intent-info{--tw-text-opacity:1;color:rgb(96 165 250/var(--tw-text-opacity,1))}.link.intent-neutral{--tw-text-opacity:1;color:rgb(255 255 255/var(--tw-text-opacity,1))}.link.variant-animated.intent-neutral:before{content:var(--tw-content);background-color:hsla(0,0%,100%,.5)}.link.variant-animated.intent-info:before{content:var(--tw-content);--tw-bg-opacity:1;background-color:rgb(37 99 235/var(--tw-bg-opacity,1))}.link.variant-animated.intent-primary:before{content:var(--tw-content);--tw-bg-opacity:1;background-color:rgb(79 70 229/var(--tw-bg-opacity,1))}.link.variant-ghost.intent-neutral,.link.variant-underlined.intent-neutral{text-decoration-color:hsla(0,0%,100%,.5)}.mx-auto{margin-left:auto;margin-right:auto}.my-2{margin-top:.5rem;margin-bottom:.5rem}.my-6{margin-top:1.5rem;margin-bottom:1.5rem}.-mt-5{margin-top:-1.25rem}.ml-4{margin-left:1rem}.mr-1{margin-right:.25rem}.mr-2{margin-right:.5rem}.mt-1{margin-top:.25rem}.block{display:block}.inline-block{display:inline-block}.inline{display:inline}.flex{display:flex}.hidden{display:none}.h-8{height:2rem}.min-h-screen{min-height:100vh}.min-h-svh{min-height:100svh}.w-24{width:6rem}.w-8{width:2rem}.max-w-full{max-width:100%}.max-w-screen-lg{max-width:1024px}.flex-1{flex:1 1 0%}.grow{flex-grow:1}.cursor-pointer{cursor:pointer}.flex-col{flex-direction:column}.flex-wrap{flex-wrap:wrap}.items-start{align-items:flex-start}.justify-center{justify-content:center}.justify-between{justify-content:space-between}.gap-1{gap:.25rem}.gap-2{gap:.5rem}.gap-x-4{-moz-column-gap:1rem;column-gap:1rem}.gap-y-2{row-gap:.5rem}.space-y-2>:not([hidden])~:not([hidden]){--tw-space-y-reverse:0;margin-top:calc(.5rem*(1 - var(--tw-space-y-reverse)));margin-bottom:calc(.5rem*var(--tw-space-y-reverse))}.space-y-4>:not([hidden])~:not([hidden]){--tw-space-y-reverse:0;margin-top:calc(1rem*(1 - var(--tw-space-y-reverse)));margin-bottom:calc(1rem*var(--tw-space-y-reverse))}.space-y-6>:not([hidden])~:not([hidden]){--tw-space-y-reverse:0;margin-top:calc(1.5rem*(1 - var(--tw-space-y-reverse)));margin-bottom:calc(1.5rem*var(--tw-space-y-reverse))}.overflow-hidden{overflow:hidden}.scroll-smooth{scroll-behavior:smooth}.truncate{overflow:hidden;text-overflow:ellipsis;white-space:nowrap}.bg-gray-925{--tw-bg-opacity:1;background-color:rgb(9 9 21/var(--tw-bg-opacity,1))}.bg-gradient-to-r{background-image:linear-gradient(to right,var(--tw-gradient-stops))}.from-primary-600{--tw-gradient-from:#4f46e5 var(--tw-gradient-from-position);--tw-gradient-to:rgba(79,70,229,0) var(--tw-gradient-to-position);--tw-gradient-stops:var(--tw-gradient-from),var(--tw-gradient-to)}.to-accent-400{--tw-gradient-to:#e879f9 var(--tw-gradient-to-position)}.bg-clip-text{-webkit-background-clip:text;background-clip:text}.p-1{padding:.25rem}.px-4{padding-left:1rem;padding-right:1rem}.py-2{padding-top:.5rem;padding-bottom:.5rem}.py-4{padding-top:1rem;padding-bottom:1rem}.py-6{padding-top:1.5rem;padding-bottom:1.5rem}.pb-2{padding-bottom:.5rem}.pt-2{padding-top:.5rem}.text-center{text-align:center}.font-sans{font-family:ui-sans-serif,system-ui,sans-serif,Apple Color Emoji,Segoe UI Emoji,Segoe UI Symbol,Noto Color Emoji}.text-2xl{font-size:1.5rem;line-height:2rem}.text-lg{font-size:1.125rem;line-height:1.75rem}.text-sm{font-size:.875rem;line-height:1.25rem}.font-bold{font-weight:700}.font-medium{font-weight:500}.font-semibold{font-weight:600}.leading-normal{line-height:1.5}.text-transparent{color:transparent}.antialiased{-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale}.text-title{color:var(--title-text-color)}.text-body{color:var(--body-text-color)}.\!text-caption{color:var(--caption-text-color)!important}.text-caption{color:var(--caption-text-color)}.dark{--display-text-color:#fff;--title-text-color:var(--display-text-color);--caption-text-color:#6e6e81;--body-text-color:#d6d6e1;--placeholder-text-color:#4d4d5f;--ui-border-color:#232323}[data-shade="900"]:where(.dark,.dark *),[data-shade="925"]:where(.dark,.dark *),[data-shade="950"]:where(.dark,.dark *){--ui-border-color:#383838}@media (min-width:640px){.sm\:gap-1{gap:.25rem}}@media (min-width:768px){.md\:flex-row{flex-direction:row}.md\:space-y-0>:not([hidden])~:not([hidden]){--tw-space-y-reverse:0;margin-top:calc(0px*(1 - var(--tw-space-y-reverse)));margin-bottom:calc(0px*var(--tw-space-y-reverse))}.md\:p-4{padding:1rem}.md\:px-6{padding-left:1.5rem;padding-right:1.5rem}.md\:pt-6{padding-top:1.5rem}}@media (min-width:1024px){.lg\:dark\:bg-gray-900:is(.dark *){--tw-bg-opacity:1;background-color:rgb(18 18 32/var(--tw-bg-opacity,1))}}</style></head><body class="bg-gray-925 min-h-screen min-h-svh font-sans leading-normal antialiased lg:dark:bg-gray-900"><main class="min-w-screen container mx-auto flex min-h-screen max-w-screen-lg flex-col px-4 py-6 md:px-6"><header class="space-y-2 pt-2 md:pt-6"><a title="{$title}" href="{$link}" target="_blank" rel="noopener noreferrer"><h1 class="flex text-2xl"><span class="icon-[tabler--rss] mr-2 h-8 w-8"/><span class="lg2:text-3xl from-primary-600 to-accent-400 inline-block bg-gradient-to-r bg-clip-text font-bold text-transparent"><xsl:value-of select="$title" disable-output-escaping="yes"/></span></h1></a><p class="text-body pt-2 text-lg py-4"><xsl:value-of select="$description" disable-output-escaping="yes"/></p><p class="text-caption text-sm">
              This RSS feed for the
              <a class="link intent-neutral variant-animated !text-caption font-bold" title="{$title}" href="{$link}" target="_blank" rel="noopener noreferrer"><xsl:value-of select="$title"/></a>
              website.
            </p><p class="text-body text-sm hidden" id="subscribe-links">
              You can subscribe this RSS feed by
              <a class="link intent-neutral variant-animated font-bold" title="Feedly" data-href="https://feedly.com/i/subscription/feed/" target="_blank" rel="noopener noreferrer">Feedly</a>,
              <a class="link intent-neutral variant-animated font-bold" title="Inoreader" data-href="https://www.inoreader.com/feed/" target="_blank" rel="noopener noreferrer">Inoreader</a>,
              <a class="link intent-neutral variant-animated font-bold" title="Newsblur" data-href="https://www.newsblur.com/?url=" target="_blank" rel="noopener noreferrer">Newsblur</a>,
              <a class="link intent-neutral variant-animated font-bold" title="Follow" data-href="follow://add?url=" rel="noopener noreferrer">Follow</a>,
              <a class="link intent-neutral variant-animated font-bold" title="RSS Reader" data-href="feed:" data-raw="true" rel="noopener noreferrer">RSS Reader</a>
              or
              <a class="link intent-neutral variant-animated font-bold" title="{$title} 's feed source" data-href="" data-raw="true" rel="noopener noreferrer">View Source</a>.
            </p><script>
              document.addEventListener('DOMContentLoaded', function () {
                document.querySelectorAll('a[data-href]').forEach(function (a) {
                  const url = new URL(location.href)
                  const feed = url.searchParams.get('url') || location.href
                  const raw = a.getAttribute('data-raw')
                  if (raw) {
                    a.href = a.getAttribute('data-href') + feed
                  } else {
                    a.href = a.getAttribute('data-href') + encodeURIComponent(feed)
                  }
                })
                document.getElementById('subscribe-links').classList.remove('hidden')
              })
            </script></header><hr class="my-6"/><section class="flex-1 space-y-6 p-1 md:p-4"><xsl:choose><xsl:when test="/rss/channel/item"><xsl:for-each select="/rss/channel/item"><article class="space-y-2"><details><summary class="max-w-full truncate"><xsl:if test="title"><h2 class="text-title inline cursor-pointer text-lg font-semibold"><xsl:value-of select="title" disable-output-escaping="yes"/></h2></xsl:if><xsl:if test="pubDate"><time class="text-caption ml-4 mt-1 block text-sm"><xsl:value-of select="pubDate"/></time></xsl:if></summary><div class="text-body px-4 py-2"><p class="my-2"><xsl:choose><xsl:when test="description"><xsl:value-of select="description" disable-output-escaping="yes"/></xsl:when></xsl:choose></p><xsl:if test="link"><a class="link variant-animated intent-neutral font-bold" href="{link}" target="_blank" rel="noopener noreferrer">
                            Read More
                          </a></xsl:if></div></details></article></xsl:for-each></xsl:when><xsl:when test="/atom:feed/atom:entry"><xsl:for-each select="/atom:feed/atom:entry"><article class="space-y-2"><details><summary class="max-w-full truncate"><xsl:if test="atom:title"><h2 class="text-title inline cursor-pointer text-lg font-semibold"><xsl:value-of select="atom:title" disable-output-escaping="yes"/></h2></xsl:if><xsl:if test="atom:updated"><time class="text-caption ml-4 mt-1 block text-sm"><xsl:value-of select="atom:updated"/></time></xsl:if></summary><div class="text-body px-4 py-2"><p class="my-2"><xsl:choose><xsl:when test="atom:summary"><xsl:value-of select="atom:summary" disable-output-escaping="yes"/></xsl:when><xsl:when test="atom:content"><xsl:value-of select="atom:content" disable-output-escaping="yes"/></xsl:when></xsl:choose></p><xsl:if test="atom:link/@href"><a class="link variant-animated intent-neutral font-bold" href="{atom:link/@href}" target="_blank" rel="noopener noreferrer">
                            Read More
                          </a></xsl:if></div></details></article></xsl:for-each></xsl:when></xsl:choose></section><hr class="my-6"/><footer><div class="flex flex-col justify-between space-y-4 md:flex-row md:space-y-0"><div class="space-y-4"><a class="flex text-2xl font-bold" href="https://rss.beauty" title="RSS.Beauty"><span class="text-title icon-[tabler--rss] mr-1 h-8 w-8"/><span class="text-title">RSS</span>.
                  <span class="from-primary-600 to-accent-400 bg-gradient-to-r bg-clip-text text-transparent">Beauty</span></a><div class="text-caption">Make Your RSS Beautiful</div></div><div class="space-y-4"><div class="flex flex-wrap gap-x-4 gap-y-2"><a class="link intent-neutral variant-animated" target="_blank" title="GitHub" href="https://github.com/ccbikai/RSS.Beauty">GitHub</a><a class="link intent-neutral variant-animated" target="_blank" title="X/Twitter" href="https://404.li/kai">X/Twitter</a></div><div class="text-title flex gap-1 overflow-hidden font-medium">
                  Made with ❤️‍🔥 By
                  <div class="flex items-start justify-center gap-2 text-center font-semibold sm:gap-1"><div class="block"><a href="https://html.zone" target="_blank" title="HTML.ZONE" class="block pb-2">HTML.ZONE</a><div class="-mt-5 grow overflow-hidden"><svg class="w-24" aria-hidden="true" height="22" viewBox="0 0 283 22" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M1.24715 19.3744C72.4051 10.3594 228.122 -4.71194 281.724 7.12332" stroke="url(#paint0_linear_pl)" stroke-width="4"/><defs><linearGradient id="paint0_linear_pl" x1="282" y1="5.49999" x2="40" y2="13" gradientUnits="userSpaceOnUse"><stop stop-color="#facc15"/><stop offset="1" stop-color="#a855f7"/></linearGradient></defs></svg></div></div></div></div></div></div></footer></main></body></html></xsl:template></xsl:stylesheet>
```

`两个文件内容里的文本部分请按照个人要求自行修改，应该不算太难，可以部署后对照实际效果进行文本部分的修改。`


### 11. 订阅文件乱码问题

`Hexo-generator-feed`插件生成的订阅文件在本地直接预览会出现乱码的问题，本插件也有该情况，虽然不影响上线后的效果，但是在执行`Hexo server`预览的过程中可能会导致无法显示美化后的预览效果，暂时无法解决，可以尝试先部署上线一次，然后再对照修改对应文本部分，或者采用`VSCode`插件`Live Server`，直接预览`hexo generate`生成的静态文件，实测可以规避乱码问题，方便预览效果进行修改。


### 12. 修改配置

然后，添加或修改`_config.yml`文件中的`feed`部分配置，如果之前没有使用可以参考我的配置：


``` bash
# 更加美观的RSS订阅源
# see：https://github.com/willow-god/hexo-pretty-feed
feed:
  enable: true
  content: false
  content_limit: 40
  type: atom
  path: atom.xml
  limit: 25
  pretty_atom_file: /config/feed/atom.xsl
  pretty_rss2_file: /config/feed/rss2.xsl
```

**具体相对地址需要看你的文件放置的位置，这里只是举个栗子！**


**一切妥当就可以尝试部署了，应该就可以达到心仪的效果啦！xsl文件也可以上网搜寻其他的文件内容，这里只是以一个现有的模板进行演示。**


::link-card
---
title: 本文原创LiuShen
description: LiuShen
icon: https://i1.wp.com/bixin.wuaze.com/i/2025/05/08/876672.webp
link: https://blog.liushen.fun/posts/caee2d9f
---
::


### 参考教程

::link-card
---
title: RSS.Beauty
description: Github
icon: https://biu.biuxin.com/2025/05/09/717977.webp
link: https://blog.liushen.fun/posts/caee2d9f
---
::

::link-card
---
title: hexo-generator-feed
description: Github
icon: https://biu.biuxin.com/2025/05/09/717977.webp
link: https://github.com/hexojs/hexo-generator-feed
---
::

::link-card
---
title: 让你的 RSS/Atom feed 更好看
icon: https://biu.200038.xyz/2024/09/19/040857.webp
description: Spike Leung
link: https://taxodium.ink/pretty-feed.html
---
::


### 结尾来个图片

![哲风壁纸](https://biu.200038.xyz/2025/04/23/815251.webp)


图片来自[哲风壁纸](https://haowallpaper.com/)