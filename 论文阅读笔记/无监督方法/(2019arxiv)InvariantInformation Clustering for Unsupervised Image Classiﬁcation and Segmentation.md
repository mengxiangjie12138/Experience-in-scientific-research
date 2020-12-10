## InvariantInformation Clustering for Unsupervised Image Classiﬁcation and Segmentation

### 代码

github.com/xu-ji/IIC

### 动机

结合互信息提升无监督聚类和图像分割的效果。

### 方法（聚类/分类）

无监督问题

1. 将输入图片x经过仿射变换得到x'；
2. 单数个epoch：将x和​x'传入参数共享的成熟网络（ResNet或VGG11）提取特征，经过全连接层得到属于每个类别的概率分布z​和​z'​；
3. 单数个epoch：假设$z$和$z'$相互独立，根据2得到的边缘概率分布，计算z和z'​的联合概率分布矩阵​P'​；
4. 单数个epoch：使用以下公式打破独立性，得到新的联合概率分布矩阵P​；

<img src="https://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/IIC-1.png" alt="IIC1" style="zoom:5%;" />

5. 单数个epoch：根据P​计算如下互信息作为目标函数，通过最大化目标函数（最小化互信息的相反数）来优化网络，使用BP算法回传；

<img src="https://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/IIC-2.png" alt="IIC2" style="zoom:10%;" />

6. 偶数个epoch：使用overclustering方法，将图片分为更多类别，类比单数个epoch，得到更大的联合概率分布矩阵，计算损失并回传。

半监督问题

1. 使用上述无监督方法预训练出基本模型；
2. 使用logistic loss和带label的数据微调网络。

### tricks

1. Overclustering

原理：将数据强制聚类为更多的类别可以提高网络的性能（文中提到）

方法：使用多种变换方法得到多对x'​（​n​对），认为每对x'为新的类别，所以总共有​c*n​类，得到更大的联合概率分布矩阵。

2. Sobel算子

图像边缘检测算子，使图片的形状特征更明显。

### 超参数

1. 学习率：1e-4
2. 优化器：Adam
3. overclustering时使用的数据增强方法数量r：5

### 结果

mnist数据集：最高ACC 99.2

### 缺点

1. 只能处理类别分布均匀的数据集。

文中提到如下公式，最大化I(z,z')​即最大化​H(z)​并最小化​H(z|z')​，

<img src="https://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/IIC-3.png" alt="IIC3" style="zoom:10%;" />

最小化H(z|z')​的意义为拉近​z​和​z'​的距离。

最大化H(z)​的意义为使各个聚类簇内的样本数量趋于均衡。不均衡数据集与此优化方向冲突。























