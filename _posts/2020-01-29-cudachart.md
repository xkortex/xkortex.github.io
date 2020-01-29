---
layout: post
title: CUDA and SM architecture compatibility
tags:  cuda nvidia sm architecture caffe tensorflow pytorch
---

# CUDA architecture funtimes


First, read this: 
[Matching SM architectures (CUDA arch and CUDA gencode) for various NVIDIA cards](https://arnon.dk/matching-sm-architectures-arch-and-gencode-for-various-nvidia-cards/)

Condensed here:

| Gen     | Year    | CUDA Min-Max | SM/Compute Arch |
|---------|---------|--------------|-----------------|
| Tesla   | 2006    | ?            | ?               |
| Fermi   | 2010-04 | 3.2-8        | 20              |
| Kepler  | 2012-04 | 5-           | 30, 35, 37      |
| Maxwell | 2014-02 | 6-           | 50, 52, 53      |
| Pascal  | 2016-04 | 8-           | 60, 61, 62      |
| Volta   | 2017-12 | 9-           | 70, 72          |
| Turing  | 2018-09 | 10-          | 75              |
| Ampere  | 2020?   | 11-          | 80              |
| Hopper  | ?       | 12?          | ?               |

[CUDA Compatibility](https://docs.nvidia.com/deploy/cuda-compatibility/index.html)

Captured here, refer to the link for updates: 

###  CUDA Toolkit and Compatible Driver Versions
| CUDA Toolkit          | Linux x86_64 Driver Version |
|-----------------------|-----------------------------|
| CUDA 10.2 (10.2.89)   | \>= 440.33                   |
| CUDA 10.1 (10.1.105)  | \>= 418.39                   |
| CUDA 10.0 (10.0.130)  | \>= 410.48                   |
| CUDA 9.2 (9.2.88)     | \>= 396.26                   |
| CUDA 9.1 (9.1.85)     | \>= 390.46                   |
| CUDA 9.0 (9.0.76)     | \>= 384.81                   |
| CUDA 8.0 (8.0.61 GA2) | \>= 375.26                   |
| CUDA 8.0 (8.0.44)     | \>= 367.48                   |
| CUDA 7.5 (7.5.16)     | \>= 352.31                   |
| CUDA 7.0 (7.0.28)     | \>= 346.46                   |