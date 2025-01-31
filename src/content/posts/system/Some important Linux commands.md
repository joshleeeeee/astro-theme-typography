---
title: 一些好用但鲜为人知的 Linux 命令
tags:
  - linux
categories:
  - 操作系统
pubDate: 2022-07-08 11:15:20

---

## 系统监视

### Uptime

Uptime会返回**服务器运行时长**、**当前时间**、**用户数量**和**内存使用平均数**等信息。

``` bash
$ uptime
```

### Wall

Wall可以向当前登录到系统的每个人的终端发送消息

``` bash
$ wall "Your message"
```

### Top

实时显示 CPU 和内存使用情况的进程列表。

``` bash
$ top
```

### lsof

lsof是一个单一的命令，用于一个基本的目的：**L**i**s**t **O**pen **F**iles。这在遇到说文件被使用的挂载问题时特别有用。这个命令可以快速识别哪些文件被哪些进程使用。

``` bash
$ lsof
```

## 网络

### Netcat

`Netcat`、`nc`主要用于端口扫描，但实际上是一个伟大的实用网络工具，可供系统管理员在他们的后袋中用于任何任务。Netcat可以支持端口扫描、文件复制、端口转发、代理服务器和托管服务器......可以说，它的功能非常全面。

``` bash
# Example Usage:
$ nc -vz <host> <port> # 检查给定端口上两个主机之间的连接
$ nc -l 8080 | nc <host> 80 # 创建一个代理服务器
```

### Netstat

Netstat返回各种网络的详细信息，如路由表（routing tables）、网络连接（network connections）、成员资格（memberships）、统计信息（stats）、标志（flags）等。

```bash
# Example Usage 
$ netstat -a # 查看所有网络端口
$ netstat -tlpn # 查看所有监听中的端口

# Key Flags
-s = display networking statistics
-v = be verbose
-r = show routing tables
-i = display interface table
-g = show group memeberships
```

### Nslookup

用于获取网络或本地的服务器信息。它查询DNS以找到服务器信息，这对网络调试很有用。

```bash
# Example Usage
$ nslookup bilibili.com
Server:		183.60.83.19
Address:	183.60.83.19#53
Non-authoritative answer:
Name:	bilibili.com
Address: 47.103.24.173
Name:	bilibili.com
Address: 139.159.241.37
Name:	bilibili.com
Address: 120.92.78.97
Name:	bilibili.com
Address: 119.3.70.188
Name:	bilibili.com
Address: 8.134.50.24
# Key Flags
-port = Change port number for connection
-type = Change type of query. 
-domain = Sets search list to name
```

### TCPDump

用于捕获和分析进出你的系统的流量。它是一个强大的多功能工具，专门用于调试和排除网络问题，但也可以作为一个安全工具使用。

``` bash
# Example Usage
$ tcpdump
$ tcpdump -i <interface> <ipaddress or hostname> <port>
```

## 其他

### rsync

用于将文件和目录复制到目的地，类似于`cp`命令。但是，它也允许复制到远程位置，并且可以提供进度条，这通常用于备份

```bash
# Example Usage
$ rsync -vap --ignore-existing <source_file> <destination_file>

#  Key flags:
v = verbrose
r = recursive
p = preserve permissions
g = group
o = owner
a = archive
--progress = progresss bar
```

### screen

如果你需要在远程运行一个长时间的任务（如系统备份、ftp 传输等等），用 screen 就不用担心 SSH 会话中断而导致的任务中断了，Screen 会在断开连接的情况下继续运行你的命令！

``` bash
# Example Usage
$ screen # 启动一个 screen 会话
$ screen -ls # 显示正在运行中的服务
$ screen -r # 连接会话
```

### date

``` bash
# 将Unix timestamp转换为人类可读的日期形式
$ date --date @1657252922
Fri Jul  8 12:02:02 CST 2022

# 获取当前的时间戳
$ date "+%s"
1657252922
```

### systemd

```bash
# 列出所有Systemd服务
$ systemctl -l -t service | less
```
