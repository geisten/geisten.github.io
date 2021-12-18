---
title: "The geisten basic math"
date: 2021-12-10T15:34:30-04:00
categories:
  - blog
tags:
  - basics
  - theory
---

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

The geisten project is a minimalistic library written in the C programming language. Our goal is to implement neural networks as efficiently as possible with as little resource consumption as necessary.

The basic idea of this resource-efficient neural network is based on the principles of a binary network. The compressed 1-bit neural network allows running complex models on resource-limited devices.
The algorithm achieved nearly the accuracy of real-valued networks without extra computational cost.

### The forward process

Non-binary input values must be converted first. If the input values are not available as binary values, they must first be transformed. The transformation takes place based on a threshold value. If the value is above the threshold, the value is converted to 1; below, to 0.

$$ a(x) = \begin{cases}  +1 &  x \ge \alpha \\ -1 & x < \alpha \end{cases} $$

![forward process]({{ site.url }}{{ site.baseurl }}/assets/images/forward_process.drawio.svg)

$$ \mathcal{z} = \mathcal{\tilde{A}} * \mathcal{\tilde{W}} $$

With the binary input vector \\(\mathcal{\tilde{A}} \in {0, 1}\\) and weights matrix at output channel _i_: \\(\mathcal{\tilde{W_i}} \in {-1, 1}\\). The vector \\(\mathcal{\tilde{A}}\\) and matrix \\(\mathcal{\tilde{W}}\\) are multiplied via bit wise logic and popcount operations to get the integer result \\(\mathcal{z}\\).  After the binary activation step, the integer results \\(\mathcal{z}\\) become real values within a certain range to generate a binary output feature map for the next layer.
In each bit, the result of basic multiplication \\(a \times w_i$` is one of three values {−1, 0, 1}. If we let binary "0" stand for the value −1 in b, the truth table of binary multiplication is then shown in the following table.

| a        | w          | pos (+1)  | neg (-1) |
| ------------- |:-------------:| :-----:|:-----:|
| 0     | 0 | 0 |0 |
| 0     | 1 | 0 |0 |
| 1     | 0 | 0 |1 |
| 1     | 1 | 1 |0 |

With popcount operation counting number of "1" in a binary sequence, we can get the binary
convolution.

$$\begin{align*}\mathcal{\tilde{A}} * \mathcal{\tilde{W_i}} &= popcount(pos) - popcount(neg) \\
 &= popcount(\mathcal{\tilde{A}} \land  \mathcal{\tilde{W_i}}) - popcount(\mathcal{\tilde{A}} \land  \overline{\mathcal{\tilde{W_i}}})\end{align*}$$


[ReActNet: Towards Precise Binary Neural Network with Generalized Activation Functions](https://arxiv.org/pdf/2003.03488.pdf)
