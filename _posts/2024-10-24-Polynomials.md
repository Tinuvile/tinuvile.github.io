---
title: "多项式"
date: 2024-10-24
categories: [CS70]
tags: [多项式, CS70, 离散数学]
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
---

## 多项式(Polynomials)

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>  
<body>  
    <blockquote>  
        <p>
        <strong>Property 1: </strong>A non-zero polynomial of degree \(d\) has at most \(d\) roots.
        </p>
        <p>
        <strong>Property 2: </strong>Given \(d + 1\) pairs \((x_1, y_1), \) \(. . . ,\) \((x_{d+1}, y_{d+1})\), with all the \(x_i\) distinct, there is a unique polynomial \(p(x)\) of degree (at most) \(d\) such that \(p(x_i) = y_i\) for \(1 ≤ i ≤ d + 1\).
        </p>
    </blockquote>  
</body>

## 多项式插值(Polynomial Interpolation)

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>
<body>
    <p>
    假设我们现在知道\(y_1=1\)并且\(y_j=0(2 ≤ j ≤ d + 1)\)，现在我们要求一个符合条件的多项式\(p(x)\)。我们首先考虑\(q(x)=(x-x_2)(x-x_3)···(x-x_{d+1})\)，现在\(2 ≤ j ≤ d + 1\)是符合条件的，考虑\(q(x_1)=(x_1-x_2)(x_1-x_3)···(x_1-x_{d+1})\)，它显然等于某个常数而不等于0。我们令\(p(x)=q(x)/q(x_1)\)，即得到了符合我们要求的多项式。
    </p>
    <p>
    我们把\(y_1=0\)改为\(y_i=0\)，定义\(\Delta_i(x)=\frac{\prod_{j\neq i}(x-x_j)}{\prod_{j\neq i}(x_i-x_j)}\)为通过这些点的多项式。对于给定的点\((x_1,y_1),···,(x_{d+1},y_{d+1})\)，可以构造\(d+1\)个多项式\(\Delta_1(x),\Delta_2(x),···,\Delta_{d+1}(x)\)，通过这些可以表示出目标多项式\(p(x) = \sum_{i=1}^{d+1} y_i \Delta_i(x)\)。
    </p>
</body>

## 有限域(Finite Fields)

当系数与变量的取值是复数，或者说是有理数时，Property1 和 Property2 同样成立，但如果它们被限制在自然数或整数的范围内，则不成立。
但在模素数的情况下，Property1 和 Property2 仍然成立。

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>
<body>
     <p>
     当我们用以素数\(m\)为模的数字时，我们称我们正在一个有限域上工作，用\(F_m\)或\(GF(m)\)表示(for Galois Field)。
     </p>
</body>

[Wiki 上的相关介绍](<https://en.wikipedia.org/wiki/Field_(mathematics)>)<br>
[伽瓦罗域](https://en.wikipedia.org/wiki/Finite_field)

## 计数(Counting)

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>
<body>
     <p>
     对于一个次数最高为 2 的多项式\(p(x)\)，其形式为\(p(x)=a_2x^2+a_1x+a_0\)，在模\(m\)的情况下，每个系数可以取\(m\)个不同的值，因此有\(m^3\)种可能的多项式；而如果给定一个点，那么可能的多项式个数就会变为\(m^2\)，事实上二者间的关系可以用下表表示：
     </p>
</body>

| Polynomials of Degree ≤ d over F<sub>m</sub> |
| -------------------------------------------- | ------------------------------- |
| # of points                                  | # of polynomials                |
| ------------                                 | ------------------------------- |
| d + 1                                        | 1                               |
| d                                            | m                               |
| d − 1                                        | m<sup>2</sup>                   |
| ...                                          | ...                             |
| d − k                                        | m<sup>(k + 1)</sup>             |
| ...                                          | ...                             |
| 0                                            | m<sup>(d + 1)</sup>             |
