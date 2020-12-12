# 无监督-基于自动编码器（AE）

### 1.Auto-Encoding Variational Bayes（VAE）  arxiv2013

- 在普通自动编码器（AE）的基础上对瓶颈层进行处理

- 将Encoder输出的features(Y)经过两个平行的全连接层，分别计算出features的期望向量（mean vector）和方差向量（variance vector）

- 构造一个和mean vector与variance vector相同维度的标准正态分布向量N，将mean vector与N相乘，再加上variance vector，得到采样变量（sampled variable）

- 将采样变量放入Decoder部分进行重构。

- 加入新的损失，最小化构造的正态分布与标准正态分布之间的KL散度

<img src="http://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/VAE-loss.png" alt="VAE" style="zoom:10%;" />

![VAE](http://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/VAE-method.png)

- 注1：该算法经常用于图像生成的强化学习
- 注2：GAN网络兴起后VAE已经很少被使用

### 2.Unsupervised Deep Embedding for Clustering Analysis（DEC）  arxiv2015

- 第一部分将原始图片x作为输入使用MSE损失训练一个全连接自动编码器（AE）
- 第二部分取出训练完全的自动编码器的Encoder部分作为特征提取器，提取x的特征得到z
- 使用kmeans对所有样本得到的特征进行聚类，得到系列聚类中心u
- 将u作为聚类层初始化权重，特征z作为聚类层输入，计算z和u之间的相似度得到类别的概率分布q

![DEC-q](http://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/DEC-q.jpg)

- 使用q进行计算得到辅助概率分布p

![DEC-p](http://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/DEC-p.jpg)

- 计算pq之间的KL散度作为损失作为第二部分网络的约束

![DEC-method](http://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/DEC-method.jpg)

- 注：第二部分聚类层的优化过程与kmeans的算法思路相似，通过不断迭代聚类中心直到中心与类内各个点之间的距离和最小为止