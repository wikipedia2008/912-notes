## [CNN-Aware Binary Map For General Semantic Segmentation](https://arxiv.org/pdf/1609.09220.pdf)

TL;DR

这篇是ＩＣＩＰ２０１６ Best Paper. 主要创新是对AlexNet的ｆｃ７的ｆｅａｔｕｒｅ maps去做ｈａｓｈｉｎｇ, 目的是讲high-dimensional 的deep features转换成binary codes. 
最后对每一个ｉｍａｇｅ会生成一个ｂｉｎａｒｙ map, 然后分割过程是采用的superpixel merging, 与传统方法不同在于使用的是这个binary codes.

**其实可以在这个binary codes上做bounding box regression**

### Iterative Quantization Hashing

本文采用的ｈａｓｈｉｎｇ的方法是cvpr11年的[Iterative Quantization: A Procrustean Approach to Learning Binary Codes](http://web.engr.illinois.edu/~slazebni/publications/cvpr11_small_code.pdf)

该方法的主要思路是：

１． 对原始高维特征做PCA，设为`Ｖ`，
2. 然后`V`中每一个元素都要映射到一个binary space, 在这个过程中，要使信息损失最少，就要解一个optimization problem: `min||B - V||`
３． 上面是简单的映射，作者发现把`V`做一个旋转，　会降低quantization error, 所以上面公式变为: `min ||B - V*R||`, 这里`R`是一个旋转矩阵（正交）
4. 在上式中，`B`和`R`是我们要求的，　作者采用了`k-means-like iterative quantization(ITQ)`,即固定一个求另一个。

具体的代码实现：

* 先初始化Ｒ，　即一个随机的正交矩阵
```matlab
R = randn(nbits, nbits)
[U, ~, V] = svd(R);
R = U(:, 1:nbits);
```
* 设置一个`max_iter`，　迭代去优化`B`和`R`
```matlab
for i = 1 : max_iter
    % Rotate V
    Z = V * R;
    % Compute B
    U2 = -1 ×　ones(size(Z, 1), size(Z, ２))；
    U2(Z >= 0) = 1;
    % Project V into a binary space.
    C = U2' * V;
    [S1, ~, S2] = svd(C);
    R = S1 * S2';
end
```

**其实这个方法可以直观的想象为，我们来旋转我们的特征点的集合，来使其与另一个集合一一对应上**
