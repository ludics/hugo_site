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
- multi-class classifier, separates different identities using softmax
- learn an embedding, triplet loss(anchor, positive, negative)

==> Both have drawbacks



