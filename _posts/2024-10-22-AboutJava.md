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

总结（接口）：

- 所有方法必须是 public；
- 所有变量必须是 public static final；
- 无法实例化；
- 默认情况下，所有方法都是抽象的，除非指定为 default；
- 可以为每个类实现多个接口。

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

### Abstract Data Types (ADTS)

以上文接口部分的代码为例，我们称 List61B 为 Abstract 数据类型。因为它只附带实现而并未以任何具体方式展示这些实现。

### Java Libraries

Java 中具有一些内置的 Abstract 数据类型在 Java 库中。java.util 库中有三个最重要的 ADT：

- List：项的有序集合，常用实现是 ArrayList；
- Set：严格唯一的项的无序集合（无重复），常用实现是 HashSet；
- Map：键值对的集合，可以通过 key 访问该值，常用实现是 HashMap。

### Abstract classes

抽象类可以理解成介于 interfaces 和 concrete 类之间的新类，总体来说，它可以做所有 interfaces 可以做的，甚至更多。它的特征如下：

- 方法可以是 public 或者 private；
- 可以包含任何类型的变量；
- 无法实例化；
- 默认情况下，方法是具体的，除非指定为 abstract；
- 每个类只能实现一个。

### Packages

## Autoboxing

### Industrial Strength Syntax

### Autoboxing and Unboxing

Java 只有 8 个基元类型，其他都是引用类型。在 Java 语法中，我们不能提供原始类型作为泛型的实际类型参数，而需要使用相应的 reference type。不过幸运的是，Java 可以在原始类型和包装类型之间进行隐式转换，即会在原始类型和相应引用类型之间"box"和"unbox"值。

<table>  
  <thead>  
    <tr>  
      <th>Primitive</th>  
      <th>Class</th>    
    </tr>  
  </thead>  
  <tbody>  
    <tr>  
      <td>byte</td>  
      <td>Byte</td>
    </tr>  
    <tr>  
      <td>short</td>  
      <td>Short</td>
    </tr>  
    <tr>  
      <td>int</td>  
      <td>Integer</td>
    </tr>
    <tr>  
      <td>long</td>  
      <td>Long</td>
    </tr>
    <tr>  
      <td>float</td>  
      <td>Float</td>
    </tr>
    <tr>  
      <td>double</td>  
      <td>Double</td>
    </tr>
    <tr>  
      <td>boolean</td>  
      <td>Boolean</td>
    </tr>
    <tr>  
      <td>char</td>  
      <td>Character</td>
    </tr>
  </tbody>  
</table>

但需要注意的是：

- 数组是永远不会自动进行 boxing 或者 unboxing 的；
- box 和 unbox 会对性能产生可衡量的影响，运行速度会变慢；
- 包装类型使用的内存比基元类型多很多。

### Widening

类似的，Java 也会在代码需要时自动短值赋长值进行加宽。

## Immutability

不可变数据类型，即其实例在实例化后无法以任何可观察的方式进行改变。任何具有非私有变量的数据类型都是可变的，除非用 final 进行了声明。
但需要注意的是，将引用声明为 final 并不会使引用指向的对象不可变，例如：

```java
public final ArrayDeque<String>() deque = new ArrayDeque<String>();
```

变量 deque 初始化后，始终指向同一个 ArrayDeque 实例，但可以修改这个 ArrayDeque 的内容，如添加、删除和更改元素。同时使用 Reflection API 甚至可以对私有变量进行更改。

## Generics

### Creating Another Generic Class

```java
package Map61B;

import java.util.List;
import java.util.ArrayList;

/***
 * An array-based implementation of Map61B.
 ***/
public class ArrayMap<K, V> implements Map61B<K, V> {

    private K[] keys;
    private V[] values;
    int size;

    public ArrayMap() {
        keys = (K[]) new Object[100];
        values = (V[]) new Object[100];
        size = 0;
    }

    /**
    * Returns the index of the key, if it exists. Otherwise returns -1.
    **/
    private int keyIndex(K key) {
        for (int i = 0; i < size; i++) {
            if (keys[i].equals(key)) {
            return i;
        }
        return -1;
    }

    public boolean containsKey(K key) {
        int index = keyIndex(key);
        return index > -1;
    }

    public void put(K key, V value) {
        int index = keyIndex(key);
        if (index == -1) {
            keys[size] = key;
            values[size] = value;
            size += 1;
        } else {
            values[index] = value;
        }
    }

    public V get(K key) {
        int index = keyIndex(key);
        return values[index];
    }

    public int size() {
        return size;
    }

    public List<K> keys() {
        List<K> keyList = new ArrayList<>();
        for (int i = 0; i == size; i++) {
            keyList.add(keys[i]);
        }
        return keyList;
    }
}
```

### ArrayMap and Autoboxing Puzzle

### Type upper bounds

在泛型中使用 extends 时，与类继承不同，此处表明的是限制与约束。

```java
public class Box<T extends Comparable<T>> {
    //内容
}
```

这意味着类型 T 必须实现 Comparable 接口，即任何传递给 Box 的类型必须可以进行比较。

## Lists, Sets, and ArraySet

### Lists in Real Java Code

之前我们学习的是自己创建 AList 和 SLList，Java 库实际上提供了关于列表的一些内置接口和实现，我们可以使用全名进行访问：

```java
java.util.List<Integer> L = new java.util.ArrayList<>();
```

也可以通过导入 Java 库的方式

```java
import java.util.List;
import java.util.ArrayList;

public class Example {
    public static void main(String[] args) {
        List<Integer> L = new ArrayList<>();
        L.add(5);
        L.add(10);
        System.out.println(L);
    }
}
```

### Sets

```java
import java.util.Set;
import java.util.HashSet;
```

## Throwing Exceptions

隐式异常会导致正常的控制流停止，我们可以使用 throw 关键词引发自己的异常，这样可以提供自己的错误消息，还可以将信息提供给程序中的错误处理代码，这样就是一个我们故意抛出的显式异常

### Catching Exceptions

通过 catch 异常，我们可以防止程序崩溃，关键词 try 和 catch 会中断程序的正常流程，从而保护程序免受异常的影响。例如：

```java
Dog d = new Dog("Lucy", "Retriever", 80);
d.becomeAngry();

try {
    d.receivePat();
} catch (Exception e) {
    System.out.println("Tried to pat: " + e);
}
System.out.println(d);
```

此代码的输出是

```text
$ java ExceptionDemo
Tried to pat: java.lang.RuntimeException: grrr... snarl snarl
Lucy is a displeased Retriever weighing 80.0 standard lb units.
```

我们还可以使用 catch 语句来采取纠正措施

```java
Dog d = new Dog("Lucy", "Retriever", 80);
d.becomeAngry();

try {
    d.receivePat();
} catch (Exception e) {
    System.out.println(
    "Tried to pat: " + e);
    d.eatTreat("banana");
}
d.receivePat();
System.out.println(d);
```

输出为：

```text
$ java ExceptionDemo
Tried to pat: java.lang.RuntimeException: grrr... snarl snarl
Lucy munches the banana

Lucy enjoys the pat.

Lucy is a happy Retriever weighing 80.0 standard lb units.
```

### Checked vs Unchecked Exceptions

同时，也存在一些必须处理才能通过编译器编译的异常，我们将这些称为"checked"异常，必须选中。如下图所示：

<div class="photo">
     <img src="/assets/images/checked_exceptions.png">
</div>

而处理它们的方式有两种：

- catch
- specify

```java
// catch
public static void main(String[] args) {
    try {
        gulgate();
    } catch(IOException e) {
        System.out.println("Averted!");
    }
}

// specify
public static void main(String[] args) throws IOException {
    gulgate();
}
```

## Iteration

Java 允许我们使用一种方便的语法（有时称为"foreach"或者"enhanced for"）来循环遍历 List，例如：

```java
List<Integer> friends =
new ArrayList<Integer>();
friends.add(5);
friends.add(23);
friends.add(42);
for (int x : friends) {
    System.out.println(x);
}
```

此方法我们可以自己实现，使用迭代器，首先定义一个返回迭代器对象的方法

```java
public Iterator<E> iterator();
```

然后使用它遍历列表

```java
List<Integer> friends = new ArrayList<Integer>();
Iterator<Integer> seer = friends.iterator();

while (seer.hasNext()) {
    System.out.println(seer.next());
}
```

这个方法的效果与上面完全相同。

## Packages

### Creating a Package

1. 将包名称放在此包中每个文件的顶部

   ```java
    package jason.tinuvile.bird;

    public class Bird {
        private String name;
    }
   ```

2. 将文件储存在具有相应文件夹名称的文件中，该文件夹的名称应该与包匹配

   ```text
   <your_project_root>
   │
   └───jason
       └───tinuvile
           └───bird
               └───Bird.java
   ```

### Default packages

任何文件顶部没有明确包名的 Java 类都将被自动视为 default 包的一部分。

### JAR Files

## Access Control

- private 私有成员只有给定类中的代码才能访问，子类、包和其他外部类都无法访问；
- package private 意味着属于同一个 package 的类可以访问，但子类不可以；
- protected 只有同一包和子类可以访问；
- public 访问权限对所有人打开。

## Encapsulation, API, ADT
