# 学习笔记

供自用

## 目录

## 机器学习基础

### 损失

#### 1. softmax Loss
$$ $$
  

#### 2. Cross-Entropy Loss
交叉熵损失用来描述两个概率分布之间的距离，熵越大说明预测结果越混乱具有不确定性，熵越小则说明结果越准确。计算公式为：
$$L = -\frac{1}{N}\sum_{i}\sum_{c=1}^{M}y_{ic}log(p_{ic})$$
其中：
- $M$代表类别数
- $y_{ic}$代表符号函数，如果样本$i$的真实类别等于$c$则取1，否则取0
- $p_{ic}$代表样本$i$属于类别$c$的预测概率
交叉熵损失设计到每个类别样本概率的计算，因此通常和$sigmoid$或$softmax$函数一起使用
**优缺点**
优点：
- 当模型效果差的时候，网络学习速度快；模型效果好的时候，网络学习速度会变慢（比均方误差好）
缺点：
- 只是关注了对正确标签预测概率的准确性，忽略了错误标签的差异。（对错误分类的样本损失是0）
- 随着分类数目的增加，分类层的线性变化矩阵参数会增加。

