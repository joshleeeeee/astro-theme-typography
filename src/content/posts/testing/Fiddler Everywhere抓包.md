---
title: How to Using FiddlerEverywhere
tags:
  - 软件测试
categories:
  - 测试
pubDate: 2021-12-30 10:43:04
---


# Fiddler EveryWhere 环境安装

## 1. 安装

Fiddler 功能强大，同时占用空间小，能记录所有的客户端和服务器端的 http 和https 请求，方便测试人员进行接口测试。官方下载地址：[https://www.telerik.com/fiddler/fiddler-everywhere](https://www.telerik.com/fiddler/fiddler-everywhere)
由于笔者使用的是Mac OS，而经典版的只支持Windows，所以我们这里下载最新版的Fiddler EveryWhere，安装步骤如下：

1. 打开下载好的Flddler Everywhere.dmg, 弹出如下界面，点击Agree同意

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640593811469-23c32878-d752-4194-ad64-440e49715942.png#clientId=u91997ebf-e755-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=462&id=u65574b15&margin=%5Bobject%20Object%5D&name=image.png&originHeight=924&originWidth=1292&originalType=binary&ratio=1&rotation=0&showTitle=false&size=238581&status=done&style=none&taskId=ue5ead5d1-6ea0-451e-9e83-e8502853275&title=&width=646)

<center>图1 同意许可证协议</center>

2. 将左侧Fiddler的LOGO拖拽到右侧的Applications文件夹即可完成安装

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640593831598-f0e34881-5d53-4a6a-b09e-9608a0e7bd44.png#clientId=u91997ebf-e755-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=260&id=u78250005&margin=%5Bobject%20Object%5D&name=image.png&originHeight=520&originWidth=1000&originalType=binary&ratio=1&rotation=0&showTitle=false&size=143184&status=done&style=none&taskId=u2f4daead-5a3a-48f2-beee-a8bdbcb51af&title=&width=500)

<center>图2 拖拽到Applications完成安装</center>

3. 软件安装过程非常简单，读者可自行完成安装。笔者安装的 Fiddler Everywhere 为 3.0.1 版。安装完成后，启动 Fiddler Everywhere，出现如下图的欢迎界面（需要注册并登陆）。意思是你可以有三种方法去使用Fiddler：

- [System Traffic Capturing（系统流量捕捉）](https://docs.telerik.com/fiddler-everywhere/traffic/capture-traffic#system-capturing)
- [Preconfigured Browser Capturing（预先配置的浏览器捕捉）](https://docs.telerik.com/fiddler-everywhere/traffic/capture-traffic#preconfigured-browser-capturing)
- [Debug mobile devices（调试手机设备）](https://docs.telerik.com/fiddler-everywhere/traffic/configure-android)

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640610425935-14fa3ade-cfbc-498a-a95a-ea6e35a91c0e.png#clientId=u91997ebf-e755-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=953&id=u58ccdcc3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1906&originWidth=3360&originalType=binary&ratio=1&rotation=0&showTitle=false&size=739273&status=done&style=none&taskId=ub2fb9fbc-24dd-4fb9-8a28-e2ad414ac8c&title=&width=1680)
<center>图3 欢迎界面</center>

## 2. 使用

程序界面如下图所示：
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640615048826-4606e2fe-b4d1-4640-86de-e580e43c7efe.png#clientId=u0480e3e3-b0c3-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=430&id=u8ed2e18e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=859&originWidth=1373&originalType=binary&ratio=1&rotation=0&showTitle=false&size=564110&status=done&style=none&taskId=u7ed7e4e3-23db-4148-9f5f-afe4e60a8fc&title=&width=686.5)
图4 Fidder Everywhere界面示意图

- 工具条：即选项卡，可以选择实时流量抓取区（Live Traffic）和对接口进行测试（Composer），Fiddler Everywhere 的 Composer 比较类似 Postman ，接口测试起来非常方便
- 会话区：Fiddler Everywhere 捕获的流量会实时呈现在这里
- 请求存储区：用于存储接口

目前许多网站都会采用https 协议来进行传输，相比于 http 协议，主要是增加了传输加密和安全认证等功能，从而提高了传输的安全性。但需要注意的是，Fiddler 刚安装完成是并不能显示 https 协议的会话，需要进行相应的设置，并进行证书安装。Mac下操作步骤如下：

1. 进入设置

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640615943351-7d8fdaaa-1f92-4ed9-b21f-8e03edf02e4a.png#clientId=u0480e3e3-b0c3-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=207&id=ucd6a5d79&margin=%5Bobject%20Object%5D&name=image.png&originHeight=413&originWidth=660&originalType=binary&ratio=1&rotation=0&showTitle=false&size=44416&status=done&style=none&taskId=ub7c9bfa6-accc-43ff-9824-5212f1cc15d&title=&width=330)
图5 进入设置

2. `Trust root certificate`，信任根证书，并勾选`Capture HTTPS traffic`和`Ignore server certificate errors(unsafe)`即可，如下图所示：

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640616079974-b82653d1-c1a3-47e1-84d6-d4ef5a0c2ee9.png#clientId=u0480e3e3-b0c3-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=371&id=ucdab4c85&margin=%5Bobject%20Object%5D&name=image.png&originHeight=741&originWidth=815&originalType=binary&ratio=1&rotation=0&showTitle=false&size=62167&status=done&style=none&taskId=u5f58a4a9-daea-4b9a-9ef3-b9c2abb8f89&title=&width=407.5)
图6 设置

> **为什么要先学fiddler？**
> 学习接口测试必学http协议，如果直接先讲协议，为了更好的理解协议，先从抓包开始。结合抓包工具讲http协议更容易学一些。
> **为什么使用Fiddler Everywhere而不是经典版的Fiddler？**
> Fiddler Everywhere是一款跨平台（Windows、Mac、Linux）的Web调试代理工具，**本文将用Mac系统进行演示**

# Fiddler Everywhere 的使用

## 1. 证书问题

### 为什么需要证书？

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640657551777-7933a31f-cf65-415f-b510-26da8db10270.png#clientId=ud5a02840-c4ce-4&from=paste&id=u0f9bb090&margin=%5Bobject%20Object%5D&name=image.png&originHeight=629&originWidth=1253&originalType=binary&ratio=1&size=346351&status=done&style=none&taskId=u8c5067a6-2133-4b94-a0a8-590dbb2155f)
先说结论：**捕获HTTPS必须要导入Fiddler的证书。**
知道什么是证书之前需要了解下 "非对称加密"

- 对称加密：客户端和服务器用一个秘钥加密和解密。对称加密效率高
- 非对称加密：将公钥公布于众，客户端拿公钥加密，服务器拿自己的私钥解密，这样即使数据被截获，别人也解密不出明文内容。效率低。

非对称加密有两个秘钥，公钥和私钥，而这两个秘钥只要用一个加密，另一个就能解密，我们正常加密数据用公钥加密，用私钥解密
而我们还有一种用法就是服务器发数据用私钥加密，客户端用公钥解密，那么客户如果用公钥正确解密出数据，那么就证明这个数据一定是服务器发的，因为私钥只有它知道，这个过程我们一般不叫加密，叫签名，也就是服务器对数据签个名，代表这个确确实实是它发的。
其实我们正常情况下因为对称加密效率虽高，但是不安全，因为它告诉对方秘钥的时候这个秘钥容易被截获，但是我们如果用非对称加密，安全是安全，效率又太低，所以一般采用对称加密来加密数据，非对称加密配送对称加密的秘钥。
因为公钥是在网络上进行传输的，那么假如遭遇了如下图所示的中间人攻击，那么A的私钥就可能是伪造的。那么如何验证公钥的合法性呢？------证书

#### 什么是证书？

证书就是由认证机构，采用它们自己的私钥，对发送方的公钥和发送方的信息进行数字加密。各大CA（认证机构）的证书已经默认被添加到了浏览器和操作系统中。
服务器生成自己的密匙对——公钥和私钥
服务器在认证机构注册自己的公钥
认证机构（CA）用自己机构的私钥对，服务器的公钥进行数字签名并生成证书（里面带了这个签名过得公钥和服务器一些信息）
认证机构把证书给客户端
客户端用认证机构的公钥验证数字签名
认证成功后用里面带的服务器的公钥加密并发消息给服务器
服务器用自己的私钥解密
这样一来就可以解决数据传输的安全问题了
**问题：**

1. 如果黑客在服务器在认证机构注册公钥的时候截取数据呢？

这个完全不用担心，CA证书的申请，流程很多，而且较为严格，比如准备很多文件，再比如CA那边如果通过后还会要申请方这边的管理员验证之类的。

2.  认证机构的公钥咋传输的？如果黑客改了呢？
     如果改了那么这个证书就不会验证成功，其实各大CA的公钥已经在系统和浏览器中内置了。看下边的例子：

百度的证书信息：
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640657019644-95dc849d-9b2d-4497-a9bf-38f700db26e1.png#clientId=ud5a02840-c4ce-4&from=paste&height=503&id=u971f78d8&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1006&originWidth=968&originalType=binary&ratio=1&size=129821&status=done&style=none&taskId=u6d626c1f-a67e-4d7b-a974-3311ad40176&width=484)
系统自带的CA证书：
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640657126234-7e8885c9-17ca-4db4-aaad-62f3835f5948.png#clientId=ud5a02840-c4ce-4&from=paste&height=533&id=u229763fe&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1066&originWidth=1754&originalType=binary&ratio=1&size=348068&status=done&style=none&taskId=uafb0f014-a246-4b14-8352-6569d8b2609&width=877)

#### 抓包工具为什么需要导入证书？

1.客户端发一个HTTPS请求，被Fiddler拦截并且Fiddler伪装成客户端发请求给服务器

2. 服务器向假装成客户端的FIddler返回了CA证书
3. 自己制作了一张证书，假装服务器给客户端发了自己做的证书。获取服务器的公钥
4. 客户端生成对称秘钥，并用Fiddler假冒的公钥加密发送
5. Fiddler用自己的私钥解密获取对称秘钥
6. ……
   这样的话Fiddler能完全获取解析到双方加密的数据。
   实验证明：
   当我们正常访问百度，查看证书：
   ![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640657378811-5edc519b-5f5c-4a6e-94da-775332ec912e.png#clientId=ud5a02840-c4ce-4&from=paste&height=274&id=u5f70cca6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=548&originWidth=968&originalType=binary&ratio=1&size=77921&status=done&style=none&taskId=u91663e24-17c8-4f55-9b8d-e393d8b6fbc&width=484)
   开启Fiddler后，我们再访问百度：
   ![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640657457772-adaccab7-dd63-47f0-8038-8ff363591a70.png#clientId=ud5a02840-c4ce-4&from=paste&height=274&id=u93bfe19f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=548&originWidth=968&originalType=binary&ratio=1&size=69522&status=done&style=none&taskId=u02f6a0b0-7e1c-41f1-a193-d0ee7adfc81&width=484)

### 安装根证书

1. 点击`Trust root certificate` （Mac会需要输入系统密码）
1. 勾选`Capture HTTPS traffic`
1. Save保存即可安装成功，就可以开始抓HTTPS啦（可能需要重启Fiddler Everywhere）

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640653855844-db0b09d5-1c20-48a7-9ccd-5d4b8deeca57.png#clientId=ud5a02840-c4ce-4&from=paste&height=457&id=u1b989ab2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=914&originWidth=1374&originalType=binary&ratio=1&size=86091&status=done&style=none&taskId=u130e6fde-0a0e-4df1-908e-03aa1ca453a&width=687)

### 删除证书

~~如果之前装过一些fiddler证书，安装的姿势不对，导致新的证书不起作用，这时候需要先删掉之前的证书了~~

1. 在启动台（Launchpad）的其他中找到钥匙串（Keychain Access），或者在聚焦搜索(spotlight search)中搜钥匙串(Keychain Access)也可以找到。

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640653360285-2fc1515d-b37b-4778-ad89-28da9124f386.png#clientId=ud5a02840-c4ce-4&from=paste&height=428&id=u5a106717&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1710&originWidth=1940&originalType=binary&ratio=1&size=1536904&status=done&style=none&taskId=u6653436e-1d22-4f68-b857-f754941ef5a&width=485)

2. 我们可以在Default keychains -> login -> Certificerts 中可以找到Fiddler的根证书`DO_NOT_TRUST_FiddlerRoot`，右键即可删除。

![Screen Shot 2021-12-28 at 8.56.31 AM.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640653053085-f7c72e1e-ace3-42bd-9e06-9d70abc43c24.png#clientId=ud5a02840-c4ce-4&from=drop&height=525&id=ufd76be43&margin=%5Bobject%20Object%5D&name=Screen%20Shot%202021-12-28%20at%208.56.31%20AM.png&originHeight=1050&originWidth=1730&originalType=binary&ratio=1&size=333806&status=done&style=none&taskId=u88402c20-ecee-4452-aefd-3ce5dc2079f&width=865)

## 2. 手机APP抓包

### 前言

fiddler在抓手机app的请求时候，通常也会抓到来自PC的请求，导致会话消息太多，那么如何把来自pc的请求过滤掉，只抓来自APP的请求呢？
必备环境：
1.电脑上已装fiddler
2.手机和电脑在同一局域网

### 设置

1. Fiddler Everywhere -> Settings -> Connections，勾选`Allow remote computers to connect`
1. 8866端口为Fiddler的监听端口，后续手机中会用到。我这里的端口默认是8866，具体的端口号按实际情况来。

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640657823128-00ac8f66-acb9-4ced-8651-255538277d2e.png#clientId=ud5a02840-c4ce-4&from=paste&height=462&id=ub0a896eb&margin=%5Bobject%20Object%5D&name=image.png&originHeight=924&originWidth=1220&originalType=binary&ratio=1&size=98985&status=done&style=none&taskId=u235089de-adcf-4e1e-98dc-191c6a769a8&width=610)

### 查看本机IP

打开终端（Terminal），输入`ifconfig`（Windows下为`ipconfig`），找到IP，如下图：
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640658171429-b5397f86-f69e-4b0b-9604-bbe5e5962711.png#clientId=ud5a02840-c4ce-4&from=paste&height=490&id=udce83a69&margin=%5Bobject%20Object%5D&name=image.png&originHeight=980&originWidth=1460&originalType=binary&ratio=1&size=315478&status=done&style=none&taskId=u90757d8b-ad51-4872-8cd6-ed175d15843&width=730)

### 手机设置代理

1. 手机设置->WLAN设置->选择该wifi，点右边的箭头（有的手机是长按弹出选项框）。
2. 将代理换为手动进行配置：
   1. 配置主机名：与主机IP保持一致
   1. 端口：8866（Fiddler的监听端口）
3. 保存后即可抓取手机上的请求了

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640658467018-d3b6cd03-14f7-46b6-98fb-b928e64c1152.png#clientId=ud5a02840-c4ce-4&from=paste&height=600&id=u514a9a0f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=2400&originWidth=1080&originalType=binary&ratio=1&size=386468&status=done&style=none&taskId=ud2bfee96-4063-4cea-a081-b7d6b9ab64b&width=270)

### 抓取HTTPS请求

1. 如果app都是http请求，是不需要安装证书，能直接抓到的，如果是https请求，这时候手机就需要下载证书了
2. 打开手机浏览器输入地址：`[主机IP]:[Fiddler端口]`，比如我这里是`172.20.249.225:8866`
3. 出现如下画面，点箭头所指的位置，点击安装就可以了。
4. 不同手机安装证书方法可能会有所差异

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640658621484-fb4a1cf4-80fe-41fc-818a-58440f08e7be.png#clientId=ud5a02840-c4ce-4&from=paste&height=600&id=u03fe8fa4&margin=%5Bobject%20Object%5D&name=image.png&originHeight=2400&originWidth=1080&originalType=binary&ratio=1&size=336559&status=done&style=none&taskId=u27b8e1d7-e322-40d4-a12b-f78086b3563&width=270)

## 3. 查看GET和POST请求

### 前言

前面讲了关于Fiddler Everywhere抓包的一些基本配置，配置完之后就可以抓到我们想要的数据了，接下来就是如何去分析这些数据。
本篇以~~洛谷~~的请求为例，简单分析get与post数据有何不一样，以后也能分辨出哪些是get，哪些是post了。

### GET请求

1. 打开Fiddler Everywhere，然后浏览器输入~~洛谷~~首页地址：[https://www.luogu.com.cn/](https://www.luogu.com.cn/)
1. 点开右侧Inspectors下的Headers区域，查看Request Headers
1. Request Headers区域里面的就是请求头信息，可以看到打开~~洛谷~~首页的是get请求

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640660392365-f227b5e8-9069-46c7-805a-f2fa8233e8d2.png#clientId=ud5a02840-c4ce-4&from=paste&height=847&id=u161f5b42&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1694&originWidth=2954&originalType=binary&ratio=1&size=658107&status=done&style=none&taskId=ue5c0bb18-7e7a-4067-a07c-f9752707051&width=1477)

### POST请求

1. 打开登录首页：[https://www.luogu.com.cn/auth/login](https://www.luogu.com.cn/auth/login)
1. 输入账号和密码点击登录后，查看箭头所指的地方，可以看出是post请求

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640660623396-078060b0-1b7d-47df-b1ef-b8c6a443c3ef.png#clientId=ud5a02840-c4ce-4&from=paste&height=836&id=uc99a67de&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1672&originWidth=2930&originalType=binary&ratio=1&size=570133&status=done&style=none&taskId=u374eef56-514e-43a8-a692-c5936ffb4c9&width=1465)

### 如何找出需要的请求

1. 点开漏斗（Advanced Filters）

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640661222167-1c7904fc-d43f-4409-8662-5de3c49934be.png#clientId=ud5a02840-c4ce-4&from=paste&height=149&id=u17cf6361&margin=%5Bobject%20Object%5D&name=image.png&originHeight=298&originWidth=738&originalType=binary&ratio=1&size=47448&status=done&style=none&taskId=u7af8db3e-4942-4107-8c82-a23a58cced9&width=369)

2. 比如我们要只抓~~洛谷~~的请求，那我们可以设置条件：`url contains luogu.com.cn`，如下图：

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640661346550-3182c8b7-9dd1-4a4d-ab72-1e5818db18db.png#clientId=ud5a02840-c4ce-4&from=paste&height=243&id=u060ca743&margin=%5Bobject%20Object%5D&name=image.png&originHeight=486&originWidth=1584&originalType=binary&ratio=1&size=46528&status=done&style=none&taskId=u4f7538bd-3a8a-420c-a76e-04bf000edc8&width=792)

3. APPLY后即可只抓取~~洛谷~~的请求了

### GET和POST请求的区别

1. 关于get和post的功能上区别就不说了，大家自己查资料，这里主要从fiddler抓包的层面查看请求参数上的区别
1. get请求的Raw参数查看，主要分三部分：

- 第1部分是请求url地址
- 第2部分是host地址
- 第3部分是请求头部信息header

3. 再查看博客登录请求的Raw信息，post的信息分四部分。
   –前面3块内容都一样，第3部分和第4部分中间会空一行
   –第4部分内容就是post请求的请求body（get请求是没body的）

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640661504949-a98643d2-a5fa-4f9e-8ab6-59602fd2653a.png#clientId=ud5a02840-c4ce-4&from=paste&id=u4315b707&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1206&originWidth=2728&originalType=binary&ratio=1&size=241764&status=done&style=none&taskId=u8744e3da-02e0-4ef5-a6b3-f561cd156c8)

## 4. 工具介绍

本篇简单的介绍下fiddler界面的几块区域，以及各自区域到底是干什么用的，以便于更好的掌握这个工具
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640674569685-f19f6c91-3935-4b47-a33c-3fff8b1807a2.png#clientId=u7122d5b3-7751-4&from=paste&id=u622d3926&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1720&originWidth=2684&originalType=binary&ratio=1&size=1062283&status=done&style=none&taskId=ua5bcab46-db78-41ea-ad7f-577c8aec7dd)

### 会话框

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640674701033-185c7bfa-9c48-404c-897c-5fe9a93b88e1.png#clientId=u7122d5b3-7751-4&from=paste&height=752&id=uaa55e174&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1504&originWidth=2374&originalType=binary&ratio=1&size=432729&status=done&style=none&taskId=uc55ecb15-82d5-4f31-8724-927bed613f5&width=1187)
会话框主要查看请求的一些请求的一些基本信息，如# 、URL、HTTP Version、Result、Method、Process、Remote IP、Body Size、Comments，具体如下表：

| 字段         | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| #            | 这一栏是代表这个请求大概是什么内容                           |
| URL          | 请求的路径                                                   |
| HTTP Version | HTTP的版本，如HTTP/1.1                                       |
| Result       | HTTP状态码，如200(成功)、3xx（重定向相关）、4xx（找不到资源，一般是请求地址有问题）、5xx（一般是服务器本身的错误） |
| Method       | 请求方法，如：GET、POST、HEAD、OPTIONS、PUT、PATCH、DELETE、CONNECT |
| Process      | 进程                                                         |
| Remote IP    | 远程IP                                                       |
| Body Size    | 请求产生的数据大小                                           |
| Comments     | 类似于备注，可以右键一个请求进行Comment                      |

### Request和Response

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640675940937-4f16b1f9-14fd-4209-b0ae-6ece73471d70.png#clientId=u7122d5b3-7751-4&from=paste&height=705&id=ua59d7701&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1410&originWidth=1668&originalType=binary&ratio=1&size=202806&status=done&style=none&taskId=u36979706-d773-404f-9176-e507ccb2675&width=834)

1. Request是客户端发出去的数据，Response是服务端返回过来的数据，这两块区域功能差不多
2. headers:请求头，这里包含client、cookies、transport等
3. Params：请求时所带的参数
4. cookies:查看cookie详情
5. raw:查看一个完整请求的内容，可以直接复制
6. body：经过格式化后的主体

### decode解码

Fiddler Everywhere 会自动进行解码，无需再手动执行了

## 5. 接口测试（Composer）

### 前言

Fiddler最大的优势在于抓包，我们大部分使用的功能也在抓包的功能上，fiddler做接口测试也是非常方便的。
Fiddler Everywhere的Composer功能非常强大又简单易用，逐渐向Postman靠齐

### Composer简介

点开右侧Composer区域，可以看到如下界面，就是测试接口的界面了
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640678119078-90c576d1-dbdd-47b0-990e-978e4fcf271b.png#clientId=u7122d5b3-7751-4&from=paste&height=743&id=u5a285ff6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1486&originWidth=2160&originalType=binary&ratio=1&size=379324&status=done&style=none&taskId=u552d1256-9edc-456b-a7ae-ccc9676dc49&width=1080)

### JSON数据

1.有些post的请求参数和返回参数是Json格式的，如洛谷的登录请求：[https://www.luogu.com.cn/api/auth/userPassLogin](https://www.luogu.com.cn/api/auth/userPassLogin)
2.在登录页面手动输入账号和密码，登录成功。
3.找到这个登录成功的会话，查看json数据如下图：
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640678847288-a5b7a450-e9c8-46fe-9a4f-ee96c6f454e0.png#clientId=u4eb01b0d-14ef-4&from=paste&height=708&id=eIMOk&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1416&originWidth=2672&originalType=binary&ratio=1&size=418635&status=done&style=none&taskId=u74c2a5e5-08eb-4f19-b253-a43cc0a84b7&width=1336)

### 模拟GET请求

1. 在Composer区域地址栏输入博客首页：[http://luogu.com.cn](http://luogu.com.cn)
1. 选择GET请求，点Execute执行，请求就可以发送成功啦
1. 请求成功下方的Response会生成会话记录，可以查看本条请求的响应详情

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640678533645-70089a68-edda-494c-bd72-0351f7f580a8.png#clientId=u4eb01b0d-14ef-4&from=paste&height=703&id=ue62eb919&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1406&originWidth=2134&originalType=binary&ratio=1&size=236423&status=done&style=none&taskId=u1888eaa3-d645-467e-bd7e-5111dc4c8d9&width=1067)

### 模拟POST请求(实战登陆洛谷)

这里的模拟POST请求我们以登陆洛谷为案例进行讲解。

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640679522748-884ae901-a8e4-4556-ad4c-558c02cd6cc3.png#clientId=u4eb01b0d-14ef-4&from=paste&height=543&id=uc7fa684c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1086&originWidth=776&originalType=binary&ratio=1&size=109193&status=done&style=none&taskId=ub1045001-cc79-4974-af7e-5b8923c6105&width=388)

洛谷登陆链接：[https://www.luogu.com.cn/auth/login](https://www.luogu.com.cn/auth/login)
如上图，洛谷的登陆需要输入用户名+密码+验证码才能登陆成功，从表面上来看，我们只需要两个接口就能登陆成功，一个是**获取验证码的GET请求接口**，一个是**登陆的POST接口**，先GET验证码，然后根据验证码加上我们的用户名和密码调用登陆接口进行登陆，但实际并非想象中的那么简单，以下为抓包流程：

#### 1. 过滤

我们只需要抓取洛谷的接口，如下图，在Search栏输入洛谷的域名：`luogu.com.cn`，就只会抓取洛谷的请求了
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640679920250-1800bbf6-6542-4f72-a15f-608ec6d1e714.png#clientId=u4eb01b0d-14ef-4&from=paste&height=197&id=u66e6e53f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=394&originWidth=1290&originalType=binary&ratio=1&size=50517&status=done&style=none&taskId=ua69cadf4-eb38-4b7a-9b31-76402404643&width=645)

#### 2. 抓取验证码接口

在洛谷的登陆界面点击刷新验证码，抓到验证码的接口，可以在Response->Prieview中看到验证码的图像
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640680063693-89a861ee-f97a-401f-85ea-2e9eef7b1fcd.png#clientId=u4eb01b0d-14ef-4&from=paste&height=682&id=uc0ef65ba&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1364&originWidth=2674&originalType=binary&ratio=1&size=242834&status=done&style=none&taskId=u21211102-ccde-40bd-bb67-297f4682ab6&width=1337)为了方便接口测试，我们右键这个验证码请求->点击Edit in Composer，如下图：
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640680123720-dfdbd993-de7a-4b1b-9a83-c840fd916da0.png#clientId=u4eb01b0d-14ef-4&from=paste&height=335&id=u49fa8116&margin=%5Bobject%20Object%5D&name=image.png&originHeight=670&originWidth=1046&originalType=binary&ratio=1&size=49333&status=done&style=none&taskId=u03e6dc20-240d-4bea-bb3f-a3d536b1a65&width=523)
可以发现接口的地址为：[https://www.luogu.com.cn/api/verify/captcha?_t=1640680004860.4568](https://www.luogu.com.cn/api/verify/captcha?_t=1640680004860.4568)。参数`_t`为时间，也就是距 1970 年 1 月 1 日之间的毫秒数，如下图：
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640680624518-6a756b3d-a096-40e1-8e36-a29b7450732e.png#clientId=u4eb01b0d-14ef-4&from=paste&height=635&id=udc03cbb7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1270&originWidth=2148&originalType=binary&ratio=1&size=156076&status=done&style=none&taskId=u3a05d164-db91-47c1-9929-a6ce4a15298&width=1074)
我们还可以将这个请求进行保存，点击EXCUTE旁边的**SAVE**，输入**请求的名称**，**选择所在的文件夹**，点击SAVE保存即可，如下图：
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640680867409-20134ab2-2eaf-4f40-af98-c69259c82574.png#clientId=u4eb01b0d-14ef-4&from=paste&height=518&id=u93b8417b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1036&originWidth=1288&originalType=binary&ratio=1&size=77625&status=done&style=none&taskId=uf22bae5f-2da3-48e9-94a5-ecc7620cf5b&width=644)

#### 3. 抓取登陆接口

我们在洛谷输入正确的用户名、密码和验证码后点击登陆。
在Fiddler中寻找刚才发送的登陆请求，由于我们已知洛谷的登陆请求为POST方法，所以可以根据Method排序去找POST请求。找到一个POST请求的Request区Body中有刚刚输入的账号/密码/验证码的信息，这个就是洛谷登陆接口了`[https://www.luogu.com.cn/api/auth/userPassLogin](https://www.luogu.com.cn/api/auth/userPassLogin)`，如下图：
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640681255480-a2d083a1-c8ad-436f-be70-42a30caaeccf.png#clientId=u4eb01b0d-14ef-4&from=paste&height=699&id=uebdbca2d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1398&originWidth=2624&originalType=binary&ratio=1&size=400274&status=done&style=none&taskId=u7f8ae96b-d6cf-4a8d-9438-39ae85509ec&width=1312)
接下来我们还是跟步骤2一样存储一下这次的请求，右键登陆请求 -> Edit in Composer，然后SAVE一下Request（我这边把请求名称取名为了“登陆”），现在我们左下角的的Requests区就有了两个请求：
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640681766877-7cdaa757-34ff-4f6f-8606-fbff738b9676.png#clientId=u4eb01b0d-14ef-4&from=paste&height=132&id=u4c1f6935&margin=%5Bobject%20Object%5D&name=image.png&originHeight=264&originWidth=390&originalType=binary&ratio=1&size=12811&status=done&style=none&taskId=u3ab5c7e8-8a16-4089-b2b3-8fa602e1e39&width=195)

#### 4. 测试登陆

按照最初的想法，先调用验证码接口，查看到验证码：`zn22`
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640683611672-ce0f90f7-f8d3-4363-a5d1-e0fe80dc9190.png#clientId=u4eb01b0d-14ef-4&from=paste&height=521&id=u4d687e0e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1042&originWidth=2544&originalType=binary&ratio=1&size=346273&status=done&style=none&taskId=u89dcd9ea-a95d-40c3-8e25-28d592a57b5&width=1272)
然后使用`zn22`这个验证码加上我们自己的用户名密码去调用登陆接口，登陆请求的Body中有三个参数`username`、`password`、`captcha`分别对应着用户名、密码、验证码，这些我们根据实际情况去修改，如下图：
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640683934041-dcfc086b-3a9b-47b5-8f3b-7f0b5fc37605.png#clientId=u4eb01b0d-14ef-4&from=paste&height=252&id=u4e470572&margin=%5Bobject%20Object%5D&name=image.png&originHeight=504&originWidth=858&originalType=binary&ratio=1&size=45399&status=done&style=none&taskId=u895971f9-f0f8-4b3c-92ef-493603f47b5&width=429)
修改完请求体后点击EXCUTE执行，响应体中给我们提示报错了，提示`会话超时，请刷新页面后重试`：
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640684089545-777b1546-e274-4dc7-ba3f-ff83945717cf.png#clientId=u4eb01b0d-14ef-4&from=paste&height=241&id=uebfd7d54&margin=%5Bobject%20Object%5D&name=image.png&originHeight=482&originWidth=840&originalType=binary&ratio=1&size=48262&status=done&style=none&taskId=u83836e9b-c26c-465f-a140-b986337051a&width=420)
出现这种类似的错误信息，原因一定出在请求的请求头中，服务器对请求头进行了限制，比如验证Cookies、和为了防止跨站攻击而设置的验证`X-CSRF-TOKEN`等，所以才会出现此类情况。
接下来，分析POST登陆请求的请求头：

```
Host:www.luogu.com.cn
Connection:keep-alive
Content-Length:82
sec-ch-ua:" Not A;Brand";v="99", "Chromium";v="96", "Google Chrome";v="96"
X-CSRF-TOKEN:1640768448:U3hwS2h4azHVGgygSHLD9oaY7Z+4Bf9U8VwT1rWLEYQ=
sec-ch-ua-mobile:?0
User-Agent:Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Safari/537.36
Content-Type:application/json
Accept:application/json, text/plain, */*
X-Requested-With:XMLHttpRequest
sec-ch-ua-platform:"macOS"
Origin:https://www.luogu.com.cn
Sec-Fetch-Site:same-origin
Sec-Fetch-Mode:cors
Sec-Fetch-Dest:empty
Referer:https://www.luogu.com.cn/auth/login
Accept-Encoding:gzip, deflate, br
Accept-Language:en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7
Cookie:__client_id=d60b5430b77152d9bc168bca64ace8883254e127; _uid=0
```

上述的请求头中，除了`X-CSRF-TOKEN`和`Cookie`其他都不需要变动。
`X-CSRF-TOKEN`可以在GET [https://www.luogu.com.cn/auth/login](https://www.luogu.com.cn/auth/login)的Body中找到，如下图：
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640688812956-20ce959d-ce0f-4311-98f5-84c5a21cea30.png#clientId=u4eb01b0d-14ef-4&from=paste&height=743&id=u528184f2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1486&originWidth=1540&originalType=binary&ratio=1&size=184730&status=done&style=none&taskId=u343124f6-1b1c-4d8b-a016-c406532aa9c&width=770)
而`Cookes`可以在Response -> Cookies中找到，右键Value可以进行复制，如下图：
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640689021227-5188ab7e-6e1a-48eb-823b-77b99fcdd62a.png#clientId=u4eb01b0d-14ef-4&from=paste&id=u4cc5b6bc&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1382&originWidth=1496&originalType=binary&ratio=1&size=120132&status=done&style=none&taskId=ua6a3b551-06d2-464e-b4b5-224bec993e4)
知道了这两个是如何获取的就可以继续我们的测试登陆了，具体步骤也就变成了：

1. GET [https://www.luogu.com.cn/auth/login](https://www.luogu.com.cn/auth/login)，获取到`Cookies`和`X-CSRF-TOKEN`，并记录下来。
1. 带上`Cookies`去GET [https://www.luogu.com.cn/api/verify/captcha](https://www.luogu.com.cn/api/verify/captcha?_t=1640680004860.4568)，记录下获取到的验证码。
1. POST [https://www.luogu.com.cn/api/auth/userPassLogin](https://www.luogu.com.cn/api/auth/userPassLogin)：需要修改Headers中的`Cookies`和`X-CSRF-TOKEN`，请求体Body中的`captcha`参数更换为步骤二获取到的验证码。

登陆成功如下图，就可以拿`syncToken`以及响应的`Cookies`去请求需要登陆的接口了。
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640700817965-537e93ad-4fa3-45e1-b067-6b70febf4e5f.png#clientId=u4eb01b0d-14ef-4&from=paste&height=500&id=u3a621cd4&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1000&originWidth=2140&originalType=binary&ratio=1&size=140955&status=done&style=none&taskId=u57548a35-5a70-41ba-8b3e-2ea933b1fd8&width=1070)

### GET请求（URL详解）

#### 前言

上一篇介绍了Composer的功能，可以模拟get和post请求，get请求有些是不带参数的，这种比较容易，直接放到url地址栏就行。有些get请求会带有参数，本篇详细介绍url地址格式。

#### url详解

1. url就是我们平常打开百度在地址栏输入的：[https://www.baidu.com](https://link.zhihu.com/?target=https%3A//www.baidu.com/),如下图，这个是最简单的url地址，打开的是百度的主页
   ![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640701252513-7680a86d-de60-4bce-b171-5473698d02f7.png#clientId=u4eb01b0d-14ef-4&from=paste&height=109&id=u243fddf2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=218&originWidth=872&originalType=binary&ratio=1&size=20716&status=done&style=none&taskId=u3de04a31-96bf-4429-a26e-da56e92cc34&width=436)
1. 再看一个稍微复杂一点的url，在百度输入框输入：洛谷

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640701349404-6f4d7e89-e811-4073-bb88-761e64113ca9.png#clientId=u4eb01b0d-14ef-4&from=paste&height=290&id=uae1bd74d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=580&originWidth=1550&originalType=binary&ratio=1&size=258004&status=done&style=none&taskId=u099d85b7-adfd-4682-9bd7-f001a8fe6b7&width=775)

3. 查看url地址栏，对比之前的百度首页url地址，后面多了很多参数。当然最主要的参数是:wd=上海悠悠博客园（后面的一大串可以暂时忽略）
3. 那么问题来了，这些参数有什么作用呢？
   可以做个简单的对比，在地址栏分别输入：
   [https://www.baidu.com](https://link.zhihu.com/?target=https%3A//www.baidu.com/)
   [https://www.baidu.com/s?wd=洛谷](https://www.baidu.com/s?wd=洛谷)
   对比打开的页面有什么不一样，现在知道作用了吧，也就是说这个多的”/s？wd=洛谷”就是搜索的结果页面

#### url解析

1. 以[https://www.baidu.com/s?wd=洛谷](https://www.baidu.com/s?wd=洛谷)这个URL请求为例
1. 那么一个完整的url地址，基本格式：`https://host:port/path?xxx=aaa&ooo=bbb`

- http/https：这个是协议类型，如图中所示
- host:服务器的IP地址或者域名，如图中2所示
- port:HTTP服务器的默认端口是80，这种情况下端口号可以省略。
  如果使用了别的端口，必须指明，例如：192.168.3.111:8080，这里的8080就是端口
- path:访问资源的路径,如图中3所示/s (图中3是把path和请求参数放一起了)
- ？:url里面的？这个符号是个分割线，用来区分问号前面的是path，问号后面的是参数
- url-params:问号后面的是请求参数，格式：xxx=aaa，如图4区域就是请求参数
- &：多个参数用&符号连接

#### UrlEncode编码

1. 如果url地址的参数带有中文的，一般在url里面会是这样的，如第二点里的wd=%E6%B4%9B%E8%B0%B7。像看到%B4这种编码的就是经过url编码过的，需要解码就能看到是什么中文了
1. 用urlencode在线编码/解码工具，地址：[https://www.urldecoder.org/](https://www.urldecoder.org/)

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640702305942-3954b68c-a956-4bba-81e2-25222443f9c5.png#clientId=u4eb01b0d-14ef-4&from=paste&height=514&id=e6hEL&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1028&originWidth=1296&originalType=binary&ratio=1&size=101970&status=done&style=none&taskId=u61e52925-c969-44c2-9d8e-c32a529ed71&width=648)

#### 请求参数（params）

1. 在url里面请求参数一般叫params，每个参数对应的都有name和value值
1. 多个参数情况如下：

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640702120243-36a51902-8455-4de3-be58-cdd9b4415bd2.png#clientId=u4eb01b0d-14ef-4&from=paste&height=301&id=u49b080c6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=602&originWidth=1322&originalType=binary&ratio=1&size=54926&status=done&style=none&taskId=uf9718da2-c8b4-4dac-b051-7afae7b74e4&width=661)
#### 

### POST请求（body）

前言上一篇讲过get请求的参数都在url里，post的请求相对于get请求多了个body部分，本篇就详细讲解下body部分参数的几种形式。
注意：post请求的参数可以放在url，也可以放在body，也可以同时放在url和body，当然post请求也可以不带参数。
只是一般来说，post请求的参数习惯放到body部分

#### body数据类型

常见的post提交数据类型有四种：

1. 第一种：application/json：这是最常见的json格式，也是非常友好的深受小伙伴喜欢的一种，比如：

``` json
{“input1”:”xxx”,”input2”:”ooo”,”remember”:false}
```

2. 第二种：application/x-www-form-urlencoded：浏览器的原生 form 表单，如果不设置 enctype 属性，那么最终就会以 application/x-www-form-urlencoded 方式提交数

```
input1=xxx&input2=ooo&remember=false
```

3. 第三种：multipart/form-data:这一种是表单格式的，数据类型如下：

```
WebKitFormBoundaryrGKCBY7qhFd3TrwA 
Content-Disposition: form-data; 
name=”file”; 
filename=”chrome.png” 
Content-Type: image/png PNG
content of chrome.png 
WebKitFormBoundaryrGKCBY7qhFd3TrwA
```

4. 第四种：text/xml:这种直接传的xml格式

``` xml
<!--?xml version="1.0"?-->
<methodcall>
	<methodname>examples.getStateName</methodname>
	<params>
		<param>
			<value><i4>41</i4></value>
		</param>
	</params>
</methodcall>
```

#### x-www-form-urlencoded

浏览器的原生 <form> 表单，如果不设置 enctype 属性，那么最终就会以 application/x-www-form-urlencoded 方式提交数据。请求类似于下面这样（无关的请求头在本文中都省略掉了）：

```
POST http://www.example.com HTTP/1.1
Content-Type: application/x-www-form-urlencoded;charset=utf-8

title=test&sub%5B%5D=1&sub%5B%5D=2&sub%5B%5D=3
```

首先，Content-Type 被指定为 application/x-www-form-urlencoded；其次，提交的数据按照 key1=val1&key2=val2 的方式进行编码，key 和 val 都进行了 URL 转码。大部分服务端语言都对这种方式有很好的支持。例如 PHP 中，$_POST['title'] 可以获取到 title 的值，$_POST['sub'] 可以得到 sub 数组。
很多时候，我们用 Ajax 提交数据时，也是使用这种方式。例如 [JQuery](http://jquery.com/) 和 QWrap 的 Ajax，Content-Type 默认值都是「application/x-www-form-urlencoded;charset=utf-8」。

## 6. HTTP协议简介

### 什么是HTTP

1.HTTP协议是Hyper Text Transfer Protocol（超文本传输协议）的缩写,是用于从万维网（WWW:World Wide Web ）服务器传输超文本到本地浏览器的传送协议。
2.HTTP（HyperText Transfer Protocol）协议是基于TCP的应用层协议，它不关心数据传输的细节，主要是用来规定客户端和服务端的数据传输格式，最初是用来向客户端传输HTML页面的内容。默认端口是80
3.http（超文本传输协议）是一个基于请求与响应模式的、无状态的、应用层的协议

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640619386343-78d9e46e-62bc-423c-b83e-ee57ccc6796f.png#clientId=ud5a02840-c4ce-4&from=paste&height=91&id=udb6ab925&margin=%5Bobject%20Object%5D&name=image.png&originHeight=181&originWidth=551&originalType=binary&ratio=1&size=91585&status=done&style=none&taskId=ub4f70909-adf1-4e4d-a0a4-920dd5b7d6d&width=275.5)

### 请求报文

1.HTTP请求报文主要由请求行、请求头部、空一行、请求正文4部分组成
（当然，如果不算空的一行，那就是3个部分）

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640619434832-7ad09a62-04a8-4df4-8570-f9b3a3681512.png#clientId=ud5a02840-c4ce-4&from=paste&height=83&id=u16487a5b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=165&originWidth=466&originalType=binary&ratio=1&size=29770&status=done&style=none&taskId=u34948465-9320-4075-9eb7-2b2ea78ff6f&width=233)

2.下图是fiddler工具抓的post请求报文（工具使用看fiddler篇），可以对照上图，更清楚的理解http的请求报文内容。

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640619447803-80eee587-fc38-4bb3-b1f4-8d88d93a31c7.png#clientId=ud5a02840-c4ce-4&from=paste&height=304&id=ub4e87829&margin=%5Bobject%20Object%5D&name=image.png&originHeight=405&originWidth=689&originalType=binary&ratio=1&size=286034&status=done&style=none&taskId=u84122fdc-c376-45d9-9187-231148bd61e&width=517)

### 响应报文

1.HTTP响应报文主要由状态行、消息报头、空一行、响应正文4部分组成
（当然，如果不算空的一行，那就是3个部分）
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640619475314-4d6b4c02-c0f1-48a6-b09e-3b4bf2e23bff.png#clientId=ud5a02840-c4ce-4&from=paste&height=89&id=u69d64ef3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=177&originWidth=480&originalType=binary&ratio=1&size=42588&status=done&style=none&taskId=u37c7f229-951a-4edf-83c0-c25977643ba&width=240)
2.下图就是一个请求的响应内容，用fiddler抓包工具可以查看
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640619495356-6aabf974-1989-42a7-a231-d22a9010b1e8.png#clientId=ud5a02840-c4ce-4&from=paste&height=266&id=u568c6bf6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=305&originWidth=683&originalType=binary&ratio=1&size=101063&status=done&style=none&taskId=ud945d181-b577-4cf6-bce3-d4fe5c0bebc&width=595.5)

### 完整的HTTP内容

1. 一个完整的http协议其实就两块内容，一个是发的请求，一个服务端给的响应。
1. 以下是请求[https://github.com/timeline.json](https://link.zhihu.com/?target=https%3A//github.com/timeline.json) 这个地址后，用fiddler抓包导出为文本，查看完整的http请求内容。（具体操作查看《fiddler 1.10会话保存》）

![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640619802283-8e0c2a83-8d8c-49f9-9227-442b22f3687e.png#clientId=ud5a02840-c4ce-4&from=paste&height=249&id=u56bae526&margin=%5Bobject%20Object%5D&name=image.png&originHeight=498&originWidth=720&originalType=binary&ratio=1&size=256217&status=done&style=none&taskId=u2c20f1db-2b85-404c-987b-d02af12f5f1&width=360)
内容如下：
以下是请求报文

```
GET https://github.com/timeline.json HTTP/1.1
Host: github.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:44.0) Gecko/20100101 Firefox/44.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate, br
Cookie: xxx(已省略)
```

以下是请求报文

```
GET https://github.com/timeline.json HTTP/1.1
Host: github.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:44.0) Gecko/20100101 Firefox/44.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate, br
Cookie: xxx(已省略)
X-Request-Id: d09e199dc290c6f0dc79fe49007069ab
X-Runtime: 0.004161
Content-Security-Policy: xxx(已省略)
Strict-Transport-Security: xxx(已省略)
X-Content-Type-Options: nosniff
X-Frame-Options: deny
X-XSS-Protection: 1; mode=block
X-Runtime-rack: 0.007388
X-GitHub-Request-Id: FE36:2B0A9:177175F:23C092D:594FD998
Content-Length: 379
```

以下是响应正文（json格式）

```
{“message”:”Hello there, wayfaring stranger. If you’re reading this then you probably didn’t see our blog post a couple of years back announcing that this API would go away: http://git.io/17AROg Fear not, you should be able to get what you need from the shiny new Events API instead.”,”documentation_url”:”https://developer.github.com/v3/activity/events/#list-public-events”}
```

### 请求行

#### 8种请求行

请求行有三个主要参数：请求方法、url、协议版本。
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12654026/1640619977741-e90599f2-d723-465d-96b2-f2140879645d.png#clientId=ud5a02840-c4ce-4&from=paste&height=206&id=u7ea8c926&margin=%5Bobject%20Object%5D&name=image.png&originHeight=227&originWidth=554&originalType=binary&ratio=1&size=52238&status=done&style=none&taskId=u7d0a54bb-1801-431e-be64-4d73ec63556&width=502)

#### 请求方法

请求方式简介get请求指定的页面信息，并返回实体主体。post向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。POST请求可能会导致新的资源的建立和/或已有资源的修改。HEAD类似于get请求，只不过返回的响应中没有具体的内容，用于获取报头OPTIONS返回服务器针对特定资源所支持的HTTP请求方法，也可以利用向web服务器发送‘*’的请求来测试服务器的功能性PUT向指定资源位置上传其最新内容DELETE请求服务器删除Request-URL所标识的资源TRACE回显服务器收到的请求，主要用于测试或诊断CONNECTHTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器。

- **注意：**
  1）方法名称是区分大小写的。
  2）最常见的的就是通常说的get和post方法。

#### url详解

1.打开百度，在搜索框输入任意文字，搜索后，复制地址栏的url地址：

```
https://www.baidu.com/s?wd=%E4%B8%8A%E6%B5%B7%E6%82%A0%E6%82%A0%E5%8D%9A%E5%AE%A2&rsv_spt=1&rsv_iqid=0x91baaabd00070ba2&issp=1&f=8&rsv_bp=1&rsv_idx=2
```

2.那么一个完整的url地址，基本格式如下：

```
https://host:port/path?xxx=aaa&ooo=bbb
```

- http/https：这个是协议类型，如图中1所示
- host:服务器的IP地址或者域名，如图中2所示
- port:HTTP服务器的默认端口是80，这种情况下端口号可以省略。如果使用了别的端口，必须指明，例如：192.168.3.111:8080，这里的8080就是端口
- path:访问资源的路径,如图中3所示/s (图中3是把path和请求参数放一起了)
- ？:url里面的？这个符号是个分割线，用来区分问号前面的是path，问号后面的是参数
- url-params:问号后面的是请求参数，格式：xxx=aaa，如图4区域就是请求参数
- &：多个参数用&符号连接

#### 协议版本

根据HTTP标准，HTTP请求可以使用多种请求方法。
HTTP1.0定义了三种请求方法： GET, POST 和 HEAD方法。
HTTP1.1新增了五种请求方法：OPTIONS, PUT, DELETE, TRACE 和 CONNECT 方法。