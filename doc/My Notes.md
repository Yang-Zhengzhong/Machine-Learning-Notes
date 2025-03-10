# My Notes



## 一、机器学习基础知识

### 1.1 监督学习与无监督学习

>​	监督学习的学习对象有明确的输入和输出值，通过学习寻找其中的映射关系。

>​	无监督学习的学习对象仅有输入值，没有明确的输出结果，学习过程便是将这些值按某些规律进行分类。

### 1.2 线性回归模型

> ​	线性回归的概念已经很熟悉了，这个问题同样也可以用机器学习的方法解决，以下是课程中针对一个房价-面积单一特征模型的线性回归过程。对于大部分机器学习过程，梯度下降都是一个优秀的求解方法`果真吗？`。

##### 代价函数

> ​	可以采用方差作为代价函数，具体表述为
> $$
> J(w,b)=\frac{1}{2m}\sum_{i=1}^m(f_{w,b}(x^{(i)})-y^{(i)})^2
> $$
> 其中$w,b$分别为线性回归模型的斜率与截距，$m$是学习样本数量，$f_{w,b}$是当前算法的映射输出，$y^{(i)}$是实际的输出值（这里采用$\frac{1}{2m}$是机器学习里的一种常用形式，平方项求导后会多出来一个系数2，正好约掉，形式更工整）。

##### 梯度下降

> ​	梯度下降是一种常用的优化求解方法，迭代计算规律如下
> $$
> \begin{split}
> w=w-\alpha\frac{\partial}{\partial w}J(w,b)\\
> b=b-\alpha\frac{\partial}{\partial b}J(w,b)
> \end{split}
> $$
> 其中$\alpha$为学习率，即下降时的步长。该过程称为批量梯度下降，即每一步都在查看所有的训练样本。

##### 多特征变量学习（即多元线性回归）

> ​	场景修改为：$x_1$表示房屋面积，$x_2$表示卧室数量，$x_3$表示楼层数，$x_4$表示房屋年龄，$y$表示房屋价格。$\vec{x}^{(i)}$表示第$i$组样本的特征
> $$
> \vec{x}^{(i)}=[x_1^{(i)} \; x_2^{(i)}\; x_3^{(i)}\; x_4^{(i)}]
> $$
> 回归模型表示为
> $$
> f_{w,b}(x)=\vec{w}\cdot \vec{x}+b
> $$

> 迭代规律有一定变化：
> $$
> \begin{split}
> w_i=w_i-\alpha\frac{\partial}{\partial w_i}J(w,b)\\
> b=b-\alpha\frac{\partial}{\partial b}J(w,b)
> \end{split}
> $$

+ 向量化编写代码可以显著提高运算效率(硬件进行并行运算)

> ​	样本的参数初始值选择应考虑特征的变化范围，一般规律为特征变化范围大的参数值小，特征取值范围小的参数值大。当特征变化范围过大时，如$300\leq x_1\leq2000$，通常会采取一些方法对取值范围进行放缩：
>
> 1. 取其上界和下界的倒数$(\frac{1}{2000},\frac{1}{300})$；
> 2. Z-score归一化，即提取均值和标准差，随后取$x_{1,normalization}=\frac{x_1-\mu_1}{\sigma_1}$。
>
> 这种操作有助于提高梯度下降的速度。

