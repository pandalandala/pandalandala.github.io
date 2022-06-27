---
title: Deep Learning Specialization | Course 1 - Neural Networks and Deep Learning
date: 2021-07-11 20:19:04
description: Deep Learning Specialization Course 1/5 by Deeplearning.AI on Coursera<br>Neural Networks and Deep Learning
tags: DeepLearning
categories: DeepLearning
cover: https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/img/202206052009945.png
password: 
---
{% note info flat %}
文章可能有不完善之处，详见[这里](https://pandalandala.github.io/2022/06/06/TO-DO-LIST/)；如在阅读过程中遇到其他问题或 bug，或对 blog 有更多的意见或建议，欢迎[在这里提issue](https://github.com/pandalandala/pandalandala.github.io/issues)或点击下方链接发送邮件！[![Mail](https://img.shields.io/badge/Email-zxrshawn@icloud.com-blue?style=flat&logo=mail.ru)](mailto:zxrshawn@icloud.com)
{% endnote %}

{% note warning flat %}文章图片设置为 lazyload（延迟加载）；如遇图片加载失败请尝试刷新当前网页或科学上网。
{% endnote %}

# C1-1 深度学习概论(Introduction to Deep Learning)

## 1.1 欢迎来到深度学习工程师微专业(Welcome)

## 1.2 什么是神经网络?(What is a Neural Network)

这是一种强大的学习算法，灵感来自大脑的工作方式。

+ 例 1：单神经网络给定房地产市场上房屋大小的数据，你想要拟合一个函数来预测它们的价格。这是一个线性回归问题，因为价格作为规模的函数是一个连续的产出。我们知道价格不可能是负的，所以我们创建了一个从 0 开始的**“修正线性单元”函数（ReLU function）**。

  <img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052048410.png" alt="image-20220605204809353" style="zoom:80%;" />

  <img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052100123.png" alt="image-20220605210018069" style="zoom:80%;" />

  输入为房子的大小 x，输出为价格 y，“神经元”实现了 ReLU 函数（蓝线）。

+ 例 2：多重神经网络。房子的价格还会受到其他因素的影响，比如面积、卧室数量、邮编和财富。神经网络的作用是预测价格，并自动生成隐藏的单位。我们只需要给出输入 x 和输出 y 来进行监督学习。值得注意的是神经网络给予了足够多的关于 x 和 y 的数据，给予了足够的训练样本。神经网络非常擅长计算从 x 到 y 的精准映射函数。

  <img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052100338.png" alt="image-20220605210049275" style="zoom:80%;" />

##     1.3 神经网络的监督学习(Supervised Learning with Neural Networks)

也许对于房地产和在线广告来说可能是相对的标准一些的神经网络，正如我们之前见到的。对于图像应用，我们经常在神经网络上使用**卷积（Convolutional Neural Network）**，通常缩写为**CNN**。对于序列数据，例如音频，有一个时间组件，随着时间的推移，音频被播放出来，作为**一维时间序列（one-dimensional time series / temporal sequence）**，所以音频是最自然的表现。对于序列数据，经常使用**RNN**，一种**递归神经网络（Recurrent Neural Network**），语言、英语和汉语字母表或单词都是逐个出现的，所以语言也是最自然的序列数据，因此更复杂的 RNN 版本经常用于这些应用。

对于更复杂的应用比如自动驾驶，给出一张图片，可能会显示更多的 CNN 卷积神经网络结构，其中的雷达信息是完全不同的，可能会有一些更复杂的混合的神经网络结构。

从历史经验上看，处理非结构化数据是很难的，与结构化数据比较，让计算机理解非结构化数据很难，而人类进化得非常善于理解音频信号和图像，文本是一个更近代的发明，但是人们真的很擅长解读非结构化数据。

多亏深度学习和神经网络，计算机现在能更好地解释非结构化数据，这为我们创造了机会。许多新的应用被使用，例如语音识别、图像识别、自然语言文字处理。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052101334.png" alt="image-20220605210112265" style="zoom: 67%;" />

##    1.4 为什么深度学习会兴起？(Why is Deep Learning taking off?)   

由于社会的数字化、更快的计算速度和神经网络算法发展中的创新，深度学习正在兴起。要使神经网络达到高水平的表现，必须考虑两件事:能够训练一个足够大的神经网络，以及大量的标签数据。神经网络的训练过程是迭代的。事实上如今最可靠的方法来在神经网络上获得更好的性能，往往就是**要么训练一个更大的神经网络，要么投入更多的数据**。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052101164.png" alt="image-20220605210139105" style="zoom:80%;" />

训练神经网络可能需要很长时间，这会影响你的工作效率。更快的计算速度有助于迭代和改进新算法。通过将**Sigmod**函数转换成 ReLU 函数，便能够使得一个叫做梯度下降（gradient descent）的算法运行的更快，这就是一个相对比较简单的算法创新的例子。

## 1.5 关于这门课(About this Course)

##    1.6 课程资源(Course Resources)

Contact us: [feedback@deeplearning.ai](mailto:feedback@deeplearning.ai)

Companies: [enterprise@deeplearning.ai](mailto:enterprise@deeplearning.ai)

Universities: [academic@deeplearning.ai](mailto:academic@deeplearning.ai)

# C1-2 神经网络基础(Basics of Neural Network programming)

## 2.1 二分类(Binary Classification)

在二元分类问题中，结果是一个离散值的输出。例如：Cat vs Non-Cat 训练的目标是训练一个分类器，使其输入是一幅由特征向量 x 表示的图像，并预测对应的标签 y 是 1(Cat)还是 0(Non-Cat)。图像以三个独立的矩阵存储在计算机中，分别对应于图像的红、绿、蓝颜色通道。这三个矩阵的大小与图像相同，例如，猫图像的分辨率是 64 × 64 像素，三个矩阵(RGB)都是 64 × 64。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052101873.png" alt="image-20220605210156806" style="zoom:80%;" />

$x$：表示一个维数据，为输入数据，维度为$(n_x,1)$； 

$y$：表示输出结果，取值为$(0,1)$；

$(x^{(i)},y^{(i)})$：表示第$i$组数据，可能是训练数据，也可能是测试数据，此处默认为训练数据；

$X=[x^{(1)},x^{(2)},...,x^{(m)}]$：表示所有的训练数据集的输入值，放在一个$n_x*m$的矩阵中，其中$m$表示样本数目; 

$Y=[y^{(1)},y^{(2)},...,y^{(m)}]$：对应表示所有训练数据集的输出值，维度为$1*m$。

用一对$(x,y)$来表示一个单独的样本，$x$代表$n_x$维的特征向量，$y$表示标签(输出结果)只能为 0 或 1。 而训练集由$m$个训练样本组成。有时候为了强调这是训练样本的个数，会写作$M_{train}$，当涉及到测试集的时候，我们会使用$M_{test}$来表示测试集的样本数。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052102423.png" alt="image-20220605210210365" style="zoom: 67%;" />

## 2.2 逻辑回归(Logistic Regression)

Logistic 回归是一种用于监督学习问题的学习算法，输出$y$全部为 0 或 1。**logistic回归的目标是最小化其预测和训练数据之间的误差。**

对于二元分类问题来讲，给定一个输入特征向量$X\in \mathbb{R} ^{n_x}$，$X$对应一张图片，你想识别这张图片看它是否是一只猫的图片，这时一个算法能够输出预测$\widehat{y}$，也就是对实际值$y$的估计。我们用$w$ (weights)来表示逻辑回归的参数，这也是一个$n_x$维向量（因为实际上是特征权重，维度与特征向量相同），参数里面还有$b$ (threshold)，这是一个实数（表示偏差）。所以给出输入$x$以及参数$w$和$b$之后，我们要产生输出预测值$\widehat{y}$。首先尝试$\widehat{y}=w^Tx+b$。这是一个线性函数，不适合用在二元分类问题上。因为想让$\widehat{y}$表示实际值$y$等于 1 的机率的话，$\widehat{y}$应该在 0 到 1 之间。因此在逻辑回归中，我们的输出应该是由上面得到的线性函数式子作为自变量的 sigmoid 函数中，公式为$\widehat{y}=\sigma(w^Tx+b)$，将线性函数转换为非线性函数。**sigmoid函数**的公式为$\sigma \left( z\right) =\dfrac{1}{1+e^{-z}}$，图像如下。因此当实现逻辑回归时，你的工作就是去让机器学习参数$w$以及$b$这样才使得$\widehat{y}$成为对$y=1$这一情况的概率的一个很好的估计。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052102522.png" alt="image-20220605210231452" style="zoom:80%;" />

## 2.3 逻辑回归的损失函数（Logistic Regression Cost Function）

我们通过**损失函数$L(\widehat{y},y)$**衡量预测输出值和实际值有多接近。一般我们用预测值和实际值的平方差或者它们平方差的一半，但是通常在逻辑回归中我们不这么做，因为当我们在学习逻辑回归参数的时候，会发现我们的优化目标不是凸优化，只能找到多个局部最优值，梯度下降法很可能找不到全局最优值，虽然平方差是一个不错的损失函数，但是我们在逻辑回归模型中会定义另外一个损失函数，其函数表达式和原理如下图所示。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206061144786.png" alt="image-20220606114443693" style="zoom:80%;" />

损失函数是在单个训练样本中定义的，它衡量的是算法在单个训练样本中表现如何，为了衡量算法在全部训练样本上的表现如何，我们需要定义一个**算法的损失函数**，算法的损失函数是对$m$个样本的损失函数求和然后除以$m$，如下图所示。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206061144900.png" alt="image-20220606114459837" style="zoom:80%;" />

损失函数只适用于像这样的单个训练样本，而代价函数是参数的总损失，所以在训练逻辑回归模型时候，我们需要找到合适的 $w$ 和$b$，来让代价函数$J$的总损失降到最低。

## 2.4 梯度下降（Gradient Descent）

+ **初始化**：在梯度下降法中，可以用如图那个小红点来初始化参数$w$和$b$，也可以采用随机初始化的方法，对于逻辑回归几乎所有的初始化方法都有效，因为函数是凸函数，无论在哪里初始化，应该达到同一点或大致相同的点。

+ **朝最陡的下坡方向走一步，不断地迭代**

+ **直到走到全局最优解或者接近全局最优解的地方**

  下面将详细说明如何迭代。$:=$表示更新参数。 $a$表示学习率（learning rate），用来控制步长（step），即向下走一步的长度$\dfrac{dJ\left( w\right) }{dw}$就是函数$J(w)$对$w$求导，在代码中我们会使用$dw$表示这个结果。整个梯度下降法的迭代过程就是不断地向下走，直至逼近最小值点。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052102908.png" alt="image-20220605210253846" style="zoom:80%;" />

另外，每次迭代更新的修正表达式如下。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206061145152.png" alt="image-20220606114530098" style="zoom:80%;" />

## 2.5 导数（Derivatives）（略）

## 2.6 更多的导数例子（More Derivative Examples）（略）

## 2.7 计算图（Computation Graph）

## 2.8 计算图导数（Derivatives with a Computation Graph）

仅给出如下的计算图及其导数。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052103551.png" alt="image-20220605210310493" style="zoom: 80%;" />

## 2.9 逻辑回归的梯度下降（Logistic Regression Gradient Descent）

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206061146669.png" alt="image-20220606114614593" style="zoom: 67%;" />

## 2.10 m个样本的梯度下降(Gradient Descent on m Examples)

对$m$个样本来说，其损失函数表达式如下：

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206061146279.png" alt="image-20220606114643207" style="zoom: 67%;" />

损失函数关于$w$和$b$的偏导数可以写成所有样本点偏导数和的平均形式：

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206061146596.png" alt="image-20220606114656538" style="zoom:67%;" />

代码实现：

```python
J=0;dw1=0;dw2=0;db=0;
for i = 1 to m
    z(i) = wx(i)+b;
    a(i) = sigmoid(z(i));
    J += -[y(i)log(a(i))+(1-y(i)）log(1-a(i));
    dz(i) = a(i)-y(i);
    dw1 += x1(i)dz(i);
    dw2 += x2(i)dz(i);
    db += dz(i);
J/= m;
dw1/= m;
dw2/= m;
db/= m;
w=w-alpha*dw
b=b-alpha*db
```

## 2.11 向量化(Vectorization)

向量化计算$w^Tx$将会非常快。以下是代码实现：

```python
import numpy as np #导入numpy库
a = np.array([1,2,3,4]) #创建一个数据a
print(a)
# [1 2 3 4]
import time #导入时间库
a = np.random.rand(1000000)
b = np.random.rand(1000000) #通过round随机得到两个一百万维度的数组
tic = time.time() #现在测量一下当前时间
#向量化的版本
c = np.dot(a,b)
toc = time.time()
print("Vectorized version:" + str(1000*(toc-tic)) +"ms") #打印一下向量化的版本的时间

#继续增加非向量化的版本
c = 0
tic = time.time()
for i in range(1000000):
    c += a[i]*b[i]
toc = time.time()
print(c)
print("For loop:" + str(1000*(toc-tic)) + "ms")#打印for循环的版本的时间
```

## 2.12 向量化的更多例子（More Examples of Vectorization）

我们将对 m 个样本的梯度下降进行向量化。向量化前的代码参照 2.10，向量化后的代码如下：

```python
J=0;dw=np.zeros((n_x,1));db=0;
for i = 1 to m
    z(i) = wx(i)+b;
    a(i) = sigmoid(z(i));
    J += -[y(i)log(a(i))+(1-y(i)）log(1-a(i));
    dz(i) = a(i)-y(i);
    dw += x(i)dz(i);
    db += dz(i);
J/= m;
dw/= m;
db/= m;
w=w-alpha*dw
b=b-alpha*db
```

## 2.13 向量化logistic回归(Vectorizing Logistic Regression)

在向量化前，对每一个样本我们都要进行如下 logistic 回归的前向传播步骤。
$$
z^{(1)}=w^Tx^{(1)}+b\\
z^{(2)}=w^Tx^{(2)}+b\\
z^{(3)}=w^Tx^{(3)}+b
$$

$$
a^{(1)}=\sigma (z^{(1)})\\
a^{(2)}=\sigma (z^{(2)})\\
a^{(3)}=\sigma (z^{(3)})
$$

现在我们希望在一个步骤中计算$z_1$、$z_2$、$z_3$等。因此我们**构建相应的矩阵**并计算$Z$，即$(z^{\left( 1\right)}z^{\left( 2\right)}...z^{\left( m\right)})=w^Tx+(bb...b)$，我们将上式记作$Z=W^TX+(bb...b)$，其 numpy 命令为`Z = np.dot(w.T,X) + b`。接下来通过恰当地运用$\sigma$一次性计算所有$a$，即$A=(a^{\left( 1\right)}a^{\left( 2\right)}...a^{\left( m\right)})=\sigma(z)$。这就是在同一时间内完成一个所有$m$个训练样本的前向传播向量化计算方法。

在 2.14 中将利用向量化高效地计算反向传播并以此来计算梯度。

## 2.14 向量化logistic回归的梯度计算（Vectorizing Logistic Regression's Gradient）

之前的梯度计算中我们一直利用$dz^{(i)}=a^{(i)}-y^{(i)}$，在向量化中，我们依旧**构建相应的矩阵**来计算$m$个训练数据的梯度：$dZ=A-Y=(a^{(1)}-y^{(1)}a^{(2)}-y^{(2)}...a^{(m)}-y^{(m)})$。所以我们仅需要一行代码，就能完成所有的计算。

至此，我们已经去掉了一个 for 循环。但我们仍有一个遍历训练集的循环用于计算$dw$和$db$，如下所示：

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052108980.png" alt="image-20220605210851915" style="zoom:80%;" />

对这个 for 循环我们也使用向量化手段。对于$db$，不难想到在 Python 中的代码为`db=(1/m)*np.sum(dZ)`；对于$dw$，考虑其计算公式可得`dw=(1/m)*X*dz.T`，这样就避免了在训练集上使用 for 循环。

因此**单次迭代**的**梯度下降算法**的代码如下：

```python
Z = np.dot(w.T,X) + b
A = sigmoid(Z)
dZ = A-Y
dw = 1/m*np.dot(X,dZ.T)
db = 1/m*np.sum(dZ)

w = w - alpha*dw
b = b - alpha*db
```

现在我们利用前五个公式完成了前向和后向传播，也实现了对所有训练样本进行预测和求导，再利用后两个公式，梯度下降更新参数。我们的目的是不使用 for 循环，所以我们就通过一次迭代实现一次梯度下降，但如果你<u>希望多次迭代进行梯度下降，那么仍然需要 for 循环，放在最外层</u>。

## 2.15 Python中的广播机制（Broadcasting in Python）

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052108509.png" alt="image-20220605210807432" style="zoom:67%;" />

先来学习上面的代码。解释两条指令：解释一下`A.sum(axis = 0)`中的参数`axis`。<u>axis 用来指明将要进行的运算是沿着哪个轴执行，在 numpy 中，0 轴是垂直的，也就是列，而 1 轴是水平的，也就是行</u>；而第二个`A/cal.reshape(1,4)`指令则调用了**numpy中的广播机制**。这里使用$3\times 4$的矩阵 A 除以$1\times 4$的矩阵$cal$。技术上来讲，其实并不需要再将矩阵 $cal$`reshape`(重塑)成$1\times 4$，因为矩阵$cal$本身已经是$1\times 4$了。但是当我们写代码时不确定矩阵维度的时候，通常会对矩阵进行重塑来确保得到我们想要的列向量或行向量。重塑操作`reshape`是一个常量时间的操作，时间复杂度是$O(1)$，它的调用代价极低。

**numpy广播机制：如果两个数组的后缘维度的轴长度相符或其中一方的轴长度为1，则认为它们是广播兼容的。广播会在缺失维度和轴长度为1的维度上进行**，示例如下图。（注：后缘维度的轴长度：`A.shape[-1]` 即矩阵维度元组中的最后一个位置的值）

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052109930.png" alt="image-20220605210907856" style="zoom:80%;" />

## 2.16 关于Python与numpy向量的使用（A note on python or numpy vectors）

虽然在 Python 有广播的机制，但是在 Python 程序中，为了保证矩阵运算的正确性，可以使用 reshape()函数来对矩阵设定所需要进行计算的维度，这是个好的习惯；

如果用`a = np.random.randn(5)`来定义一个向量，则这条语句生成的 a 的维度为 $(5, )$，既不是行向量也不是列向量，称为秩（rank）为 1 的 array，如果对 a 进行转置，则会得到 a 本身，这在计算中会给我们带来一些问题。

如果需要定义$(5,1)$或者$(1,5)$向量，要使用下面标准的语句：

```python3
a = np.random.randn(5,1)
b = np.random.randn(1,5)
```

可以使用**assert语句**对向量或数组的维度进行判断。assert 会对内嵌语句进行判断，即判断 a 的维度是不是$(5,1)$，如果不是，则程序在此处停止。使用 assert 语句也是一种很好的习惯，能够帮助我们及时检查、发现语句是否正确。

```python3
assert(a.shape == (5,1))
```

也可以使用**reshape函数**对数组设定所需的维度。

```python3
a.reshape((5,1))
```

## 2.17 Jupyter/iPython Notebooks快速入门（Quick tour of Jupyter/iPython Notebooks）

## 2.18 logistic回归损失函数详解（Explanation of logistic regression cost function）

在 logistic 回归中，我们约定如下式子：

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052109027.png" alt="image-20220605210933954" style="zoom:67%;" />

需要指出的是我们讨论的是二分类问题的损失函数，因此$y$的取值只能是 0 或者 1。上述的两个条件概率公式可以合并成如下公式：
$$
p(y|x)=\widehat{y}^y(1-\widehat{y})^{(1-y)}
$$
不难验证$(1)$式满足上述两个条件概率公式。因此$p(y|x)=\widehat{y}^y(1-\widehat{y})^{(1-y)}$就是$p(y|x)$的完整定义。由于对数函数是严格单调递增的函数，考虑最大化$log(p(y|x))$，即
$$
ylog\widehat{y}+(1-y)log(1-\widehat{y})
$$
而这就是前面提到的损失函数的负数$-L(\widehat{y},y)$。当训练学习算法时需要算法输出值的概率是最大的（以最大的概率预测这个值），因此实现了在 logistic 回归中将损失函数最小化。

下面考虑**在$m$个训练样本的整个训练集中如何表示logistic回归的损失函数**。假设所有的训练样本服从同一分布且相互独立，也即独立同分布的，所有这些样本的联合概率就是每个样本概率的乘积：

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206061147310.png" alt="image-20220606114744251" style="zoom:80%;" />

如果做最大似然估计，需要寻找一组参数，使得给定样本的观测值概率最大，但令这个概率最大化等价于令其对数最大化，在等式两边取对数：

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052109320.png" alt="image-20220605210952259" style="zoom:80%;" />

由于训练模型时，目标是让成本函数最小化，所以我们不是直接用最大似然概率，要去掉这里的负号，最后为了方便，可以对成本函数进行适当的缩放，我们就在前面加一个额外的常数因子$\dfrac{1}{m}$：

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206061147854.png" alt="image-20220606114751792" style="zoom:80%;" />

# C1-3 浅层神经网络(Shallow neural networks)

## 3.1 神经网络概述（Neural Network Overview）

如下图所示是一个 sigmoid 单元以及其损失函数表达式。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052110946.png" alt="image-20220605211027881" style="zoom:80%;" />

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052111666.png" alt="image-20220605211111604" style="zoom:80%;" />

**把许多sigmoid单元堆叠起来可以形成一个神经网络**，如下图所示。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052111778.png" alt="image-20220605211123710" style="zoom:80%;" />

它包含了之前计算的两个步骤：首先通过公式计算出值$z$，然后通过$\sigma(z)$计算值$a$。在这个神经网络第一层对应的 3 个节点，首先计算第一层网络中的各个节点相关的数$z^{[1]}$，接着计算$a^{[1]}$，再计算下一层网络；我们会使用符号$^{[m]}$表示第$m$层网络中节点相关的数，这些节点的集合被称为第$m$层网络。类似 logistic 回归，在计算后需要使用计算，接下来你需要使用另外一个线性方程对应的参数计算$z^{[2]}$，计算$a^{[2]}$，此时$a^{[2]}$就是整个神经网络最终的输出，也可用$\widehat{y}$表示神经网络的输出。整个计算过程如下：

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052112599.png" alt="image-20220605211212532" style="zoom: 80%;" />

接下来看反向传播的神经网络计算过程，仅给出示意图：

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052112975.png" alt="image-20220605211220914" style="zoom:80%;" />

## 3.2 神经网络的表示（Neural Network Representation）

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052112394.png" alt="image-20220605211237332" style="zoom:80%;" />

在如图所示的神经网络中，我们有输入特征$x_1$、$x_2$、$x_3$，它们被竖直地堆叠起来，这叫做神经网络的**输入层**；然后这里有另外一层我们称之为**隐藏层**（中间的的四个结点），这些中间结点的准确值我们是不知道到的，也就是说你看不见它们在训练集中应具有的值；在本例中最后一层只由一个结点构成，而这个只有一个结点的层被称为**输出层**，它负责产生预测值。上图所示的神经网络我们一般称为一个两层的神经网络，因为我们不将输入层看作一个标准的层。

之前用向量$x$表示输入特征。这里有个可代替的记号$a^{[0]}$可以用来表示输入特征。$a$表示激活的意思，它意味着网络中不同层的值会传递到它们后面的层中，输入层将$x$传递给隐藏层，所以我们将输入层的激活值称为$a^{[0]}$；下一层即隐藏层也同样会产生一些激活值，那么我将其记作$a^{[1]}$，所以具体地，这里的第一个单元或结点我们将其表示为$a_1^{[1]}$，第二个结点的值我们记为$a_2^{[1]}$，以此类推。所以这里的$a^{[1]}$是一个四维向量，如下图所示：

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052112961.png" alt="image-20220605211251903" style="zoom:80%;" />

+ 由上面我们可以总结出，在神经网络中，我们以相邻两层为观测对象，前面一层作为输入，后面一层作为输出，两层之间的$w$参数矩阵大小为$(n_{out},n_{in})$，$b$参数矩阵大小为$(n_{out},1)$，这里是作为$z=wX+b$的线性关系来说明的，在神经网络中，$w^{[i]}=w^T$。
+ 在 logistic 回归中，一般我们都会用$(n_{in},n_{out})$来表示参数大小，计算使用的公式为：$z=w^TX+b$。

## 3.3 计算一个神经网络的输出（Computing a Neural Network's output）

+ 用圆圈表示神经网络的计算单元，逻辑回归的计算有两个步骤，首先按步骤计算出$z$，然后以 sigmoid 函数为激活函数计算$z$（得出$a$），一个神经网络只是这样子做了好多次重复计算。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052113775.png" alt="image-20220605211304716" style="zoom:80%;" />

+ 接下来做向量化计算。
  <img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052113612.png" alt="image-20220605211328531" style="zoom:80%;" />

  接下来将了解如何能够计算出不止一个样本的神经网络输出，而是能一次性计算整个训练集的输出。

## 3.4 多样本向量化（Vectorizing across multiple examples）

+ 如果有一个非向量化形式的实现，而且要计算出它的预测值，对于所有训练样本，需要让从 1 到实现这四个等式：

  <img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052113578.png" alt="image-20220605211343519" style="zoom:80%;" />

+ 下面进行向量化：

  <img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052114103.png" alt="image-20220605211413033" style="zoom:80%;" />

  因此：

  <img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052114371.png" alt="image-20220605211426304" style="zoom: 67%;" />

  对矩阵$A$、$Z$、$X$，水平方向上，对应于不同的训练样本；竖直方向上，对应不同的输入特征，而这就是神经网络输入层中各个节点。下一节中将证明为什么这是一种正确向量化的实现。

## 3.5 向量化实现的解释（Justification for vectorized implementation）

对单个样本的计算要写成$z^{[1](i)}=W^{[1]}x^{(i)}+b^{[1]}$这种形式，因为当有不同的训练样本时，将它们堆到矩阵$X$的各列中，那么它们的输出也就会相应的堆叠到矩阵$Z^{[1]}$的各列中。现在我们就可以直接计算矩阵$Z^{[1]}$加上$b^{[1]}$，因为列向量$b^{[1]}$和矩阵$Z^{[1]}$的列向量有着相同的尺寸，而 Python 的广播机制对于这种矩阵与向量直接相加的处理方式是，将向量与矩阵的每一列相加。 所以这一节只是说明了为什么公式$z^{[1](i)}=W^{[1]}x^{(i)}+b^{[1]}$是前向传播的第一步计算的正确向量化实现，但事实证明，类似的分析可以发现，前向传播的其它步也可以使用非常相似的逻辑，即如果将输入按列向量横向堆叠进矩阵，那么通过公式计算之后，也能得到成列堆叠的输出。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052114889.png" alt="image-20220605211442805" style="zoom:80%;" />

## 3.6 激活函数（Activation functions）

使用一个神经网络时，需要决定使用哪种激活函数用隐藏层上，哪种用在输出节点上。到目前为止只用过 sigmoid 激活函数，但有时其他的激活函数效果会更好。更通常的情况下，使用不同的函数$g(z^{[1]})$，$g$可以是除了 sigmoid 函数以外的非线性函数。**tanh函数**或者双曲正切函数是总体上都优于 sigmoid 函数的激活函数。
$$
a=tanh(z)=\dfrac{e^z-e^{-z}}{e^z+e^{-z}}
$$
在机器学习另一个很流行的函数是：修正线性单元函数（ReLu 函数）。这有一些选择激活函数的经验法则：如果输出是 0、1 值（二分类问题），则输出层选择 sigmoid 函数，然后其它的所有单元都选择 Relu 函数。这是很多激活函数的默认选择，如果在隐藏层上不确定使用哪个激活函数，那么通常会使用 Relu 激活函数。有时，也会使用 tanh 激活函数，<u>但 Relu 的一个优点是：当是负值的时候，导数等于 0。</u>

这里也有另一个版本的 ReLU 被称为**Leaky ReLU函数**。当$z$是负值时，这个函数的值不是等于 0，而是轻微的倾斜，如图。这个函数通常比 Relu 激活函数效果要好，尽管在实际中 Leaky ReLU 使用的并不多。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052115397.png" alt="image-20220605211500317" style="zoom:80%;" />

**ReLU函数和Leaky ReLU函数的优点是：**

+ 在$z$的区间变动很大的情况下，激活函数的导数或者激活函数的斜率都会远大于 0，在程序实现就是一个 if-else 语句，而 sigmoid 函数需要进行浮点四则运算，在实践中，使用 ReLU 激活函数神经网络通常会比使用 sigmoid 或者 tanh 激活函数学习的更快。

+ sigmoid 和 tanh 函数的导数在正负饱和区的梯度都会接近于 0，这会造成梯度弥散，而 Relu 和 Leaky ReLU 函数大于 0 部分都为常数，不会产生梯度弥散现象。（同时应该注意到的是，Relu 进入负半区的时候，梯度为 0，神经元此时不会训练，产生所谓的稀疏性，而 Leaky ReLU 不会有此问题）

$z$在 ReLu 函数的梯度一半都是 0，但是，有足够的隐藏层使得$z$值大于 0，所以对大多数的训练数据来说学习过程仍然可以很快。

在选择自己神经网络的激活函数时，通常的建议是：如果不确定哪一个激活函数效果更好，可以把它们都试试，然后在验证集或者发展集上进行评价。然后看哪一种表现的更好，就去使用它。

## 3.7 为什么需要非线性激活函数？（why need a nonlinear activation function?）

事实证明：要让你的神经网络能够计算出有趣的函数，你必须使用非线性激活函数。为了说明问题我们令$a^{[i]}=z^{[i]}$，那么这个模型的输出$y$仅仅只是输入特征$x$的线性组合。过程如下：

+ $a^{[1]}=z^{[1]}=W^{[1]}x+b^{[1]}$

+ $a^{[2]}=z^{[2]}=W^{[2]}a^{[1]}+b^{[2]}=W^{[2]}(W^{[1]}x+b^{[1]})+b^{[2]}$

+ $a^{[2]}=z^{[2]}=W^{[2]}W^{[1]}x+W^{[2]}b^{[1]}+b^{[2]}$

  $\Rightarrow   a^{[2]}=z^{[2]}=W^{'}x+b^{'}$

事实证明，如果你使用线性激活函数或者没有使用一个激活函数，那么无论你的神经网络有多少层一直在做的只是计算线性函数，所以不如直接去掉全部隐藏层。在我们的简明案例中，事实证明如果你在隐藏层用线性激活函数，在输出层用 sigmoid 函数，那么这个模型的复杂度和没有任何隐藏层的标准 logistic 回归是一样的。

总而言之，**绝大部分情况下不能在隐藏层用线性激活函数**，可以用 ReLU 或者 tanh 或者 leaky ReLU 或者其他的非线性激活函数，唯一可以用线性激活函数的通常就是输出层；除了这种情况，会在隐层用线性函数的，除了一些特殊情况，比如与压缩有关的，那方面在这里将不深入讨论。

## 3.8 激活函数的导数（Derivatives of activation functions）

导数是我们比较熟悉的，直接给出：

+ **sigmoid**：$g'(z)=g(z)(1-g(z))=a(1-a)$

+ **tanh**：$g'(z)=1-(g'(z))^2=1-tanh^2(z)$
+ **ReLU**：$g'\left( z\right) =\begin{cases}0(z<0)\\ 1(z>0)\\ undefined(z=0)\end{cases}$
+ **Leaky ReLU**：$g'\left( z\right) =\begin{cases}0.01(z<0)\\ 1(z>0)\\ undefined(z=0)\end{cases}$

## 3.9 神经网络的梯度下降（Gradient descent for neural networks）

以本节中的浅层神经网络为例，我们给出神经网络的梯度下降法的公式。

+ 参数：$W^{[1]},b^{[1]},W^{[2]},b^{[2]}$；
+ 输入层特征向量个数：$n_x=n^{[0]}$；
+ 隐藏层神经元个数：$n^{[1]}$；
+ 输出层神经元个数：$n^{[2]}=1$；
+ $W^{[1]}$的维度为$(n^{[1]},n^{[0]})$，$b^{[1]}$的维度为$(n^{[1]},1)$；
+ $W^{[2]}$的维度为$(n^{[2]},n^{[1]})$，$b^{[2]}$的维度为$(n^{[2]},1)$。

下面为该例子的神经网络反向梯度下降公式（左）和其代码向量化（右）：

![image-20220606115020414](https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206061150500.png)

## 3.10（选修）直观理解反向传播（Backpropagation intuition）

![image-20220606115039833](https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206061150915.png)

## 3.11 随机初始化（Random+Initialization）

如果在初始时，两个隐藏神经元的参数设置为相同的大小，那么两个隐藏神经元对输出单元的影响也是相同的，通过反向梯度下降去进行计算的时候，会得到同样的梯度大小，所以在经过多次迭代后，两个隐藏层单位仍然是对称的。无论设置多少个隐藏单元，其最终的影响都是相同的，那么多个隐藏神经元就没有了意义。

在初始化的时候，$W$参数要进行随机初始化，$b$则不存在对称性的问题它可以设置为 0。

以 2 个输入，2 个隐藏神经元为例：

```python
W = np.random.randn((2,2))*0.01
b = np.zero((2,1))
```

这里我们将 W 的值乘以 0.01 是为了尽可能使得权重 W 初始化为较小的值，这是因为如果使用 sigmoid 函数或者 tanh 函数作为激活函数时，W 比较小，则$Z=WX+b$所得的值也比较小，处在 0 的附近，0 点区域的附近梯度较大，能够大大提高算法的更新速度。而如果 W 设置的太大的话，得到的梯度较小，训练过程因此会变得很慢。

# C1-4 深层神经网络(Deep Neural Networks)

## 4.1 深层神经网络（Deep L-layer neural network）

有较多隐藏层的神经网络为**深层神经网络**。在不同层所拥有的神经元的数目，对于每层$l$都用$a^{[l]}$来记作$l$层激活后结果，我们会在后面看到在正向传播时，最终能你会计算出$a^{[l]}$。通过用激活函数$g$计算$a^{[l]}$，激活函数也被索引为层数$l$，然后我们用$w^{[l]}$来记作在$l$层计算$z^{[l]}$值的权重。类似的，$z^{[l]}$里的$b^{[l]}$也一样。

## 4.2 深层网络中的前向传播（Forward propagation in a Deep Network）

前向传播可以归纳为多次迭代$z^{[l]}=w^{[l]}a^{[l-1]}+b^{[l]}$，$a^{[l]}=g^{[l]}(z^{[l]})$。向量化实现过程可以写成$Z^{[l]}=W^{[l]}a^{[l-1]}+b^{[l]}$，$A^{[l]}=g^{[l]}(Z^{[l]})(A^{[0]}=X)$。这里只能用一个显式 for 循环，从 1 到$l$，然后一层接着一层去计算。

## 4.3 核对矩阵的维数（Getting your matrix dimensions right）

对于第$l$层神经网络，单个样本其各个参数的矩阵维度为：

+ $W^{[l]}:(n^{[l]},n^{[l-1]})$
+ $b^{[l]}:(n^{[l]},1)$
+ $dW^{[l]}:(n^{[l]},n^{[l-1]})$
+ $db^{[l]}:(n^{[l]},n^{[l-1]})$
+ $Z^{[l]}:(n^{[l]},1)$
+ $A^{[l]}:(n^{[l]},1)$

## 4.4 为什么使用深层表示？（Why deep representations?）

+ **人脸识别和语音识别**

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052118709.png" alt="image-20220605211859621" style="zoom:80%;" />

对于人脸识别，神经网络的第一层从原始图片中提取人脸的轮廓和边缘，每个神经元学习到不同边缘的信息；网络的第二层将第一层学得的边缘信息组合起来，形成人脸的一些局部的特征，例如眼睛、嘴巴等；后面的几层逐步将上一层的特征组合起来，形成人脸的模样。随着神经网络层数的增加，特征也从原来的边缘逐步扩展为人脸的整体，由整体到局部，由简单到复杂。层数越多，那么模型学习的效果也就越精确。

对于语音识别，第一层神经网络可以学习到语言发音的一些音调，后面更深层次的网络可以检测到基本的音素，再到单词信息，逐渐加深可以学到短语、句子。

所以从上面的两个例子可以看出随着神经网络的深度加深，模型能学习到更加复杂的问题，功能也更加强大。

+ **电路逻辑计算**

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052119989.png" alt="image-20220605211913900" style="zoom:80%;" />

假定计算异或逻辑输出：$y=x_{1}\oplus x_{2}\oplus x_{3}\oplus... \oplus x_n $。

对于该运算，若果使用深度神经网络，每层将前一层的相邻的两单元进行异或，最后到一个输出，此时整个网络的层数为一个树形的形状，网络的深度为$O(log_2(n))$，共使用的神经元的个数为$n-1$。但是如果不适用深层网络，仅仅使用单隐层的网络（如右图所示），需要的神经元个数为$2^{n-1}$个 。同样的问题，但是深层网络要比浅层网络所需要的神经元个数要少得多。

## 4.5 搭建深层神经网络块（Building blocks of deep neural networks）

+ **正向函数**：在$l$层，你会有正向函数，输入$a^{[l-1]}$并且输出$a^{[l]}$，为了计算结果你需要用$W^{[l]}$和$b^{[l]}$，以及输出到缓存的$ z^{[l]}$。然后用作反向传播的反向函数，是另一个函数，输入$da^{[l]}$，输出$da^{[l-1]}$，你就会得到对激活函数的导数，也就是希望的导数值$da^{[l]}$。$a^{[l-1]}$是会变的，前一层算出的激活函数导数。在这个方块（第二个）里你需要$ W^{[l]}$和$ b^{[l]}$，最后你要算的是$dz^{[l]}$。然后这个方块（第三个）中，这个反向函数可以计算输出$dW^{[l]}$和$db^{[l]}$。

+ **反向函数**：对反向传播的步骤而言，我们需要算一系列的反向迭代，就是这样反向计算梯度，你需要把$da^{[l]}$的值放在这里，然后这个方块会给我们$da^{[l-1]}$的值，以此类推，直到我们得到$da^{[2]}$和$da^{[l]}$，你还可以计算多一个输出值，就是$da^{[0]}$，但这其实是你的输入特征的导数，并不重要，起码对于训练监督学习的权重不算重要，你可以止步于此。反向传播步骤中也会输出$dW^{[l]}$和$db^{[l]}$，这会输出$dW^{[3]}$和$db^{[3]}$等等。目前为止你算好了所有需要的导数，稍微填一下这个流程图。

  神经网络的一步训练从$a^{[0]}$开始，也就是然$x$后经过一系列正向传播计算得到$\widehat{y}$，之后再用输出值计算这个（第二行最后方块），再实现反向传播。现在你就有所有的导数项了也，$W$会在每一层被更新为$W=W-\alpha dW$，$b$也一样，$b=b-\alpha db$，反向传播就都计算完毕，我们有所有的导数值，那么这是神经网络一个梯度下降循环。

  <img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/posts/202206052119749.png" alt="image-20220605211932649" style="zoom:80%;" />

## 4.6 前向传播和反向传播（Forward and backward propagation）

+ **前向传播（Forward propagation）**：

  Input：$a^{[l-1]}$

  Output：$a^{[l]},cache(z^{[l]})$

  + 公式：
    $$
    z^{[l]}=W^{[l]}a^{[l-1]}+b^{[l]}\\
    a^{[l]}=g^{[l]}(z^{[l]})
    $$

  + 向量化程序：
    $$
    Z^{[l]}=W^{[l]}A^{[l-1]}+b^{[l]}\\
    A^{[l]}=g^{[l]}(Z^{[l]})
    $$

+ **反向传播（Backward propagation）**：

  Input：$da^{[l]}$

  Output：$da^{[l-1]},dW^{[l]},db^{[l]}$

  + 公式：
    $$
    dz^{[l]}=da^{[l]}*g'^{[l]}(z{[l]})\\
    dW^{[l]}=dz^{[l]}\cdot a^{[l-1]}\\
    db^{[l]}=dz^{[l]}\\
    da^{[l-1]}=W^{[l]T}\cdot dz^{[l]}
    $$
    将$da^{[l-1]}$代入$dz^{[l]}$，有：
    $$
    dz^{[l]}=W^{[l+1]T}\cdot dz^{[l+1]}*g'^{[l]}(z{[l]})
    $$

  + 向量化程序：
    $$
    dZ^{[l]}=dA^{[l]}*g'^{[l]}(Z{[l]})\\
    dW^{[l]}=\dfrac{1}{m}dZ^{[l]}\cdot A^{[l-1]}\\
    db^{[l]}=\dfrac{1}{m}np.sum(dZ^{[l]},axis=1,keepdims=True)\\
    dA^{[l-1]}=W^{[l]T}\cdot dZ^{[l]}
    $$

## 4.7 参数VS超参数（Parameters vs Hyperparameters）

参数即是我们在过程中想要模型学习到的信息，如$W^{[l]}$，$b^{[l]}$。超参数即为控制参数的输出值的一些网络信息，也就是超参数的改变会导致最终得比如算法中的 learning rate $a$（学习率）、iterations(梯度下降法循环的数量)、$L$（隐藏层数目）、$n^{[l]}$（隐藏层单元数目）、choice of activation function（激活函数的选择）都需要你来设置，这些数字实际上控制了最后的参数$W$和$b$的值，所以它们被称作超参数。

实际上深度学习有很多不同的超参数，之后我们也会介绍一些其他的超参数，如 momentum、mini batch size、regularization parameters 等等。设置超参数有一条经验规律：经常试试不同的超参数，勤于检查结果，看看有没有更好的超参数取值，你将会得到设定超参数的直觉。

## 4.8 深度学习和大脑的关联性（What does this have to do with the brain?）

一个神经网络的逻辑单元可以看成是对一个生物神经元的过度简化，但迄今为止连神经科学家都很难解释究竟一个神经元能做什么，它可能是极其复杂的；它的一些功能可能真的类似 logistic 回归的运算，但单个神经元到底在做什么目前还没有人能够真正可以解释。
