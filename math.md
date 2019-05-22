## 概率论

$$
P(AB)=P(A)P(B|A)=P(B)P(A|B)\\P(A)=\frac{P(B)P(A|B)}{P(B|A)}\\P(B_i|A)=\frac{P(B_i)P(A|B_i)}{P(A)}\\P(A)=\sum{P(AB_i)}=\sum_{i=1}^{n}{P(B_i)P(A|B_i)}\\P(B_i|A)=\frac{P(B_i)P(A|B_i)}{\sum_{i=1}^{n}{P(B_i)P(A|B_i)}}
$$





| 名称              | 期望   | 方差    | 备注                                     |
| ----------------- | ------ | ------- | ---------------------------------------- |
| 伯努利分布        | p      | 1-p     | 0-1分布                                  |
| 二项式分布B(n, k) | np     | np(1-p) |                                          |
| 泊松分布          | lambda | lambda  | 当二项分布，n很大，p很小时，趋近泊松分布 |
|                   |        |         |                                          |



+ 概率分布

  二项分布
  $$
  p(x=k)=C_n^{k}p^k(1-p)^{n-k}
  $$



  泊松分布

  离散分布，lambda是平均发生的次数，由二项分布转的话，lambda=np
$$
p(x=k)=\frac{\lambda^k}{k!}e^{-\lambda}
$$
  抽样分布

  卡方分布chi-square distribution
$$
X\~\chi^2
$$

+ **自由度**(degree of freedom, df)指的是计算某一统计量时，取值不受限制的变量个数。通常df=n-k。其中n为样本数量，k为被限制的条件数或变量个数，或计算某一统计量时用到其它独立统计量的个数。自由度通常用于抽样分布中。
+ **极大似然估计**  MLE，估计参数，使观测值概率最大。给出似然函数，取log求偏导，解方程
+ 

reference: https://blog.csdn.net/anshuai_aw1/article/details/82735201

https://wenku.baidu.com/view/7d812885f021dd36a32d7375a417866fb84ac0b1.html

https://github.com/apachecn/prob140-textbook-zh/blob/master/docs/7.md

题库: https://zhuanlan.zhihu.com/p/42473598



### 矩阵变换

reference: <https://blog.csdn.net/qq_23030843/article/details/81064881>



+ 协方差矩阵可用来表示多维随机变量的[概率密度](https://baike.baidu.com/item/概率密度)，从而可通过协方差矩阵达到对多维随机变量的研究。
+  $A*A^T$是对称矩阵，然后$SVD$



狄利克雷函数
$$
f(x)=
\begin{cases}
1\qquad x为有理数\\
0\qquad x为无理数\\
\end{cases}
$$


双调排序->适合GPU跑

八叉树->空间树



### 傅里叶变换

reference: <https://blog.csdn.net/randy_01/article/details/83217314>

reference: <https://www.cnblogs.com/h2zZhou/p/8405717.html>

傅里叶级数：将函数用三角函数展开
$$
f(x)=A_0+\sum_{i=1}^{k}{A_isinax+B_icosax}
$$
大概是这样的，任意的函数，（不管周期长度），都可以由三角函数的叠加去逼近。

证明了三角函数是一组正交基，即
$$
\int{sinnx}=0\\
\int{cosnx}=0\\
\int_{-\pi}^{\pi}{sinkx*cosnx}=0\\
$$
这样连着f左右两边同时积分，就可以求出对应级数的系数



傅里叶变换：傅立叶变换就是把信号中的基分离出来，从时间转换到频率。即从声音的振幅转换成对应的乐谱。

时域相当于原来的叠加的图像，转换后成为若干竖线，降低了计算难度（积分变乘除，乘除变加减）

频道，就是频率的通道，不同的频道就是将不同的频率作为一个通道来进行信息传输

去掉曲线内的特定频率成分--滤波

TODO： FFT

---

### 可导与可微的关系

一元函数中，可微和可导是等价的
多元函数中，某一点可微的条件是在所有方向上都可导（多元函数全微分存在，偏导数均存在）



