## NLP

+ word2vec : https://www.bilibili.com/video/av41393758/?p=2

english - wordNet 语言的分类信息，像个python的词典库，可以做校验

one-hot [0 1 0 ... 0 ]

distribution similarity 通过上下文获取一个词的大量的值，关于词汇语义

计算word2vec

损失函数：本质让每个词向量能够预测其周围的词汇，反之亦然（vice versa）

$ w_-t $ 上下文除了t的词

skip-gram：定义一个概率分布，给定一个中心词汇，某个单词在它上下文中出现的概率

连乘 \Pai

$ j (i) = \prod_{position}  \prod_{-r to r} P (w_t|w_j) $

取log 转为求和 -> 每个词的概率乘积 to 每个词预测概率log取平均 归一化处理

当求一个词的概率时 softmax 一下 $ P(objective|center_{word}) = \frac{exp(u_o^t * v_c)}{\sum{exp(u_w^t * v_c)}} $

v时中心词 vec，u时预测词 vec

每个词有2个词向量，是为了计算方便，作为center一种，上下文 时是另一种，二者相互独立  ，并且可能出现了这个词的center，上下文不会出现同一个词，如果一样的话，点积概率最大

center word （one hot * matrix）, context(word2vec)

只关注词义，词的位置可以忽视，即距离中心词的距离

两个词越相似，点积越大 (如果用余弦函数去算的话会更好，但是更难算)
 
$ J(sita) = log (\frac {exp(u_0^T*v_c)}{\sum{exp(u_w^T*v_c)}}) $

求梯度时，求偏导，然后 log 展开成减法，log，e约掉，左边为$u_0$，右边用链式法则，后面求和符号换序，再exp的链式法则，发现后面的系数刚好是softmax里计算的概率 p(x|center)

化简得 偏导 $  J(sita) = u_0 - \sum{P(x|c)u_x} $ 前面是观察值，后面是期望向量

链式法则 对 f(g(u)) 求导， 对f, g分别求导

+ SGD （stochastic gradient descent）

如果在训练word2vec中的话，随机选取一个位置，学习到的梯度直接用于计算下一个的梯度，而不是全算完在更新

+ 句子 向量

+ 词袋 bag-of-words BoW

一个句子 = 词汇 词向量的加权平均值   $ V_{sentence} = \frac{1}{|sentence-word-number|}\sum{\frac{a}{a+p(w)}v_w} $ a 是常数，p(w)是词出现的频率

（log likelihood 对数似然）

论文 ： A Simple but Tough-to-beat Baseline for sentence embeddings

计算第一部分的主成分，再减去第一部分的投影 这部分参考PCA 主成分分析算法， 一个词的概率 与 词的出现频率，词与句子之间的关联程度

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

最大熵 ： $P(w_3 | w_2, w_1, subject)= \frac{e^{(lambda_1(w_1,w_2,w_3)+lambda_2(w_3,subject)}}{(Z(w_1,w_2,subject))}$

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

+ TF-IDF

词频-逆文档频率, log(tot/cor + 1) : 提取关键词->关键词向量，找相似文章->通过关键词的簇，提取文章摘要

https://www.cnblogs.com/cppb/p/5976266.html

+ 协方差矩阵

+ BPE

+ n-gram

+ c-bow

+ softmax

+ markdown 公式

https://blog.csdn.net/lihaoweicsdn/article/details/83895143

+ i am vegitable
