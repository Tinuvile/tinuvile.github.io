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

静态变量应使用类的名称而不是特定实例来访问。但事实上，Java 在技术上允许通过实例名称访问静态变量。

### public static void main(String[ ] args)

args 是一个用于接受命令行输入的字符串数组，它允许用户在运行程序时传递动态值，从而使 Java 应用能根据不
同输入执行不同操作。

## Testing

### Ad Hoc Testing

### JUnit Testing

org.junit 库提供了许多有用的方法与功能来简化测试的编写。

- 我们将 import 语句添加到文件的顶部；

  ```java
  import org.junit.Test;
  import static org.junit.Assert.*
  ```

- 然后再每个检测前面加上

  ```java
  @Test
  ```

## Intro and interfaces

### The Problem

重载的缺点：

- 非常重复且丑陋，因为代码块几乎相同；
- 需要维护的代码更多；
- 如果我们希望添加变量类型，则需要写更多的重载函数。

### Hypernyms, Hyponyms, and Interface Inheritance

接口涉及到 Java 中的关系层次，最基础的即为上位词与下位词。现在有 SLList 和 AList 两个 Java 列表类，我们希望创建一个更通用的列表类，命名为 List61B，它就是 SLList 和 AList 的上位词，也是 Java 中所说的接口 interface。我们可以注意到，此处接口的内容中实际上只指定了需要做什么，但没有给出具体的实现。

```java
public interface List61B<Item> {
    public void addFirst(Item x);
    public void add Last(Item y);
    public Item getFirst();
    public Item getLast();
    public Item removeLast();
    public Item get(int i);
    public void insert(Item x, int position);
    public int size();
}
```

然后，我们还需要指定 AList 和 SLList 是 List61B 的下位词，我们使用关键词 implements。实际的含义是：保证下位词将拥有和定义上位词接口中指定的所有属性和方法。

```java
public class SLList<Item> implements List61B<Item>
```

### Overriding

在子类中实现接口中指定的方法时，可以在方法的顶部加入标签

```java
@Override
```

### Interface Inheritance

接口继承指的是子类继承超类的所有方法/行为的关系，这种继承可以是多代的。

### Implementation Inheritance

上面的接口中我们没有进行任何方法的实现，倘若在接口中进行方法的实现，则为实现继承，需要包含关键词 defalut，所有实现该超类的子类都可以使用该方法。

```java
default public void print() {
    for (int i = 0; i < size(); i += 1) {
        System.out.print(get(i) + " ");
    }
    System.out.println();
}
```

同时若我们在 SLList 重新实现这个方法并覆盖，那么当我们在 SLList 上调用该方法，都会调用覆盖后的方法。

```java
@Override
public void print() {
    for (Node p = sentinel.next; p != null; p = p.next) {
        System.out.print(p.item + " ");
    }
}
```

## Extends, Casting, Higher Order Functions

### Extends

如果我们想定义类之间的层次结构关系，例如我们想构建一个 RotatingSLList，它具有与 SLList 相同的功能
，但有一个额外的操作 rotateRight 将最后一项带到列表的前面。因此，我们希望可以继承 SLList 中的代码，
使用关键词 extends

```java
public class RotatingSLList<Item> extends SLList<Item>
```

现在，extends 让我们保留了 SLList 的基础功能，并可以进行修改和添加其他功能。实际上，通过该关键词，子
类将继承父类的所有成员，包括：

- 所有实例和静态变量
- 所有方法
- 所有嵌套类

需注意的是，构造函数不能继承，private 成员也不能由子类直接访问。但是，Java 要求所有构造函数都必须调用其超类的构造函数之一开始。

### The Object Class

Java 中的每个类实际上都是 Object 类或 Object 类的子类。而 Object 类主要提供了每个 Object 都能执行的一些操作。

### Encapsulation

封装是我们对抗复杂性的重要手段之一，也是模块化的重要手段。我们首先来讨论继承如何破坏封装。假设我们在 Dog 类中有两个方法如下：

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

从用户角度看，二者的功能是完全相同的。但倘若用户想定义一个子类并覆盖 barkMany 的方法

```java
@Override
public void barkMany(int N) {
    System.out.println("As a dog, I say: ");
    for (int i = 0; i < N; i += 1) {
        bark();
    }
}
```

程序将进入无限循环。

### Type Checking and Casting

强制类型转换强大却十分危险。

### Higher Order Functions

高阶函数是将其他函数视为数据的函数，在 Java 中，我们可以利用接口继承来实现。

## Subtype Polymorphism vs. HoFs

### Subtype Polymorphism

多态性的核心意思是“多种形式”，指对象具有多种形式或类型。假设我们想编写一个 python 程序，它打印两个对象中较大的字符串表示，那么有两种方法可以解决这个问题。

1. 显式 HoF 方法

   ```python
   def print_larger(x, y, compare, stringify):
    if compare(x, y):
        return stringify(x)
    return stringify(y)
   ```

2. 亚型多态型方法

   ```python
   def print_larger(x, y):
    if x.largerThan(y):
        return x.str()
    return y.str()
   ```

假设我们想编写一个函数 Max，该函数接受任何数组（无论类型），并返回数组中的最大项目。这在 python 或者 C++中或许可以通过重新定义运算符的含义实现，但在 Java 中，我们的思路是创建一个接口来保证任何实现类都包含一个比较方法。

```java
public interface OurComparable {
    public int compareTo(Object o);
}
```

我们这样定义实现：

- 如果 this < o，则返回-1；
- 如果 this = o，则返回 0；
- 如果 this > o，则返回 1。

```java
public class Bird implements OurComparable {
    private String name;
    private int beauty;

    public Bird(String n, int b) {
        name = n;
        beauty = b;
    }

    public void sing() {
        System.out.println(name + " says: wow");
    }

    public int compareTo(Object o) {
        //需强制类型转换为Bird
        Bird littleBird = (Bird) o;
        if (this.beauty < littleBird.beauty) {
            return -1;
        } else if (this.beauty == littleBird.beauty) {
            return 0;
        }
        return 1;
    }
}
```

那么现在我们可以将函数推广到接受对象，并确保所有对象都实现了该方法。下面的方法返回 OurComparable 类型的对象

```java
public static OurComparable max(OurComparable[] items) {
    int maxDex = 0;
    for (int i = 0; i < items.length; i += 1) {
        int cmp = items[i].compareTo(items[maxDex]);
        if (cmp > 0) {
            maxDex = i;
        }
    }
    return items[maxDex];
}
```

## Libraries, Abstract Classes, Packages
