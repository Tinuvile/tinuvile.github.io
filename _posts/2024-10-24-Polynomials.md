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

Lagrange interpolation

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

## 计数(Counting)
