## 2016-10-30

### CVPR 2017

* [proposal] remove background proposals using motion and saliency cues
* [proposal] remove inaccurate foreground proposals with sparse selection
* [proposal] Diverse ranking of segmentlets using maximal marginal relevance

* [superpixel] bottom up multiple intersections (more accurate than top-down version in CSI)

* [optimization] foreground seeds/meanshift clustering to remove seeds with small clusters (more robust in some frames that most models give wrong predictions)
* [optimization] manifold ranking/model reliablity

### 关于fcp and nlc

* 这两个都是考虑了proposal的fully connected的结构, 但是这种全局结构会把相似(颜色或其他特征)的proposal归结到一类中, 导致分类的错误。所以我们可以使用manifold的来避免这个问题
