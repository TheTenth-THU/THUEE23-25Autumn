
![[信息论的基本模型.png|信息论的基本模型]]


# 信源

## 信源的概念

> [!definition] 信源
> 信息的产生者称为**信源 (source of information)**，产生一个**随机过程**发出信息。

### 离散无记忆信源

**离散信源 (discrete source)** 是时间、取值上都离散的信源，可以表示为 
$$
X[k] \in \{ x_{1}, x_{2}, \cdots, x_{N} \}
$$

为简化讨论，可以假设 **$X[k]$ 是独立同分布的随机过程**，即：

> [!definition] 离散无记忆信源
> 持续产生**独立同分布**的符号  $X \in \{ x_{1}, x_{2}, \cdots, x_{N} \}$ 的信源，称为**离散无记忆信源 (discrete memoryless source, DMS)**，记为
> $$
> X \sim \begin{pmatrix}
> x_{1} & x_{2} & \cdots & x_{N} \\
> p_{1} & p_{2} & \cdots & p_{N}
> \end{pmatrix}, \quad
> p_{i} = \mathrm{Pr}\{ X = x_{i} \}
> $$

### 信源编码的基本要求

将信源产生的符号 $X$ 映射为 0, 1 比特串 $f(X)$ 的过程称为**信源编码 (source coding)**，产生的比特串称为**码字 (codeword)**，其长度 $l$ 称为**码长 (code length)**。

+ 若不同 $x_{i}$ 映射出的码长 $l_{i}$ 相同，称为**定长码 (fixed-length code)**；
+ 若不同 $x_{i}$ 映射出的码长 $l_{i}$ 不同，称为**变长码 (variable-length code)**。

#### 定长码的可解码条件

对**定长码**，要求
$$
f(x_{i}) \neq f(x_{j}), \quad \forall i \neq j
$$
因此固定码长 $l$ 应满足
$$
N \leq 2^{l} \implies l \geq \lceil \log N \rceil
$$
此处 $\log$ 均为以 2 为底的对数。

#### 变长码的可解码条件

对**变长码**，要求任意码字不能是另一个码字的前缀，因此又称为**前缀码 (prefix code)**。

引入**平均码长 (average code length)** 
$$
\bar{l} = \sum\limits_{i=1}^{N} p_{i} l_{i}
$$
我们希望在可解码的条件下，使 $\bar{l}$ 尽可能小。

可以证明，信源 $X \sim \begin{pmatrix} x_{1} & x_{2} & \cdots & x_{N} \\ p_{1} & p_{2} & \cdots & p_{N} \end{pmatrix}$ 的最小平均码长为
$$
\bar{l}_{\min} = - \sum\limits_{i=1}^{N} p_{i} \log p_{i}
$$

## 信源的熵

### 离散信源的熵

> [!definition] 离散信源的熵
> 离散无记忆信源 $X \sim \begin{pmatrix} x_{1} & x_{2} & \cdots & x_{N} \\ p_{1} & p_{2} & \cdots & p_{N} \end{pmatrix}$ 的**熵 (entropy)** 定义为
> $$
> H(X) = - \sum\limits_{i=1}^{N} p_{i} \log p_{i}
> $$

$H(X)$ 可以写为
$$
H(X) = \mathbb{E}_{X} [ - \log p(X) ]
$$
因而 $- \log \mathrm{Pr}\{ X = x_{i} \}$ 刻画事件 $\{ X = x_{i} \}$ 所包含的信息量，**概率越小，信息量越大**。

#### 熵的性质

考虑 $H(X) = \bar{l}_{\min}$ 的物理含义，应有 $0 \le H(X) \le \log N$。

+ 当且仅当 $$\exists i \in \{ 1, 2, \cdots,N \}, \quad p_{i} = 1$$ 时，$H(X) = 0$，此时信源没有不确定性，不包含信息；

+ 当且仅当 $$p_{i} = \dfrac{1}{N}, \quad i = 1, 2, \cdots, N$$ 时，$H(X) = \log N$，此时信源不确定性最大，包含信息量最大。
	对离散信源，**均匀分布的不确定度最大**。

#### 联合熵、条件熵

> [!definition] 联合熵
> 考虑两个离散无记忆信源 $X$ 和 $Y$，事件 $\{ X = x_{i}, Y = y_{j} \}$ 的概率为 $p_{ij} = \mathrm{Pr}\{ X = x_{i}, Y = y_{j} \}$，则 $X$ 和 $Y$ 的**联合熵 (joint entropy)** 定义为
> $$
> H(X, Y) = \mathbb{E}_{XY} [ - \log p(X, Y) ]
> = - \sum\limits_{i=1}^{N} \sum\limits_{j=1}^{M} p_{ij} \log p_{ij}
> $$
> 在没有歧义的情况下，联合熵 $H(X,Y)$ 可记为 $H(XY)$。

联合熵刻画了将 $X$ 和 $Y$ 一起编码所需的最小平均码长，即综合考虑 $X$ 和 $Y$ 的信息量。

> [!definition] 条件熵
> 考虑 $X$ 和 $Y$ 的联合分布 $p_{ij} = \mathrm{Pr}\{ X = x_{i}, Y = y_{j} \}$，在 $Y$ 已知的条件下，事件 $\{ X = x_{i} \}$ 发生的概率为
> $$
> p_{i \mid j} = \mathrm{Pr}\{ X = x_{i} \mid Y = y_{j} \} = \dfrac{\mathrm{Pr}\{ X = x_{i}, Y = y_{j} \}}{\mathrm{Pr}\{ Y = y_{j} \}} = \dfrac{p_{ij}}{p_{j}}
> $$
> 则以 $Y$ 为条件的 $X$ 的**条件熵 (conditional entropy)** 定义为
> $$
> H(X \mid Y) = \mathbb{E}_{XY} [ - \log p(X \mid Y) ] = - \sum\limits_{i=1}^{N} \sum\limits_{j=1}^{M} p_{ij} \log p_{i \mid j}
> $$

条件熵 $H(X \mid Y)$ 刻画了在已知 $Y$ 的条件下，$X$ 所包含的信息量，即在观测 $Y$ 后 $X$ 残存的不确定度。

> [!note] 熵的通信意义
> 信源的熵 $H(X)$ 刻画了信源 $X$ 所包含的信息量，其值即对 $X$ 进行无失真编码时所需的最小平均码长。
> 
> + 考虑对一个离散无记忆信源 $X$ 编码传输，当**信道速率**（每传输一个信源符号所传输的平均比特数）**$R \geq H(X)$** 时，可以实现**无失真**传输，即信源译码环节可无失真恢复 $X$；
> 
> + 考虑对两个离散无记忆信源 $X$ 和 $Y$ 做联合信源编码传输，当**信道速率 $R \geq H(X, Y)$** 时，在信源译码环节可无失真恢复 $(X, Y)$；
> 
> + 考虑对离散无记忆信源 $X$ 编码传输，编译码器可以共同观测另一个信源 ，当**信道速率 $R \geq H(X \mid Y)$** 时，在信源译码环节可无失真恢复 。

#### 熵的链式法则

> [!theorem] 熵的链式法则
> 对于任意两个离散随机变量 $X$ 和 $Y$，有
> $$
> H(X, Y) = H(Y) + H(X \mid Y) = H(X) + H(Y \mid X)
> $$

进一步地，

+ 若 **$X$ 与 $Y$ 独立**（记为 $X \perp Y$），则 $p_{ij} = p_{i}p_{j}$，$p_{i \mid j} = \dfrac{p_{i}p_{j}}{p_{j}} = p_{i}$，于是
$$
\begin{align}
H(X \mid Y) &= - \sum\limits_{i=1}^{N} \sum\limits_{j=1}^{M} p_{ij} \log p_{i \mid j} = - \sum\limits_{i=1}^{N} \sum\limits_{j=1}^{M} p_{i} p_{j} \log p_{i}  \\
&= - \sum\limits_{i=1}^{N} p_{i} \log p_{i} = H(X)
\end{align}
$$
$$
H(XY) = H(X \mid Y) + H(Y) = H(X) + H(Y)
$$
即**独立随机变量的联合熵等于各自熵之和**。观测 $Y$ 不会减少 $X$ 的不确定性。

+ 若 $X$ 是 $Y$ 的**确定性映射**（记为 $X = f(Y)$），则 $p_{i \mid j}$ 要么为 0，要么为 1，因此 $H(X \mid Y) = 0$，于是
$$
H(X, Y) = H(Y)
$$
即**确定性映射不会增加不确定性**。观测 $Y$ 会完全消除 $X$ 的不确定性。

#### 互信息

$H(X \mid Y)$ 表征通过观测 $Y$ 后 $X$ 残存的不确定度，这种观测所消除不确定度的程度，即称为**互信息 (mutual information)**。

显然，有
$$
\begin{align}
H(X) - H(X \mid Y) &= H(X) - \big( H(X, Y) - H(Y) \big) \\
&= H(X) + H(Y) - H(X, Y) \\
&= H(Y) - H(Y \mid X)
\end{align}
$$
即，通过观测 $Y$ 消除的 $X$ 的不确定度，等于通过观测 $X$ 消除的 $Y$ 的不确定度。$X$ 与 $Y$ 的**互信息是对称的**。

> [!definition] 互信息
> 离散随机变量 $X$ 和 $Y$ 的**互信息 (mutual information)** 定义为
> $$
> I(X; Y) = H(X) - H(X \mid Y) = H(Y) - H(Y \mid X)
> $$

一般地，
$$
I(X; Y) = H(X) + H(Y) - H(X, Y)
= \sum\limits_{i=1}^{N} \sum\limits_{j=1}^{M} p_{ij} \log \dfrac{p_{ij}}{p_{i} p_{j}}
$$

考虑两个离散无记忆信源 $X$ 和 $Y$，

+ 若 $X \perp Y$，则
$$
I(X; Y) = H(X) - H(X \mid Y) = H(X) - H(X) = 0
$$
即**独立信源间没有互信息**；另可证明，没有互信息的信源是独立的。

+ 若 $X = f(Y)$，则
$$
I(X; Y) = H(X) - H(X \mid Y) = H(X) - 0 = H(X)
$$
即**确定性映射的信源间互信息是其全部不确定度**。 

+ $0 \le H(X \mid Y) \le H(X)$，因此 $I(X;Y) \ge 0$，**信源之间不存在欺骗**。

### 连续信源的微分熵

对于连续随机变量 $X$，其概率分布由**概率密度函数 (probability density function, PDF)** $p_{X}(x)$ 描述，满足
$$
\dint_{-\infty}^{+\infty} p_{X}(x) \dif x = 1, \quad p_{X}(x) \geq 0
$$

> [!definition] 微分熵
> **微分熵 (differential entropy)** 定义为
> $$
> h(X) = \mathbb{E}_{X} [ - \log p_{X}(X) ] = - \dint_{-\infty}^{+\infty} p_{X}(x) \log p_{X}(x)  \dif x
> $$

微分熵 $h(X)$ **刻画了信源 $X$ 的相对不确定度**，其值可以为负数。

> [!example]- Gauss 分布的微分熵
> 对 $X \sim \mathcal{N}(\mu, \sigma^{2})$，有 $p_{X}(x) = \dfrac{1}{\sqrt{2 \pi \sigma^{2}}} \exp \left( - \dfrac{(x - \mu)^{2}}{2 \sigma^{2}} \right)$，因此
> $$
> \begin{align}
> h(X) &= - \dint_{-\infty}^{+\infty} p_{X}(x) \log p_{X}(x) \dif x \\
> &= - \dint_{-\infty}^{+\infty} p_{X}(x) \log \left( \dfrac{1}{\sqrt{2 \pi \sigma^{2}}} \exp \left( - \dfrac{(x - \mu)^{2}}{2 \sigma^{2}} \right) \right) \dif x \\
> &= - \dint_{-\infty}^{+\infty} p_{X}(x) \left( - \dfrac{(x - \mu)^{2}}{2 \sigma^{2}} \log \e - \log \sqrt{2 \pi \sigma^{2}} \right) \dif x \\
> &= \dfrac{\log \e}{2 \sigma^{2}} \dint_{-\infty}^{+\infty} (x - \mu)^{2} p_{X}(x) \dif x + \log \sqrt{2 \pi \sigma^{2}} \dint_{-\infty}^{+\infty} p_{X}(x) \dif x \\
> &= \dfrac{\log \e}{2 \sigma^{2}} \mathbb{E}[(X - \mu)^{2}] + \log \sqrt{2 \pi \sigma^{2}} \\
> &= \dfrac{\log \e}{2 \sigma^{2}} \left( \mathbb{E}^{2}\left[ (X - \mu) \right] + \mathrm{Var}\left[ (X - \mu) \right]  \right) + \log \sqrt{2 \pi \sigma^{2}} \\
> &= \dfrac{\log \e}{2 \sigma^{2}} \cdot \sigma^{2} + \log \sqrt{2 \pi \sigma^{2}} = \mark{ \log \sqrt{2 \pi \e \sigma^{2}} }
> \end{align}
> $$

#### 联合微分熵、条件微分熵

> [!definition] 联合微分熵
> 考虑两个连续随机变量 $X$ 和 $Y$，其联合概率密度函数为 $p_{X, Y}(x, y)$，则 $X$ 和 $Y$ 的**联合微分熵 (joint differential entropy)** 定义为
> $$
> h(X, Y) = \mathbb{E}_{X, Y} [ - \log p_{X, Y}(X, Y) ] = - \dint_{-\infty}^{+\infty} \dint_{-\infty}^{+\infty} p_{X, Y}(x, y) \log p_{X, Y}(x, y) \dif x \dif y
> $$
> 在没有歧义的情况下，联合微分熵 $h(X,Y)$ 可记为 $h(XY)$。

> [!definition] 条件微分熵
> 考虑 $X$ 和 $Y$ 的联合概率密度函数 $p_{X, Y}(x, y)$，条件随机变量 $X \mid Y$ 的概率密度函数为
> $$
> p_{X \mid Y}(x, y) = \dfrac{p_{X, Y}(x, y)}{p_{Y}(y)}
> $$
> 则以 $Y$ 为条件的 $X$ 的**条件微分熵 (conditional differential entropy)** 定义为
> $$
> h(X \mid Y) = \mathbb{E}_{X, Y} [ - \log p_{X \mid Y}(X, Y) ] = - \dint_{-\infty}^{+\infty} \dint_{-\infty}^{+\infty} p_{X, Y}(x, y) \log p_{X \mid Y}(x, y) \dif x \dif y
> $$

类似地，微分熵也有**链式法则**
$$
h(X, Y) = h(Y) + h(X \mid Y) = h(X) + h(Y \mid X)
$$

#### 微分熵的互信息

> [!definition] 微分熵的互信息
> 连续随机变量 $X$ 和 $Y$ 的**互信息 (mutual information)** 定义为
> $$
> I(X; Y) = h(X) - h(X \mid Y) = h(Y) - h(Y \mid X)
> $$

一般地，
$$
\begin{align}
I(X; Y) &= h(X) - h(X \mid Y) = h(X) + h(Y) - h(X, Y) \\
&= \dint_{-\infty}^{+\infty} \dint_{-\infty}^{+\infty} p_{X, Y}(x, y) \log \dfrac{p_{X, Y}(x, y)}{p_{X}(x) p_{Y}(y)} \dif x \dif y
\end{align}
$$


# 信道

## 离散幅值信道

### 离散无记忆信道模型

**离散无记忆信道 (Discrete Memoryless Channel, DMC) 模型**假设信道在每次传输时的行为独立且不依赖于之前的传输结果。DMC 由一个条件概率来描述，即**给定信源输入符号 $X = x_{i}$ 时信宿输出符号 $Y = y_{j}$ 的概率分布 $p_{j \mid i}$**。

当给定 $X$ 的分布 $p_{i}$ 时，可以得到联合分布
$$
p_{ij} = \mathrm{Pr}\{ X = x_{i}, Y = y_{j} \} = \mathrm{Pr}\{ Y = y_{j} \mid X = x_{i} \} \mathrm{Pr}\{ X = x_{i} \} = p_{i} p_{j \mid i}
$$
信宿输出 $Y$ 的边缘分布为
$$
p_{j} = \mathrm{Pr}\{ Y = y_{j} \} = \sum\limits_{i} p_{ij} = \sum\limits_{i} p_{i} p_{j \mid i}
$$
这样，**互信息 $I(X;Y)$ 就可以给定**为
$$
\begin{align}
I(X; Y) &= H(X) + H(Y) - H(X, Y) \\
&= - \sum\limits_{i} p_{i} \log p_{i} - \sum\limits_{j} p_{j} \log p_{j} + \sum\limits_{i} \sum\limits_{j} p_{ij} \log p_{ij} \\
&= - \sum\limits_{i} \sum\limits_{j} p_{ij} \log p_{i} - \sum\limits_{i} \sum\limits_{j} p_{ij} \log p_{j} + \sum\limits_{i} \sum\limits_{j} p_{ij} \log p_{ij} \\
&= \sum\limits_{i} \sum\limits_{j} p_{ij} \log \dfrac{p_{ij}}{p_{i} p_{j}} 
= \sum\limits_{i} \sum\limits_{j} p_{ij} \log \dfrac{p_{j \mid i}}{p_{j}} 
= \mark{ \sum\limits_{i} \sum\limits_{j} p_{i} p_{j \mid i} \log \dfrac{p_{j \mid i}}{\sum\limits_{i} p_{i} p_{j \mid i}}  }
\end{align}
$$

若允许通过映射**调整输入分布 $p_{i}$**，则可以在此意义下**最大化互信息 $I(X;Y)$**，这一最大值称为**信道容量 (channel capacity)**，记为 
$$
C = \max\limits_{p_{i}} I(X; Y)
= \max\limits_{p_{i}} \sum\limits_{i} \sum\limits_{j} p_{i} p_{j \mid i} \log \dfrac{p_{j \mid i}}{\sum\limits_{i} p_{i} p_{j \mid i}}
$$
这一优化问题还有两个约束条件，即概率归一化条件 $\sum\limits_{i} p_{i} = 1$ 和非负性条件 $p_{i} \geq 0$。这是一个**非凸**的带约束优化问题，有一定的求解难度。一般 DMC 的容量需要通过数值方法求解，如 Blahut-Arimoto 算法。

### 对称二进制信道 (BSC)

我们希望得到容量的解析闭式解，因此需要在**数字通信**背景下简化 DMC 模型。

> [!definition] 对称二进制信道
> **对称二进制信道 (Binary Symmetric Channel, BSC)** 是这样的 DMC：
> + 输入和输出符号均为二进制（0 和 1），
> + 每个比特在传输过程中都有一个固定的**差错概率 (cross-over probability)** $\epsilon$，即输出比特有 $\epsilon$ 的概率变为输入比特的反码。

BSC 可以等效为
$$
Y = X \oplus Z, \quad Z \sim \mathrm{Bernoulli}(\epsilon) = \begin{pmatrix}
0 & 1 \\ 1 - \epsilon & \epsilon
\end{pmatrix}
$$
其中 $Z$ 是与输入 $X$ 独立的噪声变量，$\oplus$ 表示**按位异或**运算。

使用这一等效，BSC 的容量为
$$
\begin{align}
C &= \max\limits_{p_{i}} I(X; Y) = \max\limits_{p_{i}} I(X; X \oplus Z) \\
&= \max\limits_{p_{i}} \big( H(X \oplus Z) - H(X \oplus Z \mid X) \big) \\
&= \max\limits_{p_{i}} \big( H(X \oplus Z) - H(Z) \big) \\
&= \max\limits_{p_{i}} H(X \oplus Z) + \underbrace{ \epsilon \log \epsilon + (1 - \epsilon) \log (1 - \epsilon) }_{ \text{const} } 
\end{align}
$$
因此，最大化互信息等价于**最大化 $H(X \oplus Z)$**。由于 $X \oplus Z \in \{ 0, 1 \}$，其熵的最大值为 1，**比特均匀分布**时取得，即
$$
\begin{align}
C = 1 + \epsilon \log \epsilon + (1 - \epsilon) \log (1 - \epsilon) 
\quad\text{iff}\quad &Y \sim \mathrm{Bernoulli}(0.5) \\
&\iff X \sim \mathrm{Bernoulli}(0.5)
\end{align}
$$

### 更多离散信道模型

#### 擦除信道

**二进制擦除信道 (Binary Erasure Channel, BEC)** 是另一种常见的离散信道模型。与 BSC 不同，BEC 在传输过程中不会将比特翻转为反码，而是有一定概率 $\epsilon$ **将比特「擦除」**，即**输出一个特殊符号 $e$**，表示该比特丢失。

在 BEC 中，已知输出 $Y$ 为 0 或 1 时，可以确定输入 $X$ 的值，**没有任何不确定性**；而当输出 $Y$ 为 $e$ 时，输入 $X$ **等概地**可能是 0 或 1，存在不确定性 $H(X\mid Y=e) = 1$。这样，BEC 的容量为
$$
\begin{align}
C &= \max\limits_{p_{i}} I(X; Y) = \max\limits_{p_{i}} \big( H(X) - H(X \mid Y) \big) \\
&= \max\limits_{p_{i}} \big( H(X) - \epsilon H(X \mid Y = e) \big) \\
&= \max\limits_{p_{i}} \big( H(X) - \epsilon \cdot 1 \big) = 1 - \epsilon
\end{align}
$$
当输入比特均匀分布时取得，即 $X \sim \mathrm{Bernoulli}(0.5)$。

推广到**多进制擦除信道 (M-ary Erasure Channel, MEC)**，输入输出符号集均为 $M$ 个符号 $\{ x_{1}, x_{2}, \ldots, x_{M} \}$，每个符号在传输过程中有概率 $\epsilon$ 被**擦除**为特殊符号 $e$，不变的概率为 $1 - \epsilon$。MEC 的容量为
$$
C = \log M - \epsilon \log M = (1 - \epsilon) \log M
$$
当输入符号均匀分布时取得，此时 $p_{i} \equiv \cfrac{1}{M}$。

#### 多进制对称信道

将 BSC 推广到多进制符号集，可以得到**多进制对称信道 (M-ary Symmetric Channel, MSC)**。MSC 的输入输出符号集均为 $M$ 个符号 $\{ x_{1}, x_{2}, \ldots, x_{M} \}$，每个符号在传输过程中有概率 $\epsilon$ 被**均匀地**翻转为其他 $M-1$ 个符号中的任意一个，不变的概率为 $1 - (M-1)\epsilon$。

对 MSC，有
$$
\begin{align}
I(X; Y) &= H(Y) - H(Y \mid X) = - \sum\limits_{j=1}^{M} p_{j} \log p_{j} + \sum\limits_{i=1}^{M} p_{i} \sum\limits_{j=1}^{M} p_{j \mid i} \log p_{j \mid i} \\
&= - \sum\limits_{j=1}^{M} p_{j} \log p_{j} + \sum\limits_{i=1}^{M} p_{i} \big( (1 - (M-1)\epsilon) \log (1 - (M-1)\epsilon)  \\[-1em]
&\hspace{11.5em} + (M-1) \epsilon \log \epsilon \big) \\
&= - \sum\limits_{j=1}^{M} p_{j} \log p_{j} + \underbrace{ (1 - (M-1)\epsilon) \log (1 - (M-1)\epsilon) + (M-1) \epsilon \log \epsilon }_{ \text{const} } \\
&\le \log M + \text{const}
\end{align}
$$
因此，MSC 的容量为
$$
C = \log M + (1 - (M-1)\epsilon) \log (1 - (M-1)\epsilon) + (M-1) \epsilon \log \epsilon
$$
此时，输入符号均匀分布，$p_{i} \equiv \cfrac{1}{M}$。

## 连续幅值信道

类似于离散幅值信道，**连续幅值信道 (continuous amplitude channel)** 也可以用条件概率密度函数 $p_{Y|X}(y, x)$ 来描述，所传递的信息量仍然用互信息 $I(X; Y)$ 来衡量。

若允许通过映射**调整输入分布 $p_{X}(x)$**，则可以在此意义下**最大化[[#信源#微分熵的互信息|互信息]] $I(X;Y)$**，这一最大值仍然称为**信道容量 (channel capacity)**，记为
$$
C = \max\limits_{p_{X}(x)} I(X; Y)
$$

### Gauss 信道

**Gauss 信道 (Gaussian channel)** 是一种特殊的连续幅值信道，假设信道输出 $Y$ 是输入 $X$ 与高斯白噪声 $Z$ 的和，即
$$
Y = X + Z, \qquad \text{where} \quad Z \sim \mathcal{N}(0, \sigma^{2})
$$
其中 $X$ 有功率约束 $\mathbb{E}\left[ X^{2} \right] = E_{\mathrm{s}}$。

Gauss 信道的容量为
$$
\begin{align}
C &= \max\limits_{p_{X}(x)} I(X; Y) = \max\limits_{p_{X}(x)} I(X; X + Z) 
= \max\limits_{p_{X}(x)} \big( h(X + Z) - h(X + Z \mid X) \big) \\
&= \max\limits_{p_{X}(x)} \big( h(X + Z) - h(Z) \big) 
= \max\limits_{p_{X}(x)} h(X + Z) - \log \sqrt{ 2 \pi \e \sigma^{2} }
\end{align}
$$
因此，最大化互信息等价于**最大化 $h(X + Z)$**。由于 $X$、$Z$ 独立，
$$
\mathbb{E}\left[ (X + Z)^{2} \right] = \mathbb{E}\left[ X^{2} \right] + \mathbb{E}\left[ Z^{2} \right] + 2 \mathbb{E}\left[ X \right] \underbrace{ \mathbb{E}\left[ Z \right] }_{ 0 } = E_{\mathrm{s}} + \sigma^{2}
$$
当且仅当 $X \sim \mathcal{N}(0, E_{\mathrm{s}})$ 时，$X + Z \sim \mathcal{N}(0, E_{\mathrm{s}} + \sigma^{2})$，$h(X + Z)$ 最大化为
$$
h(X + Z) = \log \sqrt{ 2 \pi \e (E_{\mathrm{s}} + \sigma^{2}) }
$$
从而
$$
C = \log \sqrt{ 2\pi \e (E_{\mathrm{s}} + \sigma^{2}) } - \log \sqrt{ 2 \pi \e \sigma^{2} } = \mark{ \log \sqrt{ 1 + \dfrac{E_{\mathrm{s}}}{\sigma^{2}} } }
$$
这里 $C$ 无量纲，单位为 bit/次。

### 带宽受限的 Gauss 信道

在实际通信系统中，信道通常是**带宽受限 (bandwidth-limited)** 的，即信号只能在有限的频率范围内传输。设信道的带宽为 $W$，则根据 **Nyquist 采样定理**，单位时间最多可以传输 $2W$ 个独立符号。

考虑带宽受限为 $W$ 的 Gauss 信道，由于这一信道中的噪声是与信号**时域相加**的、功率谱在 $[-W,W]$ 均匀的 Gauss 噪声，因此称为**加性白 Gauss 噪声 (Additive White Gaussian Noise, AWGN) 信道**。设其中噪声 $N(t)$ 的方差为 $\sigma^{2}$，则
$$
R_{N}(t, s) = \begin{cases}
\mathbb{E}\left[ N^{2}(t) \right] = \sigma^{2}, & t = s \\
0, & t \neq s
\end{cases} = \sigma^{2} \delta(t - s)
$$
因此 $N(t)$ 是**宽平稳**的，$R_{N}(\tau) = \sigma^{2} \delta(\tau)$，其功率谱密度为
$$
S_{N}(f) = \int_{-\infty}^{+\infty} R_{N}(\tau) \e^{-j 2 \pi f \tau} \dif \tau = \sigma^{2}, \quad |f| \leq W
$$
将正负频部分合并，得到单边功率谱密度为
$$
S_{N}^{\text{(single)}}(f) = 2 \sigma^{2} =: n_{0}, \quad 0 \leq f \leq W
$$

同时，记通信功率 $P$ 为单位时间内传输的平均能量，则每个符号的平均能量为 $E_{\mathrm{s}} = \cfrac{P}{2W}$。则 AWGN 信道的容量为
$$
C = 2W \log \sqrt{ 1 + \dfrac{P}{2W \sigma^{2}} } = W \log \left( 1 + \dfrac{P}{Wn_{0}} \right)
$$

> [!theorem] Shannon 公式
> 带宽受限于 $|f| \le W$、噪声功率谱密度为 $S_{N}(f) = \dfrac{n_{0}}{2}$ 的 **AWGN 信道**在功率 $P$ 下的容量为
> $$
> C = {W} \log \left( 1 + \dfrac{P}{W n_{0}} \right)
> $$
> 其中 $C$ 的单位为 bit/s。

信号功率与噪声功率的比值 $\cfrac{P}{Wn_{0}}$ 称为**信噪比 (signal-to-noise ratio, SNR)**，可记为 $\mathrm{SNR}$。因此，Shannon 公式也可以写为
$$
C = W \log (1 + \mathrm{SNR})
$$
+ 当 $\mathrm{SNR} \to 0$ 时，即在**低 SNR** 区，
$$C \to W \log\e \cdot \mathrm{SNR} =\dfrac{P}{n_{0}}\log \e \approx 1.44 \dfrac{P}{n_{0}}$$
容量 $C$ 与带宽 $W$ 无关，而与功率 $P$ 呈线性关系；
+ 当 $\mathrm{SNR} \to +\infty$ 时，即在**高 SNR** 区，$C \to W \log \mathrm{SNR}$，引入信噪比的分贝值 $\mathrm{SNR}_{\mathrm{dB}} = 10 \log_{10} \mathrm{SNR} = \cfrac{10}{\log 10}\log \mathrm{SNR}$，则
$$
C \to W \cdot \dfrac{\log 10}{10} \mathrm{SNR}_{\mathrm{dB}} \approx 0.3322 W \cdot \mathrm{SNR}_{\mathrm{dB}}
$$



# 模拟信源的数字编码

模拟信源是**时间连续、幅值连续**的信源，其输出 $s(t)$ 是一个连续时间的[[随机过程的平稳性#^b4e44e|随机过程]]，将其数字化的过程如下：

![[模拟信源的数字编码.png|模拟信源的数字编码]]

在信道另一侧，接收端对接收到的二值序列进行**译码 (digital decoding)**，恢复出数字信号，然后通过**电平重建 (level reconstruction)** 和**内插 (interpolation)**，即恢复出模拟信号 $\hat{s}(t)$。

## 抽样与内插恢复

**抽样 (sampling)** 是将连续时间信号 $s(t)$ 在时间上离散化的过程，得到离散时间信号 $x[k] = s(kT_{\mathrm{s}})$，其中 $T_{\mathrm{s}}$ 是**抽样周期 (sampling period)**，$f_{\mathrm{s}} = \dfrac{1}{T_{\mathrm{s}}}$ 是**抽样频率 (sampling frequency)**。

> [!theorem] Nyquist 抽样定理
> 设 $s(t)$ 是**带宽受限**的信号，其频谱 $S(f) = \mathcal{F}\left\{ s(t) \right\}$ 满足
> $$
> S(f) = 0, \quad |f| > W
> $$
> 则当抽样频率 $f_{\mathrm{s}} \ge 2W$ 时，可以从抽样所得信号 $x[k] = s(kT_{\mathrm{s}})$ **无失真**地恢复出 $s(t)$。这个最低抽样频率 $f_{\mathrm{s}} = 2W$ 称为 **Nyquist 频率 (Nyquist frequency)**。

从序列 $x[k]$ 恢复出 $s(t)$，可以先以 $x[k]$ 调制冲激序列得到 $\t{s}(t) = \sum\limits_{k} x[k] \delta(t-kT_{\mathrm{s}})$，其 Fourier 变换为
$$
\t{S}(f) = \mathcal{F}\left\{ \t{s}(t) \right\} 
= \sum\limits_{k} x[k] \mathcal{F} \left\{ \delta(t-kT_{\mathrm{s}}) \right\}
= \sum\limits_{k} s(kT_{\mathrm{s}}) \e^{-\J 2 \pi f k T_{\mathrm{s}}}
$$
另一方面，
$$
\begin{align}
\t{S}(f) &= \mathcal{F}\left\{ s(t) \sum\limits_{k} \delta(t-kT_{\mathrm{s}}) \right\} 
= \dfrac{1}{2\pi}S(f) * \mathcal{F}\left\{ \sum\limits_{k} \delta(t-kT_{\mathrm{s}}) \right\} \\
&= \dfrac{1}{T_{\mathrm{s}}} S(f) * \sum\limits_{k} \delta \left( f - k f_{\mathrm{s}} \right) \\
\end{align}
$$
因而需使用增益为 $T_{\mathrm{s}}$ 的**低通滤波器 (low-pass filter, LPF)** 截去 $\t{S}(f)$ 中 $|f| > W$ 的部分，才能恢复出 $S(f)$，输出即为
$$
\hat{S}(f) = \dfrac{1}{f_{\mathrm{s}}} \sum\limits_{k} s(kT_{\mathrm{s}}) \e^{-\J 2 \pi f k T_{\mathrm{s}}} \times \mathbb{1}_{|f| \leq W}
$$
其中 $\mathbb{1}_{P}$ 为事件 $P$ 的指示函数。由此，时域恢复的信源为
$$
\begin{align}
\hat{s}(t) &= \mathcal{F}^{-1}\left\{ \hat{S}(f) \right\} = \dint_{-\infty}^{+\infty} \hat{S}(f) \e^{\J 2 \pi f t} \dif f 
= \dint_{-W}^{W} \dfrac{1}{f_{\mathrm{s}}} \sum\limits_{k} s(kT_{\mathrm{s}}) \e^{-\J 2 \pi f k T_{\mathrm{s}}} \e^{\J 2 \pi f t} \dif f \\
&= \dfrac{1}{f_{\mathrm{s}}} \sum\limits_{k} s(kT_{\mathrm{s}}) \dint_{-W}^{W} \e^{\J 2 \pi f (t - kT_{\mathrm{s}})} \dif f 
= \sum\limits_{k} s(kT_{\mathrm{s}}) \dfrac{\sin (2\pi W(t-kT_{\mathrm{s}}))}{\pi f_{\mathrm{s}} (t-kT_{\mathrm{s}})}
\end{align}
$$
令抽样频率 $f_{\mathrm{s}} = 2W$ 取 Nyquist 频率，则
$$
\hat{s}(t) = \sum\limits_{k} s\left( \dfrac{k}{2W} \right) \sinc \left( 2Wt - k \right)
$$

> [!note] 抽样前的预滤波
> 实际采集到的真实信号一定是全频带的信号，为避免混叠 (aliasing) 干扰，通常先通过**预滤波器 (pre-filter)** 截去高频成分，保留期望频带内的信号，然后再进行抽样。
> 
> 人类的语音信号主要能量集中在 300  $\sim$ 3400 Hz，通常预滤波器的带宽为 3.4 kHz，抽样频率为 8 kHz。

## 量化与电平重建

**量化 (quantization)** 是将幅值连续的信号 $x[k]$ 离散化为数字信号 $\hat{x}[k]$ 的过程。设 $n$-bit 量化器 $Q$ 有 $L=2^{n}$ 个量化级别，则第 $i$ 个量化区间上
$$
Q(x) = y_{i}, \quad x \in (x_{i}, x_{i + 1}], \quad i = 1, 2, \cdots, L
$$
其中，$y_{i}$ 是**表示电平**，$x_{i}$ 是**分层电平**，$I_{i} = (x_{i}, x_{i+1}]$ 称为第 $i$ 个**量化区间 (quantization interval)**，其长度 $\varDelta_{i} = x_{i+1} - x_{i}$ 称为第 $i$ 个**量化间隔 (quantization step)**。当对每个 $i = 1, 2, \cdots, L$ 有 $\varDelta_{i} \equiv \varDelta$ 时，称为**均匀量化 (uniform quantization)**，否则称为**非均匀量化 (non-uniform quantization)**。

量化器 $Q$ 对输入 $x$ 的**量化误差 (quantization error)** 定义为
$$
e(x) = x - Q(x)
$$
因为 $x$ 可看作**随机变量 $X$**，$e(x)$ 也是随机变量。良好的量化器应使得 $\mathbb{E}\left[ e(X) \right] = 0$，此时其方差为
$$
\begin{align}
\sigma^{2} = \mathbb{E}\left[ e^{2}(X) \right] &= \dint_{-\infty}^{+\infty} (x - Q(x))^{2} p_{X}(x) \dif x \\
&= \sum\limits_{i=1}^{L} \dint_{x_{i}}^{x_{i+1}} (x - y_{i})^{2} p_{X}(x) \dif x
\end{align}
$$

> [!definition] 量化的均方误差
> 对量化器 $Q$，其量化误差的方差 
> $$
> \sigma^{2} = \mathbb{E}\left[ e^{2}(X) \right] = \sum\limits_{i=1}^{L} \dint_{x_{i}}^{x_{i+1}} (x - y_{i})^{2} p_{X}(x) \dif x
> $$
> 称为**量化的均方误差 (mean square error, MSE)**。

若信源 $x$ 超出量化器的表示范围 $[x_{1}, x_{L+1}]$，则会发生**过载失真 (saturation distortion)**，此时量化误差相当于将过载部分全部映射为 $y_{1}$ 或 $y_{L}$，量化误差可拆分为
$$
\sigma^{2} = \sigma^{2}_{\mathrm{q}} + \sigma^{2}_{\mathrm{o}}, \qquad
\begin{cases}
\sigma^{2}_{\mathrm{q}} = \sum\limits_{i=1}^{L} \dint_{x_{i}}^{x_{i+1}} (x - y_{i})^{2} p_{X}(x) \dif x, \\
\sigma^{2}_{\mathrm{o}} = \dint_{-\infty}^{x_{1}} (x - y_{1})^{2} p_{X}(x) \dif x + \dint_{x_{L+1}}^{\infty} (x - y_{L})^{2} p_{X}(x) \dif x
\end{cases}
$$

一般而言，功率较大的信源对量化噪声的容忍程度也比较高，因而我们可以引入量化器 $Q$ 的**信噪比 (signal-to-noise ratio, SNR)**，定义为
$$
\mathrm{SNR}_{\mathrm{q}} = \dfrac{\mathbb{E}\left[ X^{2} \right]}{\mathbb{E}\left[ e^{2}(X) \right]} = \dfrac{\dint_{-\infty}^{\infty} x^{2} p_{X}(x) \dif x}{\sum\limits_{i=1}^{L} \dint_{x_{i}}^{x_{i+1}} (x - y_{i})^{2} p_{X}(x) \dif x}
$$

### 均匀量化

对于均匀量化器，量化间隔 $\varDelta_{i} \equiv \varDelta$，且通常取表示电平为区间中点
$$
y_{i} = \dfrac{x_{i} + x_{i+1}}{2}, \qquad i = 1, 2, \cdots, L
$$
**均匀量化一定限制在有限范围 $[x_\mathrm{min}, x_\mathrm{max}]$ 内**，量化区间长度为 $\varDelta = \cfrac{x_{\mathrm{max}}-x_{\mathrm{min}}}{L}$。我们常令 $x_{\mathrm{min}} = -V$，$x_{\mathrm{max}} = V$，则 $\varDelta = \cfrac{2V}{L}$。

若假设量化输入 $X$ 均匀分布于 $[-V, V]$，则**量化噪声**为
$$
\sigma^{2} = \dfrac{L}{2V} \dint_{-\varDelta/2}^{\varDelta/2} x^{2} \dif x = \dfrac{\varDelta^{2}}{12} = \dfrac{(2V)^{2}}{12 L^{2}} = \dfrac{V^{2}}{3 \cdot 4^{n}}
$$
因此量化器的**信噪比**为
$$
\mathrm{SNR}_{\mathrm{q}} = \dfrac{\mathbb{E}\left[ X^{2} \right]}{\sigma^{2}} = \cfrac{\dint_{-V}^{V} x^{2} \cdot \dfrac{1}{2V} \dif x}{\dfrac{V^{2}}{3 \cdot 4^{n}}} = \dfrac{V^{2}/3}{V^{2}/(3 \cdot 4^{n})} = 4^{n} \approx 6.02 n \rmu{dB}
$$
即每增加 1 bit 的量化精度，信噪比提高约 6.02 dB。

**均匀量化对均匀分布最优。**

### 非均匀量化

#### 非均匀量化器的设计

非均匀量化器的设计目标是**最小化量化误差的均方值**，即求
$$
\arg\limits_{\{ x_{i} \}, \{ y_{i} \}}\min \sigma^{2} = \arg\limits_{\{ x_{i} \}, \{ y_{i} \}}\min \sum\limits_{i=1}^{L} \dint_{x_{i}}^{x_{i+1}} (x - y_{i})^{2} p_{X}(x) \dif x
$$

+ 对 $x_{i}$ 求偏导，得
$$
\dfrac{\partial \sigma^{2}}{\partial x_{i}} = (x_{i} - y_{i})^{2} p_{X}(x_{i}) - (x_{i} - y_{i-1})^{2} p_{X}(x_{i}) = 0
\quad \Longrightarrow \quad
x_{i} = \dfrac{y_{i} + y_{i-1}}{2}
$$
由此导出**最近邻居准则**：每个分层电平 $x_{i}$ 应取为相邻两个表示电平 $y_{i-1}$ 和 $y_{i}$ 的中点，这**与 $x$ 的分布无关**。

+ 对 $y_{i}$ 求偏导，得
$$
\dfrac{\partial \sigma^{2}}{\partial y_{i}} = -2 \dint_{x_{i}}^{x_{i+1}} (x - y_{i}) p_{X}(x) \dif x = 0
\quad \Longrightarrow \quad
y_{i} = \dfrac{\dint_{x_{i}}^{x_{i+1}} x p_{X}(x) \dif x}{\dint_{x_{i}}^{x_{i+1}} p_{X}(x) \dif x}
$$
由此导出**重心准则**：每个表示电平 $y_{i}$ 应取为对应量化区间内 $x$ 的条件期望，这**与 $x$ 的分布有关**。

> [!algo.] Lloyd-Max 算法 
> Lloyd-Max 算法综合考虑**最近邻居准则**和**重心准则**，通过迭代优化非均匀量化器的分层电平 $\{ x_{i} \}$ 和表示电平 $\{ y_{i} \}$。
> 
> ---
> 
> **GIVEN —** 
> 初始表示电平 $y_1^{(0)} < y_2^{(0)} < \cdots < y_L^{(0)}$
> 
> **REPEAT —**
> 1. 更新分层电平：
> $$
> x_{i}^{(k)} = \dfrac{y_{i}^{(k)} + y_{i+1}^{(k)}}{2}, \quad i = 1, 2, 3, \cdots, L-1
> $$
> 2. 更新表示电平：
> $$
> y_{i}^{(k+1)} = \dfrac{\dint_{x_{i-1}^{(k)}}^{x_{i}^{(k)}} x p_{X}(x) \dif x}{\dint_{x_{i-1}^{(k)}}^{x_{i}^{(k)}} p_{X}(x) \dif x}, \quad i = 1, 2, 3, \cdots, L
> $$
> 
> 　**UNTIL —** 量化噪声 $\sigma_{(k+1)}^{2}$ 小于预设阈值
> 
> **OUTPUT —**
> 最终分层电平 $\{ x_{i}^{*} \}$ 和表示电平 $\{ y_{i}^{*} \}$

#### 压扩量化

对于幅值分布高度集中的信源，如语音信号，其幅值通常服从 **Laplace 分布**或 **Gauss 分布**，均匀量化器难以取得较好的量化效果。注意到**非线性映射**可以改变随机变量的分布形状，因此可以先对信源进行**压扩 (companding)** 处理，再进行均匀量化，从而达到非均匀量化的效果。

#### 高分辨率量化

当量化级数 $L$ 很大时，量化间隔 $\varDelta_{i}$ 很小，可以近似认为在量化区间 $I_{i} = (x_{i}, x_{i+1}]$ 上，信源概率密度函数 $p_{X}(x)$ 近似为常数 $p_{X}(x_{i}^{*})$，其中 $x_{i}^{*} \in I_{i}$。此时，量化噪声可近似为
$$
\sigma^{2} \approx \sum\limits_{i=1}^{L} p_{X}(x_{i}^{*}) \dint_{x_{i}}^{x_{i+1}} (x - y_{i})^{2} \dif x = \sum\limits_{i=1}^{L} p_{X}(x_{i}^{*}) \dfrac{\varDelta_{i}^{3}}{12}
$$
由 Lagrange 中值定理，可取 $p_{X}(x_{i}^{*}) = \cfrac{1}{\varDelta_{i}} \dint_{x_{i}}^{x_{i+1}} p_{X}(x) \dif x = \cfrac{P_{i}}{\varDelta_{i}}$，从而
$$
\sigma^{2} \approx \dfrac{1}{12} \sum\limits_{i=1}^{L} P_{i} \varDelta_{i}^{2} \stackrel{\varDelta_{i} \equiv \varDelta}{=\!=\!=} \dfrac{\varDelta^{2}}{12}
$$
对其做无损压缩，最小码长为
$$
\begin{align} 
H(Q(X)) &= - \sum\limits_{i=1}^{L} \left( p_{X}(x_{i}^{*}) \varDelta \right) \log \left( p_{X}(x_{i}^{*}) \varDelta \right) \\
&= - \sum\limits_{i=1}^{L} p_{X}(x_{i}^{*}) \varDelta \log p_{X}(x_{i}^{*}) - \sum\limits_{i=1}^{L} p_{X}(x_{i}^{*}) \varDelta \log \varDelta  \\
&= - \dint_{-\infty}^{+\infty} p_{X}(x) \log p_{X}(x) \dif x - \log \varDelta  \\
&= h(X) - \log \varDelta \approx h(X) - \log \sigma - 1.8
\end{align}
$$
其中 $h(X) = - \dint_{-\infty}^{+\infty} p_{X}(x) \log p_{X}(x) \dif x$ 是信源 $X$ 的**[[#信源#连续信源的微分熵|微分熵]]**。




# 数字调制

## 数字调制概论

我们希望在实际物理信道中有效、可靠地传输 0/1 比特。为此，需要将离散的数字信号映射为适合物理信道传输的连续幅值信号，这一过程称为**数字调制 (digital modulation)**。

数字调制要解决的问题有：
+ 0/1 比特的**逻辑量**需要映射为适合物理信道传输的**物理量**，如电压、电流、电磁波等；
+ 映射后的信号需要适应物理信道的**带宽**、**噪声**限制，避免信号失真和误码；
+ 映射方案需要考虑**频谱效率**、**功率效率**等性能指标，提升通信系统的整体性能。

![[数字调制的基本结构.png|数字调制的基本结构]]


# 电平信道

## 电平信道的建模

电平信道是[[#数字调制]]过程中**电平映射后**至**最佳判决前**的环节，输入 $x_{k}$ 时间离散、幅值离散，输出 $y(t)$ 时间离散、幅值连续。

假定信道无记忆，电平信道可以建模为**条件概率分布 $p(y \mid x)$**，表示在输入电平 $x$ 时输出电平 $y$ 的概率密度函数 (PDF)。

> [!example] 加性白 Gauss 噪声电平信道
> **加性白 Gauss 噪声 (Additive White Gaussian Noise, AWGN) 电平信道**是一种常见的电平信道模型，其输入输出关系为
> $$
> y = x + z, \qquad \text{其中} \quad z \sim \mathcal{N}(0, \sigma^{2})
> $$
> 即输出电平 $y$ 是输入电平 $x$ 与高斯白噪声 $z$ 的和。对应的条件概率密度函数为
> $$
> p(y \mid x) = \dfrac{1}{\sqrt{2 \pi \sigma^{2}}} \exp\left( -\dfrac{(y - x)^{2}}{2 \sigma^{2}} \right)
> $$
^2d771b

## 二进制电平传输

本课程中，一律假设信源编码的输出比特 0/1 等概分布，即遵循**最优信源编码**的先验假设。若约定传输「0」时映射为电平 $-A$，传输「1」时映射为电平 $+A$，则输入电平 $x$ 的概率分布为
$$
p(A) = p(-A) = \dfrac{1}{2}
$$
这里简记 $p(A) = \mathrm{Pr} \{x = A\}$，$p(-A) = \mathrm{Pr} \{x = -A\}$。

这样，对于给定的电平信道 $p(y \mid x)$，可以计算输出 $y$ 的分布为
$$
p(y) = p(y \mid A) p(A) + p(y \mid -A) p(-A) 
$$
如对上述[[#^2d771b|加性白 Gauss 噪声电平信道]]，有
$$
\begin{align} 
p(y) &= \dfrac{1}{2} \dfrac{1}{\sqrt{2 \pi \sigma^{2}}} \exp\left( -\dfrac{(y - A)^{2}}{2 \sigma^{2}} \right) + \dfrac{1}{2} \dfrac{1}{\sqrt{2 \pi \sigma^{2}}} \exp\left( -\dfrac{(y + A)^{2}}{2 \sigma^{2}} \right)  \\
&= \dfrac{1}{2 \sqrt{2 \pi \sigma^{2}}} \left[ \exp\left( -\dfrac{(y - A)^{2}}{2 \sigma^{2}} \right) + \exp\left( -\dfrac{(y + A)^{2}}{2 \sigma^{2}} \right) \right]
\end{align}
$$

### 最佳判决

由于一般的信道（如上述[[#^2d771b|加性白 Gauss 噪声电平信道]]）上噪声是随机的，电平信道的输出也是随机的，而且
$$
\forall y \in \mathbb{R}, \quad p(y \mid A) > 0, \quad p(y \mid -A) > 0
$$
因此，需要一种准则在电平信道输出 $y$ 处进行**最佳判决 (optimal decision)**，即根据观测到的 $y$ 判定发送的是「0」还是「1」，以最小化**误码率 (bit error rate, BER)**。

#### 最大后验概率判决准则

直观上，对于观测到的输出电平 $y$，如果给出 $y$ 的条件为 $+A$ 的概率更大，则判定发送的是「1」；如果给出 $y$ 的条件为 $-A$ 的概率更大，则判定发送的是「0」。这一直观准则可以形式化为**最大后验概率 (maximum a posteriori, MAP) 判决准则**：
$$
\mark{ \hat{x} = \arg\limits_{x \in \{ -A, +A \}}\max \mathrm{Pr}\{x \mid y\} }
$$

#### 最大似然判决准则

由 **Bayes 公式**，有 $\mathrm{Pr}\{x = A \mid y\} = \dfrac{p(y \mid A) p(A)}{p(y)}$，$\mathrm{Pr}\{x = -A \mid y\} = \dfrac{p(y \mid -A) p(-A)}{p(y)}$，而有**等概条件** $p(A) = p(-A)$，因此 MAP 判决准则等价于
$$
\mark{ p(y \mid A) \mathop\gtrless\limits_{\hat{x}=-A}^{\hat{x}=A} p(y \mid -A) }
$$
即**最大似然 (maximum likelihood, ML) 判决准则**。

#### 最小 Euclid 距离判决准则

对上述[[#^2d771b|加性白 Gauss 噪声电平信道]]，据 ML 判决准则有：
+ $y = 0$ 时，$p(y \mid A) > p(y \mid -A)$，判决 $\hat{x} = A$；
+ $y = 0$ 时，$p(y \mid A) < p(y \mid -A)$，判决 $\hat{x} = -A$。

因此，可以得到**最佳判决阈值 (optimal decision threshold)** 为 0，即
$$
\hat{x} = \begin{cases}
+A, & y \geq 0 \\
-A, & y < 0
\end{cases}
$$
即对于 AWGN 电平信道，ML 判决准则成为**最小 (Euclid) 距离 (minimum Euclidean distance, MED) 判决准则**，分别称 $y < 0$ 和 $y > 0$ 为判决到 $\hat{x} = -A$ 和 $\hat{x} = +A$ 的**判决域 (decision region)**。

### 误符号率

设实际发送的电平为 $x$，最佳判决的输出为 $\hat{x}$，则**误符号率 (symbol error rate, SER)** 定义为
$$
P_{\mathrm{s}} = \mathrm{Pr}\{ \hat{x} \neq x \}
$$
对于上述[[#^2d771b|加性白 Gauss 噪声电平信道]]，误符号率为
$$
\begin{align}
P_{\mathrm{s}} &= \mathrm{Pr}\{ \hat{x} \neq x \} \\
&= p(A) \mathrm{Pr}\{ y<0 \mid x = A \} + p(-A) \mathrm{Pr}\{ y > 0 \mid x = -A \} \\
&= \dfrac{1}{2} \int_{-\infty}^{0} \dfrac{1}{\sqrt{2 \pi \sigma^{2}}} \e^{-\tfrac{(y - A)^{2}}{2 \sigma^{2}}} \dif y + \dfrac{1}{2} \int_{0}^{+\infty} \dfrac{1}{\sqrt{2 \pi \sigma^{2}}} \e^{-\tfrac{(y + A)^{2}}{2 \sigma^{2}}} \dif y \\
&= \dfrac{1}{2} \dint_{A}^{+\infty} \dfrac{1}{\sqrt{2 \pi \sigma^{2}}} \e^{-\tfrac{y^{2}}{2 \sigma^{2}}} \dif y + \dfrac{1}{2} \int_{A}^{+\infty} \dfrac{1}{\sqrt{2 \pi \sigma^{2}}} \e^{-\tfrac{y^{2}}{2 \sigma^{2}}} \dif y \\
&= \int_{A}^{+\infty} \dfrac{1}{\sqrt{2 \pi \sigma^{2}}} \e^{-\tfrac{y^{2}}{2 \sigma^{2}}} \dif y 
= \dint_{A/\sigma}^{+\infty} \dfrac{1}{\sqrt{2 \pi}} \e^{-\tfrac{y^{2}}{2}} \dif y
\end{align}
$$
积分 $\dint_{u}^{+\infty} \dfrac{\e^{-t^{2}/2}}{\sqrt{ 2\pi }} \dif t$ 没有初等函数表达式，通常用 **Q 函数** $Q(u)$ 表示，即上面的误符号率为
$$
P_{\mathrm{s}} = Q\left( \dfrac{A}{\sigma} \right)
$$

为讨论方便，使用信息承载符号的**二阶矩** $\sigma^{2}_{x} = \mathbb{E} \left[ x^{2} \right]$ 表示信号功率，则对于二进制电平信道，有 $\sigma^{2}_{x} = A^{2}$。定义**信噪比 (signal-to-noise ratio, SNR)** 为
$$
\mathrm{SNR} = \dfrac{\sigma^{2}_{x}}{\sigma^{2}} = \dfrac{A^{2}}{\sigma^{2}}
$$
则**误符号率**为
$$
P_{\mathrm{s}} = Q\left( \dfrac{\sigma_{x}}{\sigma} \right) = Q\left( \sqrt{\mathrm{SNR}} \right)
$$

## 多进制实电平传输

在二进制电平传输中，一个电平一次传输仅承载 1 个 bit 的信息。为了提高频谱效率，可以扩大电平值 $x$ 的取值集合，采用**多进制实电平传输**。

### 多进制电平信道的构造

设电平信道每个符号承载 $n$ 个 bit 信息，则电平信道的输入 $x$ 需要取 $M = 2^{n}$ 个不同的实数值，即 **$M$ 进制传输**。由于一个符号承载 $n = \log_{2}M$ 个 bit 信息，因此考虑对 $x$ 的二阶矩**相对承载 bit 数归一化**，定义
$$
\t{\sigma}^{2}_{x} = \dfrac{\sigma^{2}_{x}}{ \log_{2} M }= \dfrac{\mathbb{E} \left[ x^{2} \right] }{ \log_{2} M }
$$
本课程中，不考虑非 2 的整数次幂的 $M$。

为简化分析，通常采用**等间距电平**，即电平集合为
$$
\begin{align} 
\mathscr{A} = \{ -(M-1)A, -(M-3)A, \cdots, -3A, -A, \\
A, 3A, \cdots, (M-3)A, (M-1)A \} 
\end{align}
$$
$\mathscr{A}$ 中相邻两个电平的距离均为 $2A$，且电平关于 0 对称分布。

> [!example] 多进制电平的编码
> 对每个电平编码时，通常采用 **Gray 编码**，使得相邻电平仅有 1 bit 不同，以降低误码率。
> 
> 例如，$M=4$ 时，电平集合为 $\mathscr{A} = \{ -3A, -A, A, 3A \}$，可以采用如下 Gray 编码：
> 
> | 电平 $x$ | $-3A$ | $-A$ | $A$ | $3A$ |
> | :--- | :--- | :--- | :--- | :--- |
> | Gray 码 | 00 | 01 | 11 | 10 |
> 
> $M=8$ 时，电平集合为 $\mathscr{A} = \{ -7A, -5A, -3A, -A, A, 3A, 5A, 7A \}$，可以采用如下 Gray 编码：
> 
> | 电平 $x$ | $-7A$ | $-5A$ | $-3A$ | $-A$ | $A$ | $3A$ | $5A$ | $7A$ |
> | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
> | Gray 码 | 000 | 001 | 011 | 010 | 110 | 111 | 101 | 100 |

### 最佳判决

对于多进制电平信道，最佳判决仍然从**最大后验概率 (MAP) 判决准则**出发，认为
$$
\begin{align}
\hat{x} &= \arg\limits_{x \in \mathscr{A}} \max p(x \mid y)  &\text{（MAP 准则）} \\
&= \arg\limits_{x \in \mathscr{A}} \max \dfrac{p(y \mid x) p(x)}{p(y)} = \arg\limits_{x \in \mathscr{A}} \max p(y \mid x) p(x)  \\
&\stackrel{\text{等概假设}}{=\!=\!=\!=\!=\!=} \arg\limits_{x \in \mathscr{A}} \max p(y \mid x)  &\text{（ML 准则）} \\
&\stackrel{\text{AWGN}}{=\!=\!=\!=\!=} \arg\limits_{x \in \mathscr{A}} \max \dfrac{1}{\sqrt{2 \pi \sigma^{2}}} \exp\left( -\dfrac{(y - x)^{2}}{2 \sigma^{2}} \right) \\
&= \arg\limits_{x \in \mathscr{A}} \min (y - x)^{2}  &\text{（MED 准则）}
\end{align}
$$
即在输入遵循**最优信源编码**的**等概**先验、信道为 AWGN 电平信道的条件下，MAP 准则可逐步化归到 ML 和 MED 准则。根据 MED 准则，最佳判决即为选择与输出电平 $y$ 距离最近的输入电平 $x \in \mathscr{A}$，因此**判决门限**在
$$
\begin{align} 
&\left\{ \dfrac{(x_{i} + x_{i+1})}{2} \,\Bigg|\, x_{i}, x_{i+1} \in \mathscr{A}, i = 1, 2, \cdots, M-1 \right\} \\
&= \{ - (M-2)A, - (M-4)A, \cdots, -2A, \\
&\hspace{2em} 0, 2A, \cdots, (M-4)A, (M-2)A \} 
\end{align}
$$

### 差错分析

#### 误符号率

对 $M$ 进制传输，电平与判决门限之间的距离仍为 $A$，但不同于[[#二进制电平传输#误符号率|二进制情形]]的是，**中间 $(M - 2)$ 个输入电平有两个方向可能判错**，因此误符号率为
$$
\begin{align}
P_{\mathrm{s}} &= \sum\limits_{x \in \mathscr{A}} p(x) \mathrm{Pr}\{ \hat{x} \neq x \mid x \} \\
&= 2 \times \dfrac{1}{M} \times Q\left( \dfrac{A}{\sigma} \right) + (M - 2) \times \dfrac{1}{M} \times 2 Q\left( \dfrac{A}{\sigma} \right) \\
&= \dfrac{2(M - 1)}{M} Q\left( \dfrac{A}{\sigma} \right)
\end{align}
$$
与[[#二进制电平传输#误符号率|二进制情形]]类似，定义**信噪比 (SNR)** 为
$$
\mathrm{SNR} = \dfrac{\sigma^{2}_{x}}{\sigma^{2}} = \dfrac{\mathbb{E} \left[ x^{2} \right]}{\sigma^{2}} = \dfrac{1}{\sigma^{2}} \dfrac{(M^{2} - 1) A^{2}}{3}
$$
即 $\cfrac{A}{\sigma} = \sqrt{ \cfrac{3}{M^{2} - 1} \mathrm{SNR} }$，则误符号率为
$$
P_{\mathrm{s}} = \dfrac{2(M - 1)}{M} Q\left( \sqrt{ \dfrac{3}{M^{2} - 1} \mathrm{SNR} } \right)
$$

#### 误 bit 率

当 $M$ 很大时，近似取
$$
P_{\mathrm{s}} \approx 2 Q\left( \sqrt{ \dfrac{3}{M^{2} - 1} \mathrm{SNR} } \right)
$$
误符号率 $P_{\mathrm{s}}$ 并不能直接反映通信系统的性能，因为每个符号承载 $n = \log_{2} M$ 个 bit 信息，需要计算**误 bit 率 (bit error rate, BER)** $P_{\mathrm{b}}$。在 Gray 编码下，可认为只有相邻电平之间的判决错误才会导致误 bit，因此近似有
$$
P_{\mathrm{b}} \approx \dfrac{P_{\mathrm{s}}}{\log_{2} M} \approx \dfrac{2}{\log_{2} M} Q\left( \sqrt{ \dfrac{3}{M^{2} - 1} \mathrm{SNR} } \right)
$$
逐 bit 意义下，信噪比 $\mathrm{SNR} = \cfrac{\sigma_{x}^{2}}{\sigma^{2}}$ 替换为**归一化信噪比 (normalized SNR)** $\cfrac{\t{\sigma}_{x}^{2}}{\sigma^{2}}$，即
$$
P_{\mathrm{b}} \approx \dfrac{2}{\log_{2} M} Q\left( \sqrt{ \dfrac{3 \log_{2} M}{M^{2} - 1} \dfrac{\t{\sigma}_{x}^{2}}{\sigma^{2}} } \right)
$$

一般地，保留原始误符号率表达式，有
$$
P_{\mathrm{b}} \approx \dfrac{P_{\mathrm{s}}}{\log_{2} M} = \dfrac{2(M - 1)}{M \log_{2} M} Q\left( \sqrt{ \dfrac{3}{M^{2} - 1} \mathrm{SNR} } \right)
$$

## 复电平传输

复电平传输是将信息映射为**复数域**的电平信号进行传输，以提高频谱效率和抗干扰能力。复电平信道的输入 $x = x_{\mathrm{I}} + \J x_{\mathrm{Q}}$ 和输出 $y = y_{\mathrm{I}} + \J y_{\mathrm{Q}}$ 均为复数。

> [!note] 复电平实部、虚部分量的下标含义
> 在通信领域，对复数信号值通常使用下标 $\mathrm{I}$、$\mathrm{Q}$ 而不是 $x$、$y$ 或 $\mathrm{r}$、$\mathrm{i}$，其中 $\mathrm{I}$ 表示**同相分量 (in-phase component)**，$\mathrm{Q}$ 表示**正交分量 (quadrature component)**。

考虑 AWGN 复电平信道，输入输出关系为
$$
y = x + z, \qquad \text{其中} \quad z = z_{\mathrm{I}} + \J z_{\mathrm{Q}} \sim \mathcal{CN}(0, 2\sigma^{2})
$$
即输出电平 $y$ 是输入电平 $x$ 与**复 Gauss 白噪声 $z$** 的和，$z$ 满足
$$
p(z_{\mathrm{I}}, z_{\mathrm{Q}}) = \dfrac{1}{2 \pi \sigma^{2}} \exp\left( -\dfrac{z_{\mathrm{I}}^{2} + z_{\mathrm{Q}}^{2}}{2 \sigma^{2}} \right)
$$
类似于实 AWGN 电平信道，复 AWGN 电平信道的 MAP 判决仍然等价到**最小 Euclid 距离 (MED) 判决准则**，即选择与输出电平 $y$ 距离最近的输入电平 $x \in \mathscr{A}$。

### QAM 输入的分析

考虑复电平信道的输入 $x$ 取自
$$
\begin{align} 
\mathscr{A} = \{ x_{\mathrm{I}} + \J x_{\mathrm{Q}} \mid x_{\mathrm{I}}, x_{\mathrm{Q}} \in \{ -(L - 1)A, -(L - 3)A, \cdots, -A,  \\
A, \cdots, (L - 3)A, (L - 1)A \} \} 
\end{align}
$$
实轴、虚轴均取 $L$ 个等间距电平，共有 $M = L^{2}$ 个复电平。由于这种信源电平分布来自于**正交振幅调制 (quadrature amplitude modulation, QAM)**，因此称为 **$M$-QAM 星座图**。

由于复 Gauss 白噪声的实部和虚部相互独立，分别服从均值为 0、方差为 $\sigma^{2}$ 的 Gauss 分布，因此复 AWGN 电平信道可视为两路独立的**实 AWGN 电平信道**的组合，恰对应于实轴和虚轴的 $L$ 进制电平传输。

两路信道相互独立，出现差错的情况是**任意一路实 AWGN 电平信道出现差错**。因此，信道的误符号率为
$$
\begin{align}
P_{\mathrm{s}} &= 1 - \mathrm{Pr}\{ \hat{x}_{\mathrm{I}} = x_{\mathrm{I}} \} \times \mathrm{Pr} \{ \hat{x}_{\mathrm{Q}} = x_{\mathrm{Q}} \} \\
&= 1 - \left( 1 - P_{\mathrm{s, I}} \right) (1 - P_{\mathrm{s, Q}}) 
= P_{\mathrm{s, I}} + P_{\mathrm{s, Q}} - P_{\mathrm{s, I}} P_{\mathrm{s, Q}}
\end{align}
$$
其中，$P_{\mathrm{s, I}}$ 和 $P_{\mathrm{s, Q}}$ 分别为实轴和虚轴 AWGN 电平信道的误符号率，均为
$$
P_{\mathrm{s, I}} = P_{\mathrm{s, Q}} = \dfrac{2(\sqrt{ M } - 1)}{\sqrt{ M }} Q\left( \dfrac{A}{\sigma} \right)
$$
直接忽略掉二次项 $P_{\mathrm{s, I}} P_{\mathrm{s, Q}}$，得到近似误符号率为
$$
P_{\mathrm{s}} \approx \dfrac{4(\sqrt{ M } - 1)}{\sqrt{ M }} Q\left( \dfrac{A}{\sigma} \right)
$$

输入电平的二阶矩为
$$
\sigma^{2}_{x} = \mathbb{E} \left[ |x|^{2} \right] = 2 \times \dfrac{(\sqrt{ M })^{2} - 1 }{3}A^{2} = \dfrac{2(M - 1)}{3} A^{2}
$$
仍定义**信噪比 (SNR)** 为 $\cfrac{\sigma^{2}_{x}}{\sigma^{2}}$，则有 $\dfrac{A}{\sigma} = \sqrt{ \dfrac{3}{2(M - 1)} \mathrm{SNR} }$，误符号率为
$$
P_{\mathrm{s}} \approx \dfrac{4(\sqrt{ M } - 1)}{\sqrt{ M }} Q\left( \sqrt{ \dfrac{3}{2(M - 1)} \mathrm{SNR} } \right)
$$
类似地，取 **Gray 映射**，近似误 bit 率为
$$
P_{\mathrm{b}} \approx \dfrac{4}{\log_{2} M} \left( 1 - \dfrac{1}{\sqrt{ M }} \right) Q\left( \sqrt{ \dfrac{3 \log_{2} M}{2(M - 1)} \dfrac{\t{\sigma}_{x}^{2}}{\sigma^{2}} } \right)
$$
当 $M$ 较大时，$P_{\mathrm{b}} \approx \dfrac{4}{\log_{2} M} Q\left( \sqrt{ \dfrac{3 \log_{2} M}{2(M - 1)} \dfrac{\t{\sigma}_{x}^{2}}{\sigma^{2}} } \right)$。

### PSK 输入的分析

另一种常见的复电平传输需求来自**相移键控 (phase shift keying, PSK)**，其输入电平取自
$$
\mathscr{A} = \{ A \e^{\J 2 \pi k / M} \mid k = 0, 1, \cdots, M - 1 \}
$$
均匀分布在以原点为中心、半径为 $A$ 的圆周上，幅角差为 $\theta = \cfrac{2\pi}{M}$。由于 PSK 星座图的输入电平**模长相同**，因此输入电平的二阶矩为 $\sigma^{2}_{x} = A^{2}$，信噪比为 $\mathrm{SNR} = \cfrac{A^{2}}{\sigma^{2}}$。

对于 PSK 星座图，MED 判决给出的**判决门限**为相邻复电平之间的角平分线，判决域张角为 $\theta$。由**对称性**，其差错分析只用分析任一个电平的差错概率，我们选 $x = A$ 进行分析。设判决输出为 $\hat{x}$，则误符号率为
$$
\begin{align}
P_{\mathrm{s}} &= \mathrm{Pr}\{ \hat{x} \neq A \mid x = A \}  \\
&= \mathrm{Pr}\left\{ \arg(A + z) > \dfrac{\theta}{2} = \dfrac{\pi}{M} \,\Bigg|\, x = A \right\}
\end{align}
$$
求解比较困难。考虑 $M$ 较大、$\cfrac{A}{\sigma}$ 较大的情形，可近似认为 $x = A$ 点附近的判决域边界为两条**平行直线**，此时**只有 $z_{\mathrm{Q}}$ 引起差错**，因此有近似误符号率为
$$
\begin{align}
P_{\mathrm{s}} &\approx 2 \times \mathrm{Pr}\left\{ z_{\mathrm{Q}} > A \sin \dfrac{\pi}{M} \right\} = 2 Q\left( \cfrac{A \sin \dfrac{\pi}{M}}{\sigma} \right) \\
&= 2 Q\left( \sin \dfrac{\pi}{M} \sqrt{\mathrm{SNR}} \right)
\end{align}
$$
类似地，取 **Gray 映射**，近似误 bit 率为
$$
P_{\mathrm{b}} \approx \dfrac{2}{\log_{2} M} Q\left( \sin \dfrac{\pi}{M} \sqrt{ \log_{2} M \cdot \dfrac{\t{\sigma}_{x}^{2}}{\sigma^{2}} } \right)
\approx \dfrac{2}{\log_{2} M} Q\left( \dfrac{\pi}{M} \sqrt{ \log_{2} M \cdot \dfrac{\t{\sigma}_{x}^{2}}{\sigma^{2}} } \right)
$$


# 波形信道

## 波形传输

电平是一个物理量，但不能脱离物理实体存在。在通信系统中，**电平**通常通过**波形**来传输，因此需要将[[#电平信道]]延伸到**波形信道**。

### 波形映射

将离散的电平映射到连续的波形上的过程称为**波形映射**。常见的波形映射方式有：
+ **脉冲振幅调制（PAM）**：将不同的电平映射为不同幅度的脉冲信号。
+ **频移键控（FSK）**：将不同的电平映射为不同频率的正弦波。
+ **相移键控（PSK）**：将不同的电平映射为不同相位的正弦波。
+ **正交振幅调制（QAM）**：结合幅度和相位的变化来表示不同的电平。
+ **正交频分复用（OFDM）**：将数据分散到多个正交的子载波上进行传输。

本课程专注于**线性调制 (linear modulation)**，即通过线性调幅一个**成形脉冲 (shaping pulse)** $p(t)$ 来实现波形映射。传输电平为 $x$ 的符号时，对应的波形为
$$
x(t) = x p(t)
$$
其中，$p(t)$ 是**归一化**的成形脉冲，满足
$$
\int_{-\infty}^{+\infty} p^{2}(t) \dif t = 1
$$
这样，传输一个符号的能耗即为
$$
E_{s} = \mathbb{E} \left[ \int_{-\infty}^{+\infty} x^{2}(t) \dif t \right]  = \mathbb{E} \left[ x^{2} \right] \dint_{-\infty}^{+\infty} p^{2}(t) \dif t = \mathbb{E} \left[ x^{2} \right] = \sigma^{2}_{x}
$$

### 波形信道模型

本课程重点关注**加性白 Gauss 噪声**对数字通信的影响，因此引入如下波形信道模型：

> [!def.] 加性白 Gauss 噪声波形信道
> 波形信道的输入为波形 $x(t)$，输出为波形 $y(t)$，满足
> $$
> y(t) = x(t) + z(t)
> $$
> 其中，$z(t)$ 是**白 Gauss 噪声 (white Gaussian noise)**，满足
> 1. 对任意时刻 $t$，$z(t)$ 服从均值为 0 的 Gauss 分布；
> 2. 对任意时刻序列 $t_{1}, t_{2}, \cdots, t_{n}$，随机变量组 $\{ z(t_{1}), z(t_{2}), \cdots, z(t_{n}) \}$ 服从均值为 $\v{0}$ 的 $n$ 元 Gauss 分布；
> 3. 功率谱密度函数 $S_{z}(f) \equiv \cfrac{n_{0}}{2}$，其中 $n_{0}$ 为常数。

## 二元波形的最佳接收

### 简单二元波形的最佳接收

考虑最简单的二元波形传输系统，传输的波形形式为
$$
x(t) = \begin{cases}
V, & t \in [0, T], & \text{传输「1」},  \\
-V, & t \in [0, T], & \text{传输「0」}
\end{cases}
$$
即取成形脉冲为矩形脉冲
$$
p(t) = \dfrac{1}{\sqrt{ T }}, \qquad t \in [0, T]
$$

#### 直接抽样的接收

尝试**直接抽样**接收波形 $y(t)$，注意到
$$
\mathbb{E} \left[ z^{2}(t_{i}) \right] = R_{z}(t_{i} - t_{i}) = \dfrac{n_{0}}{2} \delta(0) = +\infty
$$
因此，直接抽样接收的噪声功率为无穷大，显然不可行。

#### 区段积分的接收

观察 $p(t)$ 与 $z(t)$ 的波形特征，考虑通过**区段积分**的方式处理波形 $y(t)$，即计算
$$
y = \dint_{0}^{T} y(t) \dif t = \underbrace{ \dint_{0}^{T} x(t) \dif t }_{ x } + \underbrace{ \dint_{0}^{T} z(t) \dif t }_{ z \sim \mathcal{N}\left( 0, \tfrac{n_{0}T}{2} \right) }
$$
得到一个**等效电平信道**，其输入为**原来的符号电平 $x \in \left\{ VT, -VT \right\}$**，输出为等效输出电平 $y$，满足
$$
y = x + z
$$
其中，$z$ 服从均值为 0、方差为 $\cfrac{n_{0} T}{2}$ 的 Gauss 分布。这个电平信道的**信噪比**为
$$
\mathrm{SNR} = \dfrac{\sigma^{2}_{x}}{\sigma^{2}} = \dfrac{V^{2}T^{2}}{n_{0} T / 2} = \dfrac{V^{2} T}{n_{0} / 2}
$$

### 标准等价电平信道

对于上面[[#简单二元波形的最佳接收]]问题，我们希望能获得一个**最易于处理的等效电平信道**，于是考虑将噪声的方差固定为 $\cfrac{n_{0}}{2}$，这要求处理时
$$
y = \dfrac{1}{\sqrt{ T }} \dint_{0}^{T} y(t) \dif t = \dint_{0}^{T} y(t) \cdot \dfrac{1}{\sqrt{ T }} \dif t
= \dint_{0}^{T} y(t) \cdot p(t) \dif t 
$$
此时等效电平输入为 $x \in \left\{ V\sqrt{ T }, -V\sqrt{ T } \right\}$。

事实上，对于任意**能量归一化**成形脉冲 $p(t)$，都可以通过如下方式获得一个**标准等价电平信道**：
$$
y = \dint_{-\infty}^{+\infty} y(t) \cdot p(t) \dif t = \dint_{-\infty}^{+\infty} \left[ x(t) + z(t) \right] \cdot p(t) \dif t = x + z
$$
其中，$x = \dint_{-\infty}^{+\infty} x(t) \cdot p(t) \dif t$，$z = \dint_{-\infty}^{+\infty} z(t) \cdot p(t) \dif t \sim \mathcal{N}\left( 0, \cfrac{n_{0}}{2} \right)$。

由于 $p(t)$ 是归一化的，因此**等效电平信道的输入 $x$** 与**最初[[#波形映射]]时的符号电平 $x$** 相同，即信噪比为
$$
\mathrm{SNR} = \dfrac{\sigma^{2}_{x}}{\sigma^{2}} = \dfrac{E_{\mathrm{s}}}{n_{0} / 2}
$$

考虑使用任意能量归一化的 $g(t)$ 做类似的线性处理
$$
\hat{y} = \dint_{-\infty}^{+\infty} y(t) \cdot g(t) \dif t = \dint_{-\infty}^{+\infty} x(t) \cdot g(t) \dif t + \dint_{-\infty}^{+\infty} z(t) \cdot g(t) \dif t = \hat{x} + \hat{z}
$$
其中，仍有 $\hat{z} \sim \mathcal{N}\left( 0, \cfrac{n_{0}}{2} \right)$。由 **Cauchy-Schwarz 不等式**，这一处理的信噪比为
$$
\begin{align}
\widehat{\mathrm{SNR}} &= \dfrac{ \sigma^{2}_{\hat{x}} }{ \sigma^{2}_{\hat{z}} } = \dfrac{ \mathbb{E} \left[ \left( \dint_{-\infty}^{+\infty} x(t) \cdot g(t) \dif t \right)^{2} \right] }{ n_{0} / 2 } = \dfrac{\mathbb{E} \left[ x^{2} \right] \left( \dint_{-\infty}^{\infty} p(t)g(t) \dif t \right)^{2}}{n_{0} /2} \\
&= \dfrac{E_{\mathrm{s}}}{n_{0} / 2} \cdot \left( \dint_{-\infty}^{+\infty} p(t) g(t) \dif t \right)^{2}  \\
&\leq \dfrac{E_{\mathrm{s}}}{n_{0} / 2} \cdot \left( \dint_{-\infty}^{+\infty} p^{2}(t) \dif t \right) \left( \dint_{-\infty}^{+\infty} g^{2}(t) \dif t \right) = \dfrac{E_{\mathrm{s}}}{n_{0} / 2}
\end{align}
$$
因此，使用成形脉冲 $p(t)$ 进行线性处理可以获得最大的信噪比。

> [!thm.] 二进制波形传输的最佳接收
> 对于一般的二进制传输波形 $x(t) = xp(t)$（其中 **$x \in \{ -\sqrt{E_{\mathrm{s}}}, \sqrt{E_{\mathrm{s}}} \}$**，成形脉冲 $p(t)$ 满足**能量归一化**条件），在 AWGN 波形信道 $y(t) = x(t) + z(t)$ 上传输，其**最佳接收**处理为
> $$
> y = \dint_{-\infty}^{+\infty} y(t) \cdot p(t) \dif t = x + z
> $$
> 其中 $z \sim \mathcal{N}\left( 0, \cfrac{n_{0}}{2} \right)$，该等效电平信道的**信噪比**为 $\mathrm{SNR} = \cfrac{E_{\mathrm{s}}}{n_{0} / 2}$。
> 
> 对于任给的 $g(t)$，线性处理 $\hat{y} = \dint_{-\infty}^{+\infty} x(t) g(t) \dif t$ 的信噪比不超过 $\cfrac{E_{\mathrm{s}}}{n_{0}/2}$。
^ErjinzhiBoxinZuijiaJieshou

## 多进制波形的最佳接收

### 多进制标准等价电平信道

考虑一般的 $M$ 进制波形传输系统，传输的波形形式为
$$
x(t) = x p(t)
$$
其中，$x \in \mathscr{A}$ 来自 $M$ 进制[[#电平信道#多进制电平信道的构造|电平信道]]，$p(t)$ 为能量归一化的成形脉冲。

> [!thm.] 多进制波形传输的最佳接收
> 对于一般的 $M$ 进制传输波形 $x(t) = xp(t)$（其中 $x \in \mathscr{A}$，成形脉冲 $p(t)$ 满足**能量归一化**条件），在 AWGN 波形信道 $y(t) = x(t) + z(t)$ 上传输，其**最佳接收**处理为
> $$
> y = \dint_{-\infty}^{+\infty} y(t) \cdot p(t) \dif t = x + z
> $$
> 其中 $z \sim \mathcal{N}\left( 0, \cfrac{n_{0}}{2} \right)$，该等效电平信道的**信噪比**为 $\mathrm{SNR} = \cfrac{E_{\mathrm{s}}}{n_{0} / 2}$。

### 成形脉冲未归一化的情况

对于**未归一化**的成形脉冲 $p(t)$，不妨设 $p(t) = \sqrt{ E_{p} } \hat{p}(t)$ 且 $\hat{p}(t)$ 满足能量归一化条件，考虑使用相同的线性处理方式，则
$$
\begin{align} 
y &= \dint_{-\infty}^{+\infty} y(t) \cdot p(t) \dif t = \dint_{-\infty}^{+\infty} x(t) \cdot p(t) \dif t + \dint_{-\infty}^{+\infty} z(t) \cdot p(t) \dif t \\
&= x \dint_{-\infty}^{+\infty} p^{2}(t) \dif t + \dint_{-\infty}^{+\infty} z(t) \cdot p(t) \dif t \\
&= E_{p} x + z
\end{align}
$$
其中等价噪声电平
$$
z = \dint_{-\infty}^{+\infty} z(t) \cdot p(t) \dif t \sim \mathcal{N}\left( 0, \dfrac{n_{0}}{2} \dint_{-\infty}^{+\infty} p^{2}(t) \dif t  \right)
= \mathcal{N}\left( 0, \dfrac{n_{0}}{2} E_{p} \right)
$$
即该等效电平信道的**信噪比**为
$$
\mathrm{SNR} = \dfrac{ E_{p}^{2} \sigma^{2}_{x} }{ \left( n_{0} / 2 \right) E_{p} } = \dfrac{ E_{p} E_{\mathrm{s}} }{ n_{0} / 2 }
$$

## 最佳接收的实现

### 线性调制波形接收的实现

对于以**归一化**成形脉冲 $p(t)$ **线性调制**的波形传输系统，已知最佳接收处理为
$$
y = \dint_{-\infty}^{+\infty} y(t) \cdot p(t) \dif t
$$
除开使用**积分器**实现该处理外，还可以使用**匹配滤波器 (matched filter)** 实现为：

![[波形信道最佳接收 匹配滤波.png|使用滤波器实现最佳接收]]

其中，滤波器的冲激响应为 $p(-t)$，输出即为
$$
\t{y}(t) = y(t) * p(-t) = \dint_{-\infty}^{+\infty} y(\tau) p(-(t - \tau)) \dif \tau = \dint_{-\infty}^{+\infty} y(\tau) p(\tau - t) \dif \tau
$$
因此，在时刻 $t = 0$ 处抽样，即可得到最佳接收结果
$$
y = \t{y}(0) = \dint_{-\infty}^{+\infty} y(\tau) p(\tau) \dif \tau
$$

### 波形传输的收发联合模型

波形信道的发送端为
$$
x(t) = x p(t) = x\delta(t) * p(t)
$$
同样具有**滤波器**的实现形式。因此，可以把收发两端的滤波器形式放在一个视野中，得到如下**收发联合模型**：

![[波形信道最佳接收 收发联合.png|波形传输的收发联合模型]]

信号部分的整个传输过程同样是 LTI 系统，整体的冲激响应为
$$
h(t) = p(t) * p(-t)
$$
从频域来看，传输系统的频率响应为
$$
H(f) = \mathcal{F} \left\{ p(t) * p(-t) \right\} = P(f) \cdot P^{*}(f) = | P(f) |^{2}
$$

![[波形信道最佳接收 收发联合等效.png|波形传输的收发联合等效滤波器]]

### 成形脉冲与匹配脉冲的放缩

考虑使用一般的成形脉冲 $f(t)$ 和匹配脉冲 $g(t)$，接收处理为
$$
\begin{align} 
y &= \dint_{-\infty}^{+\infty} y(t) g(t) \dif t = \dint_{-\infty}^{+\infty} x(t) g(t) \dif t + \dint_{-\infty}^{+\infty} z(t) g(t) \dif t  \\
&= x \dint_{-\infty}^{+\infty} f(t) g(t) \dif t + \dint_{-\infty}^{+\infty} z(t) \cdot g(t) \dif t
\end{align}
$$

![[波形信道最佳接收 收发联合 不归一化.png]]

考虑**最佳接收**的条件，要求成形脉冲与匹配脉冲满足
$$
f(t) = \beta_{1} p(t), \qquad g(t) = \beta_{2} p(t)
$$
其中 $p(t)$ 满足**能量归一化**条件，$\beta_{1}, \beta_{2} > 0$。此时，**等效电平信道**为
$$
y = \beta_{1} \beta_{2} x + z, \qquad z \sim \mathcal{N}\left( 0, \dfrac{n_{0}}{2} \beta_{2}^{2} \right)
$$
其**信噪比**为
$$
\mathrm{SNR} = \cfrac{ \beta_{1}^{2} \beta_{2}^{2} \sigma^{2}_{x} }{ \dfrac{n_{0}}{2} \beta_{2}^{2} } = \dfrac{ \beta_{1}^{2} \sigma_{x}^{2} }{ n_{0} / 2 }
$$
因此，**成形脉冲的放缩系数 $\beta_{1}$ 决定了信噪比的高低**，而匹配脉冲的放缩系数 $\beta_{2}$ 则不会影响信噪比。

若只给定等效系统的 $h(t)$ 或 $H(f)$，有
$$
\dint_{-\infty}^{+\infty} H(f) \dif f = h(0) = \dint_{-\infty}^{+\infty} f(\tau) g(\tau) \dif \tau = \beta_{1} \beta_{2}
$$
当可**确定 $f(t) = g(t)$** 时，即知 $\beta_{1} = \sqrt{ h(0) } = \sqrt{ \dint_{-\infty}^{+\infty} H(f) \dif f }$，可由此确定信噪比；否则，只能确定波形能量与电平能量的比值。

# 载波传输

## 无失真传输的 Nyquist 准则

我们会在一个[[#波形信道]]上**前后传输多个符号**，因此希望**前后符号之间互不干扰**。考虑在收发联合模型中传输一系列符号 $\left\{ x_{k} \right\}$，符号调制的冲激串 $\sum\limits_{k=-\infty}^{\infty} x_{k} \delta(t - kT)$ 间隔为 $T$。

![[载波传输 收发联合等效.png|载波传输的收发联合等效模型]]

要满足**无失真传输 (distortion-free transmission)**，需要收发联合滤波器的冲激响应 $h(t)$ 满足
$$
h(kT) = \begin{cases}
1, & k = 0, \\
0, & k = \pm 1, \pm 2, \pm 3, \cdots
\end{cases}
$$
即**采样时刻** $t = kT$ 处，只有当前符号对输出有贡献，其他符号均无贡献。
^CaiyangdianWushizhenZhunze

> [!note] 离散点处有约束系统的讨论
> 对上述收发联合系统的约束仅在离散点 $t = kT$ 处，因此系统可以在其他时刻有任意响应形式，从而可以设计出满足该约束的多种成形脉冲 $p(t)$。
> 
> 为讨论其频域特征，我们对 $h(t)$ **加窗**，只关注约束部分的性质。由于约束部分为离散点，需使用**宽度趋近于 0 而增益趋于 $+\infty$** 的窗函数，即使用 **Dirac 梳状函数 (Dirac comb)** $W_{T}(t) = \sum\limits_{k=-\infty}^{\infty} \delta(t - kT)$ 加窗，得到
> $$
> h_{T}(t) = h(t) W_{T}(t) = \sum_{k=-\infty}^{\infty} h(kT) \delta(t - kT)
> $$

使用 Dirac 梳状函数 $W_{T}(t) = \sum\limits_{k=-\infty}^{\infty} \delta(t - kT)$ 加窗，得到
$$
h_{T}(t) = h(t) W_{T}(t) = \sum_{k=-\infty}^{\infty} h(kT) \delta(t - kT) = \delta(t)
$$
其频域特征为
$$
\begin{align} 
\mathscr{F} \left\{ h(t)W_{T}(t) \right\} &= H(f) * \mathscr{F} \left\{ W_{T}(t) \right\} = H(f) * \dfrac{1}{T} W_{1/T}(f) \\
&= \dfrac{1}{T} \sum_{n=-\infty}^{\infty} H\left( f - \dfrac{n}{T} \right) = 1
\end{align}
$$

> [!theorem] Nyquist 准则
> 要实现**无失真传输**，收发联合滤波器的频率响应 $H(f)$ 需满足
> $$
> \sum_{n=-\infty}^{\infty} H\left( f - nR_{\mathrm{s}} \right) = T
> $$
> 其中，$R_{\mathrm{s}} = \cfrac{1}{T_{\mathrm{s}}}$ 为**符号速率**，$T_{\mathrm{s}}$ 为符号发送的间隔时间；右侧一般取 $T = T_{\mathrm{s}}$，但也可以取其他值以调整系统增益。
^NyquistZhunze

> [!note] 因果传输
> 为确保因果性，我们对符号**延时 $T$ 后抽样**，即 Dirac 梳状函数加窗结果为
> $$
> h_{T}(t) = h(t) W_{T}(t) = \sum_{k=-\infty}^{\infty} h(kT) \delta(t - kT) = \delta(t - T)
> $$
> 其频域特征为
> $$
> \mathscr{F} \left\{ h(t)W_{T}(t) \right\} = H(f) * \dfrac{1}{T} W_{1/T}(f) = \dfrac{1}{T} \sum_{n=-\infty}^{\infty} H\left( f - \dfrac{n}{T} \right) = \e^{-\J 2 \pi f T}
> $$
> 因此，**[[#^NyquistZhunze|Nyquist 准则]]**改写为
> $$
> \sum_{n=-\infty}^{\infty} H\left( f - nR_{\mathrm{s}} \right) = T \cdot \e^{-\J 2 \pi f T}
> $$

### 带限波形信道的 Nyquist 准则

Nyquist 准则表明，为实现无失真传输，收发联合滤波器的频率响应 $H(f)$ 需满足其在频域上**以符号速率 $R_{\mathrm{s}}$ 为间隔周期重复**时，叠加结果为**常数** $T$。考虑 $H(f)$ 带限于 $|f| \le W$，则
+ 若 $R_{\mathrm{s}} > 2W$，则各周期不重叠，无法满足 Nyquist 准则；
+ 若 $R_{\mathrm{s}} = 2W$，则各周期在边界处相接，称为**临界速率 (critical rate)**，此时 $H(f)$ 须为理想低通滤波器；
+ 若 $R_{\mathrm{s}} < 2W$，则各周期之间有重叠的**过渡带**，存在多种满足 Nyquist 准则的 $H(f)$ 形式。

即，Nyquist 准则要求带限波形信道的**符号速率 $R_{\mathrm{s}}$ 不得超过信道带宽 $W$ 的两倍**，否则无法实现无失真传输。 ^DaixianBoxinXindaoNyquistZhunze

> [!def.] 频谱效率
> **频谱效率 (spectral efficiency)** 描述了在单位带宽内支持传输的信息量，定义为
> $$
> \eta = \dfrac{R_{\mathrm{b}}}{W} = \dfrac{R_{\mathrm{s}}}{W} \cdot \log_{2} M
> $$
> 其中，$R_{\mathrm{b}}$ 为**比特率 (bit rate)**，$R_{\mathrm{s}}$ 为**符号速率 (symbol rate)**，$W$ 为信道带宽，$M = |\mathscr{A}|$ 为每个符号所承载的电平集合大小。
^PinpuXiaolv

### 过渡带的残留对称条件

考虑 $H(f)$ 在过渡带内的形式，设符号速率为 $R_{\mathrm{s}}$，则 Nyquist 准则要求
$$
H(f) + H(f - R_{\mathrm{s}}) = T, \qquad f \in \left[ 0, R_{\mathrm{s}} \right]
$$
若 $H(f)$ 为偶函数（即成形脉冲 $p(t)$ 为实值信号），则在过渡带内还满足
$$
H(f) + H(R_{\mathrm{s}} - f) = T, \qquad f \in \left[ 0, R_{\mathrm{s}} \right] 
$$
即 $H(f)$ 在过渡带内关于 $f = \dfrac{R_{\mathrm{s}}}{2}$ 对称，称为**残留对称条件 (residual symmetry condition)**。

## 数字基带传输

**数字基带传输 (digital baseband transmission)** 指的是**不经过频率变换**，直接在低频段（基带）上传输数字信号的方式。数字基带传输系统通常使用**升余弦滤波器**作为成形脉冲 $p(t)$，以实现无失真传输。

### 升余弦滤波系统

用余弦函数的半个周期作为 $H(f)$ 的过渡带，即得到**升余弦滤波器 (raised-cosine filter)**，其频率响应为
$$
H(f) = \begin{cases}
T, & |f| \leq \cfrac{1-\alpha}{2} R_{\mathrm{s}}, \\
\cfrac{T}{2} \left[ 1 + \cos \left( \cfrac{\pi T}{\alpha} \left( |f| - \cfrac{1-\alpha}{2T} \right) \right) \right], & \cfrac{1-\alpha}{2} R_{\mathrm{s}} < |f| \leq \cfrac{1+\alpha}{2} R_{\mathrm{s}}, \\
0, & |f| > \cfrac{1+\alpha}{2} R_{\mathrm{s}}
\end{cases}
$$
其中，$\alpha \in [0, 1]$ 为**滚降系数 (roll-off factor)**，决定过渡带的宽度；升余弦滤波器的带宽为 $W = \cfrac{1+\alpha}{2} R_{\mathrm{s}}$，频谱效率为
$$
\eta = \dfrac{R_{\mathrm{s}}}{W} \cdot \log_{2} M = \dfrac{2 \log_{2} M}{1+\alpha}
$$
特别地，
+ 当 $\alpha = 0$ 时，升余弦滤波器退化为**理想低通滤波器**，带宽为 $W = \cfrac{R_{\mathrm{s}}}{2}$；
+ 当 $\alpha = 1$ 时，升余弦滤波器的过渡带宽度最大，带宽为 $W = R_{\mathrm{s}}$。

> [!note] 升余弦基带信道的典型考法
> 升余弦滤波器是通信系统课程的经典考点，常见的考法是**给定 $R_{\mathrm{b}}$ 和 $W$（即给定 $\eta$），求满足无失真传输的 $M$ 和对应的 $\alpha$**。
> 
> 这个问题的约束条件为
> $$
> \dfrac{R_{\mathrm{b}}}{W} = \eta = \dfrac{2 \log_{2} M}{1+\alpha}
> $$
> 对此欠定问题，一般补充两个条件：
> + $M$ 取 **2 的整数次幂**，即 $M = 2^{k}, k \in \mathbb{N}^{*}$；
> + $\alpha$ 不取退化为理想低通滤波器的情况，即 $0 < \alpha \le 1$。
> 
> 此时，可通过枚举 $k$ 的方式求解该问题。
> 
> ![[k-eta-BB.png|不同进制下频谱效率随滚降系数的变动范围]]
^ShengyuxianLvboqiDianxingkaofa

另外，可以推导求出升余弦滤波器的时域**冲激响应**为
$$
h(t) = \dfrac{ \sin \left( \pi R_{\mathrm{s}} t \right) }{ \pi R_{\mathrm{s}} t } \cdot \dfrac{ \cos \left( \pi \alpha R_{\mathrm{s}} t \right) }{ 1 - \left( 2 \alpha R_{\mathrm{s}} t \right)^{2} }
$$
升余弦滤波系统的**功率**为
$$
P = E_{\mathrm{s}} R_{\mathrm{s}} = \dfrac{2W E_{\mathrm{s}}}{1 + \alpha}
$$

### 基带信号的功率谱

通信信号 $x(t)$ 是一个**随机过程 (stochastic process)**，我们希望求解其**[[随机过程的平稳性#^GonglvpuMidu|功率谱密度]] (power spectral density)**
$$
S_{X}(\omega) = \lim_{T \to +\infty} \dfrac{1}{2T} \mathbb{E}\left[ \left| \dint_{-T}^{T} x(t) \e^{-\J 2\pi f t} \dif t \right|^2 \right]
$$

给定符号序列 $\left\{ x_{k} \right\}_{-\infty}^{\infty}$ 时，$x(t)$ 的取值 $\sum\limits_{k} x_{k} p(t - kT)$ 成为一个确定的**样本轨道 (sample path)**，对其可以用确定性信号的频域分析方法。对这一样本轨道，期望函数为 $\mathbb{E} \left[ x(t) \right] = \mathbb{E} \left[ x_{k} \right] \sum\limits_{k} p(t - kT)$，自相关函数为
$$
\begin{align}
\t{R}_{x}(t + \tau, t) &= \mathbb{E} \left[ \sum\limits_{k} x_{k} p(t + \tau - kT) \cdot \sum\limits_{m} x_{m} p(t - mT) \right] \\
&= \sum\limits_{k} \sum\limits_{m} \mathbb{E} \left[ x_{k} x_{m} \right] p(t + \tau - kT) p(t - mT) \\
&= \sum\limits_{k} \sum\limits_{m} R_{x}[k - m] p(t + \tau - kT) p(t - mT) \\
\end{align}
$$
均为周期为 $T$ 的周期函数，因此 $x(t)$ 不是[[随机过程的平稳性#宽平稳随机过程|宽平稳随机过程]]。不过，可以通过**对时间 $t$ 平均**的方式，得到一个与时间无关的自相关函数
$$
\overline{ R_{x} (\tau)} = \dfrac{1}{T} \int_{0}^{T} \t{R}_{x}(t + \tau, t) \dif t
$$
于是，据 [[随机过程的平稳性#^Wiener-Khinchin|Wiener-Khinchin 关系]]，可以定义通信信号 $x(t)$ 的**功率谱密度 (power spectral density)** 为
$$
S_{x}(f) = \mathscr{F} \left\{ \overline{ R_{x}(\tau) } \right\}
$$

考虑**线性调制 (linear modulation)** 信号 $x(t) = \sum\limits_{k} x_{k} p(t - kT)$，其中 $x_{k}$ 平稳，相关为 $R[n]$。$x(t)$ 可视为冲激串 $x_{\delta}(t) = \sum\limits_{k} x_{k} \delta(t - kT)$ 经过成形脉冲 $p(t)$ 滤波后的结果，由[[随机过程的平稳性#LTI 系统对宽平稳随机过程的作用|功率谱密度的性质]]可知，$x(t)$ 的功率谱密度为 $S_{X}(f) = S_{X_{\delta}}(f) |P(f)|^{2}$。

对冲激串 $x_{\delta}(t)$，有
$$
\begin{align} 
&\begin{aligned}
\t{R}_{x_{\delta}}(t + \tau, t) &= \mathbb{E} \left[ \sum\limits_{k} x_{k} \delta(t + \tau - kT) \cdot \sum\limits_{m} x_{m} \delta(t - mT) \right] \\
&= \sum\limits_{k} \sum\limits_{m} \mathbb{E} \left[ x_{k} x_{m} \right] \delta(t + \tau - kT) \delta(t - mT) \\
&= \sum\limits_{n} \sum\limits_{m} R[n] \delta(t + \tau - (m + n)T) \delta(t - mT) \\
\end{aligned} \\
&\begin{aligned}
\overline{ R_{x_{\delta}}(\tau) } &= \dfrac{1}{T} \int_{0}^{T} \t{R}_{x_{\delta}}(t + \tau, t) \dif t \\
&= \dfrac{1}{T} \sum\limits_{n} R[n] \int_{0}^{T} \sum\limits_{m} \delta(t + \tau - (m + n)T) \delta(t - mT) \dif t \\
&= \dfrac{1}{T} \sum\limits_{n} R[n] \delta(\tau - nT)
\end{aligned} \\
&S_{X_{\delta}}(f) = \mathscr{F} \left\{ \overline{ R_{x_{\delta}}(\tau) } \right\} = \dfrac{1}{T} \sum\limits_{n} R[n] \e^{-\J 2 \pi f nT} 
\end{align}
$$
从随机过程的角度，到此就可以了。但从通信角度，希望进一步细化 $R[n]$ 的形式。考虑符号序列 $\left\{ x_{k} \right\}$ **独立同分布 (i.i.d.)**，则
$$
R[n] = \begin{cases}
\mathbb{E}[x_{k}^{2}] = \mathrm{Var}(X) + m_{X}^{2}, & n = 0, \\
\mathbb{E}[x_{k}] \mathbb{E}[x_{k+n}] = m_{X}^{2}, & n \ne 0
\end{cases}
$$
于是
$$
\begin{align} 
S_{X_{\delta}}(f) &= \dfrac{1}{T} \left(  \mathrm{Var}(X) + m_{X}^{2} + m_{X}^{2} \sum\limits_{n \ne 0} \e^{-\J 2 \pi f nT} \right) = \dfrac{\mathrm{Var}(X)}{T} + \dfrac{m_{X}^{2}}{T} \sum\limits_{n=-\infty}^{\infty} \e^{-\J 2 \pi f nT}  \\
&= \dfrac{\mathrm{Var}(X)}{T} + \dfrac{m_{X}^{2}}{T^{2}} \sum\limits_{n=-\infty}^{\infty} \delta \left( f - \dfrac{n}{T} \right)
\end{align}
$$

> [!thm.] 线性调制信号的功率谱
> 对**线性调制**信号 $x(t) = \sum\limits_{k} x_{k} p(t - kT)$，其功率谱为
> $$
> S_{X}(f) = \underbrace{ \dfrac{\mathrm{Var}(X)}{T} |P(f)|^{2} }_{ \text{连续谱} } + \underbrace{ \dfrac{m_{X}^{2}}{T^{2}} \sum\limits_{n=-\infty}^{\infty} \left| P\left( \dfrac{n}{T} \right) \right|^{2} \delta \left( f - \dfrac{n}{T} \right) }_{ \text{线谱} }
> $$
> 其中，$m_{X} = \mathbb{E}[x_{k}]$，$\mathrm{Var}(X) = \mathbb{E}[(x_{k} - m_{X})^{2}]$ 分别为符号的均值和方差，$P(f) = \mathscr{F} \{ p(t) \}$ 为成形脉冲的频谱。
^JidaiGonglvpu

当符号电平 $x_{k}$ 均值为 0 时，功率谱仅包含连续谱部分。

## 矩形包络载波传输

在实际通信系统中，数字信号往往需要通过**载波传输 (carrier transmission)** 的方式，将数字信号**调制到一个高频载波信号上**进行传输，以适应无线信道的频率特性和传输需求。

### 矩形包络二进制载波传输

考虑使用**矩形包络载波信号**作为传输波形，即用 $\pm V \cos(2 \pi f_{\mathrm{c}} t)$ 作为成形脉冲表示电平 $\pm A$，其中 $f_{\mathrm{c}}$ 为载波频率。考虑到每个符号占用时间 $T$、能量 $E_{\mathrm{s}}$，则有
$$
x(t) = \begin{cases}
\sqrt{ \cfrac{2E_{\mathrm{s}}}{T} } \cos(2 \pi f_{\mathrm{c}} t) \times \mathbb{1}_{\{ kT \le t < (k+1)T \}}, & x = \sqrt{E_{\mathrm{s}}}, \\
-\sqrt{ \cfrac{2E_{\mathrm{s}}}{T} } \cos(2 \pi f_{\mathrm{c}} t) \times \mathbb{1}_{\{ kT \le t < (k+1)T \}}, & x = -\sqrt{E_{\mathrm{s}}}
\end{cases}
$$
其中，要求 **$f_{\mathrm{c}} T$ 为正整数**，以保证不同符号间正交。

这种包络形式下，BPSK 的各符号可以切开独立处理，只需专注讨论一个符号的波形
$$
x(t) = x \cdot p(t) \sqrt{ 2 } \cos(2 \pi f_{\mathrm{c}} t)
$$
其中，$x$ 等概分布于 $\pm \sqrt{ E_{\mathrm{s}} }$，$p(t) = \sqrt{ \dfrac{1}{T} } \times \mathbb{1}_{\{ 0 \le t < T \}}$ 是**能量归一化**的矩形脉冲。可记**频移后的成形脉冲**为 $p_{\mathrm{I}}(t) = p(t) \sqrt{2} \cos(2 \pi f_{\mathrm{c}} t)$，则
$$
\dint_{-\infty}^{+\infty} p_{\mathrm{I}}^{2}(t) \dif t = \dint_{0}^{T} \dfrac{2}{T} \cos^{2}(2 \pi f_{\mathrm{c}} t) \dif t = \dfrac{2}{T} \dint_{0}^{T} \dfrac{1 + \cos(4 \pi f_{\mathrm{c}} t)}{2} \dif t = 1
$$
即 $p_{\mathrm{I}}(t)$ 仍是能量归一化的，每个符号所使用的波形能量仍为 $E_{\mathrm{s}} = \sigma_{x}^{2}$，比特能量 $E_{\mathrm{b}} = E_{\mathrm{s}}$，**信号功率**为 $P = \dfrac{E_{\mathrm{s}}}{T} = E_{\mathrm{s}}R_{\mathrm{s}} = E_{\mathrm{b}}R_{\mathrm{b}}$。

由[[#波形信道#^ErjinzhiBoxinZuijiaJieshou|二进制波形的最佳接收]]可知，矩形包络载波传输的**最佳接收**方式为
$$
y = \dint_{0}^{T} y(t)  p_{\mathrm{I}}(t) \dif t = x + \underbrace{ \dint_{0}^{T} z(t) \cdot \sqrt{ \dfrac{2}{T} } \cos(2 \pi f_{\mathrm{c}} t) \dif t }_{ z \sim \mathscr{N}\left( 0, \tfrac{n_{0}}{2} \right) }
$$
其中 $x$ 仍为原始等概分布的符号电平。这一接收的**误符号率**由[[#电平信道#二进制电平传输#误符号率|二进制等概电平信道的误符号率]]给出，为
$$
P_{\mathrm{s}} = Q\left( \sqrt{ \mathrm{SNR}} \right) = Q\left( \sqrt{ \dfrac{E_{\mathrm{s}}}{n_{0}/2} } \right)
$$

### 矩形包络多进制单路载波传输

增大每个符号所承载的信息量，可以使用 $M$ 进制符号电平 $x \in \mathscr{A}$ 进行传输。此时，传输波形为
$$
x(t) = x \cdot p(t) \sqrt{ 2 } \cos(2 \pi f_{\mathrm{c}} t), \qquad x \in \mathscr{A}
$$
一般取
$$
\mathscr{A} = \left\{ \pm A, \pm 3A, \pm 5A, \cdots, \pm (M-1)A \right\}, \qquad A = \sqrt{ \dfrac{3 E_{\mathrm{s}}}{M^{2} - 1} }
$$

同理，最佳接收方式为
$$
y = \dint_{0}^{T} y(t)  p_{\mathrm{I}}(t) \dif t = x + \underbrace{ \dint_{0}^{T} z(t) \cdot \sqrt{ \dfrac{2}{T} } \cos(2 \pi f_{\mathrm{c}} t) \dif t }_{ z \sim \mathscr{N}\left( 0, \tfrac{n_{0}}{2} \right) }
$$
其中 $x$ 服从均匀分布于 $\mathscr{A}$。此时，**误符号率**由[[#电平信道#多进制实电平传输#误符号率|多进制等概电平信道的误符号率]]给出，为
$$
P_{\mathrm{s}} = \dfrac{2M - 2}{M} Q\left( \sqrt{ \dfrac{3}{M^{2} - 1}  \dfrac{E_{\mathrm{s}}}{n_{0}/2} } \right)
$$
**误 bit 率**由[[#电平信道#多进制实电平传输#误 bit 率|多进制等概电平信道的误 bit 率]]给出，为
$$
P_{\mathrm{b}} = \dfrac{2M - 2}{M \log_{2} M} Q\left( \sqrt{ \dfrac{3\log_{2} M}{M^{2} - 1} \dfrac{E_{\mathrm{b}}}{n_{0}/2} } \right)
$$

### 矩形包络 I、Q 路载波传输

前面均只使用余弦载波移动信号频谱到高频段，称为**单路载波传输 (single-carrier transmission)**。为了更高效地利用带宽，可以使用**正交载波 (orthogonal carriers)** 同时传输两个独立的信号，称为 **I、Q 路载波传输 (I/Q carrier transmission)**。

利用余弦和正弦载波的正交性
$$
\begin{align} 
&\dint_{0}^{T} \cos(2 \pi f_{\mathrm{c}} t) \cdot \sin(2 \pi f_{\mathrm{c}} t) \dif t = 0,  \\
&\dint_{0}^{T} \cos^{2}(2 \pi f_{\mathrm{c}} t) \dif t = \dint_{0}^{T} \sin^{2}(2 \pi f_{\mathrm{c}} t) \dif t = \dfrac{T}{2}
\end{align}
$$
可以同时传输两个独立的符号 $x_{\mathrm{I}}$ 和 $x_{\mathrm{Q}}$，分别调制在余弦和正弦载波上，得到
$$
x(t) = x_{\mathrm{I}} \cdot \underbrace{ p(t) \sqrt{ 2 } \cos(2 \pi f_{\mathrm{c}} t) }_{ p_{\mathrm{I}}(t) } + x_{\mathrm{Q}} \cdot \underbrace{ p(t) \sqrt{ 2 } \sin(2 \pi f_{\mathrm{c}} t) }_{ p_{\mathrm{Q}}(t) } = x_{\mathrm{I}}(t) + x_{\mathrm{Q}}(t)
$$

对 $x_{\mathrm{I}}(t)$ 的最佳接收为
$$
\begin{align} 
y_{\mathrm{I}} &= \dint_{0}^{T} y(t)  p_{\mathrm{I}}(t) \dif t = \dint_{0}^{T} \big( x_{\mathrm{I}}(t) + x_{\mathrm{Q}}(t) + z(t) \big) \cdot \sqrt{ \dfrac{2}{T} } \cos(2 \pi f_{\mathrm{c}} t) \dif t \\
&= x_{\mathrm{I}} \cdot \underbrace{ \dint_{0}^{T} \sqrt{ \dfrac{2}{T} } \cos^{2}(2 \pi f_{\mathrm{c}} t) \dif t }_{ 1 } + x_{\mathrm{Q}} \cdot \underbrace{ \dint_{0}^{T} \sqrt{ \dfrac{2}{T} } \sin(2 \pi f_{\mathrm{c}} t) \cdot \cos(2 \pi f_{\mathrm{c}} t) \dif t }_{ 0 } \\
&\hspace{1em} + \dint_{0}^{T} z(t) \cdot \sqrt{ \dfrac{2}{T} } \cos(2 \pi f_{\mathrm{c}} t) \dif t \\
&= x_{\mathrm{I}} + \underbrace{ \dint_{0}^{T} z(t) \cdot \sqrt{ \dfrac{2}{T} } \cos(2 \pi f_{\mathrm{c}} t) \dif t }_{ z_{\mathrm{I}} \sim \mathscr{N}\left( 0, \tfrac{n_{0}}{2} \right) } 
\end{align}
$$
同理，对 $x_{\mathrm{Q}}(t)$ 的最佳接收为
$$
y_{\mathrm{Q}} = \dint_{0}^{T} y(t)  p_{\mathrm{Q}}(t) \dif t = x_{\mathrm{Q}} + \underbrace{ \dint_{0}^{T} z(t) \cdot \sqrt{ \dfrac{2}{T} } \sin(2 \pi f_{\mathrm{c}} t) \dif t }_{ z_{\mathrm{Q}} \sim \mathscr{N}\left( 0, \tfrac{n_{0}}{2} \right) }
$$
对一路的最佳接收自然地消除了另一路的干扰，I、Q 两路信号可以独立解调。

不妨设复电平 $x = x_{\mathrm{I}} + \J x_{\mathrm{Q}}$，复噪声 $z = z_{\mathrm{I}} + \J z_{\mathrm{Q}} \sim \mathscr{CN}(0, n_{0})$，则最佳接收可写为标准电平信道 $y = x + z$ 的形式。

#### 矩形包络 $M$-QAM 载波传输

取 $M$-QAM 星座图的电平集合
$$
\begin{align} 
\mathscr{A} = \{ x_{\mathrm{I}} + \J x_{\mathrm{Q}} \mid x_{\mathrm{I}}, x_{\mathrm{Q}} \in \{ \pm A, \cdots, \pm(L - 3)A, \pm(L - 1)A \} \}, \qquad\\

A = \sqrt{ \dfrac{3 E_{\mathrm{s}}}{2 (L^{2} - 1)} }
\end{align}
$$
实轴、虚轴均取 $L$ 个等间距电平，共有 $M = L^{2}$ 个复电平。

由上述分析，矩形包络 $M$-QAM 载波传输等效到 [[#电平信道#复电平传输#QAM 输入的分析|QAM 输入的复电平信道]]，其**误符号率**为
$$
P_{\mathrm{s}} = \dfrac{4(\sqrt{ M } - 1)}{\sqrt{ M }} Q\left( \sqrt{ \dfrac{3}{M - 1} \dfrac{E_{\mathrm{s}}}{n_{0}} } \right) 
$$
**误 bit 率**为
$$
P_{\mathrm{b}} = \dfrac{4(\sqrt{ M } - 1)}{\sqrt{ M } \log_{2} M} Q\left( \sqrt{ \dfrac{3 \log_{2} M}{M - 1} \dfrac{E_{\mathrm{b}}}{n_{0}} } \right)
\stackrel{M\text{较大}}{\approx} \dfrac{4}{\log_{2} M} Q\left( \sqrt{ \dfrac{3 \log_{2} M}{M} \dfrac{E_{\mathrm{b}}}{n_{0}} } \right)
$$

#### 矩形包络 $M$-PSK 载波传输

取 $M$-PSK 星座图的电平集合
$$
\mathscr{A} = \left\{ \sqrt{E_{\mathrm{s}}} \cdot \e^{\J 2 \pi m / M} \mid m = 0, 1, \cdots, M - 1 \right\}
$$

由上述分析，矩形包络 $M$-PSK 载波传输等效到 [[#电平信道#复电平传输#PSK 输入的分析|PSK 输入的复电平信道]]，其**误符号率**为
$$
P_{\mathrm{s}} = 2 Q\left( \sqrt{ \dfrac{2E_{\mathrm{s}}}{n_{0}} } \sin \dfrac{\pi}{M} \right)
$$
**误 bit 率**为
$$
P_{\mathrm{b}} = \dfrac{2}{\log_{2} M} Q\left( \sqrt{ \dfrac{2E_{\mathrm{b}} \log_{2}M}{n_{0}} } \sin \dfrac{\pi}{M} \right)
\stackrel{M\text{较大}}{\approx} \dfrac{2}{\log_{2} M} Q\left( \dfrac{\pi}{M} \sqrt{ \dfrac{2E_{\mathrm{b}} \log_{2}M}{n_{0}} } \right)
$$

## 带限载波传输

[[#矩形包络载波传输]]实现简单，但发送的信号**不带限**，不具备实际传输条件。为了适应带限信道的传输需求，需要对载波传输系统进行带限设计，只使用 $\big\lvert |f| - f_{\mathrm{c}} \big\rvert \le W$ 的频率范围进行传输。

### 单路带限载波传输

#### 系统模型

取定带限的成形脉冲 $p(t)$，其频谱 $P(f)$ 带限于 $|f| \le W$，则单路带限载波传输的发送信号为 $x_{\mathrm{BB}}(t) = \sum\limits_{k} x_{k} p(t - kT)$，调制到载波上得到
$$
x(t) = x_{\mathrm{BB}}(t) \cdot \sqrt{2} \cos(2 \pi f_{\mathrm{c}} t)
$$
接收端**使用载波解调**，经**低通滤波**后得到基带信号
$$
y_{\mathrm{BB}}(t) = \big( y(t) \cdot \sqrt{2} \cos(2 \pi f_{\mathrm{c}} t) \big)  * h_{\mathrm{LPF}_{W}}(t) 
$$
再对 $y_{\mathrm{BB}}(t)$ 进行**最佳接收**，得到
$$
\begin{align} 
\t{y}(kT) &= \dint_{-\infty}^{+\infty} y_{\mathrm{BB}}(\tau) p(\tau - kT) \dif \tau = \big( y(t) \cdot \sqrt{2} \cos(2 \pi f_{\mathrm{c}} t) \big) * h_{\mathrm{LPF}_{W}}(t) * p(-t) \Big|_{t = kT}  \\
&= \big( y(t) \cdot \sqrt{2} \cos(2 \pi f_{\mathrm{c}} t) \big) * (h_{\mathrm{LPF}_{W}}(t) * p(-t)) \Big|_{t = kT} \\
&= \big( y(t) \cdot \sqrt{2} \cos(2 \pi f_{\mathrm{c}} t) \big) * p(-t) \Big|_{t = kT}
\end{align}
$$
其中最后一步是因为 $\mathscr{F} \left\{ p(-t) \right\} = P^{*}(f)$ 带限于 $|f| \le W$，经过带宽为 $W$ 的低通滤波器后不变。这样，当**载频 $f_{\mathrm{c}} > W$** 时，可以含噪声地恢复出基带信号 $x_{\mathrm{BB}}(t)$，从而单路带限载波传输等效到**基带传输**，其成形脉冲为 $p(t)$，符号电平为 $x_{k}$。

![[单路带限载波传输.png|单路带限载波传输系统模型]]

#### 传输性能

设 $p(t)$ 为**能量归一化**且**带限于 $|f| \le W$** 的成形脉冲，载频 $f_{\mathrm{c}} > W$，符号电平 $x_{k}$ 独立同分布，均值为 0，方差为 $\sigma_{x}^{2}$，则单路带限载波传输等效到基带传输系统，**信号功率**为
$$
P = E_{\mathrm{s}} R_{\mathrm{s}} = \dfrac{\sigma_{x}^{2}}{T} = E_{\mathrm{b}} R_{\mathrm{b}}
$$

**最佳接收**过程展开为
$$
\begin{align}
y_{k} = \t{y}(kT) &= \dint_{-\infty}^{+\infty} y(t) \cdot \sqrt{2} \cos(2 \pi f_{\mathrm{c}} t) \cdot p(t - kT) \dif t \\
&= \dint_{-\infty}^{+\infty} \big( x(t) + z(t) \big) p(t - kT) \cdot \sqrt{2} \cos(2 \pi f_{\mathrm{c}} t) \dif t \\
&= \dint_{-\infty}^{+\infty} \left( \sum\limits_{i} x_{i}p(t - iT) \right) p(t - kT) \cdot 2 \cos^{2}(2 \pi f_{\mathrm{c}} t) \dif t \hspace{-1.5em}&\text{（信号）}  \\
&\hspace{1em}+ \dint_{-\infty}^{+\infty} z(t) p(t - kT) \cdot \sqrt{2} \cos(2 \pi f_{\mathrm{c}} t) \dif t & \text{（噪声）} \\
\end{align}
$$
+ 噪声项中，$p^{2}(t - kT)$ 与 $\cos(4 \pi f_{\mathrm{c}} t)$ 频域无重叠，故**时域亦正交**，因此噪声项服从分布 **$z_{k} \sim \mathscr{N}\left( 0, \cfrac{n_{0}}{2} \right)$**。
+ 信号项中，$p(t - ik)p(t - kT)$ 与 $\cos(4 \pi f_{\mathrm{c}} t)$ 亦正交，因此
$$
\begin{align}
\text{（信号）}\hspace{-0.5em} &= \sum\limits_{i} x_{i} \dint_{-\infty}^{+\infty} p(t - iT) p(t - kT) \dif t
= \sum\limits_{i} x_{i} \dint p(t) p(t - (k - i)T) \dif t  \\
&= \sum\limits_{i} x_{i} h((k-i)T) = \sum\limits_{i} x_{i} \delta[k - i] = x_{k}
\end{align}
$$
其中 $h(t) = p(t) * p(-t)$ 应满足[[#无失真传输的 Nyquist 准则|采样点无失真准则]]，以保证无码间干扰。

这样，单路带限载波传输的最佳接收可写为
$$
y_{k} = x_{k} + z_{k}, \qquad z_{k} \stackrel{\text{i.i.d}}{\sim} \mathscr{N}\left( 0, \dfrac{n_{0}}{2} \right)
$$
其中 $x_{k}$ 仍为原始符号电平。

二进制和多进制单路带限载波传输的**误符号率**和**误 bit 率**，与对应的基带传输系统相同，分别由[[#电平信道#二进制电平传输#误符号率|二进制]]和[[#电平信道#多进制实电平传输#差错分析|多进制]]等概电平信道的分析给出。

### I、Q 路带限载波传输

直接类比[[#矩形包络 I、Q 路载波传输]]，一般的 I、Q 路带限载波传输系统模型如下：

![[I、Q路带限载波传输.png|I、Q路带限载波传输系统模型]]

同样有**功率**为
$$
P = E_{\mathrm{s}} R_{\mathrm{s}} = \dfrac{\sigma_{x}^{2}}{T} = E_{\mathrm{b}} R_{\mathrm{b}}
$$

展开其**最佳接收**过程，对 Q 路有
$$
\begin{align}
y_{k}^{\mathrm{Q}} &= \dint_{-\infty}^{+\infty} y(t) \cdot \sqrt{2} \sin(2 \pi f_{\mathrm{c}} t) \cdot p(t - kT) \dif t \\
&= \dint_{-\infty}^{+\infty} \big( x^{\mathrm{I}}(t) + x^{\mathrm{Q}}(t) + z(t) \big) p(t - kT) \cdot \sqrt{2} \sin(2 \pi f_{\mathrm{c}} t) \dif t \\
&= \dint_{-\infty}^{+\infty} \left( \sum\limits_{i} x_{i}^{\mathrm{I}}p(t - iT) \right) p(t - kT) \cdot 2 \sin(2 \pi f_{\mathrm{c}} t) \cos(2 \pi f_{\mathrm{c}} t) \dif t \hspace{-2em} & \text{（I 路干扰）} \\
&\hspace{1em}+ \dint_{-\infty}^{+\infty} \left( \sum\limits_{i} x_{i}^{\mathrm{Q}}p(t - iT) \right) p(t - kT) \cdot 2 \sin^{2}(2 \pi f_{\mathrm{c}} t) \dif t &\text{（Q 路信号）} \\
&\hspace{1em}+ \dint_{-\infty}^{+\infty} z(t) p(t - kT) \cdot \sqrt{2} \sin(2 \pi f_{\mathrm{c}} t) \dif t & \text{（噪声）}
\end{align}
$$
+ 噪声项服从分布 **$z_{k}^{\mathrm{Q}} \sim \mathscr{N}\left( 0, \cfrac{n_{0}}{2} \right)$**。
+ 干扰项中，$p(t - ik)p(t - kT)$ 与 $\sin(4 \pi f_{\mathrm{c}} t)$ 频域无重叠，故时域亦正交，因此干扰项为 0。
+ 信号项中，与[[#单路带限载波传输#传输性能|单路带限载波传输]]类似，在 $h(t) = p(t) * p(-t)$ 满足[[#无失真传输的 Nyquist 准则|采样点无失真准则]]的前提下，得其值为原始符号电平 $x_{k}^{\mathrm{Q}}$。

即其**最佳接收**过程可等效为[[#电平信道#复电平传输|复电平信道]]，QAM、PSK 等调制方式下的误符号率和误 bit 率分别由 [[#电平信道#复电平传输#QAM 输入的分析|QAM]] 输入和 [[#电平信道#复电平传输#PSK 输入的分析|PSK]] 输入的复电平信道的分析给出。

### 带限载波传输的频谱效率

在带限于 $\big\lvert |f| - f_{\mathrm{c}} \big\rvert \le W$ 的频率范围内传输信号时，**占用带宽**为 $B = 2W$。定义**频谱效率 (spectral efficiency)** 为每单位带宽传输的比特率，即
$$
\eta = \dfrac{R_{\mathrm{b}}}{B} = \dfrac{R_{\mathrm{b}}}{2W} = \dfrac{R_{\mathrm{s}}}{2W} \cdot \log_{2} M
$$
若用[[#升余弦滤波系统]]作为成形脉冲，则有 $W = \dfrac{1 + \alpha}{2T}$，其中 $\alpha$ 为滚降系数 (roll-off factor)，则频谱效率可写为
$$
\eta = \dfrac{ \log_{2} M }{1+\alpha}
$$

> [!note] 升余弦带通信道的典型考法
> 类似于[[#^ShengyuxianLvboqiDianxingkaofa|基带的升余弦滤波系统]]，升余弦的带限载波传输的常见考法是**给定 $R_{\mathrm{b}}$ 和带通范围 $[f_{\mathrm{min}}, f_{\mathrm{max}}]$，求满足无失真传输的 $M$ 和对应的 $\alpha$**。
> 
> 一般地，只在正频轴上讨论，居中取**载频 $f_{\mathrm{c}} = \cfrac{f_{\mathrm{min}} + f_{\mathrm{max}}}{2}$**，两侧分别有**基带带宽 $W = \cfrac{f_{\mathrm{max}} - f_{\mathrm{min}}}{2}$**，占用带宽 $B=2W$。此时，数字载波传输系统的**频谱效率**为
> $$
> \eta = \dfrac{R_{\mathrm{b}}}{B} = \dfrac{R_{\mathrm{b}}}{f_{\mathrm{max}} - f_{\mathrm{min}}} = \dfrac{R_{\mathrm{s}}}{2W} \cdot \log_{2} M = \dfrac{ \log_{2} M }{1+\alpha}
> $$
> 
> 同样，对此欠定问题，一般补充两个条件：
> + $M$ 取 **2 的整数次幂**，即 $M = 2^{k}, k \in \mathbb{N}^{*}$；
> + $\alpha$ 不取退化情况，即 $0 < \alpha \le 1$。
> 
> 此时，可通过枚举 $k$ 的方式求解该问题。
> 
> ![[k-eta.png|不同进制下频谱效率随滚降系数的变动范围]]

### 带限载波传输信号的功率谱

对信号做频谱搬移时，**功率谱也会相应地搬移**。考虑 $x_{\mathrm{BB}}(t) = \sum\limits_{k} x_{k} p(t - kT)$ 频谱搬移到载波频率 $f_{\mathrm{c}}$，即传输信号为
$$
x(t) = x_{\mathrm{BB}}(t) \cdot \sqrt{2} \cos(2 \pi f_{\mathrm{c}} t)
$$
则[[#^JidaiGonglvpu|基带信号的功率谱]]也相应地搬移，得到带限载波传输信号的**功率谱**
$$
\begin{align} 
S_{X}(f) &= \dfrac{1}{2} \left( S_{X_{\mathrm{BB}}}(f - f_{\mathrm{c}}) + S_{X_{\mathrm{BB}}}(f + f_{\mathrm{c}}) \right)  \\
&= \dfrac{\mathrm{Var(X)}}{2T} \left( |P(f - f_{\mathrm{c}})|^{2} + |P(f + f_{\mathrm{c}})|^{2} \right) \\
&\hspace{1em} + \dfrac{ m_{X}^{2} }{2T^{2}} \sum\limits_{n=-\infty}^{\infty} \left| P\left( \dfrac{n}{T} \right) \right|^{2} \left( \delta \left( f - f_{\mathrm{c}} - \dfrac{n}{T} \right) + \delta \left( f + f_{\mathrm{c}} - \dfrac{n}{T} \right) \right)
\end{align}
$$
由于 $\sqrt{2} \cos(2 \pi f_{\mathrm{c}} t)$ 能量归一化，因此频谱搬移**能量守恒**。
