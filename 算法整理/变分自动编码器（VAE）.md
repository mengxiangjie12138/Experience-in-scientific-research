# 变分自动编码器（VAE）

### 动机

用于图像生成的强化学习

### 方法

1. 在普通自动编码器（AE）的基础上对瓶颈层进行处理
2. 将Encoder输出的features(Y)经过两个平行的全连接层，分别计算出features的期望向量（mean vector）和方差向量（variance vector）
3. 构造一个和mean vector与variance vector相同维度的标准正态分布向量N，将mean vector与N相乘，再加上variance vector，得到采样变量（sampled variable）
4. 将采样变量放入Decoder部分进行重构。
5. 加入新的损失，最小化构造的正态分布与标准正态分布之间的KL散度

<img src="http://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/VAE-loss.png" alt="VAE" style="zoom:10%;" />

![VAE](http://mengxiangjie12138-images.oss-cn-beijing.aliyuncs.com/VAE-method.png)