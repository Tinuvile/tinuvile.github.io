---
title: "java相关笔记"
date: 2024-10-11
categories: [CS61B]
tags: [Java, CS61B]
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
---

<small>[原文见 Josh Hug 教授为 CS61B 编写的教材](https://joshhug.gitbooks.io/hug61b/content/wrapping-up-java-syntax.html)</small>

## 继承如何如何破坏封装

假设我们在 Dog 类中有两个方法，如下所示：

```java
public void bark() {
    System.out.println("bark");
}

public void barkMany(int N) {
    for (int i = 0; i < N; i += 1) {
        bark();
    }
}
```

或者我们可以这样实现：

```java
public void bark() {
    barkMany(1);
}

public void barkMany(int N) {
    for (int i = 0; i < N; i += 1) {
        System.out.println("bark");
    }
}
```

封装后，从用户角度看，二者是完全相同的，但如果用户希望定义一个子类并覆盖其中的方法，就可能出现问题。例如：

```java
@Override
public void barkMany(int N) {
    System.out.println("As a dog, I say: ");
    for (int i = 0; i < N; i += 1) {
        bark();
    }
}
```

覆盖后程序就将陷入无限循环。
