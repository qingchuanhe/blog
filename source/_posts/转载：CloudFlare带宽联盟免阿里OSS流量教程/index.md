---
title: 转载：CloudFlare带宽联盟免阿里OSS流量教程
date: 2026-08-06 13:37:00 +0800
author: 清川
top: false
cover: 'https://oss.567921.xyz/siyuan/20260725164201.jpg'
tags:
  - OSS
  - CloudFlare
  - 阿里ESA
categories:
  - 笔记
---

# 转载：CloudFlare带宽联盟免阿里OSS流量教程

---

- CloudFlare带宽联盟免阿里OSS流量教程
- [https://tor.hk/post/FreeOSS](https://tor.hk/post/FreeOSS)
- 使用Cloudflare带宽联盟免去阿里云OSS香港地区的流量费用，实测800G流量无账单。

---

## CloudFlare带宽联盟免阿里OSS流量教程

## 感谢赞助

本文章由[快财宝](https://www.kuaicaibao.com/)赞助，感谢支持。赞助用于测试免流。

## 带宽联盟

**Cloudflare 带宽联盟（Bandwidth Alliance）**  是一个由 Cloudflare 发起的合作计划，联合多家云服务商和网络公司，目的是**降低甚至免除数据传输（带宽 / 出站流量）费用**具体可以查看官方页[Cloudflare云服务_数据传输_高速云数据传输服务_|Cloudflare中国官网 | Cloudflare](https://www.cloudflare-cn.com/bandwidth-alliance/)

阿里云关于带宽联盟免流的回应

![阿里云对于免流](https://oss.567921.xyz/siyuan/20260725164153.png)

## 实测

本文耗费两台服务器一台美国，一天香港，耗时约1天，测试结果cloudflare 800G流量，oss储存桶700+，未扣费也无账单。

可以放心开嫖。

下面看图

![](https://oss.567921.xyz/siyuan/20260725164222.jpg)

在凌晨开刷![](https://oss.567921.xyz/siyuan/20260725164139.jpg)

等结果，就是下面的，时间过去1天，阿里并没有任何的账单。

![CloudFlare带宽联盟免阿里OSS流量教程](https://oss.567921.xyz/siyuan/20260725164201.jpg)

![](https://oss.567921.xyz/siyuan/20260725164204.jpg)

cf 800G流量有700多G都回源，也没有产生账单。

注意：只针对阿里oss海外地域的储存桶

## 正文

本文章教你使用cloudflare的带宽联盟免去oss香港地区的流量费用，再也不用担心第二天起来破产了。

看一下效果图

![Oss流量](https://oss.567921.xyz/siyuan/20260725164148.png)

这么多流量，都没有流量费的，我们来配置一下。

### 准备工作

1.一个阿里云香港地区的储存桶，公共读权限，配置跨域。

2.一个在CloudFlare上已经托管的域名

### OSS控制台

首先创建一个储存桶，来到阿里OSS控制台

![创建bucket](https://oss.567921.xyz/siyuan/20260725164214.png)

![](https://oss.567921.xyz/siyuan/20260725164207.png)

创建完成后进入bucket，来到权限控制，将阻止公共访问关闭

![](https://oss.567921.xyz/siyuan/20260725164209.png)

> ⚠️ **此方式已废弃/不推荐使用**

~~在来到读写权限，设置为公共读~~

![权限设置](https://oss.567921.xyz/siyuan/20260725164141.png)

更新2026.7.24

~~由微信用户名清川提供的思路，可以做到比之前更加安全的方案 这里感谢大佬的￥20赞助。~~

![wechat](https://oss.567921.xyz/siyuan/20260725164150.png)

这里的Bucket ACL也就是读写权限，改为私有

![Bucket ACl](https://oss.567921.xyz/siyuan/20260725164159.png)

然后我们来到bucket授权策略 这里需要把cloudflare的ip添加进来，[cloudflare ip范围](https://www.cloudflare-cn.com/ips/)

也就是下面的这张图片

![ips](https://oss.567921.xyz/siyuan/20260725164220.png)

当然，官方也提供了文本的地址[ipv4](https://www.cloudflare-cn.com/ips-v4/#) | [ipv6](https://www.cloudflare-cn.com/ips-v6/#)

我也提供了一份直接复制粘贴即可

`173.245.48.0/20,103.21.244.0/22,103.22.200.0/22,103.31.4.0/22,141.101.64.0/18,108.162.192.0/18,190.93.240.0/20,188.114.96.0/20,197.234.240.0/22,198.41.128.0/17,162.158.0.0/15,104.16.0.0/13,104.24.0.0/14,172.64.0.0/13,131.0.72.0/22,2400:cb00::/32,2606:4700::/32,2803:f800::/32,2405:b500::/32,2405:8100::/32,2a06:98c0::/29,2c0f:f248::/32`

下面就是具体配置图片，很简单

![授权](https://oss.567921.xyz/siyuan/20260725164146.png)

~~提醒：即使使用这个方案，可以提高很大的安全性与抗风险能力,但是还是需要各位保护好自己的bucket name以及region，一旦泄露追悔莫及。~~

以上就是更新的全部内容

在来到下方数据安全中的跨域设置，设置跨域

![跨域设置](https://oss.567921.xyz/siyuan/20260725164155.png)

在来到域名管理绑定自己的自定义域名

![域名绑定](https://oss.567921.xyz/siyuan/20260725164212.png)

### CloudFlare解析

然后来到CloudFlare设置域名解析，必须开启小黄云

![域名解析](https://oss.567921.xyz/siyuan/20260725164217.png)

### SSL绑定

记得申请一张SSL证书，绑定在oss控制台

![域名绑定](https://oss.567921.xyz/siyuan/20260725164143.png)

### 测试

下面上传文件测试即可

### 进阶白嫖方法

目前CloudFlare已经成功获取到了oss文件，但是CloudFlare由于一些原因在国内访问并不流畅，所以我们可以使用阿里esa加速CloudFlare的域名，在通过Dns全球分流实现全球的免流。仅有储存费用和访问费用。可以自己去配置。

看图

![](https://oss.567921.xyz/siyuan/20260725164157.png)
