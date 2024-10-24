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

### 多项式插值(Polynomial Interpolation)

Lagrange interpolation
