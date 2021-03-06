---
layout: post
title: Deep Learning Utils
---

#### Deep Learning is stacking layers and learning end to end (learning the whole problem from input to output) 
- Networks run layer by layer, composing the input - output transformation of each layer. During learning process, the error is passed back layer by layer to tune the transformations. <http://caffe.berkeleyvision.org/>

- With classification problem, is divided into two categories: 

- Linear classification: works with simple data
 
 ![alt text](/images/linear_class_01.JPG "Linear classification")
 
- Non-linear classification: due to in practice with linearity is not enough for classification. Besides, real-world data requires more sophilicated clasifiers such as: ReLU, Sigmoid, TanH, Leaky ReLU, ELU,
 
 ![alt text](/images/linear_class_02.JPG "Linear classification")
 
 ![alt text](/images/non_linear_class.JPG "Non-linear classification")

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

 + In Caffe library, a batch size of the network which corresponds to the batch size of data. For an ImageNet training batch of 64 images N = 64. Therefore, choosing a good batch size for training is essential due to the power of GPUs. We will meet a error such as: "out of memory". 
 
 + After experience with Caffe library for training the net, i found out that, to reduce the training time and increase the accuracy of the model, the batch size shoud be increased (depends on each problem), however, increasing the batch size depends on the power of GPUs, due to increasing parameters of the net. 
 
 + Besides, designing the dataset plays as an important role in training the model. For example: lmdb, leveldb, h5df, etc.

