---
title: git提交失败的处理
top: false
cover: false
toc: true
mathjax: true
tags: ['git']
categories: ['git']
date: 2024-12-2 14:14:04
password:
summary: git提交失败如何处理
coverImg:
img:
---

# 本文只处理git提交超时，与同一电脑切换不同账号仓库提交报403的问题

## 1. git提交超时

### 1.1. 问题描述

在提交代码时，出现如下错误：

```bash
# git push
fatal: unable to access 'https://github.com/your_account/repo.git/': Failed to connect to github.com port 443 after 21069 ms: Timed out
```
这种情况就是因为git需要挂梯子才能访问到，网络不好的花，基本上都会报这个错误
### 1.2. 解决方案
先说思路，需要有个梯子，然后挂上梯子，然后把git的http或https代理（一般设置http就行了）设置为梯子所对应的端口号，之后在提交就没问题了
#### 1.2.1. 查看git配置

```bash
git config --list/-l
// 如果有设置的话，条目中会有一条下方的这种输出
http.proxy=http://127.0.0.1:7890
// 如果没有，我们手动设置即可（本地ip加梯子的端口(7890)
git config --global http.proxy http://127.0.0.1:7890
```
之后在提交就不会出现443的情况了


## 2. git提交403

### 2.1. 问题描述

在提交代码时，出现如下错误：

```bash
# git push
remote: Permission to opencv/opencv-python.git denied to yueluu.
fatal: unable to access 'https://github.com/opencv/opencv-python.git/': The requested URL returned error: 403
```
### 2.2. 产生原因
直译就是对当前仓库没有权限，要么是账号密码错误，要么是仓库设置问题不逊于操作，要么，当然一般情况下都是可以提交的，还有就是由于切换了仓库，git仓库的账号不一致导致的密码不对<font color='red'>（本文只讨论这种情况）</font> 
 > 1、当我们首次提交仓库代码的时候，肯能需要我们验证下账号密码，要么是控制台输入，要么提示我们去网页登录
### 2.3. 解决方案
我们git push的时候，实际上都会去验证本地的windows凭据（可通过：控制面板>用户账户>管理windows凭据查看），这个凭据只能保存一个，而git提交的时候会根据这个来验证，所以说我们切换不同账号的仓库提交的时候才会提示我们403
> 具体的凭据条目是：git:https://www.github.com （大致是这个样子），如果我们提交另一个git账号的仓库，按道理来说我们直接设置对应凭据的用户名与密码即可，但是不知道为什么不生效，所以还是直接删除掉该凭据，然后重新push，此时会弹出一个对话框，如图所示：

![登录提示框](http://pic.mrzhj.cn/blog/20241202-1.png)

#### 2.3.1.	浏览器账号登录
> 如果选择浏览器登录（sign in with your browser），直接选择当前仓库的账号即可，然后就会直接提交成功

#### 2.3.2. Token登录
>	如果选择Token登录的话，输入我们生成的Token即可，具体如何生成请点击->[这里](/2024/12/02/生成Token/)，之后即提交成功


#### 2.3.3. 控制台输入账号与密码
你也可以关闭提示框，此时会提示你在控制台输入账号密码，如图所示
![输入用户名密码](http://pic.mrzhj.cn/blog/20241202-3.png)
这个时候控制台会提示你输入用户名与密码，用户名正常输入，但是密码不能输入密码，会直接报错，如下
```bash
remote: Support for password authentication was removed on 
August 13, 2021. Please use a personal access token instead.
```
<font color='red'>这是因为2024年8月13号开始git就不在支持用户名密码验证了，只能通过Token验证，Token生成请点击->[这里](/2024/12/02/生成Token/)，所以密码的提示输入Token即可
</font>