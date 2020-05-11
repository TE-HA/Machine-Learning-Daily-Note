# EM算法

## 1.最大似然估计

总的来说：极大似然估计就是用样本来估计模型参数的统计学方法		

已知：

1. 样本服从分布的模型
2. 观测到的样本
3. 求解：模型的参数

```mermaid
graph LR
a[样本]-->|反推|b[模型参数]
```

最大似然函数：
$$
l(\theta)=\sum_{i=1}^mlogp(x_i;\theta)
$$
(对数是为了乘法变加法)

得出什么样的参数$\theta$能够使得出现当前这批样本的概率最大。已知某个随机样本满足何种概率分布，但是其中具体的参数不清楚，参数估计就是通过若干次实验，观察其结果，利用结果推出参数的大概值。

进阶：

两个类别，两个参数均服从高斯分布，但是参数不同（均值，方差）。==问题：抽取得到的每个样本都不知道是从哪个分布抽取的，求解目标：不同类别对应的身高的高斯分布的参数是多少。==

解决：

加入隐变量，用Z=0或者Z=1标记样本来自哪个分布，则Z就是隐变量。

最大似然函数（将不同类别的情况均考虑进来）：
$$
l(\theta)=\sum_{i=1}^mlogp(x_i;\theta)=\sum_{i=1}^mlog\sum_Z p(x_i,Z;\theta)
$$
求解：在给定初始值情况下进行迭代求解

例：

![image.png](https://i.loli.net/2020/05/11/P84HdcRyXTBEe5U.png)

## 2.EM算法推导

两边分式分子分母同时乘Q(Z)（Q(Z)是Z 的分布函数）（==凑-Jensen不等式==）：
$$
log\sum_Z p(x_i,Z;\theta)=log\sum_ZQ(Z)\frac {p(x_i,Z;\theta)}{Q(Z)}
$$
Jensen不等式：$f(x)$凸函数，X是随机变量哪个函数值的期望大于等于期望的函数值。凹函数相反。

由于$\sum_ZQ(Z)\frac {p(x_i,Z;\theta)}{Q(Z)}$是$\frac {p(x_i,Z;\theta)}{Q(Z)}$的期望，假设Y=$\frac  {p(x_i,Z;\theta)}{Q(Z)}$，则：$log\sum_ZQ\frac {P(x_i,Z;\theta)}{Q}=logE_YP(Y)Y=logE(Y)$

结论：
$$
l(\theta)=\sum_{i=1}^mlog\sum_Z p(x_i,Z;\theta)\ge\sum_{i=1}^m\sum_ZQ(Z)log\frac {p(x_i,Z;\theta)}{Q(Z)}
$$
下界比较好求，所有我们要优化这个下界来使得似然函数最大。

==优化下界，迭代到收敛==

Jenson中等式成立的条件是随机变量是常数：$Y=\frac {p(x_i,Z;\theta)}{Q(Z)}=C$

Q(Z)是Z的分布函数:$\sum_ZQ(Z)=\sum_Z\frac {p(x_i,Z;\theta)}{Q(Z)}=1$

所有的分子和等于常数C（分母相同）
$$
Q(Z)=\frac {p(x_i,Z;\theta)}{C}=\frac {p(x_i,Z;\theta)}{\sum {p(x_i,Z;\theta)}}=\frac {p(x_i,Z;\theta)}{p(x_i)}=p(z|x_i;\theta)
$$
Q(Z)表示第$i$个数据是来自$zi$的概率

EM算法流程：

1. 初始化分布参数$\theta$
2. E-step:根据参数$\theta$计算每个样本属于$zi$的概率（也就是我们的Q）
3. M-step：根据Q，求出含有$\theta$的似然函数的下界并最大化它，得到新的参数$\theta$
4. 不断的迭代更新下去

## 3.GMM（高斯混合模型）

1. 数据可以看作是从数个Gaussian Distribution中生成出来的
2. GMM由K个Gaussian Distribution组成，每个Gaussian称为一个Component
3. 类似K-means方法，求解方式跟EM一样
4. 不断的迭代更新下去

## 4.GMM聚类实例

