---
title: 算法与数据结构 Note#1
date: 2024-08-23 23:52:19
categories: 
    - 复习
    - 算法与数据结构

tags:           
    - 排序算法
    - 分治法
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


# Algorithms Note #01
> Under construction...

## Prequisites
### 函数的渐进记号
对于函数$g$:
||定义|
|-|-|
|$\Theta(f(n))$| $O(f(n))$ and $\Omega(f(n))$ |
|$O(f(n))$| $\exists c, x_0$ s.t. $\forall x>x_0, f(x)>g(x)$  |
|$\Omega(f(n))$| $\exists c, x_0$ s.t. $\forall x>x_0, f(x)<g(x)$ |

## 排序算法与证明

**对于数组混乱程度的度量**:使用**逆序对**. 对于随机排列的数组,假定它的逆序对数量为所有数对的一半, 即$\frac{1}{2}\binom{2}{n} = O(n^2)$.

### 插入排序

**循环不变式**：数组`A[0] ~ A[j-1]`是已经排序的.
|平均|最差|
|-|-|
|$O(n^2)$| $O(n\lg n)$ |

### 冒泡排序
**循环不变式**：数组`A[0] ~ A[j-1]`是已经排序的.

|平均|最差|
|-|-|
|$O(n^2)$|$O(n^2)$ |

### 为什么插入排序更优越?

### 归并排序
**循环不变式**：数组`A[0] ~ A[j-1]`是已经排序的.


**时间复杂度**：

$$ T(n) = T(\frac{n}{2}) + \Theta(n) $$

|平均|最差|
|-|-|
|$O(n\lg n)$| $O(n\lg n)$ |

### 堆排序
**空间原址性**: 对于元素只需要常数个额外的元素空间存储临时数据.
二叉堆由一个数组实现,可以看作一棵近似的完全二叉树.考虑堆中下标为`i`的元素`A[i]`:
- `A[i]`的父元素为`A[floor(i/2)]`
- `A[i]`的两个子节点为`A[2i]`(左)和`A[2i+1]`(右)

#### 堆的维护
```pseudocode
MAX-HEAPIFY (A, i)
  l= LEFT (i)
  r= RIGHT (i)
  // 比较i和他的左侧子节点
  if l <= A. heap-size and A[l] > A[i]
    largest =l
  else largest = i
  // 比较之前的最大值和i的右侧子节点
  if r<= A. heap-size and A[r] > A[largest]
    largest= r
  // 若i小于子节点之一
  if target != i
    exchange A[i] with A[largest]
    MAX-HEAPIFY (A, largest) 
```
对于子问题(`MAX-HEAPIFY (A, largest)`),最坏的情况是这棵子树层数比另一棵子树多1. 此时这棵子树的规模为$O(2n/3)$,比较与交换节点的开销为$\Theta(1)$,因此对于`MAX-HEAPIFY`有:
$$ T(n) \leq T(2n/3) + \Theta(1) $$
由主定理得,$T(n)=O(\lg n)$.

#### 建堆 & 排序
**建堆的循环不变式**：在每次调用`MAX-HEAPIFY`时,节点$i+1, i+2, \cdots, n$都是一个最大堆的根节点.

**堆排序的循环不变式**： 在每次交换`A[n]`与`A[1]`后,数组`A[i], A[i+1], ... , A[n]`是已排序的数组.

#### 堆作为优先队列

### 快速排序

```pseudocode
PARTITION(A, p, r)
  x = A[r]
  i = p - 1
  for j = p to r - 1
    if A[j] <= x
      i = i + 1
      exchange A[i] with A[j]
  exchange A[i + 1] with A[r]
  return i + 1 
```

随机选取主元`A[i]`,确保在数组中所有`A[j] <= A[i]`($j<i$), 所有`A[k] >= A[i]`($k>i$)

    证明循环不变式:这种排序方法是稳定的.
|平均 |最差 |
|-|-|
| $O(n\lg n)$|$O(n^2)$ |

*Note: 对于任意确定的比例(甚至任意的极不均匀)的划分,复杂度总是均匀的划分的常数倍.*

**随机化选择主元时的时间复杂度**：对于时间复杂度为$O(n^2)$的排序算法,例如插入排序,对于数组中任意的两项`A[i]`和`A[j]`,它们都在排序过程中被比较了. 而对于快速排序,数组中的一项只会与某个主元比较,也即,对于数组的两项`A[i]`和`A[j]`,只有`A[i]`或`A[j]`被选为主元,它们才会被比较.

### 排序算法的下界
把比较排序抽象为一棵决策树:


### 桶排序

## 分治法

### 分析时间复杂度
**代入**：
    猜测一个界，然后用数学归纳法证明这个界是正确的。

safasgf

**递归树法**： 
    将递归式转换为一棵树，其结点表示不同层次的递归调用产生的代价。然后采用边界和技术来求解递归式。

safsaf

**主方法**: 
    考虑一个分治算法的递推式:
$$ T(n) = aT(\frac{n}{b}) + f(n) $$

我们有**主定理**：
对于$T(n)$的递归式：
$$T(n) = aT(n/b)+ f(n)$$

$T(n)$有如下渐进界:
1. 若对某个常数$\epsilon >0$ 有$f(n)=O(n^{\log_b a - \epsilon})$, 则$T(n) = \Theta(n^{log_b a})$.
2. 若$f(n) = \Theta(n^{\log_b a})$, 则$T(n) = \Theta(n^{\log_b a}\lg n)$.
3. 若对某个常数 $\epsilon >0$ 有 $f(n) = \Omega (\log_b a \lg n)$, 且对某个常数 $c<1$ 和所有足够大的 $n$ 有 $af(n/b) \leq cf(n)$, 则 $T(n)=\Theta(f(n))$.



**证明**: 
考虑以下的引理: 对于递归式
$$ T(n) = 
    \begin{cases} \Theta(1), & \text{if } n = 1 \\\\ 
    aT(n/b) + f(n), & \text{if } n = b^i \end{cases} $$
其中 $i$ 是正整数. 那么
$$ T(n) = \Theta(n^{\log_b a}) + \sum_{j=0}^{\log_b n - 1} a^j f(n/b^j) $$
第一项与$n=1$时$T(n)$的时间开销有关 ( *最终,产生了$a^{\log_b n} = n^{\log_b a}$ 个规模为$\Theta(1)$ 的子问题* ); 而后一项与函数$f(n)$有关.而对于后一项的和式,令$g = \sum_{j=0}^{\log_b n - 1} a^j f(n/b^j) $, 我们证明：
1. 若对于某个常数 $\epsilon > 0$ 有 $f(n) = O(n^{\log_b a - \epsilon})$, 则 $g(n) = O(n^{\log_b a}) $.
2. 若 $f(n) = \Theta(n^{\log_b a})$, 则$g(n) = \Theta(n^{\log_b a}\lg n)$.
3. 若对于某个常数$c<1$和所有足够大的$n$有$af(n/b) \leq cf(n)$, 则$g(n) = \Theta(f(n))$.



### 最大子数组问题

**合并**：在$O(n)$内寻找包含中点的最大子数组.

$$ T(n) = T(\frac{n}{2}) + \Theta(n) $$
显然算法的时间复杂度为$\Theta(n\lg n)$.