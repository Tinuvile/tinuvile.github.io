---
title: "基本逻辑门、多路复用器和解复用器"
date: 2024-10-07
categories: [learning]
tags: [逻辑门, 复用器, 解复用器]
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
---

## 基本逻辑门及多位门

### Nand

与非门，计算两个输入的与运算，然后对结果取反，是构建所有其他逻辑门的基础；

<table>  
  <thead>  
    <tr>  
      <th>输入A</th>  
      <th>输入B</th>  
      <th>输出</th>  
    </tr>  
  </thead>  
  <tbody>  
    <tr>  
      <td>0</td>  
      <td>0</td>  
      <td>1</td>  
    </tr>  
    <tr>  
      <td>0</td>  
      <td>1</td>  
      <td>1</td>  
    </tr>  
    <tr>  
      <td>1</td>  
      <td>0</td>  
      <td>1</td>  
    </tr>  
    <tr>  
      <td>1</td>  
      <td>1</td>  
      <td>0</td>  
    </tr>  
  </tbody>  
</table>

### Not

非门，对单个输入信号取反；

<table>  
  <thead>  
    <tr>  
      <th>输入</th>  
      <th>输出</th>  
    </tr>  
  </thead>  
  <tbody>  
    <tr>  
      <td>0</td>  
      <td>1</td>  
    </tr>  
    <tr>  
      <td>1</td>  
      <td>0</td>  
    </tr>  
  </tbody>  
</table>

### And

与门，输出两个输入信号的与运算结果；

<table>  
  <thead>  
    <tr>  
      <th>输入A</th>  
      <th>输入B</th>  
      <th>输出</th>  
    </tr>  
  </thead>  
  <tbody>  
    <tr>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
    </tr>  
    <tr>  
      <td>0</td>  
      <td>1</td>  
      <td>0</td>  
    </tr>  
    <tr>  
      <td>1</td>  
      <td>0</td>  
      <td>0</td>  
    </tr>  
    <tr>  
      <td>1</td>  
      <td>1</td>  
      <td>1</td>  
    </tr>  
  </tbody>  
</table>

### Or

或门，输出两个输入信号的或运算结果；

<table>  
  <thead>  
    <tr>  
      <th>输入A</th>  
      <th>输入B</th>  
      <th>输出</th>  
    </tr>  
  </thead>  
  <tbody>  
    <tr>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
    </tr>  
    <tr>  
      <td>0</td>  
      <td>1</td>  
      <td>1</td>  
    </tr>  
    <tr>  
      <td>1</td>  
      <td>0</td>  
      <td>1</td>  
    </tr>  
    <tr>  
      <td>1</td>  
      <td>1</td>  
      <td>1</td>  
    </tr>  
  </tbody>  
</table>

### Xor

异或门，输出两个输入信号的异或运算结果，当且仅当输入信号不同时，输出为 1；

<table>  
  <thead>  
    <tr>  
      <th>输入A</th>  
      <th>输入B</th>  
      <th>输出</th>  
    </tr>  
  </thead>  
  <tbody>  
    <tr>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
    </tr>  
    <tr>  
      <td>0</td>  
      <td>1</td>  
      <td>1</td>  
    </tr>  
    <tr>  
      <td>1</td>  
      <td>0</td>  
      <td>1</td>  
    </tr>  
    <tr>  
      <td>1</td>  
      <td>1</td>  
      <td>0</td>  
    </tr>  
  </tbody>  
</table>

### 多位门

一组基本逻辑门的集合；

## 多路复用器和解复用器

### Mux

多路复用器，根据选择位的值，从多个输入中选择一个输出；

<table>  
  <thead>  
    <tr>  
      <th>输入A</th>  
      <th>输入B</th>  
      <th>选择位</th>  
      <th>输出</th>  
    </tr>  
  </thead>  
  <tbody>  
    <tr>  
      <td>X</td>  
      <td>X</td>  
      <td>0</td>  
      <td>A</td>  
    </tr>  
    <tr>  
      <td>X</td>  
      <td>X</td>  
      <td>1</td>  
      <td>B</td>  
    </tr>  
  </tbody>  
</table>

### DMux

解复用器，将单个输入信号根据选择位的值传输到多个输出中的一个；

<table>  
  <thead>  
    <tr>  
      <th>输入</th>  
      <th>选择位</th>  
      <th>输出A</th>  
      <th>输出B</th>  
    </tr>  
  </thead>  
  <tbody>  
    <tr>  
      <td>X</td>  
      <td>0</td>  
      <td>X</td>  
      <td>0</td>  
    </tr>  
    <tr>  
      <td>X</td>  
      <td>1</td>  
      <td>0</td>  
      <td>X</td>  
    </tr>  
  </tbody>  
</table>

## 多路复用和解复用的拓展

### Or8Way:

8 路或门。将 8 个单比特输入信号进行“或”运算，输出单个比特；

<table>  
  <thead>  
    <tr>  
      <th>输入1</th>  
      <th>输入2</th>  
      <th>输入3</th>  
      <th>输入4</th>  
      <th>输入5</th>  
      <th>输入6</th>  
      <th>输入7</th>  
      <th>输入8</th>  
      <th>输出</th>  
    </tr>  
  </thead>  
  <tbody>  
    <tr>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
    </tr>  
    <tr>  
      <td>1</td>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>1</td>  
    </tr>  
    <!-- More rows as needed -->  
  </tbody>  
</table>

### Mux4Way16:

4 路 16 位多路复用器。根据两位选择信号，从四个 16 位输入向量中选择一个输出；

<table>  
  <thead>  
    <tr>  
      <th>输入0</th>  
      <th>输入1</th>  
      <th>输入2</th>  
      <th>输入3</th>  
      <th>选择位</th>  
      <th>输出</th>  
    </tr>  
  </thead>  
  <tbody>  
    <tr>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>00</td>  
      <td>输入0</td>  
    </tr>  
    <tr>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>01</td>  
      <td>输入1</td>  
    </tr>  
    <tr>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>10</td>  
      <td>输入2</td>  
    </tr>  
    <tr>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>11</td>  
      <td>输入3</td>  
    </tr>  
  </tbody>  
</table>

### Mux8Way16:

8 路 16 位多路复用器。根据三位选择信号，从八个 16 位输入向量中选择一个输出；

<table>  
  <thead>  
    <tr>  
      <th>输入0</th>  
      <th>输入1</th>  
      <th>输入2</th>  
      <th>输入3</th>  
      <th>输入4</th>  
      <th>输入5</th>  
      <th>输入6</th>  
      <th>输入7</th>  
      <th>选择位</th>  
      <th>输出</th>  
    </tr>  
  </thead>  
  <tbody>  
    <tr>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>000</td>  
      <td>输入0</td>  
    </tr>  
    <tr>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>X</td>  
      <td>001</td>  
      <td>输入1</td>  
    </tr>  
    <!-- More rows as needed -->  
  </tbody>  
</table>

### DMux4Way:

4 路解复用器。将单个输入信号根据两位选择信号分配到四个输出之一；

<table>  
  <thead>  
    <tr>  
      <th>输入</th>  
      <th>选择位</th>  
      <th>输出0</th>  
      <th>输出1</th>  
      <th>输出2</th>  
      <th>输出3</th>  
    </tr>  
  </thead>  
  <tbody>  
    <tr>  
      <td>X</td>  
      <td>00</td>  
      <td>X</td>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
    </tr>  
    <tr>  
      <td>X</td>  
      <td>01</td>  
      <td>0</td>  
      <td>X</td>  
      <td>0</td>  
      <td>0</td>  
    </tr>  
    <tr>  
      <td>X</td>  
      <td>10</td>  
      <td>0</td>  
      <td>0</td>  
      <td>X</td>  
      <td>0</td>  
    </tr>  
    <tr>  
      <td>X</td>  
      <td>11</td>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
      <td>X</td>  
    </tr>  
  </tbody>  
</table>

### DMux8Way:

8 路解复用器。将单个输入信号根据三位选择信号分配到八个输出之一；

<table>  
  <thead>  
    <tr>  
      <th>输入</th>  
      <th>选择位</th>  
      <th>输出0</th>  
      <th>输出1</th>  
      <th>输出2</th>  
      <th>输出3</th>  
      <th>输出4</th>  
      <th>输出5</th>  
      <th>输出6</th>  
      <th>输出7</th>  
    </tr>  
  </thead>  
  <tbody>  
    <tr>  
      <td>X</td>  
      <td>000</td>  
      <td>X</td>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
    </tr>  
    <tr>  
      <td>X</td>  
      <td>001</td>  
      <td>0</td>  
      <td>X</td>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
      <td>0</td>  
    </tr>  
    <!-- More rows as needed -->  
  </tbody>  
</table>

[具体实现程序](https://github.com/Tinuvile/nand2tetris/tree/master/nand2tetris/projects/1)
