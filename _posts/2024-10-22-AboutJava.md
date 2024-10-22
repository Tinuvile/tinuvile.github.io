---
title: "Java相关简介"
date: 2024-10-22
categories: [CS61B]
tags: [Java, CS61B]
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
---

[原文见 Josh Hug 为 Berkeley CS61B 编写的教材](https://joshhug.gitbooks.io/hug61b/content/)

## Essentials

### Static Typing

在 Java 中，每个变量和表达式都有一个 static type 变量可以且只可以包含该类型的值。另外，变量的类型永远不会改变。

## Objects

### Static Methods

Java 中的所有代码都必须是类（或类似的东西）的一部分，大部分代码都是在 methods 内部编写的。

### Instance Variables and Objects Instantiation

类可以进行实例化，实例可以保存数据。注意：<br>

- Java 中的 Object 是任何类的实例；
- 类中自己的变量，也称实例变量或非静态变量，必须在类中声明；
- 在类中创建的方法没有关键词，我们将这类方法称为实例方法或非静态方法；
- 要调用该方法，我们必须先使用关键词 new 进行实例化；
- 一旦对象被实例化，就可以将其分配给适当类型的声明变量；
- 类的变量和方法也称为类的成员；
- 类 Bird 的成员使用 Bird.xxx 进行访问；

### Constructors in Java

我们通常使用构造函数在面向对象语言中构造对象，我们只需向类中加一个"constructor"

```java
public class Bird {
    public int beauty;

    //constructor
    public Bird(int w) {
        beauty = b;
    }

    public void sing() {
        if (beauty < 10) {
            System.out.println("yipyipyip!");
        } else if (beauty < 30) {
            System.out.println("ye. ye.");
        } else {
            System.out.println("boooooool!");
        }
    }
}
```

### Array Instantiation, Arrays of Objects

数组在 Java 中同样使用 new 关键词进行实例化，实例化对象的数组也是一样。

```java
public class Array {
    public static void main(String[] args) {
        /* Create an array of five integers. */
        int [] ArrayDemo = new int[5];
        ArrayDemo[3] = 2;
        /* Create an array of two birds. */
        Bird[] birds = new Bird[2];
        Bird[0] = new Bird(9);
        Bird[1] = new Bird(28);
    }
}
```

### Class Methods vs. Instance Methods

Java 允许我们定义两种类型的方法：

- 类方法，静态方法。例如：

  ```java
  x = Math.sqrt(100);
  ```

- 实例方法，非静态方法。例如：

  ```java
  Math m = new Math();
  x = m.sqrt(100);
  ```

实例方法是只能由类的特定实例执行的操作，静态方法是类自身执行的操作。

### Static Variables
