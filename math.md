## 概率论



| 名称              | 期望   | 方差    | 备注                                     |
| ----------------- | ------ | ------- | ---------------------------------------- |
| 伯努利分布        | p      | 1-p     | 0-1分布                                  |
| 二项式分布B(n, k) | np     | np(1-p) |                                          |
| 泊松分布          | lambda | lambda  | 当二项分布，n很大，p很小时，趋近泊松分布 |
|                   |        |         |                                          |
|                   |        |         |                                          |
|                   |        |         |                                          |
|                   |        |         |                                          |
|                   |        |         |                                          |
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

reference: https://blog.csdn.net/anshuai_aw1/article/details/82735201

https://wenku.baidu.com/view/7d812885f021dd36a32d7375a417866fb84ac0b1.html

https://github.com/apachecn/prob140-textbook-zh/blob/master/docs/7.md