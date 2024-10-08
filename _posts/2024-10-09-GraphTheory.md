---
title: "图论基础"
date: 2024-10-09
categories: [learning]
tags: [图论]
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
---

<small>本文为 CS70Note5 的学习笔记</small>

## 基础概念与常用术语

### 无向图与定向图

### 顶点(vertex/vertices)

### 边(edge)

### 度(degree)

    the degree of vertex u ∈ V is the number of edges incident to u, i.e., degree(u) = |{v ∈ V : {u, v} ∈ E}|

对于有向图

    the in-degree of a vertex u is the number of edges from other vertices to u
    the out-degree of u is the number of edges from u to other vertice

### 一些术语

<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <style>  
        table {  
            margin: auto; /* 将表格整体居中 */  
            border-collapse: collapse;  
            width: 80%; /* 可根据需要调整宽度 */  
        }  
        th, td {  
            border: 1px solid #000; /* 边框样式 */  
            text-align: center; /* 内容居中对齐 */  
            padding: 8px;  
        }  
        .note {  
            font-size: 0.8em; /* 设置较小的字体尺寸 */  
            text-align: center;  
        }  
    </style>  
</head>
<body>
<table>  
  <thead>  
    <tr>  
      <th></th>  
      <th>no repeated vertices</th>  
      <th>no repeated edges</th>  
      <th>start = end</th>  
    </tr>  
  </thead>  
  <tbody>  
    <tr>  
      <td>Walk</td>  
      <td></td>  
      <td></td>   
      <td></td>   
    </tr>  
    <tr>  
      <td>Path</td>   
      <td>✓</td>  
      <td>✓</td>  
      <td></td>  
    </tr>  
    <tr>  
      <td>Tour</td>   
      <td></td>  
      <td></td>  
      <td>✓</td>  
    </tr>  
    <tr>  
      <td>Cycle</td>   
      <td>✓*</td>   
      <td>✓</td>  
      <td>✓</td>  
    </tr>  
  </tbody>  
</table>

<p class="note">*except for start and end vertices</p>
</body>

## 科尼斯堡七桥问题(Seven Bridges of Koenigsberg)

> Given a graph G (in this case, G is an abstraction of Königsberg), is there a walk in G that uses each edge exactly once? We call any such walk in a graph an Eulerian walk.

> Theorem 5.1 (Euler’s Theorem (1736)). An undirected graph G = (V, E) has an Eulerian tour iff G is even
> degree, and connected (except possibly for isolated vertices)
