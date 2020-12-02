# 线性回归

## 基本要素

### 模型  

$$
y^=x1w1+x2w2+b、
$$

* w1，w2表示权重，b为bias偏差，这三个是参数，且均为标量
  
* 模型输出 y^ 是线性回归对真实价格 y 的预测或估计。
  
#### 模型训练

##### 训练数据

$$
\hat{y}^{(i)} = x_1^{(i)} w_1 + x_2^{(i)} w_2 + b.
$$

* 样本数为 n ，索引为 i 的样本的特征为 x(i)1 和 x(i)2 ，标签为 y(i) 。

##### 损失函数

* 平方损失（square loss）

$$
\ell^{(i)}(w_1, w_2, b) = \frac{1}{2} \left(\hat{y}^{(i)} - y^{(i)}\right)^2,
$$

>样本预测值与实际值的差的平方，其中系数为认为给定，为了其求导系数等于1

*通常使用所有样本误差的平均来衡量模型预测质量,即

$$
\ell(w_1, w_2, b) =\frac{1}{n} \sum_{i=1}^n \ell^{(i)}(w_1, w_2, b) =\frac{1}{n} \sum_{i=1}^n \frac{1}{2}\left(x_1^{(i)} w_1 + x_2^{(i)} w_2 + b - y^{(i)}\right)^2
$$

* 训练过程中，我们希望找到一组数据模型使训练样本损失最小，即
$$ w_1^*, w_2^*, b^* = \operatorname*{argmin}_{w_1, w_2, b}\  \ell(w_1, w_2, b).$$

##### 优化算法

* 解析解：可以直接求出</br>数值解：通过优化算法迭代尽可能降低损失的值
* 小批量随机梯度优化算法

$$
w_1 \leftarrow w_1 -   \frac{\eta}{|\mathcal{B}|} \sum_{i \in \mathcal{B}} \frac{ \partial \ell^{(i)}(w_1, w_2, b)  }{\partial w_1} = w_1 -   \frac{\eta}{|\mathcal{B}|} \sum_{i \in \mathcal{B}}x_1^{(i)} \left(x_1^{(i)} w_1 + x_2^{(i)} w_2 + b - y^{(i)}\right)\\
$$

$$
w_2 \leftarrow w_2 -   \frac{\eta}{|\mathcal{B}|} \sum_{i \in \mathcal{B}} \frac{ \partial \ell^{(i)}(w_1, w_2, b)  }{\partial w_2} = w_2 -   \frac{\eta}{|\mathcal{B}|} \sum_{i \in \mathcal{B}}x_2^{(i)} \left(x_1^{(i)} w_1 + x_2^{(i)} w_2 + b - y^{(i)}\right)\\
$$

$$
b \leftarrow b -   \frac{\eta}{|\mathcal{B}|} \sum_{i \in \mathcal{B}} \frac{ \partial \ell^{(i)}(w_1, w_2, b)  }{\partial b} = b -   \frac{\eta}{|\mathcal{B}|} \sum_{i \in \mathcal{B}}\left(x_1^{(i)} w_1 + x_2^{(i)} w_2 + b - y^{(i)}\right)
$$

> $\mathcal{B}$代表每个小批量中的样本个数（批量大小，batch size），$η$称作学习率（learning rate）并取正数。需要强调的是，这里的批量大小和学习率的值是人为设定的，并不是通过模型训练学出的，因此叫作超参数（hyperparameter）。
>  
>它的算法很简单：先选取一组模型参数的初始值，如随机选取；接下来对参数进行多次迭代，使每次迭代都可能降低损失函数的值。在每次迭代中，先随机均匀采样一个由固定数目训练数据样本所组成的小批量（mini-batch）$\mathcal{B}$ ，然后求小批量中数据样本的平均损失有关模型参数的导数（梯度），最后用此结果与预先设定的一个正数的乘积作为模型参数在本次迭代的减小量。

