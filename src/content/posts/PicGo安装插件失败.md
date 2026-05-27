---
title: 是坑我就踩：PicGo 安装插件失败
published: 2026-05-27
pinned: false
description: PicGo 安装 gitee-uploader 1.1.2 插件失败
tags: [PicGo, npm, 踩坑系列]
category: 是坑我就踩
draft: false
image: ./images/firefly3.avif
---

## 问题现象

本来想用 PicGo + Gitee 来配置图床，此时还未意识到用 Gitee 当作图床的诸多限制，网上找了教程，需要在 PicGo 中安装一个插件 `gitee-uploader`。

在插件设置中安装，死活安装不上，点击安装后状态变成安装中，过了几秒状态又回到安装，软件界面上也没有任何提示。

## 解决

首先，在 PicGo 中查看日志：

![查看日志](https://cdn.jsdelivr.net/gh/7Keep-Confi/img_bed_01/20260527211407225.png)

打开日志文件，查看报错信息：

![查看报错信息](https://cdn.jsdelivr.net/gh/7Keep-Confi/img_bed_01/20260527211619261.png)

```
EPERM: operation not permitted, open '[node 有关的文件路径]'
```

可以发现是权限问题，**没有写入权限** 访问 npm 缓存目录。

那我个人的解决方式就是退出 PicGo，再用管理员身份运行 PicGo 。

![用管理员身份运行](https://cdn.jsdelivr.net/gh/7Keep-Confi/img_bed_01/20260527212212888.png)

这时候再去安装插件就畅通无阻了，安装完成后在插件设置会显示已安装的插件。

## 其他分析

其实这个权限问题并不是第一次见，我在安装其他工具的拓展时比如 `newman` 也遇到过，感觉应该是 npm 默认目录和 Windows 权限冲突了，问了 AI 这个问题，给我的响应是：

Node.js/npm 环境安装在 `D:\Tools\Work\newman\` 这个自定义路径下，而不是 Windows 默认的用户目录（`C:\Users\你的用户名\AppData\Roaming\npm`）

暂时先不改，不知道会不会影响到全局还是其他东西的配置。