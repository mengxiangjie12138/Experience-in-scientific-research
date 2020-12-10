## Bag of Tricks for Image Classification with Convolutional Neural Networks

### 代码地址

https://github.com/dmlc/gluon-cv

### 动机

在ResNet50的基础上总结并验证能够提高网络效果的小trick。

### 方法（tricks）

#### 数据预处理

1. 随机裁剪
2. 随机翻转
3. 标准化亮度，色彩和饱和度
4. 加入PCA噪声
5. 归一化

#### 超参数

1. 当batch size为256时，选择0.1作为初始学习率，当batch size更大时，我们将初始学习率提高到0.1×b/256

相关文章：

Accurate, large minibatch SGD: training imagenet in 1 hour

Deep residual learning for image recognition

2. 学习率预热

设置初始学习率为接近0的数r，在第n个batch（1<n<m）将学习率设置为nr/m























