---
title: "纠错码"
date: 2024-11-1
categories: [CS70]
tags: [多项式, CS70, 离散数学]
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
---

## Error Correcting Codes

粗略来说，纠错码可以分为两种：

- 代数码，基于有限域上的多项式；
- 组合码，基于图论。

### Erasure Errors

我们考虑两种情况，第一种情况以 Internet 为例，信息（或者说文件）会被分解成数据包，不可靠性体现在部分数据包可能在传输过程中丢失。

<div style="display: flex; align-items: center; justify-content: center;">  
  <table style="border-collapse:collapse; margin: 0 10px;">  
    <tr>  
      <td style="border: 1px solid black; padding: 20px; text-align: center; font-size: 24px; width: 50px; height: 50px;">3</td>  
      <td style="border: 1px solid black; padding: 20px; text-align: center; font-size: 24px; width: 50px; height: 50px;">1</td>  
      <td style="border: 1px solid black; padding: 20px; text-align: center; font-size: 24px; width: 50px; height: 50px;">5</td>  
      <td style="border: 1px solid black; padding: 20px; text-align: center; font-size: 24px; width: 50px; height: 50px;">0</td>  
    </tr>  
  </table>  
  <div style="font-size: 50px;">&#8594;</div>  
  <table style="border-collapse:collapse; margin: 0 10px;">  
    <tr>  
      <td style="border: 1px solid black; padding: 20px; text-align: center; font-size: 24px; width: 50px; height: 50px;"></td>  
      <td style="border: 1px solid black; padding: 20px; text-align: center; font-size: 24px; width: 50px; height: 50px;">1</td>  
      <td style="border: 1px solid black; padding: 20px; text-align: center; font-size: 24px; width: 50px; height: 50px;">5</td>  
      <td style="border: 1px solid black; padding: 20px; text-align: center; font-size: 24px; width: 50px; height: 50px;"></td>  
    </tr>  
  </table>  
</div>

<br>

我们将此类错误称为 <strong> erasure errors</strong>。

现在假设该消息由 n 个数据包组成，并且假设在传输过程中最多丢失 k 个。接下来我们将把 n 个数据包的初始消息编码为由
n + k 个数据包组成的冗余编码，以便接收者可以从任意 n 个收到的数据包中重建消息。

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>
<body>
    <p>
    我们假设每个数据包的内容是一个数字模\(q\)，\(q\) 是一个素数。例如，数据包的内容可能是一个 32 位的字符串，可以视为介于0和\(2^{32} - 1\)之间的一个数，那么我们可以选择任何一个大于2的素数作为\(q\)。我们用\(m_1,m_2,...,m_n\)表示要发送的信息，其中每个\(m_i\)都是\(GF(q)\)域中的一个数。则有：<br>
    <ul>  
        <li>存在一个 \( n-1 \) 次的唯一多项式 \( P(x) \)，使得对 \( 1 \leq i \leq n \) 均有 \( P(i) = m_i \)；</li>  
        <li>我们通过计算 \( P(n+j) \) 来生成额外的数据信息；</li>  
        <li>这样我们就可以根据 \( P(x) \) 在任意 \( n \) 个不同点的值来重建它，并通过它还原出初始的信息。</li>  
    </ul>
    </p>
</body>

### Polynomial Interpolation Revisited

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>
<body>
    <p>
    我们的问题目标与之前一致，求解一个符合条件的多项式\(p(x) = a_d x^d + · · · + a_1x + a_0\)。首先，我们可以写出包含\(d+1\)个线性方程的方程组，变量是多项式的系数\(a_0,···,a_d\)，通过求解这些方程式来得到多项式\(p(x)\)的系数。
    </p>
</body>

### General Errors

<head>  
    <meta charset="UTF-8">    
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>  
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>  
</head>
<body>
    <p>
    现在假设Alice希望通过一个更嘈杂的频道与Bob进行交流，她的信息是\(m_1,···,m_n\)，我们可以将\(m_i\)视为字符（类似于英文字母之类）。由于频道嘈杂，这些字符信息在传输过程中会被损坏。现在Bob接受到了与发送数量相同的字符数，但其中有\(k\)个字符已经损坏，但Bob不知道是哪\(k\)个。<br>
    我们仍然将每个视为一个模\(q\)的数字，对于英文字母，我们可以选择一个大于26的数字为\(q\)，例如29。信息使用多项式\(P(x)\)表示，满足\(P(1)=m_1,P(2)=m_2,···,P(n)=m_n\)。根据之前的论述，Alice需要向Bob传递至少\(n+2k\)个字符。<br>
    现在Bob需要重建的多项式是次数为\(n-1\)，且满足\(P(i)=r_i\)至少在\(n+k\)个点上成立，现在关键问题是Bob不知道错误发生位置。他将采取的方法是错误定位多项式(error-locator polynomial) \(E(x) = (x − e_1)(x − e_2) · · · (x − e_k)\)，这是一个\(k\)次多项式，\(e_i\)表示错误发生的位置。<br>
    我们可以注意到\(P(i)E(i) = r_iE(i)\)在(\(1 ≤ i ≤ n + 2k)\)上成立，因为在错误的位置定位多项式等于0。<br>
    定义\(Q(x) := P(x)E(x)\)，我们可以得到：<br>
    \(Q(x) = a_{n+k−1}x^{n+k−1} + a_{n+k−2}x^{n+k−2} + · · · + a_1x + a_0\)<br>
    \(E(x) = x^k + b{k−1}x^{k−1} + · · · + b_1x + b_0\)<br>
    利用\(Q(i) = r_iE(i)\)构建方程组，
    \(a_{n+k−1}i^{n+k−1} + a_{n+k−2}i^{n+k−2} + · · · + a_1i + a_0 = r_i(i^k + b_{k−1}i^{k−1} + · · · + b_1i + b_0) (mod q)\)
    可以解出各项的系数。
    </p>
</body>

### Distance properties
