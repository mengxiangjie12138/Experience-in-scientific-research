## Graph Attention Networks

### 动机

1. 解决了之前GCN中的问题
2. 不需要提前建立的邻接矩阵

### 方法

1. 单一图注意力层

为了确定图中第$ij$个样本之间的边权重，首先使用权重为$w$的全连接层对低$i$个和第$j$个样本的特征进行变换。

<img src="https://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/GAT-1.png" alt="GAT1" style="zoom:3%;" />

之后根据如下公式计算边权重，

<img src="https://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/GAT-2.png" alt="GAT2" style="zoom:15%;" />

其中$a$代表可训练参数，$\cdot\|\cdot$代表特征拼接，$N_i$代表第$i$个样本的邻域。无初始化图时该邻域代表所有样本点。

整合之后，得到最终的图注意力层计算公式如下，

<img src="https://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/GAT-3.png" alt="GAT3" style="zoom:10%;" />

2. 多头注意力模型

每层由多个随机初始化的单一注意力层组合而成，组合方式包括拼接和取平均。假设总共有K个头

拼接：

<img src="https://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/GAT-4.png" alt="GAT4" style="zoom:15%;" />

平均：

<img src="https://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/GAT-5.png" alt="GAT5" style="zoom:15%;" />

### 扩展

单一图注意力层的计算公式可以转换为如下公式：

<img src="https://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/GAT-6.png" alt="GAT6" style="zoom:10%;" />

其中$\alpha$为更新后的邻接矩阵，$h'$为所有输出特征，$h$为所有输入特征。























