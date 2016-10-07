## Data Processing

在进行计算的时候，往往要对特征进行一下预处理，主要为:

### Mean Substraction

即减去均值, 但是这里要注意的是如果是分类的任务，那么均值应该在training set上去计算，然后
将test set减去同样的均值，而不能在全部数据上计算

```python
X -= np.mean(X, axis = 0)
```

### Normalization

这一步是为了将数据各个维度的特征转换到相似的尺度，可以每一维除以其标准差

```python
X /= np.std(X, axis = 0)
```

经过上面这两步,数据会变成下面这样子

![norm](http://cs231n.github.io/assets/nn2/prepro1.jpeg "norm")

### PCA and Whitening

另一种方式是PCA, 具体计算如下：

* 先计算协方差矩阵，它描述了任意两个维度的数据的相关程度，其中对角线即是每一维数据的方差

```python
X -= np.mean(X, axis = 0)
cov = np.dot(X.T, X) / X.shape[0]
```

* 然后做svd分解

```python
U,S,V = np.linalg.svd(cov)
```

* 然后decorrelate the data, 即将数据按特征向量进行旋转

```python
Xrot = np.dot(X, U)
```
这里如果`U`只取一部分，即是降维.

* Whitening

whitening是来normalize the scale of the data, 其将数据转换为一个`0`均值，identity covariance matrix的高斯分布

```python
Xwhiten = Xrot / np.sqrt(S + 1e-5) 
```

经过这种方式的变换后的数据样子为:

![pca](http://cs231n.github.io/assets/nn2/prepro2.jpeg "pca")

具体图像可视化的样子为：

![pca](http://cs231n.github.io/assets/nn2/cifar10pca.jpeg "pca")



