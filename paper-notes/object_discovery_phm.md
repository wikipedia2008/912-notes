## [Unsupervised Object Discovery and Localization in the Wild:Part-based Matching with Bottom-up Region Proposals](http://www.di.ens.fr/willow/pdfscurrent/cho2015.pdf)

TL;DR

part-based matching 与 foreground localization交替进行

### part-based matching

先是做proposal, 然后对两个regions `R` 和 `R'`, 他们的matching confidence如下定义:

`p(m | R, R') = \sum_x p(m,x|R,R') = \sum_x p(m|x,R,R')p(x|R,R') = p(m_a) \sum_x p(m_g|x) p(x|R,R')`

这里`x`是指物体的pose displacement.
`m_a`: appearance matching(独立于`x`). `m_g`: geometric matching.
p(x|R,R')定义了两个同类物体offset为`x`的一个概率.

`p(m_a)`和`p(m_g)`都好定义，但是估计`p(x|R,R')`就比较困难，文章提出了一种probabilistic hough matching的方法重新reformulate了上式。


首先定义了一个hough voting score, 它等于所有可能匹配的概率和:

`h(x|R,R')` = \sum_m p(m|x,R,R') = \sum_m p(m_a) p(m_g|x)`

这定义了一个pseudo likelihoods of common objects at offset `x`, 作者用这个`h(x|R,R')`替换了`p(x|R,R')`

### foreground localization

定义了一个standout score。
