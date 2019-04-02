---
title: "Paper Read on Face Recognition"
date: 2019-03-28T15:20:36+08:00
draft: false
tags: ["academic"]
---

## ArcFace: Additive Angular Margin Loss for Deep Face Recognition
### Abstract
Design of loss function that enhance discriminative power.

ArcFace: Additive Angular Margin Loss, has a clear geometric interpretation due to the geodesic distance on the hypersphere. 

### Introduction

DCNNs map face image into a feature that has small intra-class and large inter-class distance.

Two lines to train:
1. multi-class classifier, separates different identities using softmax
2. learn an embedding, triplet loss(anchor, positive, negative)

==> Both have drawbacks
1. Softmax: $$W \in R^{d \mul n}$$ increases linearly with n; learned feature separable for closed-set classification but not discriminative
2. triplet loss: combinatorial explosion; semi-hard sample mining difficult

Enhanced softmax: 
1. Centre loss by Wen et al., obtain intra-class compactness; updating centres is difficult. 
2. multiplicative angular margin penalty, enforce intra-class compactness and inter-class discrepancy, leading to better discriminative. Angular margin, Sphereface. 
3. CosFace, adds cosine margin penalty to the target logit

This paper: ArcFace, further improve discrimanative power of face recognition & stabilise training process.



