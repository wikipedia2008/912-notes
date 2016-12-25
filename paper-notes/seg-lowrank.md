## [Semantic Single Video Segmentation with Robust Graph Representation]()

TL;DR

### Goal

单个视频的多物体(semantic)分割

### Method

proposal generation ==> outlier removal ==> spectral clustering ==> segmentation completion

其中第二步outlier removal是在proposal adjacency graph上找一个low rank representation，
文中将同时覆盖前景和背景的proposal看做outlier, 而其他proposal大多在时空上是稳定的，会导致low-rank结构。
