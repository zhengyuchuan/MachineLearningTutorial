1.逻辑回归用来解决二分类问题。



与感知机设置阈值来预测分类的方式不同，逻辑回归使用输出一个概率值来预测分类结果。

将线性回归的结果代入一函数，来获取概率，函数为sigmoid函数。
$$
sigmoid(x) = \frac{1}{1+e^{-x}}
$$
函数图像：



![sigmoid](image/sigmoid.png)



损失函数推导过程：

样本的标签值：
$$
y \in(0, 1)
$$
假设样本i属于正样本（y=1）的概率为：P，那么当样本属于负样本（y=-1）的概率就是1-P。表达式：
$$
P(y|x)=\begin{cases}P,&y=1 \\ 1-P,&y=0 \end{cases}
$$
整理为一个表达式：
$$
P(y|x) = P^y(1-P)^{1-y}
$$
那么当m个样本时，发生的概率为：
$$
\begin{align}
P(Y|X) &= \prod^m_{i=1}P^{yi}(1-P)^{1-yi} 
\\ 其中：P &= \frac{1}{1+e^{-oi}}
\\ oi &= W X_i + b
\end{align}
$$
根据极大似然估计，最大化这个概率值。连乘不好计算(概率值是个很小的数，连乘可能导致计算机计算的结果为0)，这里求**对数**，因为求对数不改变单调性，改为对数后再让这个对数值最大化，相当于求负对数值的最小值：
$$
logP(Y|X) = \sum^m_{i=1}(y_ilogP+ (1-y_i)log(1-P))
$$

$$
L=-logP(Y|X) = \sum^m_{i=1}(-y_ilogP - (1-y_i)log(1-P))
$$

根据极大似然估计推导出的损失函数也是交叉熵损失函数

损失函数分别对$\omega$和$b$求导：
$$
\begin{align}
\frac{\partial{L}}{\partial{W}} &= \frac{\partial{L}}{\partial{P}}\frac{\partial{P}}{\partial{O}}\frac{\partial{O}}{\partial{W}}
\\ &= (\sum^m_{i=1}(\frac{y_i}{P} + \frac{y_i - 1}{1-P}))  * P(1-P) * X
\\ &= \sum^m_{i=1}(y_i - P)X
\\ 其中X代表单个样本的特征向量，P代表sigmoid函数
\\ P &= \frac{1}{1+e^{-( W X_i + b)}}
\end{align}
$$




---





softmax回归用来解决多分类问题。是逻辑回归的一般形式。

![](/Users/admin/Documents/MachineLearningTutorial/MLNotes/image/softmaxreg.svg)

为了支持多分类问题，需要将输出转换为概率，使其总和为1。可以使用softmax函数：
$$
\hat{y_i} = \frac{exp(o_i)}{\sum_k{exp(o_k)}}
$$
其中$o_i$代表输出层第i个元素，输出层一共k个元素。最大的$\hat{y_i}$代表预测值。



假设输出层有n个输出神经元:
$$
P = \prod_{i=1}^{n}p_i^{y_i}
$$




softmax的整体表达式为：
$$
O = XW + B \\
\hat{Y} = softmax(O)
$$


softmax回归的损失函数，使用极大似然估计推导出：

概率和似然的关系：概率用于已知一些参数的情况下，预测接下来观测上所得到的结果；似然是已知某些观测所得到的结果时，对有关事物的性质参数进行估值。似然函数可以理解为条件概率的逆反。



似然函数：
$$
\begin{align}
P(Y|X) &= \prod_{i=1}^{m}P(y_i|x_i)
\\ &= \prod_{i=1}^{m}\prod_{j=1}^{n}p(y_{ij}|x_{ij})
\end{align}
$$
根据极大似然估计，最大化这个似然函数，相当于最小化负对数。求对数连乘会变成连加：
$$
\begin{align}
L &= -log(P(Y|X))
\\ &= -\sum_{i=1}^{m}\sum_{j=1}^{n}logp
\\ &= -\sum_{i=1}^{m}\sum_{j=1}^{n}y_jlog(\frac{e^{oj}}{\sum_{k=1}^{n}e^{ok}})
\\ &= \sum_{i=1}^{m}\sum_{j=1}^{n}y_j(log\sum_{k=1}^{n}e^{ok} - o_j)
\\ &= \sum_{i=1}^{m}(log\sum_{k=1}^{n}e^{ok} - \sum_{j=1}^{n}y_io_i)
\\ 其中o_j代表第j个输出层神经元
\\ O = WX + B
\end{align}
$$


损失函数对$o_j$求导（$o_j$是标量，O是向量，标量对向量求导还是向量。对W求导较复杂，W是二维矩阵.）（二层累加中，除了$o_j$都视为常量，求导直接变为0了，所以只剩一层累加了）:
$$
\begin{align}
\frac{\partial{L}}{\partial{o_j}} &= \sum_{i=1}^{m}(\frac{e^{oi}}{\sum_{k=1}^{n}e^{ok}} - y_i)
\\ &= \sum_{i=1}^{m}(softmax(o_i) - y_i)
\end{align}
$$




































