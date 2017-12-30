---
layout: post
title: Deep Learning Utils
---
- How to calculate the output of a convolution layer as follows:
    + W1 = (W0 - F + 2P) / S + 1
- How to calculate the output of a deconvolution layer as follows:
    + W1 = S * (W0 - 1) + F - 2 * P
- Where:
    1. W0 is the input size
    2. W1 is the output size
    3. F is the receptive field (~kernel_size)
    4. P is the padding (default: 0)
    5. S is the stride (default: 1)
- It is just the ‘opposite’ operation of the convolution (basically exchange the forward and backward pass).

- To set the input size and the output size has the same size spatially when S = 1 set zero padding to be 
    + P = ( F - 1 ) /2
- The depth of the output size: it corresponds to the number of filters    
