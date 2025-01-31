---
title: Using Clash in Linux Server
tags:
  - linux
categories:
  - 操作系统
pubDate: 2022-08-07 09:34:49

---

> Background: Too slow to install some dependent environments

## Download

We can go to the [Clash Releases Page](https://github.com/Dreamacro/clash/releases) and find the corresponding system download address.The following demonstration with `CentOS Linux 7 for x86`.


Download using wget:

> If direct wget is slow, you can use SFTP to upload to a Linux server after local download.
```bash
wget https://github.com/Dreamacro/clash/releases/download/v1.11.4/clash-linux-386-v1.11.4.gz
```

Decompression file Using gunzip and rename it to clash:

``` bash
gunzip clash-linux-386-v1.11.4.gz
mv clash-linux-386-v1.11.4.gz clash
```

Add exceutable permissions to Clash:
``` bash
chmod +x clash
```

## Configuration

Put the clash configuration (`config.yml`, `Country.mmdb`) of your computer into the clash directory of Linux Server.

You can also download `Country.mmdb` manually by visiting this [link](https://github.com/Dreamacro/maxmind-geoip/releases).

## Launch

Running Clash in the background:

```
nohup ./clash &
```

## System Proxy

Setting system proxy in the shell:

```
export {http,https}_proxy=127.0.0.1:7890
```

## Verify

Verify Proxy:
```
curl ip.gs
```

Visit to Google:
```
curl google.com
```