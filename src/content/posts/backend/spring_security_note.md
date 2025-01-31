---
title: Spring Security Note（TODO）
tags:
  - 后端
categories:
  - 后端
pubDate: 2022-06-05 15:34:41
---




## 简介

Spring Security 是 Spring 家族中的一个安全管理框架。

一般 Web 应用需要进行**认证**和**授权**

认证：验证当前访问系统的是不是本系统的用户，并且要确认具体是哪个用户

授权：经过认证后判断当前用户是否有权限进行某个操作


## Quick start

## 认证（Authentication）

### 登录校验流程

### 解决问题

#### 思路分析

##### 登录

1. 自定义登录接口
   1. 调用 `ProviderManager` 的方法进行认证，如果认证通过生成 JWT
   2. 把用户信息存入 Redis 中
2. 自定义 `UserDetailsService`
   1. 在这个类中实现列中去查询数据库

##### 校验

定义 JWT 认证过滤器
1. 获取 Token
2. 解析 Token 获取其中的 userId
3. 从 Redis 中获取用户信息
4. 存入 `SecurityContextHolder`