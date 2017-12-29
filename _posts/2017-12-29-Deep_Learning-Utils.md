---
layout: post
title: Deep Learning Utils
---
> How to calculate the output of a convolution layer as follows:
- W1 = (W0 −F+2P)/S + 1 where 
> How to calculate the output of a deconvolution layer as follows:
- W1 = S * (W0−1)+ F−2∗P
- where:
  ✓ W0 is the input size
  ✓ W1 is the output size
  ✓ F is the receptive field (filter width)
  ✓ p is the padding (default: 0)
  ✓ s is the stride (default: 1)

> It is just the ‘opposite’ operation of the convolution (basically exchange the forward and backward pass).
