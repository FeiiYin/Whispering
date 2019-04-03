## NLP

+ attention & self attention & transformer

can be described as mapping a query and a set of key-value pairs to an output

https://www.cnblogs.com/robert-dlut/p/8638283.html

https://zhuanlan.zhihu.com/p/53682800

+ 概率图模型 & HMM & CRF

https://zhuanlan.zhihu.com/p/55238865

贝叶斯网络 ： https://www.cnblogs.com/ironstark/p/5087081.html

贝叶斯链式法则 = = 

高斯分布 == 正态分布 GMM 高斯混合模型 (待看)

隐变量 latent variable  观测不到但能影响结果或是模型参数的变量 https://blog.csdn.net/Ding_xiaofei/article/details/80207084

最大熵 ： $P(w_3 | w_2, w_1, subject)=\frac_{e^{(lambda_1(w_1,w_2,w_3)+lambda_2(w_3,subject)}}{(Z(w_1,w_2,subject))}$

HMM https://www.cnblogs.com/skyme/p/4651331.html  关于路径选取，取路径概率（乘积）最大，关于模型隐变量选取，取求和概率最大

每一个HMM模型都等价于某个CRF,相当于是前面的参数为1，并且HMM中是事件之间相互独立的，转移概率来推动时间变化，CRF中用特征函数来监督时间

Viterbi algorithm

CRF 条件随机场 https://www.imooc.com/article/27795   特征函数集合，求值后 进行归一化乘权重求和，是逻辑回归的序列化版本

+ EM算法 最大期望算法（Expectation-Maximization algorithm, EM）

初始化答案参数或隐变量，极大似然估计出模型参数，再用此时模型极大似然估计出隐变量，初始与最后估计相近收敛（估计的时候用概率）

https://www.jianshu.com/p/1121509ac1dc

+ 最大似然估计

https://zhuanlan.zhihu.com/p/26614750

+ smoothing & 长尾效应(long tail phenomenon) & 拉普拉斯平滑（加一平滑）& Add-k Smoothing（Lidstone’s law）& 插值

https://blog.csdn.net/u013802188/article/details/40348587

https://blog.csdn.net/baimafujinji/article/details/51297802

平滑加的分母 V， V  是所有的可能的不同的n-Gram的数量，在这个例子中，它其实就是语料库中的词汇量，而这个词汇量是不包括 <s> 的，但却需要包括 </s>。

插值：Pinterp(wn|wn−2,wn−1)=λ1P(wn)+λ2P(wn|wn−1)+λ3P(wn|wn−2,wn−1)

+ 上采样 & 下采样

上采样：利用插值放大图像； 下采样，直接取区域内的平均像素值，缩小图像；

https://blog.csdn.net/stf1065716904/article/details/78450997

+ 协方差矩阵

+ BPE

+ n-gram

+ c-bow

+ softmax

+ markdown 公式

https://blog.csdn.net/lihaoweicsdn/article/details/83895143

+ i am vegitable
