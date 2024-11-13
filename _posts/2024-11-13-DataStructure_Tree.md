---
title: "数据结构——树"
date: 2024-11-13
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

## 二叉搜索树(Binary Search Trees)

为了改进搜索性能，我们可以使用二叉搜索，最基础的改进是引用中间节点，然后翻转节点指针遍历两边；同样，我们可以这样向每个递归半部分的中间添加指针以进一步优化，这样就形成了二叉树，每个节点都一分为二。

<div class="photo">
     <img src="/assets/images/CS61B/BSTbegin.png">
</div>

BTS 二叉搜索树：除了需要满足二叉树的定义，对树中的每个节点还需满足：

- 节点 X 左侧子树中的每个节点的值都小于 X 的值；
- 节点 X 右侧子树中的每个节点的值都大于 X 的值。

基础的 BST 模块如下：

```java
private class BST<Key> {
    private Key key;
    private BST left;
    private BST right;

    public BST(Key key, BST left, BST Right) {
        this.key = key;
        this.left = left;
        this.right = right;
    }

    public BST(Key key) {
        this.key = key;
    }
}
```

接下来我们完成 BTS 模块中的一些操作。

### 搜索

find 操作的代码如下：

```java
static BST find(BST T, Key sk) {
   if (T == null)
      return null;
   if (sk.equals(T.key))
      return T;
   else if (sk < T.key)
      return find(T.left, sk);
   else
      return find(T.right, sk);
}
```

### 插入

```java
static BST insert(BST T, Key ik) {
  if (T == null)
    return new BST(ik);
  if (ik < T.key)
    T.left = insert(T.left, ik);
  else if (ik > T.key)
    T.right = insert(T.right, ik);
  return T;
}
```

### 删除

删除操作中，我们需要将情况分为三类：

- 无子节点：直接删除其父指针即可；
- 只有一个子节点：将父节点的子指针分配给节点的子节点即可；
- 有两个子节点：我们选择一个新节点来替换需要删除的节点，新节点需要满足二叉搜索树的条件，可以用于替换的是左侧子树中的最大节点或右侧子树中的最小节点。这称为 Hibbard delete。

代码如下：

```java
private static BTS findMin(BTS node) {
    while (node.left != null) {
        node = node.left;
    }
    return node;
}

static BTS delete(BTS T, Key dk) {
    if (T == null) {
        return null;
    }
    if (dk < T.key) {
        T.left = delete(T.left, dk);
    } else if (dk > T.key) {
        T.right = delete(T.right, dk);
    } else {
        if (T.left == null && T.right == null) {
            return null;
        } else if (T.left == null) {
            return T.right;
        } else if (T.right == null) {
            return T.left;
        } else {
            BTS successor = findMin(T.right);
            T.key = successor.key;
            T.right = delete(T.right, successor.key);
        }
    }
    return T;
}
```

## B-树
