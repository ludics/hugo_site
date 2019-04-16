---
title: "Paper Reading on Face Recognition"
date: 2019-03-28T15:20:36+08:00
draft: false
tags: ["academic"]
---

## ArcFace: Additive Angular Margin Loss for Deep Face Recognition

### Abstract

Design of loss function that enhance discriminative power.

<!--more-->

ArcFace: Additive Angular Margin Loss, has a clear geometric interpretation due to the geodesic distance on the hypersphere. 

### Introduction

DCNNs map face image into a feature that has small intra-class and large inter-class distance.

Two lines to train:

1. multi-class classifier, separates different identities using softmax
2. learn an embedding, triplet loss(anchor, positive, negative)

==> Both have drawbacks
$$
W \in \mathbb{R}^{d \times n}
$$

1. Softmax loss: increases linearly with n; learned feature separable for closed-set classification but not discriminative
2. Triplet loss: combinatorial explosion; semi-hard sample mining difficult

Enhanced softmax: 

1. Centre loss by Wen et al., obtain intra-class compactness; updating centres is difficult. 
2. multiplicative angular margin penalty, enforce intra-class compactness and inter-class discrepancy, leading to better discriminative. Angular margin, Sphereface. 
3. CosFace, adds cosine margin penalty to the target logit

This paper: ArcFace, further improve discrimanative power of face recognition & stabilise training process. Dot product between feature & last fc layer equal to the cosine distance after feature & weight norm. Use arc-cosine to cal the angle between current feature & target weight. Add an additive angular margin to target angle, get target logit back by cosine. Re-scale logits by fixed feature norm, subsequent same as softmax. 

Advantages:

- Engaging, directly optimises the geodesic distance
- Effective, achieves sota perfomance
- Easy, easy to implement
- Efficient, adds negligible computational complexity

### Proposed Approach
#### ArcFace
Softmax loss:

$$
L_1 = -\frac{1}{N} \sum_{i=1}^N \log \frac{e^{W_{y_i}^T x_i + b_{y_i}}}{\sum_{j=1}^n e^{W_j^T x_i + b_j}}
$$

- Does not explicitly optimise the feature embedding, result in performance gap under large intra-class variations and large-scale test scenarios



## Support Vector Guided Softmax Loss for Face Recognition

SV-Softmax, inherit the advantages of mining-based and margin-based losses into one framework.


## Large-scale Bisample Learning on ID versus Spot Face Recognition

Mainly two new methods:

- CVC training strategy that enhances IvS performance
- DP-Softmax(dominant prototype) to make scalable on large-scale classes



## Orthogonal Deep Features Decomposition for Age-Invariant Face Recognition

Main Formulas:

$$
x = x_{age} * x_{id}
$$

$$
x_{age} = \parallel x \parallel _2
$$

$$
x_{id} = \lbrace \frac{x_1}{\parallel x \parallel _2}, \frac{x_2}{\parallel x \parallel _2}, \cdots, \frac{x_n}{\parallel x \parallel _2}  \rbrace
$$




## Quality Aware Network for Set to Set Recognition

