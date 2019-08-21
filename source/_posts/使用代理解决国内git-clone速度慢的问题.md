---
title: 使用代理解决国内git clone速度慢的问题
date: 2019-08-21 16:26:28
tags:
  - github
categories:
  - git
index_img: '/img/github.jpeg'
---

众所周知，国内访问GitHub速度感人，无论clone还是push操作等待时间都让人抓狂，不过如果你有网络代理工具，则可利用代理接管所有git操作
<!-- more -->
---

# 解决方法如下

## 准备
* 准备好代理工具，如clash，shadowsocks等


## 步骤
1. 开启代理工具，查看对应代理工具的端口号
	- clash 一般为7891
	![clash](/img/Jietu20190821-165505.jpg)

	- shadowsocks 一般为1080

2. 打开终端（windows系统可打开powershell或其cmd），执行以下命令
```
git config --global http.proxy socks5://127.0.0.1:1080
git config --global https.proxy socks5://127.0.0.1:1080
```

完成后再尝试git clone等操作会发现速度明显提升
> 注意： 经过这种操作后每次执行git操作都要确保已经开启了代理工具，否则可能会报无法连接的错误

## 几个问题
1. 以后每次执行git命令都需要开启代理，如果有时代理又不能使用时，我们需要取消git代理，可在终端中执行以下命令
```
git config --global --unset http.proxy
git config --global --unset https.proxy
```
2. 上述方法是挂了全局代理，即只要是git操作就通过代理，但有时我们需要访问的不是GitHub而是国内的码云等代码仓库，使用代理反而很慢，此时更好的方法是只对github进行代理，不会影响国内仓库
```
git config --global http.https://github.com.proxy socks5://127.0.0.1:1080
git config --global https.https://github.com.proxy socks5://127.0.0.1:1080
```
---
<center>本文完结</center>