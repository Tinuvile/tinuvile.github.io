---
title: "数据结构——哈希"
date: 2024-11-19
categories: [CS61B]
tags: [Java, CS61B]
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
---

[详细介绍见 Josh Hug 为 Berkeley CS61B 编写的教材](https://joshhug.gitbooks.io/hug61b/content/)

[最新版本](https://cs61b-2.gitbook.io/cs61b-textbook)

[一个数据结构可视化网站](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html)

## Data Indexed Arrays

数组的基本操作运行时间是非常优秀的，我们希望能将数据转化成索引并将其储存在数组中。

首先我们考虑的方法叫做 <strong>DataIndexedIntegerSet</strong>，创建一个 <strong>ArrayList</strong>，默认情况下的值全部为 <strong>false</strong>，输入的索引对应的值则为 <strong>true</strong>。但这种方法一来内存占用过多，二来只能用于 <strong>int</strong>。

于是我们进行改进，方法为 <strong>DataIndexedWordSet</strong>，我们试图将 <strong>string</strong> 与索引一一对应。这种情况下有两种方法：一是使用 <strong>string</strong> 字符串的首字母，已有重复再看下一个字母；或者，我们采用二十六进制将字符串转化数字，这种方法可以保证字符串与数字是一一对应的。

而我们知道有一种称为 <strong>ASCII</strong> 的字符格式，每个字符都有一个整数，最大对应的数字是 126，我们使用 126 进制实现 <strong>DataIndexedEnglishWordSet</strong> 即可。但对于中文，最大对应的数字是 40959，想要储存一个 3 个字符的中文词汇，我们需要用到大于 39 万亿的数组，这太大了！因此我们希望做出改进，改进方法就是使用 <strong>hashCode</strong>。

## Hash Code

我们希望将对象转化为数字表示形式。使用 <strong>Hash Code</strong> 将键转换为不同的值，再将该数字转换为索引来访问数组。

```java
public class String {
    public int hashCode() {
        // implementation here
    }
}
```

但这样转换需要的数组太大，占用内存过多，我们希望将大数也进一步转换为介于 0 和 9 之间的值，即采用模运算

```java
Math.floorMod(key.hashCode(), array.length)
```

## Handling Collisions

在哈希表中，当数组中有多个具有相同索引的元素时，就会发生冲突。通常的处理方法有两种：

- 线性探测(Linear Probing)：当发生哈希碰撞时，线性探测会检查数组中的下一个位置，如果该位置被占用，则继续检查下一个位置，直到找到一个空闲的位置。这种方法常见于分布式哈希表中。
- 外部链接(External Chaining)：更简单的解决方案是将具有相同哈希值的所有键一起储存在另一个集合中，称为 <strong>bucket</strong>。

## Resizing & Hash Table Performance

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>
<body>
     <p>
     无论我们的 <strong>hashCode</strong> 算法多好，在添加了一定量的键值后一定会出现越来越多的冲突。因此，在哈希表填满后，我们需要对哈希表底层数组进行拓展，这种方法有点类似于之前 <strong>ArrayList</strong> 中拓展数组的方法。
     </p>
     <p>
     我们使用 <strong>Load Factor</strong> 来跟踪哈希表的填充程度，定义为插入的元素数量于数组总物理长度的比率，即\(\text{load factor} = \frac{\text{size()}}{\text{array.length}}\)。然后我们定义我们允许的最大负载因子，如果添加键值对导致超出，则哈希表需要进行大小调整。
     </p>
</body>
