---
title: "The geisten basic math"
date: 2021-12-10T15:34:30-04:00
categories:
  - blog 
tags:
  - basics
  - theory
published: true
---

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>

<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

The geisten project is a minimalistic library written in the C programming language. Our goal is to implement neural networks as efficiently as possible with as little resource consumption as necessary.

The basic idea of this resource-efficient neural network is based on the principles of a binary network. The compressed 1-bit neural network enables complex models on devices with limited resources and achieves nearly the accuracy of real-valued networks without the additional computational overhead.

Each layer is calculated as follows:

- Convert the input data into the discrete values 1 and 0 (binarization).s
- Multiply input data with the weights matrix.
- Calculate the activation function based on the summed matrix elements. 

![forward process]({{ site.url }}{{ site.baseurl }}/assets/images/forward_process.drawio.svg)

## The forward process details

Non-binary input values must be converted first. If the input values are not available as binary values, they must first be transformed. The transformation takes place based on a threshold value $\alpha$. If the value is above the threshold, the value is converted to 1; below, to -1.

$$
a(x) = \begin{cases} +1 & x \ge \alpha \\ -1 & x < \alpha \end{cases}
$$

The popular frameworks used to train neural networks (like PyTorch) work with 32 or 16-bit resolution floating-point numbers. However, our target platforms do not always have a dedicated floating-point computing unit. For this reason, we will convert all these values additionally into integers to not slow down the calculation further. A resolution factor $r$ does the conversion from the trained floating-point value $\alpha'$ into an integer $\alpha$. 

$$
\alpha = r \cdot \alpha'
$$

For example, the MNIST data was also converted to floating-point numbers for training. These must first be converted back to integer values before binarization.

$$
\alpha = \alpha' * r_i * r_r
$$

With the trained binarization factor $\alpha'$, the input factor $r_i$ and the resolution factor $r_r$. The weight matrix is trained with help of a scaling factor $f_w$. 

$$
\mathcal{W} = f_w \cdot \mathcal{\tilde{W}}
$$

Activation function $f$:

$$
f(z) = f(\tilde{z} \cdot f_w) 
$$

Binarization:

$$
a(x) = \begin{cases} +1 & (x \cdot f_w) \ge \alpha \\ -1 & (x \cdot f_w) < \alpha \end{cases}
$$

The forward process is based on the matrix multiplication between the input vector and the weight matrix:

$$
\mathcal{z} = \mathcal{\tilde{A}} * \mathcal{\tilde{W}}
$$

With the binary input vector $\mathcal{\tilde{A}} \in {-1, 1}$ and weights matrix at output channel _i_:  $\mathcal{\tilde{W_i}} \in {-1, 1}$. The vector $\mathcal{\tilde{A}}$  and matrix $\mathcal{\tilde{W}}$ are multiplied via bit wise logic and _popcount_ operations to get the integer result $\mathcal{z}$. 

With the _popcount_ operation counting number of "1" in a binary sequence, we can get the binary convolution:

$$
\mathcal{\tilde{A}} * \mathcal{\tilde{W_i}} = 2 \cdot popcount(XOR(a, w_i)) - bitsize(a)


$$

After the binary activation step, the integer results $\mathcal{z}$ become real values within a certain range to generate a binary output feature map for the next layer.

[ReActNet: Towards Precise Binary Neural Network with Generalized Activation Functions](https://arxiv.org/pdf/2003.03488.pdf)
