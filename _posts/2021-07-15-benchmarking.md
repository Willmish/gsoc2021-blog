---
layout: post
title: "Benchmarking"
date: 2021-07-15
categories: Posts
---

This post/page is a collection of benchmarks made both on the Beaglebone Black rev. C and my PC with NVIDIA GTX960M GPU.
On host PC the operations are performed with 32-bit buffer and on BBB with 16-bits (as of 15.07.21 support for 32-bit is on the way).

## Array addition float
![float_BBB](https://raw.githubusercontent.com/JDuchniewicz/gsoc2021-blog/gh-pages/data/array_addition_float/array_addition_float%20on%20BBB.png)
![float_PC](https://raw.githubusercontent.com/JDuchniewicz/gsoc2021-blog/gh-pages/data/array_addition_float/array_addition_float%20on%20host%20PC.png)

## Array addition fixed-point 16-bit
![fixed16_BBB](https://raw.githubusercontent.com/JDuchniewicz/gsoc2021-blog/gh-pages/data/array_addition_fixed16/array_addition_fixed16%20on%20BBB.png)
![fixed16_PC](https://raw.githubusercontent.com/JDuchniewicz/gsoc2021-blog/gh-pages/data/array_addition_fixed16/array_addition_fixed16%20on%20host%20PC.png)
