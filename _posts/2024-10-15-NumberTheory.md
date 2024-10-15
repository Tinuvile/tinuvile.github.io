---
title: "数论基础"
date: 2024-10-15
categories: [CS70]
tags: [离散数学, CS70, 数论]
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
---

## 1.模运算(Modular Arithmetic)

### Definition

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>  
<body>  
    <blockquote>  
        <p>we can define \(x \pmod{m}\) (in words: “\(x\) modulo \(m\)”) to be the remainder \(r\) when we divide \(x\) by \(m\). I.e., if \(x \pmod{m} ≡ r\), then \(x = mq+r\) where \(0 ≤ r ≤ m−1\) and \(q\) is an integer.</p>   
    </blockquote>  
</body>

### Computation

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>  
<body>
    <p>
    while carrying out any sequence of additions, subtractions or multiplications \(\pmod{m}\), we get the same answer if we reduce any intermediate results \(\pmod{m}\). This can considerably simplify the calculations.
   </p>
</body>

在执行模运算时，如果我们能减少任何中间结果模 m，结果不会变化，但可以大大简化运算。

### Set Representation

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>  
<body>
    <strong>全等模</strong>
    <p>For any integer m, we say that x and y are congruent modulo m if they differ by a multiple of m or, in symbols, \(x ≡ y \pmod{m} ⇐⇒ m\) divides \((x − y).\)</p> 
    <p>Notice that x and y are congruent modulo m iff they have the same remainder modulo m; in other words,<br>
    \(x ≡ y \pmod{m} ⇐⇒ x \pmod{m} = y \pmod{m}.\)</p>
    <strong>剩余类模</strong><br>
    <p>
    residue classes <strong>剩余类模</strong><br>
residue classes \(\pmod{m}\): the union of all congruent modulo m.
    </p>
</body>

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>  
<body>  
    <blockquote>
    Theorem 6.1. If \( a \equiv c \pmod{m} \) and \( b \equiv d \pmod{m} \), then \( a + b \equiv c + d \pmod{m} \) and \( a \cdot b \equiv c \cdot d \pmod{m} \).
    </blockquote>
</body>

## 2.幂运算(Exponentiation)

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>  
<body>  
    <p>
    How do we compute \(x^y\)\(\pmod{m}\), where \(x\), \(y\), and \(m\) are natural numbers and \(m > 0\)?
    </p>
</body>

```plaintext
// 快速幂算法(模幂算法)
algorithm mod-exp(x, y, m)
    if y = 0 then return (1)
    else
        z = mod-exp(x, y div 2, m)
        if y (mod 2) ≡ 0 then return (z * z (mod m))
        else return (x * z * z (mod m))
```

## Bijections(双射)

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>  
<body>  
    <blockquote>
    A bijection is a function for which every \(b ∈ B\) has a unique pre-image \(a ∈ A\) such that \(f(a) = b\).
    </blockquote>
</body>

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>  
<body>  
    <blockquote>
    Lemma: For a finite set \(A\), \(f : A → A\) is a bijection if there is an inverse function \(g : A → A\) such that \(∀x ∈ A\), \(g( f (x)) = x\).
    </blockquote>
</body>

## Inverses(逆)

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>  
<body>  
    <p>
    when we wish to divide by x \(\pmod{m}\), we need to find \(y \pmod{m}\) such that \(x · y ≡ 1 \pmod{m}\); then dividing by \(x\) modulo \(m\) will be the same as multiplying by \(y\) modulo \(m\). Such a \(y\) is called the multiplicative inverse of \(x\) modulo \(m\).
    </p>
</body>

乘法逆模只有在 m 与 x 互质时才存在。此外，当存在时，它是唯一的。

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>  
<body>  
    <blockquote>
    Theorem 6.2. Let \(m\), \(x\) be positive integers such that \(gcd(m, x) = 1\). Then \(x\) has a multiplicative inverse modulo \(m\), and it is unique (modulo \(m\)).
    </blockquote>
    <p>
    \(gcd(x,y)\)表示\(x\)和\(y\)的最大公约数。
    </p>
</body>

## 欧几里得算法计算逆(Euclid's Algorithm)
