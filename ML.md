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

u和v一开始向量里是随机的数，小随机数，大部分目标函数非凸，初始化很重要

每次梯度下降好像只更新用到的词的向量

分母原来是求整个词表的点积和，效率太低，由于很多次和其他的词不会同时出现，所以随机选取一些不会同时出现的词的点积和作为分母

求梯度时，求偏导，然后 log 展开成减法，log，e约掉，左边为$u_0$，右边用链式法则，后面求和符号换序，再exp的链式法则，发现后面的系数刚好是softmax里计算的概率 p(x|center)

化简得 偏导 $  J_t(sita) = u_0 - \sum{P(x|c)u_x} $ 前面是观察值，后面是期望向量

链式法则 对 f(g(u)) 求导， 对f, g分别求导

初始阶段可以先遍历整个词表更新梯度，也可以先取窗口大小的center word，然后SGD

PCA可视化 可以将词向量变成二维的图片

本质目的 获取词的共同点，这个词和其他词共同出现的概率时多少

co-occurence & SVD 方法，不用梯度下降，只统计词频，（a在b后出现了多少次）这会生成一个系数矩阵，他的长宽是词表的大小，通过SVD（奇异值分解）降维。但是这个方法主要获取词之间的相似性，不能获取其他pattern。通常skip-gram better

Glove vector方法，相当于是结合了两种训练的方法，在反向的函数中涉及到两块的矩阵

最后center vector 和context vector可以连接起来，或sum up（效果更好）

第三集的TA：多义词的vector是他在各个意义的vector的线性叠加，可以通过稀疏编码来对其进行语义解释

一种内在的评价方法：类比，比如 取余弦距离最近（男人-女人+国王）= 皇后，不仅包含语义，语法的关系也有类比。

另一种是对下游的模型训练再比较，如NMT，NER

+ SVD

https://www.cnblogs.com/pinard/p/6251584.html

方阵 有 特征向量和特征值，分解成 $M = X A X^T$ X 是特征向量的拼接，转成酉矩阵 即 X*X^T = 1

SVD是对于矩阵的，用 N*N^T 和 N^T*N 构造两个方针，分别求出其特征向量的酉矩阵放在两边，中间奇异矩阵是左边的特征值的开放

降维的时候是因为特征值的前面几个和占了前面的99%以上，后面的 以及左右矩阵对应的可以省去

+ PCA 

http://www.cnblogs.com/pinard/p/6239403.html

推导太数学，跳过了部分

SVD是基于这个的，对于数据降维，把n维的数据降到n'维，就是投影，然后投影更分散，也可以说所有点到新的超平面的距离最小，可以拿二维的散点映射到一维时，就是选择一个向量使其投影最分散

过程，先对数据中心化，就是平移使数据和为0，算协方差矩阵 XX^T，然后求特征值，取前n'个最大的，降维通过新方阵转置乘以原维度的数据即可。如果要主成分大于多少的，即选取特征值的大小占总特征值和的多少。 相当于是对数据的协方差矩阵进行降维

KPCA 由于数据可能不是线性，不能直接投影，用核函数将其映射到一个更高位的空间，在PCA降维

协方差 是 用于衡量两个变量的总体误差，即协方差表示的是两个变量总体误差的期望。，方差是衡量自己的总体误差。如果两个变量的变化趋势一致，也就是说如果其中一个大于自身的期望值，另外一个也大于自身的期望值，那么两个变量之间的协方差就是正值。 如果两个变量的变化趋势相反，即其中一个大于自身的期望值，另外一个却小于自身的期望值，那么两个变量之间的协方差就是负值。

$ COV(X, Y) = E[(X-E(X))(Y-E(Y))] = E[XY]-E[X]E[Y] $ 二者相互独立的话协方差为0

注意这里求协方差矩阵一般是 用样本方差（除n-1），而不用总体方差（除n），因为自己的数据往往不会是全部数据

样本方差和总体方差的区别：https://blog.csdn.net/hearthougan/article/details/77859173

+ sigmoid 

激活函数  $ J(x) = \frac{1}{1+e^{-x}} $  把实数映射到0和1之间 转成概率

有 $ J(-x) = 1 - J(x) $ 概率转化

+ SGD （stochastic gradient descent）

如果在训练word2vec中的话，随机选取一个位置，学习到的梯度直接用于计算下一个的梯度，而不是全算完在更新

+ 句子 向量

+ 词袋 bag-of-words BoW

词袋预测word2vec的话，吧上下文词向量求和 然后与中心 词向量作点积 然后同上

一个句子 = 词汇 词向量的加权平均值   $ V_{sentence} = \frac{1}{|sentence-word-number|}\sum{\frac{a}{a+p(w)}v_w} $ a 是常数，p(w)是词出现的频率

（log likelihood 对数似然）

论文 ： A Simple but Tough-to-beat Baseline for sentence embeddings

计算第一部分的主成分，再减去第一部分的投影 这部分参考PCA 主成分分析算法， 一个词的概率 与 词的出现频率，词与句子之间的关联程度

+ attention & self attention & transformer

can be described as mapping a query and a set of key-value pairs to an output

https://www.cnblogs.com/robert-dlut/p/8638283.html

https://zhuanlan.zhihu.com/p/53682800

这篇很全很清楚   https://blog.csdn.net/qq_41664845/article/details/84969266 

时序信息通过 时序向量表示，与初始向量加和计算。

补充细节： <https://zhuanlan.zhihu.com/p/60821628?utm_source=qq&utm_medium=social&utm_oi=761286192158244864>



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

loss for softmax：通常是cross-entropy

交叉熵：$ H(p, q) = -\sum{p(c)log q(c)} $ p(c) 是真实概率（one-hot向量，只取正确的），q(c)是预估概率，即softmax计算得到的，然后最小化该式

对于所有数据来说 $ J(sita) = \frac{1}{N}\sum{-log(softmax(f))} $  $ f = W*x $最小化该值, W是softmax的参数

 $ J(sita) = \frac{1}{N}\sum{-log(softmax(f))}+\lambda\sum{\theta_k^2} $ 后面的偏置使参数能够减小，防止参数过大，过拟合

https://www.jianshu.com/p/695136c5647b 

TODO！

+ sigmoid 

$ sigmoid(z) = \frac{1}{1+e^{-z}} $

如果只是线性函数的叠加， 

+ 正则化

防止过拟合，往一个方向上收缩，L1正则化，L2正则化

reference: https://blog.csdn.net/red_stone1/article/details/80755144

+ 数据白化

  reference: https://www.zhihu.com/question/49385441/answer/115737855?utm_source=qq&utm_medium=social&utm_oi=761286192158244864

  reference: [http://ufldl.stanford.edu/wiki/index.php/%E7%99%BD%E5%8C%96#.E4.B8.AD.E6.96.87.E8.AF.91.E8.80.85](http://ufldl.stanford.edu/wiki/index.php/白化#.E4.B8.AD.E6.96.87.E8.AF.91.E8.80.85)

  在PCA之前规范数据的操作，目标使特征之间的相关性较低，使所有特征具有相同的方差。

  用于处理图像，剔除冗余信息。

  1）使数据均值为0，2）构造协方差矩阵（条件1），3）除以$$\sqrt{\lambda_i}$$ （条件2），4）如果特征值接近0，除了会导致数据上溢，适当正则化除以$$\sqrt{\lambda_i + e}$$

+ 规范化

  $h_i = f(a_i)$

  $ h^{'}_i = f( \frac{u}{v}(a_i-u_i)+b_i) $

  用均值和方差进行分布调整，使激活值落入梯度敏感区间，训练速度加快；每一次数据调整为相同分布，消除极端值，提升训练稳定性

+ WT只能在同一个词表下做，如果encoder和decoder共享词表，那么encoder的输入，decoder的输入和输出，设成一致；否则只能在decoder的输入和输出做。如果输入和输出维度不同，那么这两个矩阵的语义肯定不强相关，做不了WT

+ 负采样

  reference: [https://baike.baidu.com/item/%E8%B4%9F%E9%87%87%E6%A0%B7/22884020?fr=aladdin](https://baike.baidu.com/item/负采样/22884020?fr=aladdin)

  正样本，生成上下文无关的词，负样本，类似于随机从词表中选词

  使用负采样，把正例和负例进行二分类。训练前向

  训练词向量模型的目标不是为了得到一个多么精准的语言模型，而是为了获得它的副产物——词向量。

+ BERT

  Bidirectional Encoder Representation from Transformers

  把下游具体NLP任务的活逐渐移到预训练产生词向量上

  结果：上下文无关的static向量变成上下文相关的dynamic向量，比如苹果在不同语境vector不同。

  操作：encoder操作转移到预训练产生词向量过程实现。

  **训练出的word-level向量变成sentence-level的向量**

  reference: https://www.cnblogs.com/rucwxb/p/10277217.html

+ markdown 公式

https://blog.csdn.net/lihaoweicsdn/article/details/83895143

+ i am vegitable
