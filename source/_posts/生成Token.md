---
title: git生成Token
top: false
cover: false
toc: true
mathjax: true
tags: ['git']
categories: ['git']
date: 2024-12-2 10:11:32
password:
summary: git生成Token
coverImg:
img:
---

## 生成步骤

> Setting -> Developer settings -> Personal access tokens -> Tokens(classic) -> Generate new token(classic)

![填写信息](http://pic.mrzhj.cn/blog/20241202-4.png)
>1. 有效期，自己选择，可以选择永不过期，但是git好像会自动清除1年内未使用的token
>2. 选择权限，一般选择repo即可（给予该token对于该仓库pull与push的权限），如果需要管理用户权限，可以勾选user

<p style="color:red;font-size:23px;">注意，注意，注意：生成后的token一定要及时保存，因为你只要离开当前页面，该token就不会再显示了！！！</p>