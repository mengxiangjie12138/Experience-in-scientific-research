注：本节内容较多，可用`ctrl+F`快速查找关键词。

#### 数据类型

##### 整体类型

- DataFrame-二维表格
- Series-单列数据

#### 导入库

```python
import pandas as pd
```

#### 查看基本信息

##### 查看形状

```python
rows, cols = data.shape
print("数据共有 %s 行，有 %s 列。" % (rows, cols))
```

##### 查看前几列

```python
head = data.head()
```

- 可通过参数改变查看的行数，`head(10)`代表查看前10行。

##### 查看最后几列

```python
tail = data.tail()
```

- 可通过参数改变查看的行数，`tail(10)`代表查看后10行。

##### 查看总体信息

```python
data.info(null_counts=True)
```

- `null_counts=True`代表结果中包括打印每列空值个数

#### 基本操作

##### 数据删除

```python
data.drop([索引],axis=1)
```

```
参数
data：索引，为列表
axis：0代表删除行，1代表删除列
```

##### 数据计算

- 加减乘除可直接对Series或DataFrame使用，也可对DataFrame中的某行某列使用（数据必须为数值型或字符串，字符串相加代表拼接）
- 例

```python
data['calculate'] = data['calculate'] / 100
```

##### 数据排序

**对Series**

```python
sort_values(ascending=False)
```

- `ascending`默认为True，代表升序；为False时代表降序。

**对Framework**

```python
sort_values(ascending=False, by='列名')
```

- `ascending`默认为True，代表升序；为False时代表降序。
- `by`代表排序的依据列，可选择多列。

##### 数据筛选

- 形式类似于索引。
- 可与判断函数结合使用，如`data[data['name'].isnull()]`筛选name列为空数据的行。

**行筛选**

```python
data[筛选条件]
# 或
data.loc[筛选条件]
```

- 返回满足条件的行
- 常用逻辑表达式：`~`取反，`&`与，`|`或。注意：逻辑表达式的优先级较低，使用时前后部分最好加上括号。

**行列筛选**

```python
data.loc[行筛选条件, 列筛选条件]
```

##### 相关函数

**筛选函数`map`**

```python
data.map(条件)
```

- 例

```python
data['new'] = data['number'].map(lambda x: 1 if x > 500 else 0)
```

**字符串匹配**

```python
data.contains('字符串')
```

- 可用逻辑表达式在字符串内|或&相连多个字符

```python
data[data['name'].str.contains('aa|bb|cc|dd')]  # 匹配到其中任意子字符串都符合要求
```

- 其他数据类型可先转换成字符串再进行匹配

```python
data[data['name'].str.contains('aa')]
```

#### 数据清洗

##### 数据去重

- 查看重复值

```python
data[data.duplicated()]
```

- 删除重复值

```python
data.drop_duplicates(inplace=True)
```

```
参数
- subset：默认判定正行是否重复，可以选择固定列，判定某些列是否重复
- keep：可以为first或last，表示选择最前一项保留或最后一项保留，默认为first
- inplace：是否在原数据上进行更改，默认为False
```

##### 缺失值处理

- 填充缺失值

```python
data['name'].fillna(1)  # 缺失值全部填充为1
```

#### 常用内置函数

##### 判断函数

```python
sample.isin(集合/列表)  # 判断是否在集合或列表中
sample.isnull()  # 判断是否为空
```

##### 分组函数`groupby`

```python
data['data'] = data['time'].groupby(data['name'])  # 根据name进行分组，返回time列数据
```

```
参数
- by：分组依据
- axis：0表示按行分组，1表示按列分组
```

- 分组后添加聚合函数，对每组进行聚合

##### 聚合函数

```python
data.size()  # 统计个数
data.sum()  # 求和
data.mean()  # 计算平均数
data.std()  # 计算标准差
data.max()  # 选出最大值
data.min()  # 选出最小值
data.agg()  # 自定义聚合函数
```

- 聚合函数特殊用法

```python
data[['1','2','3']] = data.groupby(data['name']).agg({'1': 'min', '2': 'size', '3': 'sum'})
```

- 注意：字典`key`值不能重复

##### 离散函数

```python
pd.cut()  # 等距离散化
```

```
参数
x：1维ndarray或Series，表示要划分的数据
bins：整数，将x划分为多少个等距的空间
labels：设置区间名称，可为列表或数组，若为False则返回整数填充的区间名
duplicates：如果分组的bin边缘不唯一，该参数为raise则报告ValueError，为drop则直接删除非唯一值
```

```python
pd.qcut()  # 等频离散化
```

```
参数
x：1维ndarray或Series，表示要划分的数据
labels：设置区间名称，可为列表或数组，若为False则返回整数填充的区间名
q：分位数，用来指定区间的数量，表示要划分为几组
duplicates：如果分组的bin边缘不唯一，该参数为raise则报告ValueError，为drop则直接删除非唯一值
```

##### 其他函数

**阈值计算**

```python
data.quantile(q=百分比)
```

- 例

```python
data['number'].quantile(q=0.75)  # 返回number列中所有数据中位于75%位置的数字（上四分位数）
```

**单列数据去重`unique`**

```python
data['列名'].unique()
```

- 例

```python
user_num = len(data['user_id'].unique())
print("数量:",user_num)
```

```
数量:  7630
```

- 计算每个元素重复的次数

```python
data['列名'].value_counts()
```

#### 时间类型数据处理

##### 时间格式转化

```python
data['time'] = pd.to_datetime(data['raw_time'], unit='s')
```

- `unit`代表最小时间单位

##### 时间戳

```python
pd.Timedelta(hours=8)  # 代表一个八小时的时间戳
```

- 时间类型数据可直接加减乘除计算

```python
data['time'] + pd.Timedelta(hours=8)  # 代表在原时间基础上经过八小时
```

##### 时间点

```python
pd.Timestamp(2018,3,19)  # 代表2018年3月19日
```



















