---
layout: post
title: "Benchmarking"
date: 2021-07-15
categories: Posts
---

This post/page is a collection of benchmarks made both on the Beaglebone Black rev. C and my PC with NVIDIA GTX960M GPU.
On host PC the operations are performed with 32-bit buffer and on BBB with 16-bits (as of 15.07.21 support for 32-bit is on the way).

## Array addition float
#### Without optimizations
<p float="left">
  <img src="https://raw.githubusercontent.com/JDuchniewicz/gsoc2021-blog/gh-pages/data/array_addition_float/array_addition_float%20on%20BBB.png" width="45%" />
  <img src="https://raw.githubusercontent.com/JDuchniewicz/gsoc2021-blog/gh-pages/data/array_addition_float/array_addition_float%20on%20host%20PC.png" width="45%" />
</p>
It can be seen that in case of BBB the GPU is always slower than CPU and this is exacerbated with the increasing size of the data transferred to and fro the GPU. The overhead of data transfers is very big, so in future tests I will see how expensive the operations on the GPU have to be to make up for the overhead.

On the PC the differences are much smaller, which shows that the bus transfers between CPU and GPU are much faster. Also the execution time is much faster, because the CPU and GPU are much stronger.

#### -O3 enabled
<p float="left">
  <img src="https://raw.githubusercontent.com/JDuchniewicz/gsoc2021-blog/gh-pages/data/array_addition_float/array_addition_float%20on%20BBB%20-O3.png" width="45%" />
  <img src="https://raw.githubusercontent.com/JDuchniewicz/gsoc2021-blog/gh-pages/data/array_addition_float/array_addition_float%20on%20BBB%20-O3-element.png" width="45%" />
</p>

It can be seen that enabling optimizations made the code execute faster in both cases. Also the time per-element is a good metric because it shows whether the processor is executing optimally or sub-optimally and in our case we can see that the relationship is almost linear in both cases.

## Array addition fixed-point 16-bit
#### Without optimizations
<p float="left">
  <img src="https://raw.githubusercontent.com/JDuchniewicz/gsoc2021-blog/gh-pages/data/array_addition_fixed16/array_addition_fixed16%20on%20BBB.png" width="45%" />
  <img src="https://raw.githubusercontent.com/JDuchniewicz/gsoc2021-blog/gh-pages/data/array_addition_fixed16/array_addition_fixed16%20on%20host%20PC.png" width="45%" />
</p>

In case of fixed-point operations, the results are very similar to floating-point for the BBB. However, for the host PC GPU execution is significantly slower (probably due to fixed-to-float transformations).

#### -O3 enabled
<p float="left">
  <img src="https://raw.githubusercontent.com/JDuchniewicz/gsoc2021-blog/gh-pages/data/array_addition_fixed16/array_addition_fixed16%20on%20BBB%20-%20O3.png" width="45%" />
  <img src="https://raw.githubusercontent.com/JDuchniewicz/gsoc2021-blog/gh-pages/data/array_addition_fixed16/array_addition_fixed16%20on%20BBB%20-%20O3-element.png" width="45%" />
</p>

For the fixed-point operations, we can see that a significant speedup is achieved on the CPU side, with a slighly lesser speedup on the GPU. Also time-per-element for the GPU is rising which shows that it is less resilient to scalabilty than in the floating-point case.

-------
Upcoming:
* check more expensive operations 
* test convolution 2D on BBB 
* test chaining different operations
