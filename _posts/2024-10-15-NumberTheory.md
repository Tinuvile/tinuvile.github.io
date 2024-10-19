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
    <strong>\(x\) and \(y\) are congruent modulo \(m\) （全等模）</strong><br>
    <p>For any integer m, we say that x and y are congruent modulo m if they differ by a multiple of m or, in symbols, \(x ≡ y \pmod{m} ⇐⇒ m\) divides \((x − y).\)</p> 
    <p>Notice that x and y are congruent modulo m iff they have the same remainder modulo m; in other words,<br>
    \(x ≡ y \pmod{m} ⇐⇒ x \pmod{m} = y \pmod{m}.\)</p>
    <strong>residue classes（剩余类模）</strong><br>
    <p>
    residue classes \(\pmod{m}\): the union of all congruent modulo \(m\).
    </p>
</body>

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>  
<body>  
    <blockquote>
    <strong>Theorem 6.1.</strong> If \( a \equiv c \pmod{m} \) and \( b \equiv d \pmod{m} \), then \( a + b \equiv c + d \pmod{m} \) and \( a \cdot b \equiv c \cdot d \pmod{m} \).
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
    <strong>Lemma:</strong> For a finite set \(A\), \(f : A → A\) is a bijection if there is an inverse function \(g : A → A\) such that \(∀x ∈ A\), \(g( f (x)) = x\).
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
    when we wish to divide by \(x \pmod{m}\), we need to find \(y \pmod{m}\) such that \(x · y ≡ 1 \pmod{m}\); then dividing by \(x\) modulo \(m\) will be the same as multiplying by \(y\) modulo \(m\). Such a \(y\) is called the multiplicative inverse of \(x\) modulo \(m\).
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
    <strong>Theorem 6.2.</strong> Let \(m\), \(x\) be positive integers such that \(gcd(m, x) = 1\). Then \(x\) has a multiplicative inverse modulo \(m\), and it is unique (modulo \(m\)).
    </blockquote>
    <p>
    \(gcd(x,y)\)表示\(x\)和\(y\)的最大公约数。
    </p>
</body>

---

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>  
<body>  
    <strong><i>Proof</i></strong><br>
    <p>
    考虑\(m\)个数字的序列\(0,x,2x,...,(m-1)x\)，假设它们都是不同的modulo \(m\)，而由于从\(0\)到\(m\)只有\(m\)个值可取为模的值，则必须存在\(ax ≡ 1\) \(\pmod{m}\)，则\(a\)是\(x\)唯一的乘法逆模。<br>
    若对于\( 0 ≤ b ≤ a ≤ m − 1\)存在\(ax ≡ bx\) \(\pmod{m}\)，那么则有\((a − b)x ≡ 0\) \(\pmod{m}\)，但\(x\)和\(m\)是一对素数，故而产生矛盾，则只有唯一的乘法逆模。<br>
    事实上可以证明，上述定理是充要条件。<br>
    假设\(x\)有一个逆\(a\)，则\(ax ≡ 1\) \(\pmod{m}\)，也即\(ax-km=1\)，那么根据<a href="https://oi-wiki.org/math/number-theory/bezouts/" target="_blank">Bézout's lemma</a>，可以推出\(x\)和\(m\)互质。
    </p>
</body>

## 欧几里得算法计算逆(Euclid's Algorithm)

### Euclid's algorithm

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>  
<body>  
    <blockquote>
    <strong>Theorem 6.3.</strong> Let \(x ≥ y > 0\). Then \(gcd(x, y)\) \(=\) \(gcd(y, x\pmod{y})\).
    </blockquote>
</body>

```plaintext
algorithm gcd(x, y)
     if y = 0 then return(x)
     else return(gcd(y, x (mod y)))
```

> <strong>Theorem 6.4.</strong> The algorithm above correctly computes the gcd of x and y.

### Extended Euclid's algorithm

```plaintext
algorithm extended-gcd(x, y)
     if y = 0 then return(x, 1, 0)
     else
         (d, a, b) := extended-gcd(y, x (mod y))
         return((d, b, a - (x div y) * b))
```

### Division in modular arithmetic

## 算术基本定理(Fundamental Theorem of Arithmetic)

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>  
<body>  
    <blockquote>
    <strong>Claim:</strong> Let \(x\), \(y\), and \(z\) be positive integers such that \(gcd(x, y) = 1\). If
    \(x | yz\), then \(x | z\).
    </blockquote>
</body>

---

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>  
<body>  
    <blockquote>
    <strong>Fundamental Theorem of Arithmetic:</strong> Every positive integer \(n > 1\) can be expressed uniquely in the form \(p_1 p_2 · · · p_k\), where each \(p_i\) is a (not necessarily unique) prime number, up to reordering of the prime factors.
    </blockquote>
</body>

---

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>
<body>
    <strong><i>Proof</i></strong>
    <p>
    假设我们可以用两个质因数分解来表示\(n\)，\(n = p_1 p_2 · · · p_k \) \(= q_1q_2 · · · q_l\)，不妨设\(k ≤ l\)；<br>
    首先考虑\(p_1\)，因为\(p_1|n\)，所以有\(p_1|q_1 q_2 · · · q_l\)，若\(p_1\)属于\(q_l\)，得证；若不属于，对于\(1 ≤ j ≤ l − 1\)有\(gcd(p_1,q_j) = 1\)，那么则必有\(p_1 | q_l\)，则\(p_1 = q_l\)；<br>
    类似的，我们可以证明\(p_2 ,p_3 ,··· ,p_k\)，在这一过程中，我们会对\(q_j\)进行重新排序。
    </p>
</body>

## 中国余数定理(Chinese Remainder Theorem)

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>  
<body>  
    <blockquote>
    For \(m\), \(n\) with \(gcd(m, n) = 1\) that there is exactly one \(x\) \( \pmod{mn} \) that satisfies the equations:<br>
    \(x ≡ a\) \( \pmod{n} \) and \(x ≡ b\) \( \pmod{m} \).
    </blockquote>
</body>

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>  
<body>  
    <blockquote>
    <strong>Chinese Reminder Theorem: </strong>
    Let \( n_1, n_2, \ldots, n_k \) be positive integers that are coprime to each other. Then, for any sequence of integers \( a_i \), there is a unique integer \( x \) between 0 and \( N = \prod_{i=1}^{k} n_i \) that satisfies the congruences:  
\[  
\begin{align*}  
x &\equiv a_1 \pmod{n_1} \\
x &\equiv a_2 \pmod{n_2} \\
&\vdots \\
x &\equiv a_k \pmod{n_k}  
\end{align*}  
\]  
Moreover,  
\[  
x \equiv \left( \sum_{i=1}^{k} a_i b_i \right) \mod N  
\]  
    </blockquote>
</body>
