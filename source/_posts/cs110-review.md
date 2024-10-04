---
title: CS110 Review
date: 2024-09-25 02:06:46
tags:
---

## 缓存与虚拟内存

**缓存的组相联策略**:

首先,考虑一条地址的组成:
| Tag | Index | Offset|
|-|-|-|
|存储在cache line中以确定数据 |所属的缓存组的编码 |在cache line中的偏移量 |

对于一个缓存模块, N组相联也就意味着每组有N个缓存块.

**block 与 page**