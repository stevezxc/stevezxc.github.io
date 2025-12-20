---
layout: post
title: "使用 VPS 搭建自建机场
date: 2025-12-20 16:58:54 +0800
modified_date: now
author: Stevezxc
categories: code
---

最近天朝对机场中转入口的通报越来越严，严重影响全天候挂代理的使用体验。遂决定自建机场。

<!--more-->

## VPS 提供商

由于是作为备用机场，只需关键时能用就行，这里推荐一个免费的 [IPv6 only VPS](https://hax.co.id/)，缺点是需要半夜抢机器，且需要配置 Warp 才能使用 IPv4。附上我使用的 [Warp 脚本](https://gitlab.com/fscarmen/warp/)。

## 搭建机场

为了在非常时期抗封锁，选用 VLESS-Vision-REALITY 方案，附上我使用的 [配置脚本](https://github.com/zxcvos/Xray-script/)。

- 一定要禁用回国流量；
- 建议使用 443 端口，高位端口据称容易受到 GFW 的怀疑，因为许多人用所谓一键配置时都选择高位端口；
- SNI 建议不要使用许多人推崇的大型网站的域名，原因同上，应当使用 VPS 所在地的一些其他网站；
- 不要使用 HTTP 下的各种面板，和裸奔没有区别。

## 客户端配置

需要使用支持 REALITY 的客户端，比如 Xray 核心，V2Ray 核心是不支持的。而 Xray 不支持负载均衡，我又不想迁移到 Clash 或 Sing-box，所以日常仍然使用 V2Ray，只在需要时切换到 Xray。

## 参见

[XTLS Xray examples](https://github.com/XTLS/Xray-examples)
