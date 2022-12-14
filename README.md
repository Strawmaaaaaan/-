# 学习笔记

供自用

## 目录
## 
#### 1. unhashable error


## 机器学习基础

### 损失

#### 1. softmax Loss
softmax的作用就是把一个序列通过下列公式变成概率值。
$$S_j = e^{a_{j}} / \sum_{k=1}^{N}e^{a_{k}}$$
它能够保证：
- 所有的概率值都是[0,1]之间
- 所有的概率值之和等于1


  

#### 2. Cross-Entropy Loss
交叉熵损失用来描述两个概率分布之间的距离，熵越大说明预测结果越混乱具有不确定性，熵越小则说明结果越准确。计算公式为：
$$L = -\frac{1}{N}\sum_{i}\sum_{c=1}^{M}y_{ic}log(p_{ic})$$
其中：
- M代表类别数
- $y_{ic}$代表符号函数，如果样本i的真实类别等于c则取1，否则取0
- $p_{ic}$代表样本i属于类别c的预测概率  


交叉熵损失设计到每个类别样本概率的计算，因此通常和sigmoid或softmax函数一起使用  
**优缺点**  
优点：  
- 当模型效果差的时候，网络学习速度快；模型效果好的时候，网络学习速度会变慢（比均方误差好）  
缺点：  
- 只是关注了对正确标签预测概率的准确性，忽略了错误标签的差异。（对错误分类的样本损失是0）
- 随着分类数目的增加，分类层的线性变化矩阵参数会增加。  

## Pytorch
#### 1. Backward和Optimize
- optimizer.zero_grad( ): 将梯度清零，不清零的话梯度会和上一个batch的数据相关。该函数要写在反向传播和梯度下降之前。
 
- loss.backward(): Pytorch的反向传播通过autograd包实现，根据tensor张量进行过的数学运算来自动计算梯度。使用tensor.backward()后，所有的梯度自动计算，tensor的梯度会累加到它的.grad属性里面。

- optimizer.step(): step()函数的作用是执行一次优化步骤，通过梯度下降法来更新参数的值。因为梯度下降是基于梯度的，所以在执行optimizer.step()函数前应先执行loss.backward()函数来计算梯度。

**注意**：optimizer只负责通过梯度下降进行优化，而不负责产生梯度，梯度是tensor.backward()方法产生的。

在Pytorch的计算图中，包含两种元素：tensor和function。其中function就是一些可求导的运算，tensor可以细分为叶子结点和非叶子结点。在使用backward()函数反向计算tensor的梯度时，只是计算满足这几个条件的tensor的梯度：1. 叶子结点的tensor 2. reguires_grad=True 3. 依赖该tensor的所有tensor的requirs_grad=True.   
如下图所示，在进行了m.backward()以后，非叶子结点如y的梯度会被释放掉，如果想要保留非叶子结点的梯度，**可以使用m.backward(retain_graph=True)**
![image](https://github.com/Strawmaaaaaan/-/blob/main/backword_1.png)  
- detach()函数的作用是返回一个新的tensor张量，且requires_grad = False，起到截断梯度的效果，域源张量共享数据内存**注意：即使后续将其requires_grad置为true也不会具有梯度**
- clone()函数返回一个和源张量同样形状和device的张量，但是不与源数据共享内存，但是提供梯度的回溯
- .clone().detach()这样的组合只做简单的数据复制，不共享数据也不共享梯度，两个张量没有关联

#### 2. 检查梯度
##### （1）出现nan的情况：
- 


## 算法基础
### 其他
#### 1.单调栈
单调栈是栈的一种特殊形式，顾名思义入栈的同时要保证栈内的元素是单调递增或者单调递减的，利用这样的思想可以找到当前元素左边第一个比其大的元素（单调递减栈）或者第一个比其小的元素（单调递增栈）  
对于单调递减栈，首先要压入一个最大值INT_MAX，保证栈不为空，如果当前元素小于栈顶元素则入栈，否则将栈顶元素出栈直至栈顶元素大于当前元素，接着将当前元素进栈。  
**例题**：[Leetcode : 901. 股票价格跨度](https://leetcode.cn/problems/online-stock-span/)




