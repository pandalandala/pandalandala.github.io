---
title: Deep Learning Specialization | Course 2 - Improving Deep Neural Networks - Hyperparameter Tuning, regularization and Optimization
date: 2021-07-24 20:19:04
description: Deep Learning Specialization Course 2/5 by Deeplearning.AI on Coursera<br>Improving Deep Neural Networks - Hyperparameter Tuning, regularization and Optimization
tags: DeepLearning
categories: DeepLearning
cover: https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/img/202206052021019.png
password: 
---
{% note info flat %}
文章可能有不完善之处，详见[这里](https://pandalandala.github.io/2022/06/06/TO-DO-LIST/)；如在阅读过程中遇到其他问题或 bug，或对 blog 有更多的意见或建议，欢迎[在这里提issue](https://github.com/pandalandala/pandalandala.github.io/issues)或点击下方链接发送邮件！[![Mail](https://img.shields.io/badge/Email-zxrshawn@icloud.com-blue?style=flat&logo=mail.ru)](mailto:zxrshawn@icloud.com)
{% endnote %}

{% note warning flat %}文章图片设置为 lazyload（延迟加载）；如遇图片加载失败请尝试刷新当前网页或科学上网。
{% endnote %}

# C2-1 深度学习的实用层面(Practical aspects of Deep Learning)

## 1.1 训练/开发/测试集（Train / Dev / Test Sets）

对于一个需要解决的问题的样本数据，在建立模型的过程中，我们会将问题的 data 划分为以下几个部分：

+ **训练集（train set）**：用训练集对算法或模型进行训练过程；

+ **验证集（development set）**：利用验证集或者又称为简单交叉验证集（hold-out cross validation set）进行交叉验证，选择出最好的模型；

+ **测试集（test set）**：最后利用测试集对模型进行测试，获取模型运行的无偏估计。

##### 小数据时代

在小数据量的时代，如：100、1000、10000 的数据量大小，可以将 data 做以下划分：

+ 无验证集的情况：70% / 30%；
+ 有验证集的情况：60% / 20% / 20%；

通常在小数据量时代，以上比例的划分是非常合理的。

##### 大数据时代

但是在如今的大数据时代，对于一个问题，我们拥有的 data 的数量可能是百万级别的，所以验证集和测试集所占的比重会趋向于变得更小。验证集的目的是为了验证不同的算法哪种更加有效，所以验证集只要足够大能够验证大约 2-10 种算法哪种更好就足够了，不需要使用 20%的数据作为验证集。如百万数据中抽取 1 万的数据作为验证集就可以了。测试集的主要目的是评估模型的效果，如在单个分类器中，往往在百万级别的数据中，我们选择其中 1000 条数据足以评估单个模型的效果。

+ 100 万数据量：98% / 1% / 1%；
+ 超百万数据量：99.5% / 0.25% / 0.25%（或者 99.5% / 0.4% / 0.1%）

##### 注：

+ 建议验证集要和训练集来自于同一个分布，可以使得机器学习算法变得更快；
+ 如果不需要用无偏估计来评估模型的性能，则可以不需要测试集。

## 1.2 偏差，方差（Bias /Variance）

假设这就是数据集，如果给这个数据集拟合一条直线，可能得到一个逻辑回归拟合，但它并不能很好地拟合该数据，这是**高偏差（high bias）**的情况，我们称为**欠拟合（underfitting）**。

相反的如果我们拟合一个非常复杂的分类器，比如深度神经网络或含有隐藏单元的神经网络，可能就非常适用于这个数据集，但是这看起来也不是一种很好的拟合方式。这时分类器为**高方差（high variance）**，数据**过度拟合（overfitting）**。

在两者之间，可能还有一些像图中这样的，复杂程度适中，数据拟合适度的分类器，这个数据拟合看起来更加合理，我们称之为**适度拟合（just right）**，是介于过度拟合和欠拟合中间的一类。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052121482.png" alt="image-20220605212145397" style="zoom: 80%;" />

---

下面给出几种拟合示例。我们沿用猫咪图片分类这个例子，左边一张是猫咪图片，右边一张不是。理解偏差和方差的两个关键数据是**训练集误差（Train set error）**和**验证集误差（Dev set error）**，为了方便论证，假设我们可以辨别图片中的小猫，我们用肉眼识别几乎是不会出错的。通过查看训练集误差和验证集误差，我们便可以诊断算法是否具有高方差。也就是说衡量训练集和验证集误差就可以得出不同结论。所有的示例图如下。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052123084.png" alt="image-20220605212316013" style="zoom:80%;" />

+ **低偏差、高方差：**假定训练集误差是 1%，为了方便论证，假定验证集误差是 11%，可以看出训练集设置得非常好，而验证集设置相对较差，我们可能过度拟合了训练集，在某种程度上，验证集并没有充分利用交叉验证集的作用，像这种情况，我们称之为“高方差”。

+ **高偏差、低方差：**假设训练集误差是 15%，我们把训练集误差写在首行，验证集误差是 16%，假设该案例中人的错误率几乎为 0%，人们浏览这些图片，分辨出是不是猫。算法并没有在训练集中得到很好训练，如果训练数据的拟合度不高，就是数据欠拟合，就可以说这种算法偏差比较高。相反，它对于验证集产生的结果却是合理的，验证集中的错误率只比训练集的多了 1%，所以这种算法偏差高，因为它甚至不能拟合训练集。

+ **高偏差、高方差：**假设训练集误差是 15%，偏差相当高，但是，验证集的评估结果更糟糕，错误率达到 30%，在这种情况下，我会认为这种算法偏差高，因为它在训练集上结果不理想，而且方差也很高，这是方差偏差都很糟糕的情况。

+ **低偏差、低方差：**最后，训练集误差是 0.5%，验证集误差是 1%，用户看到这样的结果会很开心，猫咪分类器只有 1%的错误率，偏差和方差都很低。

这些分析都是基于假设预测的，假设人眼辨别的错误率接近 0%，一般来说，**最优误差也被称为贝叶斯误差**，所以，最优误差接近 0%。如果最优误差或贝叶斯误差非常高，比如 15%，那么 15%的错误率对训练集来说也是非常合理的，偏差不高，方差也非常低。

---

最后，我们补充性地给出偏差和方差都很高的数据集示例：它会过度拟合部分数据，用紫色线画出的分类器具有高偏差和高方差，偏差高是因为它几乎是一条线性分类器，并未拟合数据，而采用曲线函数或二次元函数会产生高方差，因为它曲线灵活性太高以致拟合了这两个错误样本和中间这些活跃数据。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052123236.png" alt="image-20220605212333199" style="zoom:80%;" />

## 1.3 机器学习基础（Basic Recipe for Machine Learning）

在训练机器学习模型的过程中，可能需要解决高偏差或高方差的情况：

+ 是否存在**High bias** ?
  + 增加网络结构，如增加隐藏层数目；
  + 训练更长时间；
  + 寻找合适的网络架构，使用更大的 NN 结构；

+ 是否存在**High variance**？
  + 获取更多的数据；
  + 正则化（ regularization）；
  + 寻找合适的网络结构；

在大数据时代，深度学习对监督式学习大有裨益，使得我们不用像以前一样太过关注如何平衡偏差和方差的权衡问题。通过以上方法可以使得在不增加另一方的情况下减少一方的值。下面我们将讲解正则化，训练一个更大的网络几乎没有任何负面影响，而训练一个大型神经网络的主要代价也只是计算时间，前提是网络是比较规范化的。

## 1.4 正则化（Regularization）

利用正则化来解决 High variance 的问题，**正则化是在损失函数中加入一项正则化项**。

##### 逻辑回归

加入正则化项的代价函数：
$$
J(w,b)=\dfrac{1}{m}\sum ^{m}_{i=1}l(\widehat{y}^{(i)},y^{(i)})+\dfrac{\lambda}{2m}||w||_2^2
$$
上式为逻辑回归的**L2正则化**。

+ **L2正则化：**$\dfrac{\lambda}{2m}||w||_2^2=\dfrac{\lambda}{2m} \sum ^{n_x}_{j=1} w_j^2=\dfrac{\lambda}{2m}w^Tw$
+ **L1正则化：**$\dfrac{\lambda}{2m}||w||_1=\dfrac{\lambda}{2m} \sum ^{n_x}_{j=1} |w_j|$

其中$\lambda$为正则化因子。

**注意**：`lambda`在 python 中属于保留字，所以在编程的时候，用`lambd`代表这里的正则化因子$\lambda$。

##### 神经网络中的正则化代价函数

在神经网络中，加入正则化项的代价函数为：
$$
J(w^{[1]},b^{[1]},...,w^{[L]},b^{[L]})=\dfrac{1}{m}\sum ^{m}_{i=1}l(\widehat{y}^{(i)},y^{(i)})+\dfrac{\lambda}{2m}\sum ^{L}_{l=1}||w^{[l]}||_F^2
$$
其中$||w^{[l]}||_F^2=\sum ^{n^{[l-1]}}_{i=1}\sum ^{n^{[l]}}_{j=1}(w_{ij}^{[l]})^2$，因为$w$的大小为$(n^{[l-1]},n^{[l]})$，该矩阵范数被称为**robenius范数**。

##### 权重衰减

在加入正则化项后，梯度变为：
$$
dW^{[l]}=(form\_backprop)+\dfrac{\lambda}{m}W^{[l]}
$$
用 backprop 计算出$dW$的值，backprop 会给出$J$对$W$的偏导数，实际上是$W^{[l]}$，把$W^{[l]}$替换为$W^{[l]}$减去学习率乘以$dW$。则梯度更新公式变为：
$$
W^{[l]}:=W^{[l]}-\alpha dW^{[l]}
$$
代入可得：
$$
W^{[l]}:=W^{[l]}-\alpha [(form\_backprop)+\dfrac{\lambda}{m}W^{[l]}]\\
=W^{[l]}-\alpha (form\_backprop)-\alpha\dfrac{\lambda}{m}W^{[l]}\\
=(1-\dfrac{\alpha\lambda}{m})W^{[l]}-\alpha (form\_backprop)
$$
其中$(1-\dfrac{\alpha\lambda}{m})$为一个小于 1 的项，会给原来的$W^{[l]}$一个衰减的参数，所以 L2 范数正则化也被称为**权重衰减（Weight decay）**。

## 1.5 为什么正则化可以减少过拟合呢？（Why regularization reduces overfitting?）

假设下图的神经网络结构属于过拟合状态：

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052124907.png" alt="image-20220605212402840" style="zoom:80%;" />

对于神经网络的损失函数，加入正则化项，直观上理解，正则化因子$\lambda$设置的足够大的情况下，为了使代价函数最小化，权重矩阵$W$就会被设置为接近于 0 的值。则相当于消除了很多神经元的影响，那么图中的大的神经网络就会变成一个较小的网络。当然上面这种解释是一种直观上的理解，但是实际上隐藏层的神经元依然存在，但是他们的影响变小了，便不会导致过拟合。
$$
J(w^{[1]},b^{[1]},...,w^{[L]},b^{[L]})=\dfrac{1}{m}\sum ^{m}_{i=1}l(\widehat{y}^{(i)},y^{(i)})+\dfrac{\lambda}{2m}\sum ^{L}_{l=1}||w^{[l]}||_F^2
$$
下面给出数学解释。假设神经元中使用的激活函数为$g(z)=tanh(z)$，在加入正则化项后：当$\lambda$增大，导致$W^{[l]}$减小，$Z^{[l]}=W^{[l]}a^{[l-1]}+b^{[l]}$便会减小，由上图可知，在$z$较小的区域里，$tanh(z)$函数近似线性，所以每层的函数就近似线性函数，整个网络就成为一个简单的近似线性的网络，从而不会发生过拟合。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052124094.png" alt="image-20220605212420055" style="zoom:80%;" />

## 1.6 Dropout 正则化（Dropout Regularization）

**Dropout（随机失活）**就是在神经网络的 Dropout 层，为每个神经元结点设置一个随机消除的概率，对于保留下来的神经元，我们得到一个节点较少，规模较小的网络进行训练。如下图所示。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052124550.png" alt="image-20220605212455491" style="zoom:80%;" />

实现 Dropout 的方法为**反向随机失活（Inverted dropout）**。

首先要定义向量 d，$d^{[3]}$表示一个三层的**dropout**向量：`d3 = np.random.rand(a3.shape[0],a3.shape[1])`

首先假设对 layer 3 进行 dropout：

```python
keep_prob = 0.8  # 设置神经元保留概率
d3 = np.random.rand(a3.shape[0], a3.shape[1]) < keep_prob
a3 = np.multiply(a3, d3)
a3 /= keep_prob
```

其中需要`a3 /= keep_prob`是因为依照例子中的 keep_prob = 0.8 ，那么就有大约 20%的神经元被删除了，也就是说$a^{[3]}$中有 20%的元素被归零了，在下一层的计算中有$Z^{[4]}=W^{[4]}\cdot a^{[3]}+b^{[4]}$，所以为了不影响的$Z^{[4]}$期望值，所以需要$W^{[4]}\cdot a^{[3]}$的部分除以一个 keep_prob。Inverted dropout 通过`a3 /= keep_prob`，则保证无论 keep_prob 设置为多少，都不会对$Z^{[4]}$期望值产生影响。

**注：在测试阶段不要用dropout，因为那样会使得预测结果变得随机。**

## 1.7 理解 Dropout（Understanding Dropout）

这里我们以单个神经元入手，单个神经元的工作就是接收输入，并产生一些有意义的输出，但是加入了 Dropout 以后，输入的特征都是有可能会被随机清除的，所以该神经元不会再特别依赖于任何一个输入特征，也就是说不会给任何一个输入设置太大的权重。所以通过传播过程，dropout 将产生和 L2 范数相同的收缩权重的效果。通过传播所有权重，dropout 将产生收缩权重的平方范数的效果，和之前讲的正则化类似；实施 dropout 的结果是它会压缩权重，并完成一些预防过拟合的外层正则化；对不同权重的衰减是不同的，它取决于激活函数倍增的大小。对于不同的层，设置的 keep_prob 也不同，一般来说神经元较少的层，会设 keep_prob=1.0，神经元多的层，则会将 keep_prob 设置的较小。

**缺点**：dropout 的一大缺点就是其使得 Cost function 不能再被明确的定义，以为每次迭代都会随机消除一些神经元结点，所以我们无法绘制出每次迭代$J(W,b)$下降的图。

**使用Dropout：**	关闭 dropout 功能，即设置 keep_prob = 1.0；运行代码，确保$J(W,b)$函数单调递减；再打开 dropout 函数。

## 1.8 其他正则化方法（Other regularization methods）

## 1.9 正则化输入（Normalizing inputs）

## 1.10 梯度消失与梯度爆炸（Vanishing / Exploding gradients）

## 1.11 神经网络的权重初始化（Weight Initialization for Deep NetworksVanishing /Exploding gradients）

## 1.12 梯度的数值逼近（Numerical approximation of gradients）

## 1.13 梯度检验（Gradient checking）

## 1.14 关于梯度检验实现的注记（Gradient Checking Implementation Notes）

# C2-2 优化算法 (Optimization algorithms)

## 2.1 Mini-batch 梯度下降（Mini-batch gradient descent）

## 2.2 理解Mini-batch 梯度下降（Understanding Mini-batch gradient descent）

## 2.3 指数加权平均（Exponentially weighted averages）

## 2.4 理解指数加权平均（Understanding Exponentially weighted averages）

## 2.5 指数加权平均的偏差修正（Bias correction in exponentially weighted averages）

## 2.6 momentum梯度下降（Gradient descent with momentum）

## 2.7 RMSprop——root mean square prop（RMSprop）

## 2.8 Adam优化算法（Adam optimization algorithm）

## 2.9 学习率衰减（Learning rate decay）

## 2.10 局部最优问题（The problem of local optima）

# C2-3 超参数调试，batch正则化和程序框架（Hyperparameter tuning, Batch Normalization and Programming Frameworks)

## 3.1 调试处理（Tuning process）

## 3.2 为超参数选择和适合范围（Using an appropriate scale to pick hyperparameters）

## 3.3 超参数训练的实践：Pandas VS Caviar（Hyperparameters tuning in practice: Pandas VS Caviar）

## 3.4 正则化网络的激活函数（Normalizing activations in a network）

## 3.5 将 Batch Norm拟合进神经网络（Fitting Batch Norm into a neural network）

## 3.6 Batch Norm为什么奏效？（Why does Batch Norm work?）

## 3.7 测试时的Batch Norm（Batch Norm at test time）

## 3.8 Softmax 回归（Softmax Regression）

## 3.9 训练一个Softmax分类器（Training a softmax classifier）

## 3.10 深度学习框架（Deep learning frameworks）

## 3.11 TensorFlow（TensorFlow）

