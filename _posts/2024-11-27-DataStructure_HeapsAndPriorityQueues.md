---
title: "数据结构——堆和优先级队列"
date: 2024-11-27
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

## Priority Queues

二叉搜索允许我们有效地进行快速搜索树，但如果我们更关心如何快速找到最小或是最大的元素呢？下面先给出最小优先级队列 Priority Queue 的 Abstract 数据类型：

```java
/** (Min) Priority Queue: Allowing tracking and removal of
 * the smallest item in a priority queue. */
public interface MinPQ<Item> {
    /** Adds the item to the priority queue. */
    public void add(Item x);
    /** Returns the smallest item in the priority queue. */
    public Item getSmallest();
    /** Removes the smallest item from the priority queue. */
    public Item removeSmallest();
    /** Returns the size of the priority queue. */
    public int size();
}
```

## Heaps

对于 PQ 操作，前面文章中所有数据结构中，用二叉搜索树实现是运行时间最佳的，但仍然可以进一步优化提升。
