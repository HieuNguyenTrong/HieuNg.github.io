---
layout: post
title: Deep Learning Utils
---
- How to calculate the output of a convolution layer/ a pooling layer as follows:

    + W1 = (W0 - F + 2P) / S + 1
    + Caffe library always does the ceiling operation.
   
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

Note: 

 + In Caffe library, a batch size of the network which corresponds to the number of filtets. Therefore, choosing a good batch size for training is essential due to the power of GPUs. We will meet a error such as: "out of memory". 
 
 + After experience with Caffe library for training the net, i found out that, to reduce the training time and increase the accuracy of the model, the batch size shoud be increased, however, increasing the batch size depends on the power of GPUs, due to increasing parameters of the net. 
 
 + Besides, designing the dataset playes as an important role in training the model. For example: lmdb, leveldb, h5df, etc.
 
 - I will explain more details about how to design a good database for Caffe library in the next post. 
