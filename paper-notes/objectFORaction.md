## [What do 15,000 object categories tell us about classifying and localizing actions?](http://ieeexplore.ieee.org/document/7298599/)

* 文章提出了新的观点，研究：先获取了视频中物体的类别是否有助于action classify 和action localize。

* 为了研究物体和运动的关系，文章做了以下研究：

* Qualitative experiment: 物体和运动是否有关系？
  Method:    统计同一类别的action中物体出现的概率，并根据概率大小做出可视化图像。
  Conclusion:特定类别的物体确实与特定的action有关系。

* Quantitative classification experiment
  Method:    1仅使用运动特征和表观特征
  　　　　　 2使用运动+表观＋object class特征
             在UCF和THUMOX14两个数据集上，加入物体类别信息后，action classrify效果明显变好。
             在KTH上，由于该数据集的运动所包含的物体少，效果提升不明显。
  Conclusion:使用object class有助于action classrify.

* Quantitative localization experiment
  Method:    类似classification 的条件对比实验
  Conclusion:使用object class有助于action localization.

* Actions have preference
  Method:    对比实验。条件：
  　　　　　 1 Object preference
             2 Object avoidance(表示在15000种类别中重要性排名最低的类，重要性倒序)
             3 Object preference + motion
             4 Object avoidance + motion
  Conclusion:4种条件表现最好的是4.
  对于action classification，有些object class比其他的更重要。在所有视频可学习到的所有15000种物体类别中，加入关键object
  class(约100种)信息对action classification 的提升非常明显。而加入非关键的物体类别信息对action提升不明显有时甚至效果变差。

* Object-action relations are generic
  Conclusion:在第一个数据集上学习到的object class和action classcification 的关系可以transfer到一个新的数据集中，使得action效果得到
  提升。


* 结论: 确定物体类别信息确实有助于action。对于action classification有比较明显的提升，对于action localization 略有提高。
