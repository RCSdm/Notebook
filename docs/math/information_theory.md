## 信息量与信源熵
### 基础概念
信息的特征是不确定性。

**自信息量**：度量某一事件、信源某一具体符号的不确定性。

$$ I\left(x_{i}\right)=-\log p\left(x_{i}\right) $$

**信源熵**：信源的平均不确定度。

$$ H(X)=E[I(X)]=-\sum_{i} p\left(x_{i}\right) \log p\left(x_{i}\right) $$

- 概率越大的事件，其发生带来的信息量越小，系统剩余的不确定度越大；概率越小的事件，其发生带来的信息量越大，系统剩余的不确定度越小
- 类别个数相同时，越均匀，信息熵越大。

**条件熵**

$$ H(Y \mid X) $$

已知 \(X\) 后，关于 \(Y\) 的平均不确定度。

$$ H(Y \mid X)=-\sum_{ij} p(x_{i}, y_{j}) \log p(y_{j} \mid x_{i}) $$

**联合熵**

$$ H(X, Y) $$

表示 \(X\) 和 \(Y\) 同时发生的不确定度。

$$ H(X, Y)=-\sum_{ij} p(x_{i}, y_{j}) \log p(x_{i}, y_{j}) $$

$$ H(X, Y)=H(X)+H(Y \mid X)=H(Y)+H(X \mid Y) $$

**互信息量**：已知某一条件 \(Y\)，使得对 \(X\) 的不确定度减少了。衡量条件 \(Y\) 提供了多少关于 \(X\) 的信息量。

$$ I(x_{i} ; y_{j})=\log \frac{p(x_{i} \mid y_{j})}{p(x_{i})}=\log \frac{\text{后验概率}}{\text{先验概率}} \quad (i=1,2, \ldots, n, j=1, \ldots, m) $$

**平均互信息量**: 平均意义上的互信息量

$$
I(X ; Y) = \sum_{i, j} p(x_{i}, y_{j}) \log \frac{p(x_{i} | y_{j})}{p(x_{i})} 
$$

$$
I(X ; Y) = H(X)-H(X | Y)
$$

**各概念关系**：

$$ H(X,Y) = H(X) + H(Y \mid X) = H(Y) + H(X \mid Y) $$

$$ I(X;Y) = H(X) - H(X \mid Y) $$

$$ I(Y;X) = H(Y) - H(Y \mid X) = I(X;Y) $$

$$ I(X;Y) = H(X) + H(Y) - H(X,Y) $$

### 概念补充：

**KL散度(相对熵)**

$$ D_{KL}(Q||P) = \sum_{x \in X} Q(x) \log \left[\frac{Q(x)}{P(x)}\right] $$

理解1:

> KL散度是两个概率分布 \(P\) 和 \(Q\) 差别的非对称性的度量。KL散度是用来度量使用基于 \(Q\) 的编码来编码来自 \(P\) 的样本平均所需的额外的比特个数。 典型情况下，\(P\) 表示数据的真实分布，\(Q\) 表示数据的理论分布，模型分布，或 \(P\) 的近似分布。

理解2:

> 相对熵可以衡量两个随机分布之间的距离，当两个随机分布相同时，它们的相对熵为零，当两个随机分布的差别增大时，它们的相对熵也会增大。所以相对熵（KL散度）可以用于比较文本的相似度，先统计出词的频率，然后计算。

**交叉熵**：用一个猜测的分布 \(Q\) 的编码去编码真实的分布 \(P\)，得到的最优编码长度期望值 / 用分布 \(Q\) 拟合分布 \(P\)，得到的信息熵

$$ CEH(P,Q) = - \sum_{x \in X} P(x) \log Q(x) $$

$$ D_{KL}(P||Q)= CEH(P,Q) - H(P) $$

交叉熵有一个重要的性质：最小化交叉熵等价于做最大似然估计。

由KL散度（相对熵）定义：

$$ D_{KL}(P \mid Q) = CEH(P, Q) - H(P) $$

即可看出：条件熵和相对熵间差了一个分布 \(P\) 的信息熵，当我们考虑用分布 \(Q\) 拟合真实分布 \(P\) 时，若 \(H(P)\) 是一个常数，则拟合性能完全由 \(CEH(P, Q)\) 确定，也就是说目标分布不变时，交叉熵和相对熵 (KL 散度）在行为上是等价的，都反应了 \(P, Q\) 分布的相似程度，最小化交叉熵 \(CEH(P, Q)\) 等价于最小化KL散度 \(D_{KL}(P \mid Q)\)。

### 通信模型
从信息量传输的角度看：

发出的信息量 \(H(x) \to\) 信道中损失的信息量 \(H(X \mid Y) \to\) 接收端获得的信息量 \(I(X;Y)\)

- \(H(X \mid Y)\)：疑义度，表示由于信道上存在干扰和噪声而损失掉的平均信息量
- \(H(Y \mid X)\)：噪声熵

## 通信与信道容量

信道容量：信道所能传送的最大信息量

$$ C = \max_{p(x_i)} I(X;Y) $$

单位时间的信道容量：单位时间内所能传送的最大信息量

$$ C_t = \frac{1}{t} \max_{p(x_i)} I(X;Y) $$

**信道转移概率矩阵**：

$$
P = \begin{bmatrix}
p_{11} & p_{12} & \cdots & p_{1n} \\
p_{21} & p_{22} & \cdots & p_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
p_{m1} & p_{m2} & \cdots & p_{mn} \\
\end{bmatrix}
$$

对称DMC信道

- 如果转移概率矩阵 \(P\) 的每一行都是第一行的置换（即包含同样元素），称该矩阵是输入对称的。
- 如果转移概率矩阵 \(P\) 的每一列都是第一列的置换（即包含同样元素），称该矩阵是输出对称的。
- 输入输出都对称的离散无记忆信道称为对称DMC信道。
- 信道容量：

$$ C = \log m - H(Y \mid x_i) = \log m + \sum_{j = 1}^{m} p_{ij} \log p_{ij} $$

**BSC通道**（二进制对称DMC信道）

- 信道容量：

$$ C = \log 2 - H(\varepsilon, 1-\varepsilon) = 1 - H(\varepsilon) $$

**香农公式**：AWGN信道的信道容量。香农公式是加性高斯白噪声信道中的信道容量，这是香农公式的成立条件。

$$ C= W \log(1+SNR) = W \log\left(1+\frac{P_s}{N_0 W}\right) $$

- \(W\)：信道频带宽度，简称带宽，单位Hz。
- \(SNR\)：信噪比（Signal to Noise Ratio），是信号功率（单位为W）与噪声功率（单位为W）的比值。

$$ ndb = 10 \log SNR $$

- \(P_s\)：信号发射功率。
- \(N_o\)：高斯白噪声的单边功率谱密度。

提高信道容量的方式

- 提升信道带宽
- 提升信噪比
  - 提升发射功率
  - 降低信道噪声

香农限：当带宽不受限制时，传送1比特信息，信噪比最低只需-1.6dB。

## 信源编码

目的：提高通信系统的有效性

参数说明：

- \(L\)：输入编码器的信息位长度
- \(m\)：进制数
- \(K_L\)：编码后的码字长度
  - 定长编码中，\(K_L\) 是定值
  - 变长编码中，\(\overline{K_L}\) 是平均码字长度
- \(\eta\)：编码前后的信息量比值
- \(\overline{K}\)：每一个信息位用几位编码来表示
  - \(L=1\)、二进制的情况下，\(\overline{K_L}=K_L\)

### 无失真信源编码

- 定长编码
- 无失真条件：

$$ R \ge H(\textbf{X}) $$

- 输出信息率：

$$ R = \frac{K_L}{L} \log m $$

- 编码效率：

$$ \eta = \frac{H(\textbf{X})}{R} $$

### 哈夫曼编码

- 变长编码
- 无失真条件：

$$ H(X) \le \overline{R} \le H(X) +\frac{\log m}{L} $$

- 平均输出信息率：

$$ \overline{R} = \frac{\overline{K_L}}{L} \log m $$

- 编码效率：

$$ \eta = \frac{H(X)}{\overline{R}} $$

- 码字平均长度：

$$ \overline{K_L} = \sum_i p(x_i) K_i $$

- 平均码长：

$$ \overline{K} = \frac{\overline{K_L}}{L} $$