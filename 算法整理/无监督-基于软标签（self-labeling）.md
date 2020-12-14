# 无监督-基于软标签

### 1.Deep Clustering for Unsupervised Learning of Visual Features  arxiv2019

- 原始图片x传入特征提取器得到features，该features分别传入聚类部分和分类部分
- 聚类部分：将features经过kmeans聚类得到类别的指派作为软标签（Y）
- 分类部分：将features经过全连接层组成的分类器得到类别的概率分布作为预测（F）
- 加入软标签和概率分布的softmax损失
- 对聚类部分使用kmeans聚类损失进行约束

<img src="http://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/Deep-clustering-loss.png" alt="Deepclustering" style="zoom:20%;" />

![Deepclustering-method](http://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/Deep-clustering-method.jpg)

注：

- 该算法适用于存在预训练特征提取器的前提下。
- 对退化解问题的处理（类比有监督问题）
- 1. 当有两个类别被分到同一簇时，任选另一个簇，将簇心添加一个微小扰动后作为新的簇心，将这两个类别分布到不同的簇中，再进行后续迭代。
  2. 当数据严重不均衡（长尾数据）时，可以通过在softmax损失添加权重的方式平衡数据集，从而避免退化解

### 2.LSD-C: Linearly Separable Deep Clusters  arxiv2020

- 代码https://github.com/srebuffi/lsd-clusters
- 原始输入x与增强图像x'传入一预训练完全的自监督表示学习模型提取特征得到features
- 根据某种建图方法构建features之间的邻接矩阵（L2或余弦距离，SNE算法，KNN算法）
- 将features传入全连接分类器得到概率分布，并用以下的两个损失训练该分类器
- 最小化x与x'得到的概率分布之间的MSE损失
- 最小化聚类损失（本质上为二分类交叉熵损失）

![LSD-C-loss](http://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/LSD-C-Loss-clus.jpg)

![LSD-C-method](http://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/LSD-C-method.jpg)

### 3.Unsupervised Learning of Visual Features by Contrasting Cluster Assignments   arxiv2020

- 将原始输入x经过两次不同的裁剪得到增强图像x-t和x-s
- 将x-t和x-s分别经过相同的特征提取器得到features z-t和z-s并进行单位映射

<img src="http://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/SwAV-z_t.png" alt="SwAV-z" style="zoom:5%;" />

- 在原始网络之后添加一全连接层，输入为features，权重为C，输出为features与C之间的相似程度p-t和p-s（与DEC的聚类层相似），计算公式如下

<img src="http://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/SwAV-p.png" alt="p" style="zoom:10%;" />

- 在原始网络之后再添加一平行全连接分类器，通过features得到概率分布q-t和q-s
- 交叉计算pq之间的交叉熵损失

<img src="http://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/SwAV-loss1.png" alt="loss1" style="zoom:15%;" />

- 最大化目标函数，通过Tr（矩阵的迹）的计算最大化features和C之间的相似程度，并通过H（熵）的计算让各个预测类别的数量趋于均衡，避免退化解

<img src="http://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/SwAV-object-fun.png" alt="Object-fun" style="zoom:10%;" />

![SwAV-method](http://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/SwAV-method.jpg)

















