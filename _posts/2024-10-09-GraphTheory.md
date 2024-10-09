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

<style>  
    /* 主文档样式 */  
    body {  
        font-family: 'Arial', sans-serif;  
        line-height: 1.6;  
        color: #333;  
        padding: 20px;  
    }  
    
    /* 标题和节标题样式 */  
    h1, h2, h3, h4, h5 {  
        color: #002147;  
        text-align:  
        margin-bottom: 20px;  
    }  

    /* 单独调整证明文字和注释文字的样式 */  
    .proof-text {  
        font-size: 0.95em; /* 比正文略小 */  
        line-height: 1.5;  
        margin-bottom: 10px;  
        color: #555;  
    }  

    .small-note {  
        font-size: 0.85em; /* 较小的字体用于注释 */  
        color: #777;  
        text-align: left;  
        margin-top: 5px;  
        margin-bottom: 15px;  
    }  
</style>

## 基础概念与常用术语

### 基础概念

无向图与定向图、顶点(vertex/vertices)、边(edge)

度(degree)

    the degree of vertex u ∈ V is the number of edges incident to u, i.e., degree(u) = |{v ∈ V : {u, v} ∈ E}|.

有向图的度

    the in-degree of a vertex u is the number of edges from other vertices to u.
    the out-degree of u is the number of edges from u to other vertices.

树(tree)

    A graph is a tree if it is connected and acyclic (contains no cycles).

平面图(planar graphs)

    A graph is planar if it can be drawn on the plane without crossings.

二分图(bipartite graph)

    G = (V, E) which is a graph where the vertices are split into two groups and edges only go between groups. More formally, we have V = L ∪ R and E ⊆ L × R.

面(face)

    The faces are the regions into which the graph subdivides the plane. One of them is infinite, and the others are finite. The number of faces is denoted f

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

### 问题

> Given a graph G (in this case, G is an abstraction of Königsberg), is there a walk in G that uses each edge exactly once? We call any such walk in a graph an Eulerian walk.

### 定理

> Theorem 5.1 (Euler’s Theorem (1736)). An undirected graph G = (V, E) has an Eulerian tour iff G is even
> degree, and connected (except possibly for isolated vertices)

### 证明

必要性(only if)：我们假设 G 存在一个 Eulerian tour，那么它具有偶数度并连通。<br>

<div class="proof-text"> 
G 存在 Eulerian tour，则每两个有边相连的相邻顶点都必须在 tour 上，则图形是连通的；<br>
而由于 tour 在每个顶点处有 in 和 out，我们将这两条边进行配对，起始边与终止边配对，
全部配对后即可发现每个顶点的度数均为偶数；
</div>
<small class="small-note">注：一个偶数度图表示图中的每个顶点的度都为偶数</small>

充分性(if)：假设图 G 具有偶数度并连通，那么它具有 Eulerian tour。<br>

<div class="proof-text">
在这部分证明中我们会创建三个函数 FindTour(G,s)、Euler(G,s)以及 Splice(T,T')，并对G的大小进行归纳来证明。<br>
<br>
FindTour 函数在图中任意查找一个 tour，以 s 点为起始和终止；

</div>

```cpp
list<int> Graph::findTour(int s) {
    list<int> tour;
    stack<int> stk;
    stk.push(s);

    while (!stk.empty()) {
        int currentVertex = stk.top();
        if (!adj[currentVertex].empty()) {
            int nextVertex = adj[currentVertex].front();
            adj[currentVertex].pop_front();
            adj[nextVertex].remove(currentVertex);
            stk.push(nextVertex);
        } else {
            tour.push_front(currentVertex);
            stk.pop();
        }
    }
    return tour;
}


```

<div class="proof-text">
Euler(G,s)是一个递归算法，输出一个以s为起点和终点的Eulerian tour。递归调用FindTour找出初始路径，
然后针对从图中去除该路径后所形成的每个连通部分进行处理，然后用Splice将所有子路径合并成完整的欧拉回路；
</div>

```cpp
list<int> Graph::Euler(int s) {
    list<int> T = findTour(s);
    vector<list<int>> subTours;

    for (auto it = T.begin(); it != T.end(); ++it) {
        int vertex = *it;
        if (!adj[vertex].empty()) {
            Graph subGraph(V);
            subGraph.adj = adj;
            list<int> subTour = subGraph.Euler(vertex);
            subTours.push_back(subTour);
        }
    }
    return splice(T, subTours);
}
```

<div class="proof-text">
Splice将主路径T与其他子路径结合在一起，将每个子路径插入主路径中与其相交的位置；
</div>

```cpp
list<int> Graph::Euler(int s) {
    list<int> T = findTour(s);
    vector<list<int>> subTours;

    for (auto it = T.begin(); it != T.end(); ++it) {
        int vertex = *it;
        if (!adj[vertex].empty()) {
            Graph subGraph(V);
            subGraph.adj = adj;
            list<int> subTour = subGraph.Euler(vertex);
            subTours.push_back(subTour);
        }
    }
    return splice(T, subTours);
}
```

<div class="proof-text">
我们基于G的变数m进行归纳。<br>
基本情况：m=0，G为空，因此没有可以查找的tour；<br>
归纳假设：Euler(G,s)输出任意偶数度图G的Eulerian tour，且连通图最多有m ≥ 0条边；<br>
归纳步骤：<br>
假设G有m+1条边，通过调用FindTour函数可以找到从起始点s开始的一条路径T，
将T从G中去除，剩下的图仍然是一个偶数度图。<br>
将去除边后的图分为多个连通组件G<sub>1</sub>,G<sub>2</sub>,……,G<sub>k</sub>，
我们知道这些组件每个都是偶数度，且是连通的，而在路径T中，必然会跟G<sub>i</sub>的某个顶点s<sub>i</sub>相交。<br>
根据归纳假设调用Euler(G<sub>i</sub>,s<sub>i</sub>)，我们会得到连通分量G<sub>i</sub>的Eulerian tour，使用Splice函数将
各个连通分量的Eulerian tour 拼接起来，就得到了整体的Eulerian tour。
</div>

## 平面图、欧拉公式与着色

### 定理

> Theorem 5.2. (Euler’s formula) For every connected planar graph, v + f = e + 2

该定理也可以通过归纳证明,根据图形是否是树分为两种情况进行证明，此处省略。

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>  
<body>  
    <blockquote>  
        <p>Theorem 5.2.1. in any planar graph, \(\sum_{i=1}^{f} s_i = 2e \), \(s_i\) means the number of sides of face i.</p>   
    </blockquote>  
</body>

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>
<body>
    <p>在平面图中，如果一条边的两侧具有相同的面，则这条边会被计算两次。而对于平面图，至少有三个顶点，则每个面至少有三条边，
    即 \(s_i ≥ 3\) 。因此有\(3 f ≤ 2e\)，代入Euler公式，可以得到：
    <div style="text-align: center;">\(e ≤ 3v − 6\)</div>
    </p>
</body>

> Theorem 5.3.(Kuratowski) A graph is non-planar if and only if it contains K<sub>5</sub> or K<sub>3,3</sub>.
