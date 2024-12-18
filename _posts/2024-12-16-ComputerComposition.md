---
title: "计算机组成原理复习"
date: 2024-12-16
categories: [learning]
tags: [计算机组成原理]
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
---

## 计算机系统概率

- <strong>知识点</strong>：计算机系统硬件组成以及几个典型的性能指标

计算机系统由软件和硬件两大部分组成。二者在逻辑功能上是等效的，即对于一个具体功能，可以用两者进行实现，但是实现成本和速度会有比较大的差别。

### 硬件组成

现代计算机系统的硬件结构由五个部件组成：运算器、存储器、控制器、输入设备、输出设备。而运算器和控制器往往在一个芯片上，即是 CPU。存储器又分为内存储器（主存）和外存储器，CPU+内存为主机系统。

<div class="photo">
     <img src="/assets/images/ComputerComposition/屏幕截图 2024-12-16 174531.png">
</div>

冯·诺伊曼结构：

<div class="photo">
     <img src="/assets/images/ComputerComposition/屏幕截图 2024-12-16 174904.png">
</div>

- 运算部件：
  由运算器（ALU，算术逻辑单元）和通用寄存器组（GPR，暂存运算数据和中间结果）构成。

- 内存：
  内存由大量存储单元组成，构成一个按地址访问的一维线性空间，每个存储单元有一个对于的地址，每个存储单元又可以存放多个二进制位。内存有两个重要的寄存器，地址寄存器 AR 和数据寄存器 DR，在读写操作中发挥作用。

<div class="photo">
     <img src="/assets/images/ComputerComposition/屏幕截图 2024-12-16 175410.png">
</div>

- 控制器：
  由六部分组成。指令寄存器（IR，存放当前正在执行的指令），程序计数器 （PC，存放当前正在执行的指令的地址），指令译码器（译码形成相应的控制信号和后续的指令信息），时钟脉冲（CP，协调计算机各部件操作的同步主时钟，工作频率称为计算机的主频），微操作控制部件。

- 输入/输出设备

### 性能指标

- 主频：衡量计算机工作速度，一秒钟内发出的电子脉冲数（Hz）；
- 运算速度：每秒执行多少次指令（MIPS，百万条指令/秒）或完成多少次浮点运算（MFLOPS，百万次浮点运算/秒）；
- 基本字长：直接参与运算的数据字的二进制位数，标志着运算精度，现在多为 32 位和 64 位；
- 主存容量：现在通常是 8G，16G；
- 主存存取周期：对主存连续两次访问所允许的最小时间间隔；
- 配置的外部设备及其性能指标
