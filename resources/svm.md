## Multi-Class SVM

多类SVM希望对于正确类别的预测score值比其它错误类别的预测score值至少大于`delta`, 如下图表示:

![mc-svm](http://cs231n.github.io/assets/margin.jpg "mc-svm")

第i个example的损失可以由下式计算:

`L_i = \sum_{j \neq y_j} max(0, s_j - s_{y_i} + delta)`

这里`s_i`即为svm分类器的预测值(raw output).

举个例子：

假设对于一个example, 三个类的分类结果为`s = [13, -7, 11]`, 并且第一个类是正确的类别.
假设`delta = 10`, 那么，我们可以计算这个example的loss为:

`L_i = max(0, -7-13+10) + max(0, 11-13+10)`

可以看到the first term的损失为`0`, 因为正确类别的score(13)已经比(-7)超过了大于10,
而对于the second term, 即使11比13少，但是因为没有到10, 所以，我们这里把它的loss定义为8.

但是与2-class svm一样，如果只是这样的话，我们可以有多组权重，所以其实还要加上regularization,
一般是`L2 norm`.

## Gradient Check

使用numerical gradient检测analytic gradient

