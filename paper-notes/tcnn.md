## [Object Detection from Video Tubelets with Convolutional Neural Networks](http://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Kang_Object_Detection_From_CVPR_2016_paper.pdf)

TL;DR

### Goal

视频中的物体检测

A ImageNet Challenge: object detection from video (VID)

### Motivation

* 直接的方法是对每一帧使用图像物体检测的方法进行检测，　这样的问题在于往往一个基于图像训练的检测器，　训练样本无法覆盖一个物体的各个姿态，　但是在视频中，　物体在运动过程中，姿态会发生比较大的变化。　这样会导致图像检测器在某一些帧检测的ｃｏｎｆｉｄｅｎｃｅ高，　而在另一些则要低。　
* 解决上面问题的一种思路就是ｔｒａｃｋｉｎｇ，　但是ｔｒａｃｋｉｎｇ同样有问题，　１　是误差积累，　２　是遇到遮挡或较大的姿态变化，也不ｗｏｒｋ
* 所以，本文就是考虑到这两点做了一些工作，　其实就是一个tracking-by-detection的思路，　并没有太大的创新

### Method

* Image object proposal using selective search. Remove easy negative proposals by AlexNet.
* Object ｐｒｏｐsal scoring. GoogLeNet + SVM (hard negative mining)
* High-confidence proposal tracking. Track high-confidence detections (anchors) bidirectionally. Tracklet NMS

通过上面３步，可以生成several tubelets, 然后对ｔｕｂｅｌｅｔｓ进行classification and rescoring. 上面ｓｔｅｐ　２是对image-level proposals 进行ｓｃｏｒｉｎｇ，
但是使用它对ｔｕｂｅｌｅｔｓ进行ｓｃｏｒｉｎｇ有一些问题：　比如说，即使一个ｄｅｔｅｃｔｉｏｎ包含了物体，　检测器也有可能给个ｌｏｗ　ｓｃｏｒｅ，　所以作者提出了一个temporal convnet进行ｔｕｂｅｌｅｔｓ的ｒｅｓｃｏｉｎｇ，　细节：

* tubelet box perturbation. 1. ｔｕｂｅｌｅｔ　box augmentation. 即对每一个的位置进行采样得到一组新的ｄｅｔｅｃｔｉｏｎｓ　２．　ＮＭＳ. 对于一个ｔｕｂｅｌｅｔ　ｂｏｘ，　如果原始的ｄｅｔｅｃｔｉｏｎ　ｂｏｘ与其ｏｖｅｒｌａｐ高于某个阈值，那么用detection box代替ｔｕｂｅｌｅｔ box
* spatial max-pooling. 这个的意思是使用ｎｅｉghboring high-confidence detections去改善ｄetection scores. 即对于每一个tubelet box,只有那个具有ｍａｘｉｍａｌ confidence的ａｕｇmented box会保留
* temporal convolution and rescoring. 一个４层的网络，输入是time series的ｆｅａｔｕｒｅ: detection scores, track scores, and anchor offsets.对每一个类别训练了一个ＴＣＮＮ.

### Dataset

* ImageNet VID for object detection in videos
* YTO dataset for object localization task

### 几个没有在文中说的细节

* Multi-Context Suppression: 目的是remove false positive detections, 使用single frame可能比较难判断，但是使用multi frames可以。具体做法是讲low-confidence scores of detection boxes减去one certain value.
* Motion-Guided Propagation: 使用mean optical flow 去 propagate proposals.(short-term tracking)
* 关于tubelet rescoring, 其实可以直接使用1D bayesian去做，　ｆｅａｔｕｒｅ使用detection scores（可以使用ｍｅａｎ，　median, or top-k）


* __ＰＰＴ: http://www.ee.cuhk.edu.hk/~xgwang/CUvideo.pdf__
* __Codes：　https://github.com/myfavouritekk/T-CNN__

*by tfzhou*
