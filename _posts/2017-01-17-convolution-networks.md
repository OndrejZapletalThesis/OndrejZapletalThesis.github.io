---
title: Convolution Neural Networks
comments: true
---

**Convolutional Neural Network** (**CNN**) is specialized type of **Artificial Neural Network** that was originally used in image processing applications. Where was taken advantage of their two dimensional character. Since then they were also very successfully employed in natural language and video processing. Invention of CNNs was inspired by biology of human visual cortex. In human eye light falls on the cornea where photosensitive cells fire signal for individual neurons that are connected to these cells. Neurons in visual cortex are typically connected to only few photosensitive cells which translates into the fact that neurons react only to small portion of observed scene. Therefore **Convolutional Neural Networks** typically aren't fully connected. This has positive effect on computational complexity of network training. Usually complexity of training is rising proportionally (and not exponentially opposed to classical **Fully Connected Neural Networks**) to number of inputs.

#### Structure of **CNN**

Structure of Convolutional networks is typically composed of three different types of layers. Layer can be of **Convolutional**, **Pooling** and **Fully-connected** type. Network layers can pretty much arbitrarily combine these three types of layers (with exception of Fully-Connected layers, which always have to come last). Each type of layer has different rules for signal forward and error backward propagation.

##### Convolutional layer

As the name suggest this layer employs convolution. In the convolution terminology first parameter is called **input**, second parameter is called **kernel** and the output is typically called **feature map**. Input into Convolutional layer is either image (in case of first network layer) or **feature map** from previous layer. **Kernel** is typically of square shape and its width can range from 3 to N pixels. **Feature map** is created by convolution of **kernel** over each specified element of **input** (this is specified by **stride**, see next).

Depending on the size of **kernel** and layer's **padding** preferences the process of convolution can produce **feature map** of different size than **input**. When the size of output should be preserved it is necessary to employ **zero padding** on the edges of **input**. **Zero padding** in this case has to add as many zero elements so the convolution operation can be performed on the edge of **input**. In opposite case the **feature map** is reduced by the missing elements. Decreasing of the **feature map** can be in some cases desirable. In this case is during convolution applied **stride** to determine how many **input** elements should be skipped in each step during traversal (when the **stride** is 1 the size of **feature map** is not affected).

Each Convolutional layer is typically composition of several different **kernels**. In other words output of this layer is tensor containing **feature map** for each used kernel. Each of these is designed to underline different features of input image. In the first layers these features are typically edges. In following layers the higher the layer the more complex features are captured.

The fact that each convolution on **input** is using one **kernel** (don't confuse this with use of multiple **kernels** in previous paragraph) basically means that all connections between two neighboring layers are sharing the same weights. This might not be sufficient in some applications and there fore there is possibility to use two other types of connections. **Locally connected** which basically means that applied **kernel** is of the same size as the **input** and **tiled convolution** which means alternation of more than one set of weights on entire **input**.

##### Pooling layer

This layer is used to down sample size of the **input** layer. Sometimes this is called the **detector** stage. Output from this layer is created by various combination of **input**. Max-pooling is one of the more prevalent examples. The input is divided into equal rectangular sub-elements of size larger than 1. Output from each sub-element is then selected as maximal value of its individual elements. This decreases the size of output layer while preserving information contained in input layer and effectively compresses contained information.

##### Fully-Connected layer

Fully-Connected layer is typical layer from classical **Feed-forward fully connected Neural Network** and it is always located on the end of the layer stack. In other words it is never followed by another Convolutional layer. Utility of multiple fully connected layers at the end of the CNN stack is in some literature questioned.

#### Training

Learning process of CNN is analogues to FCNN in that both are using **Gradient Decent Methods**. Situation with **CNN** is more complicated because network is composed of layers of different types and therefore training technique must accommodate for variability between different layers.
