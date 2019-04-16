---
title: Paper Reading on Model Compression
subtitle: Compression and acceleration
tags: ["academic"]
date: 2019-03-23
draft: false
---

## A Survey of Model Compression and Acceleration for Deep Neural Networks

<!--more-->


### Abstract

Deep convolutional neural networks (CNNs) have recently achieved great success in many visual recognition tasks. However, existing deep neural network models are computationally expensive and memory intensive, hindering their deployment in devices with low memory resources or in applications with strict latency requirements. Therefore, a natural thought is to perform model compression and acceleration in deep networks without significantly decreasing the model performance. During the past few years, tremendous progress has been made in this area. In this paper, we survey the recent advanced techniques for compacting and accelerating CNNs model developed. These techniques are roughly categorized into four schemes: parameter pruning and sharing, low-rank factorization, transferred/compact convolutional filters, and knowledge distillation. Methods of parameter pruning and sharing will be described at the beginning, after that the other techniques will be introduced. For each scheme, we provide insightful analysis regarding the performance, related applications, advantages, and drawbacks etc. Then we will go through a few very recent additional successful methods, for example, dynamic capacity networks and stochastic depths networks. After that, we survey the evaluation matrix, the main datasets used for evaluating the model performance and recent benchmarking efforts. Finally, we conclude this paper, discuss remaining challenges and possible directions on this topic.

### Introduction
Deep networks with billions parameters, GPUs with high computation capability. Two example: ImageNet, LFW dataset. Reducing storage & computational cost is critical, for real-time app. Solutions from many disciplines: ML, optimization, computer arch, data compression, indexing, hardware design.

Four approaches: parameter pruning & sharing, low-rank factorization, transferred/compact convolutinal filters, knowledge distillation. 
### Parameter pruning & sharing 
- Quantization & Binarization \
Reducing the number of bits required to represent each weight. Gong & Wu: K-means scalar quantization to the parameter values. Vanhoucke: 8-bit quantization => significant speed-up, accuracy loss minimal. 16-bit representation reduced memory usage & float point operations with little loss. 
- Pruning & Sharing




