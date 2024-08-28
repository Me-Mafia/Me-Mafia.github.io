---
title: 算法与数据结构 Note#2
date: 2024-08-25 17:42:32
categories: 
    - 算法与数据结构
    - 复习

tags:           
    - 数据结构
    - 散列表
    - 自平衡树
toc: true
---

<script>
MathJax = {
  tex: {
    inlineMath: [['$', '$'], ['\\(', '\\)']]
  }
};
</script>
<script id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js">
</script>

# Algorithms Note #02

> under construction...

## 概率与随机
```c
HIRE-ASSISTANT(n)
    best = 0  // candidate 0 is a least-qualified dummy candidate
    for i = 1 to n
        interview candidate i
        if candidate i is better than candidate best
            best = i   
            hire candidate i
```


## 基本数据结构

- **栈**: **后进先出**(LIFO)的动态集合.
- **队列**: **先进先出**(FIFO)的动态集合.

### 链表

|      | 时间复杂度  |
| ---- | ----------- |
| 搜索 | $\Theta(n)$ |
| 插入 | $\Theta(1)$ |
| 删除 | $\Theta(1)$ |
|      |             |

### 有根树

- **二叉树**: 
- **分支无限的有根树**: 孩子数任意的树可以通过**左孩子右兄弟表示法**进行表示. 每个节点的指针包括:
  - `p`: 指向父节点.
  - `x.left_child`:最左边的子节点.
  - `x.right_sibling`:右侧的相邻节点.

## 散列表

 

### 散列函数
满足简单均匀散列假设：关键字被等可能地散列到$m$个槽位中的一个.

- **除法散列**: 散列函数为 $h(k) = k \mod m$. 对于$m$的选取, 应当使$m$不接近 2 的幂且为一个素数. 如果$m = 2^p$

### 解决冲突
- **链接法**: