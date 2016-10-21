## [Predicting the Where and What of actors and actions through Online Action Localization](http://crcv.ucf.edu/papers/cvpr2016/Soomro_CVPR2016.pdf)

### Goal

人的运动视频中人的Localization，及 action recognition

副产品同时有：人物前景分割， pose estimation 

### Motivation 

*
action localization 或 recognition 通常 off-line的。因此本文提出了on-line 的方法。
×
本文不仅使用颜色等低层特征，同时使用 pose和 superpixel-based forground model来协同定位。
×
创新点大概是前面所述的两点。（我想。）
文中使用 superpixel-based model做了分割，分割结果用来训练了一个SVM，来做action recognition(然而效果并不好)。

### Method

### Dataset

* JHMDB Dataset
* UCF Sports





