## [A Key Volume Mining Deep Framework for Action Recognition](http://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Zhu_A_Key_Volume_CVPR_2016_paper.pdf)

* To identify key volume/frames and conduct classification simultaneously
* 由于并没有well-labled key volume， 不能训练分类器。因此同时做两个任务：

* 1 利用网络的forward， 做分类
* 2 利用网络的backward， 做参数的训练

*  iteratively
