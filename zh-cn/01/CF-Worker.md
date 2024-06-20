## 一、前言

本期主要来简单介绍如何利用**cf worker**搭建免费的**vless**节点，部署过程应该比较简单，一方面帮助新手快速上手，另一方面分享自己的使用心得，
主要是解决目前面临的两大问题，一是按照以往的代码搭建可能会出现**1101**的错误，另一个是很多人搭建的vless节点不能100%使用**ChatGPT**以及观看**奈飞**。

## 二、实现原理

简单说明一下实现原理，因为**cloudflare**作为一家良心云，他家的worker可以运行**JavaScript**代码，因此就有一些”别有用心“的人（大神们）编写代码部署在worker上，为数据包添加vlessheader信息，达到vless代理转发的目的。
由于cloudflare在国内某种程度能访问，而CF Worker又能访问GFW以外的信息，所以通过CF Worker来转发数据就能**实现翻墙**的效果。

## 三、补充说明

免费的东西总不可能很完美，CF Worker限制每天**10万个10ms CPU time**的请求，但对于个人使用应该足够了。另外由于cf bug，现在cf worker不能直接访问cf托管的网站，比如**speedtest、ChatGPT**等，所以需要配置一个**反代ip**，用来转发cf的流量。
因此我们在实际cf worker搭建中，不仅要**优选ip**，最好还要搭配一个**反代ip**来使用。至于能不能解锁ChatGPT，关键在于你的**反代ip**或**反代域名**。目前我收集整理了一些反代域名，实际使用下来，因为ip在变化，有时候的ip能解锁ChatGPT，因此你只需要将反代域名此时对应的ip提取出来，就能使用ChatGPT了，当然需要你自行多次尝试了！毕竟免费的就要**付出时间和精力**来折腾。

## 四、搭建流程视频

具体演示详情请通过本频道YouTube视频观看获取：[CF Work搭建免费节点系列一，利用源项目作者zizifn脚本进行部署，稳定高效，100%解锁ChatGPT和奈飞流媒体](https://www.youtube.com/watch?v=L46M6Xyahm0)

## 五、相关内容

### 1.cloudflare官网

🌐**网址**：https://dash.cloudflare.com/

### 2.UUID在线生成网站

🌐**网址**：https://1024tools.com/uuid

### 3.在线优选ip网站

🌐**网址**：https://stock.hostmonit.com/CloudFlareYes

### 4.反代域名提取反代IP网站

🌐**网址**：https://ping.chinaz.com/

### 5.两种运行模式

**vless+ws有**：7个http端口可任意选择：`80、8080、8880、2052、2082、2086、2095`

**vless+ws+tls有**：6个 https 端口可任意选择：`443、8443、2053、2083、2087、2096`

### 六.优选域名

```优选域名
shopify.com
time.is
icook.hk
icook.tw
ip.sb
japan.com
malaysia.com
russia.com
singapore.com
skk.moe
www.visa.com
www.visa.com.sg
www.visa.com.hk
www.visa.com.tw
www.visa.co.jp
www.visakorea.com
www.gco.gov.qa
www.gov.se
www.gov.ua
www.digitalocean.com
www.csgo.com
www.shopify.com
www.whoer.net
www.whatismyip.com
www.ipget.net
www.hugedomains.com
www.udacity.com
www.4chan.org
www.okcupid.com
www.glassdoor.com
www.udemy.com
www.baipiao.eu.org
cdn.anycast.eu.org
cdn-all.xn--b6gac.eu.org
cdn-b100.xn--b6gac.eu.org
xn--b6gac.eu.org
edgetunnel.anycast.eu.org
alejandracaiccedo.com
nc.gocada.co
log.bpminecraft.com
www.boba88slot.com
gur.gov.ua
www.zsu.gov.ua
www.iakeys.com
edtunnel-dgp.pages.dev
www.d-555.com
fbi.gov
```



### 七.八个反代cf 域名

```反代cf 域名
edgetunnel.anycast.eu.org
cdn-all.xn--b6gac.eu.org
cdn.xn--b6gac.eu.org
cdn-b100.xn--b6gac.eu.org
cdn.anycast.eu.org
cdn-all.xijingping.link
workers.cloudflare.cyou
bestproxy.onecf.eu.org
```



### 八.解锁ChatGPT和奈飞的反代ip组（目前稳定使用半年）

```
146.70.175.98
146.70.175.99
146.70.175.100
146.70.175.101
146.70.175.102
146.70.175.103
146.70.175.104
146.70.175.116
```



### 九.优选ip工具（如果无法打开，建议开启全局代理模式）

🌐**下载链接**：https://drive.google.com/file/d/1Q8dcptZ2RxfzLwPqpqWwu8xBnBlb1071/view?usp=drivesdk

### 十.本期搭建代码

🌐**下载链接**：https://raw.githubusercontent.com/zizifn/edgetunnel/main/src/worker-vless.js