# 随机变量的基础概念

---

## 随机变量的统计特性

### 随机变量的分布

离散随机变量 $X$ 可用其**概率质量函数 (probability mass function, PMF)** $P_{X}(x) = P \left\{ X = x \right\}$ 描述；连续随机变量 $X$ 可用其**累积分布函数 (cumulative distribution function, CDF)** $F_{X}(x) = P \left\{X \leq x\right\}$ 或**概率密度函数 (probability density function, PDF)** $f_{X}(x) = \cfrac{\dif F_{X}(x)}{\dif x}$ 描述。

---

**条件于 $Y$ 的随机变量 $X$** 表示为 $X \mid Y$，其 PMF 或 PDF、CDF 分别为
$$
\begin{align} 
&P_{X \mid Y}(x \mid y) = P \left\{ X = x \mid Y = y \right\} = \dfrac{P_{X,Y}(x,y)}{P_{Y}(y)}, \\
&f_{X \mid Y}(x \mid y) = \dfrac{f_{X,Y}(x,y)}{f_{Y}(y)}, \quad F_{X \mid Y}(x \mid y) = \dint_{-\infty}^{x} f_{X \mid Y}(t \mid y) \dif t
\end{align}
$$
有**全概率公式 (law of total probability)**
$$
\begin{align}
&P_{X}(x) = \sum\limits_{y} P_{X \mid Y}(x \mid y) P_{Y}(y), \\
&F_{X}(x) = \dint_{-\infty}^{+\infty} F_{X \mid Y}(x \mid y) f_{Y}(y) \dif y, \quad
f_{X}(x) = \dint_{-\infty}^{+\infty} f_{X \mid Y}(x \mid y) f_{Y}(y) \dif y
\end{align}
$$

### 随机变量的数字特征

使用以下数字特征来描述随机变量的统计特性：
+ **均值 (mean)** 或**期望 (expectation)** $\mathbb{E} \left[ X \right] = \dint_{-\infty}^{+\infty} x f_{X}(x) \dif x$（对离散随机变量为 $\mathbb{E} \left[ X \right] = \sum\limits_{x} x P_{X}(x)$），描述随机变量的中心位置；
+ **方差 (variance)** $\mathrm{Var}[X] = \mathbb{E} \left[ |X - \mathbb{E}[X]|^{2} \right]$，描述随机变量的离散程度。

方程和均值的关系为
$$
\mathrm{Var}[X] = \mathbb{E}\left[|X|^{2}\right] - |\mathbb{E}[X]|^{2}
$$
对随机变量 $N$ 个独立同分布随机变量 $X$，考虑其和 $Y = \sum\limits_{N} X$，则
+ $\mathbb{E}[Y] = \mathbb{E} \left[ \mathbb{E} \left[ \sum\limits_{N} X \mathop{\bigg|} N \right] \right] = \mathbb{E} \left[ N \right] \mathbb{E} \left[ X \right]$；
+ $\mathrm{Var}[Y] = \mathbb{E} \left[ N \right] \mathrm{Var}[X] + \mathrm{Var}[N] \big|\mathbb{E}[X]\big|^{2}$。

对**条件于 $Y$ 的随机变量 $X$**，类似定义：
+ **条件均值 (conditional mean)** $\mathbb{E}[X|Y] = \dint_{-\infty}^{+\infty} x f_{X|Y}(x|y) \dif x$（对离散随机变量为 $\mathbb{E}[X|Y] = \sum\limits_{x} x P_{X|Y}(x|y)$），满足**重期望公式 (law of total expectation)** 
$$\mathbb{E}[X] = \mathbb{E}_{Y} \big[\mathbb{E}_{X}[X|Y]\big]$$
+ **条件方差 (conditional variance)** $\mathrm{Var}[X|Y] = \mathbb{E} \left[ \left| X - \mathbb{E}[X|Y] \right|^{2} \Big| Y \right]$，满足**全方差公式 (law of total variance)** 
$$\mathrm{Var}[X] = \mathrm{Var} \big[ \mathbb{E}[X|Y] \big] + \mathbb{E} \big[ \mathrm{Var}[X|Y] \big]$$

### 随机变量的特征函数

类似于 Fourier 变换，随机变量也有其对应的**特征函数 (characteristic function)**，它描述了随机变量在「某种意义的」频域上的分布情况。

> [!definition] 特征函数
> 随机变量 $X$ 的**特征函数 (characteristic function)** 定义为
> $$
> \phi_{X}(\omega) = \mathbb{E} \left[ \e^{\J \omega X} \right] = \dint_{-\infty}^{+\infty} \e^{\J \omega x} f_{X}(x) \dif x
> $$
^TezhengHanshu

需要注意，
+ 上述特征函数的积分中的**指数函数为 $\e^{\J \omega x}$**，而常见的 Fourier 变换中的指数函数通常为 $\e^{-\J \omega t}$；
+ 特征函数不同于一般信号的 Fourier 变换，其积分变量是随机变量 $X$ 的取值 $x$ 而非时间 $t$，所刻画的是 **$X$ 的分布（随机性）的「频」域特性**。

如果 $X$ 为离散随机变量，类比于 DTFT 与 $z$ 变换的关系，随机变量也有**母函数 (moment generating function, MGF)**。同样，不同于常见的 $z$ 变换表述，此处求和中使用的指数函数为 $z^{x}$ 而非 $z^{-x}$。

> [!definition] 母函数
> 离散随机变量 $X$ 的**母函数 (moment generating function, MGF)** 定义为
> $$
> G_{X}(z) = \mathbb{E} \left[ z^{X} \right] = \sum\limits_{x} z^{x} P_{X}(x)
> $$
> $X$ 的**特征函数**可以表示为
> $$
> \phi_{X}(\omega) = G_{X}(\e^{\J \omega})
> $$
^MuHanshu

特别地，$X \in \mathbb{Z}$ 时，母函数成为幂级数或 Laurent 级数的形式。

### 随机变量的相互关系

#### 随机变量的独立

两个随机变量 $X$ 和 $Y$ 相互**独立 (independent)**，如果对于任意 $x$ 和 $y$，都有
$$
f_{X,Y}(x,y) = f_{X}(x) f_{Y}(y)
\quad \text{或} \quad
P_{X,Y}(x,y) = P_{X}(x) P_{Y}(y)
$$
即，$X$ 的取值不影响 $Y$ 的取值，反之亦然。

#### 随机变量的相关

**相关**描述两个随机变量之间的线性关系，即寻找 $Y \simeq \alpha X$ 的关系。为此，考虑**均方误差 (MSE)**：
$$
\text{MSE} = \mathbb{E}[(Y - \alpha X)^2]
$$
我们希望寻找 $\arg \min\limits_{\alpha} \text{MSE}$，因此令
$$
\frac{\partial \text{MSE}}{\partial \alpha} = \dfrac{\partial}{\partial \alpha} \mathbb{E}[(Y - \alpha X)^2] = 0
$$
直接**交换求导与求期望**两个微积分过程，得到
$$
\mathbb{E}[-2X(Y - \alpha X)] = 0 \quad \Longrightarrow \quad \alpha = \frac{\mathbb{E}[XY]}{\mathbb{E}[X^2]}
$$

> [!definition] 相关
> 两个随机变量 $X$ 和 $Y$ 之积的期望 $\mathbb{E}[XY]$ 即称为二者的**相关** (correlation)。
^SuijiBianliangXiangguan

相关具有**双线性 (bilinear)** 性质，即对于任意常数 $a$、$b$，有
$$
\begin{cases}
\mathbb{E}[(aX_{1} + bX_{2})Y] = a\mathbb{E}[X_{1}Y] + b\mathbb{E}[X_{2}Y], \\
\mathbb{E}[X(aY_{1} + bY_{2})] = a\mathbb{E}[XY_{1}] + b\mathbb{E}[XY_{2}]
\end{cases}
$$

> [!definition] 协方差
> 两个随机变量 $X$ 和 $Y$ 的**协方差 (covariance)** 定义为
> $$
> \text{Cov}(X,Y) = \mathbb{E}[(X - \mathbb{E}[X])(Y - \mathbb{E}[Y])] = \mathbb{E}[XY] - \mathbb{E}[X]\mathbb{E}[Y]
> $$

显然，协方差也具有**双线性**性质，并且 $\text{Cov}(X,X) = \text{Var}(X)$。

> [!danger] 独立性与相关性的区别
>
> 两个随机变量 $X$ 和 $Y$ **独立**，意味着 
> $$
> f_{X,Y}(x,y) = f_{X}(x)f_{Y}(y)
> \quad \text{或} \quad
> P_{X,Y}(x,y) = P_{X}(x) P_{Y}(y)
> $$
> 而**相关**只描述两个随机变量之间的线性关系，两个随机变量 $X$ 和 $Y$ **不相关**，仅代表 
> $$
> \mathrm{Cov}\left[ X,Y \right] = 0
> \quad \text{i.e.} \quad
> \mathbb{E}[XY] = \mathbb{E}[X]\mathbb{E}[Y]
> $$
> 显然，**独立性蕴含不相关性**，但反之不然。

> [!note] 相关性的几何描述
> 考虑随机变量 $X$ 和 $Y$ 的**内积空间**，定义**内积**为
> $$
> \langle X, Y \rangle = \mathbb{E}[XY]
> $$
> 则**范数**即为
> $$
> \|X\| = \sqrt{\langle X, X \rangle} = \sqrt{\mathbb{E}[X^2]}
> $$
> 这样，$Y$ 在 $X$ 方向上的**投影**为
> $$
> \text{proj}_{X}Y = \frac{\langle X, Y \rangle}{\|X\|^2} X = \frac{\mathbb{E}[XY]}{\mathbb{E}[X^2]} X
> $$
> 与前面通过最小化 MSE 得到的结果一致。
> 
> 进一步地，考虑多个随机变量 $X_{1}, X_{2}, \ldots, X_{n}$，记 $Y$ 在这些变量张成的子空间上的投影为
> $$
> \text{proj}_{X_{1}, X_{2}, \ldots, X_{n}} Y = \alpha_{1} X_{1} + \alpha_{2} X_{2} + \cdots + \alpha_{n} X_{n} = \sum\limits_{i=1}^{n} \alpha_{i} X_{i} = \v{\alpha}^{\mathrm{T}} \v{X}
> $$
> 于是 $\v{\alpha} = \arg\min\limits_{\vu{\alpha}} \mathbb{E} \big[(Y-\vu{\alpha}^{\mathrm{T}}\v{X}) \big]$，而
> $$
> \begin{align}
> \mathbb{E} \big[(Y-\vu{\alpha}^{\mathrm{T}}\v{X})^2 \big] 
> &= \mathbb{E} \big[(Y-\vu{\alpha}^{\mathrm{T}}\v{X})^{\mathrm{T}}(Y-\vu{\alpha}^{\mathrm{T}}\v{X}) \big] \\
> &= \mathbb{E} \big[(Y-\v{X}^{\mathrm{T}}\vu{\alpha})^{\mathrm{T}}(Y-\v{X}^{\mathrm{T}}\vu{\alpha}) \big] \\
> &= \mathbb{E}[Y^2] - \mathbb{E} [Y^{\mathrm{T}} \v{X}^{\mathrm{T}}] \vu{\alpha} - \vu{\alpha}^{\mathrm{T}} \mathbb{E}[\v{X} Y] + \vu{\alpha}^{\mathrm{T}} \mathbb{E}[\v{X} \v{X}^{\mathrm{T}}] \vu{\alpha}
> \end{align}
> $$
> 对 $\vu{\alpha}$ 求梯度并令其为零，即
> $$
> \nabla_{\vu{\alpha}} \mathbb{E} \big[(Y-\vu{\alpha}^{\mathrm{T}}\v{X})^2 \big] \Big|_{\vu{\alpha} = \v{\alpha}} = -\mathbb{E}[\v{X} Y] - \mathbb{E}[\v{X} Y] + 2 \mathbb{E}[\v{X} \v{X}^{\mathrm{T}}] \v{\alpha} = 0
> $$
> 故
> $$
> \v{\alpha} = \big(\mathbb{E}[\v{X} \v{X}^{\mathrm{T}}]\big)^{-1} \mathbb{E}[\v{X} Y]
> $$
> 即，**$Y$ 与 $\v{X}$ 各元素的相关对应着其在 $\v{X}$ 张成的子空间上的投影系数**。

## 常见分布及其性质

### 典型连续随机变量

#### Gauss 分布

称连续随机变量 $X$ 服从 **Gauss 分布 (Gaussian distribution)**，如果其概率密度函数为
$$
f_{X}(x) = \dfrac{1}{\sqrt{2\pi} \sigma} \exp\left( -\dfrac{(x - \mu)^{2}}{2\sigma^{2}} \right)
$$
记为 $X \sim \mathscr{N}(\mu, \sigma^{2})$，其中 $\mu \in \mathbb{R}$，$\sigma^{2} > 0$。

若 $X \sim \mathscr{N}(\mu, \sigma^{2})$，则
+ $\mathbb{E} \left[ X \right] = \mu$，$\mathrm{Var}[X] = \sigma^{2}$。
+ **绝对值 $|X|$** 的均值为
$$
\begin{align} 
\mathbb{E} \left[ |X| \right] &= \dint_{-\infty}^{\infty} |x| f_{X}(x) \dif x = \dfrac{1}{\sqrt{2\pi} \sigma} \left( \dint_{-\infty}^{0} -x \e^{ -\tfrac{(x - \mu)^{2}}{2\sigma^{2}} } \dif x + \dint_{0}^{\infty} x \e^{ -\tfrac{(x - \mu)^{2}}{2\sigma^{2}} } \dif x \right) \\
&= \mu \left( 1 - 2\varPhi\left( -\dfrac{\mu}{\sigma} \right) \right) + \dfrac{2\sigma}{\sqrt{2\pi}} \exp\left( -\dfrac{\mu^{2}}{2\sigma^{2}} \right)
\end{align}
$$
其中 $\varPhi(x)$ 是标准 Gauss 分布的分布函数。特别地，当 $\mu = 0$ 时，有 $\mathbb{E} \left[ |X| \right] = \cfrac{2\sigma}{\sqrt{2\pi}}$，亦即 $|X - \mu|$ 或**偏离半径**的均值为 $\mathbb{E} \left[ |X - \mu| \right] = \cfrac{2\sigma}{\sqrt{2\pi}}$。
+ **奇数阶中心矩**均为零，**偶数阶中心矩**为 $\mathbb{E} \left[ (X - \mu)^{2n} \right] = \sigma^{2n} (2n - 1)!!$。
+ 对可微函数 $g(\cdot)$，有 **Stein 公式 (Stein's lemma)**
$$
\mathbb{E} \left[ g(X) (X - \mu) \right] = \sigma^{2} \mathbb{E} \left[ g'(X) \right]
$$

Gauss 分布的**特征函数**为
$$
\phi_{X}(\omega) = \mathbb{E} \left[ \exp(\J \omega X) \right] = \exp\left( \J \mu \omega - \dfrac{\sigma^{2} \omega^{2}}{2} \right)
$$

#### 均匀分布

称连续随机变量 $X$ 服从**均匀分布 (uniform distribution)**，如果其概率密度函数为
$$
f_{X}(x) = \begin{cases}
\cfrac{1}{b - a}, & a \leq x \leq b \\
0, & \text{otherwise}
\end{cases}
$$
记为 $X \sim \mathscr{U}(a, b)$，其中 $a < b$。

若 $X \sim \mathscr{U}(a, b)$，则 $\mathbb{E} \left[ X \right] = \cfrac{a + b}{2}$，$\mathrm{Var}[X] = \cfrac{(b - a)^{2}}{12}$。

均匀分布的**特征函数**为
$$
\phi_{X}(\omega) = \mathbb{E} \left[ \exp(\J \omega X) \right] = \dfrac{\e^{\J \omega b} - \e^{\J \omega a}}{\J \omega (b - a)}
$$

#### 指数分布

称连续随机变量 $X$ 服从**指数分布 (exponential distribution)**，如果其概率密度函数为
$$
f_{X}(x) = \begin{cases}
\lambda \e^{-\lambda x}, & x \geq 0 \\
0, & x < 0
\end{cases}
$$
记为 $X \sim \mathrm{Exp}(\lambda)$，其中 $\lambda > 0$。

若 $X \sim \mathrm{Exp}(\lambda)$，则
+ $\mathbb{E} \left[ X \right] = \cfrac{1}{\lambda}$，$\mathrm{Var}[X] = \cfrac{1}{\lambda^{2}}$，**$n$ 阶矩**为 $\mathbb{E} \left[ X^{n} \right] = \cfrac{n!}{\lambda^{n}}$。
+ $X$ 具有**无记忆性 (memoryless)**，即对于任意 $s, t \geq 0$，有 $P \left\{ X > s + t \mid X > s \right\} = P \left\{ X > t \right\}$。

指数分布的**特征函数**为
$$
\phi_{X}(\omega) = \mathbb{E} \left[ \exp(\J \omega X) \right] = \dfrac{\lambda}{\lambda - \J \omega}
$$

### 典型离散随机变量

#### Poisson 分布

称离散随机变量 $X$ 服从**Poisson 分布 (Poisson distribution)**，如果其概率质量函数为
$$
P_{X}(k) = \dfrac{\lambda^{k} \e^{-\lambda}}{k!}, \quad k = 0, 1, 2, \cdots
$$
记为 $X \sim \mathrm{Poisson}(\lambda)$，其中 $\lambda > 0$。

若 $X \sim \mathrm{Poisson}(\lambda)$，则
+ $\mathbb{E} \left[ X \right] = \mathrm{Var}[X] = \lambda$，**$n$ 阶矩**为 $\mathbb{E} \left[ X^{n} \right] = \sum\limits_{i=1}^{n} S(n,i) \lambda^{i}$，其中 $S(n,i)$ 为**Stirling 数 (Stirling numbers)**。
+ $X$ 个独立同 [[#Bernoulli 分布]] ($p$) 随机变量之和服从参数为 $\lambda p$ 的 Poisson 分布。

Poisson 分布的**特征函数**为
$$
\phi_{X}(\omega) = \mathbb{E} \left[ \exp(\J \omega X) \right] = \exp\left( \lambda (\e^{\J \omega} - 1) \right)
$$
即**母函数**为
$$
G_{X}(z) = \mathbb{E} \left[ z^{X} \right] = \exp\left( \lambda (z - 1) \right)
$$

#### Bernoulli 分布

称离散随机变量 $X$ 服从**Bernoulli 分布 (Bernoulli distribution)**，如果其概率质量函数为
$$
P_{X}(k) = \begin{cases}
p, & k = 1 \\
1 - p, & k = 0
\end{cases}
$$
记为 $X \sim \begin{pmatrix}1 & 0\\ p & 1-p\end{pmatrix}$，其中 $0 < p < 1$。

若 $X \sim \begin{pmatrix}1 & 0\\ p & 1-p\end{pmatrix}$，则 $\mathbb{E} \left[ X \right] = p$，$\mathrm{Var}[X] = p (1 - p)$。

Bernoulli 分布的**母函数**为
$$
G_{X}(z) = \mathbb{E} \left[ z^{X} \right] = p z + 1 - p
$$

#### 二项分布

称离散随机变量 $X$ 服从**二项分布 (binomial distribution)**，如果其概率质量函数为
$$
P_{X}(k) = \binom{n}{k} p^{k} (1 - p)^{n - k}, \quad k = 0, 1, 2, \cdots, n
$$
记为 $X \sim \mathscr{B}(n, p)$，其中 $n$ 为正整数，$0 < p < 1$。

若 $X \sim \mathscr{B}(n, p)$，则
+ $\mathbb{E} \left[ X \right] = n p$，$\mathrm{Var}[X] = n p (1 - p)$。
+ $X$ 个独立同 [[#Bernoulli 分布]] ($q$) 随机变量之和服从参数为 $(n, pq)$ 的二项分布。

二项分布的**母函数**为
$$
G_{X}(z) = \mathbb{E} \left[ z^{X} \right] = (p z + 1 - p)^{n}
$$

#### 几何分布

称离散随机变量 $X$ 服从**几何分布 (geometric distribution)**，如果其概率质量函数为
$$
P_{X}(k) = (1 - p)^{k-1} p, \quad k = 1, 2, \cdots
$$
记为 $X \sim \mathrm{Geometric}(p)$，其中 $0 < p < 1$。

若 $X \sim \mathrm{Geometric}(p)$，则
+ $\mathbb{E} \left[ X \right] = \cfrac{1}{p}$，$\mathrm{Var}[X] = \cfrac{1 - p}{p^{2}}$。
+ $X$ 具有**无记忆性**，即对 $\forall m, n \geq 1$， $P \left\{ X > m + n \mid X > m \right\} = P \left\{ X > n \right\}$。
+ $X$ 个独立同[[#几何分布]] $\mathrm{Geometric}(q)$ 随机变量之和服从参数为 $pq$ 的几何分布。
+ $X$ 个独立同[[#指数分布]] $\mathrm{Exp}(\lambda)$ 随机变量之和服从参数为 $\lambda p$ 的指数分布。

几何分布的**母函数**为
$$
G_{X}(z) = \mathbb{E} \left[ z^{X} \right] = \dfrac{p z}{1 - (1 - p) z}, \quad |z| < \dfrac{1}{1 - p}
$$

#### 负二项分布

称离散随机变量 $X$ 服从**负二项分布 (negative binomial distribution)**，如果其概率质量函数为
$$
P_{X}(k) = \binom{k - 1}{n - 1} p^{n} (1 - p)^{k-n}, \quad k = n, n+1, n+2, \cdots
$$
记为 $X \sim \mathrm{NegBin}(n, p)$，其中 $n$ 为正整数，$0 < p < 1$。[[#几何分布]]是 $n = 1$ 的负二项分布。

若 $X \sim \mathrm{NegBin}(n, p)$，则 $\mathbb{E} \left[ X \right] = \cfrac{n}{p}$，$\mathrm{Var}[X] = \cfrac{n (1 - p)}{p^{2}}$。

负二项分布的**母函数**为
$$
G_{X}(z) = \mathbb{E} \left[ z^{X} \right] = \left( \dfrac{p z}{1 - (1 - p) z} \right)^{n}, \quad |z| < \dfrac{1}{1 - p}
$$

## 多元相关的矩阵分析

对于一组随机变量 $\v{X} = \begin{pmatrix}X_{1} & X_{2} & \cdots & X_{n}\end{pmatrix}^{\mathrm{T}}$，其**相关矩阵 (correlation matrix)** 定义为
$$
\boldsymbol{R}_{\v{X}} = \mathbb{E} \left[\v{X} \v{X}^{\mathrm{H}}\right] = \begin{pmatrix}
\mathbb{E}[X_{1} X_{1}^{*}] & \mathbb{E}[X_{1} X_{2}^{*}] & \cdots & \mathbb{E}[X_{1} X_{n}^{*}] \\
\mathbb{E}[X_{2} X_{1}^{*}] & \mathbb{E}[X_{2} X_{2}^{*}] & \cdots & \mathbb{E}[X_{2} X_{n}^{*}] \\
\vdots & \vdots & \ddots & \vdots \\
\mathbb{E}[X_{n} X_{1}^{*}] & \mathbb{E}[X_{n} X_{2}^{*}] & \cdots & \mathbb{E}[X_{n} X_{n}^{*}]
\end{pmatrix} = \big( \mathbb{E}\left[ X_{i} X_{j} \right] \big)_{i,j} 
$$
显然，相关矩阵是**共轭对称**的，并且是**正定**的。

若将 $\v{X}$ 的元素下标 $n$ 视作时间，则 $\v{X}$ 可视作随机过程 $X(n)$ 的一个**样本向量 (sample vector)**，其相关矩阵为该随机过程在这些时刻的相关函数值，即
$$
\boldsymbol{R}_{\v{X}} = \big( R_{X}(i,j) \big)_{i,j}
$$

### 去相关 (decorrelation)

考虑线性变换 $\v{Y} = \boldsymbol{A} \v{X}$，其中 $\boldsymbol{A}$ 为方阵。我们希望找到  使得 $\v{Y}$ 的各分量**不相关**，即 $\mathbb{E}[Y_{i} Y_{j}^{*}] = 0$，$\forall i \neq j$，或
$$
\boldsymbol{R}_{\v{Y}} = \mathbb{E}\left[ \v{Y}\v{Y}^{\mathrm{H}} \right] = \mathbb{E}\left[ \boldsymbol{A} \v{X}\v{X}^{\mathrm{H}} \boldsymbol{A}^{\mathrm{H}} \right] = \boldsymbol{A} \boldsymbol{R}_{\v{X}} \boldsymbol{A}^{\mathrm{H}}
= \boldsymbol{\varLambda}_{\v{Y}}
$$
其中 $\boldsymbol{\varLambda}_{\v{Y}}$ 是对角阵。

因 $\boldsymbol{R}_{\v{X}}$ 是正定的，故其**特征值均非负**，且可以做**特征值分解 (EVD)**
$$
\boldsymbol{R}_{\v{X}} = \boldsymbol{Q} \boldsymbol{\varLambda}_{\v{X}} \boldsymbol{Q}^{\mathrm{H}}
$$
其中 $\boldsymbol{Q}$ 是酉矩阵，$\boldsymbol{\varLambda}_{\v{X}} = \text{diag}(\lambda_{1}, \lambda_{2}, \ldots, \lambda_{n})$，$\lambda_{i} \geq 0$。取 $\boldsymbol{A} = \boldsymbol{Q}^{\mathrm{H}}$，即可保证 $\boldsymbol{R}_{\v{Y}} = \boldsymbol{\varLambda}_{\v{X}}$。

> [!theorem] 去相关变换
> 对随机变量 $\v{X}$，取 $\boldsymbol{R}_{\v{X}}$ 的**特征值分解** $\boldsymbol{R}_{\v{X}} = \boldsymbol{Q} \boldsymbol{\varLambda}_{\v{X}} \boldsymbol{Q}^{\mathrm{H}}$，则线性变换 
> $$\v{Y} = \boldsymbol{Q}^{\mathrm{H}} \v{X}$$ 
> 各分量**不相关**，且 $\boldsymbol{R}_{\v{Y}} = \boldsymbol{\varLambda}_{\v{X}}$，这个过程称为**去相关 (decorrelation)** 或**白化 (whitening)**。

### 主成分分析 (PCA)

考虑 $\v{X}$ 沿某个方向 $\v{\alpha}$ 的**投影**
$$
\mathrm{proj}_{\v{\alpha}} \v{X} = \v{\alpha} \left( \v{\alpha}^{\mathrm{T}} \v{\alpha} \right)^{-1} \v{\alpha}^{\mathrm{T}} \v{X} 
$$
我们希望找到 $\v{\alpha}$ 使得这个投影「最大」，即
$$
\vu{\alpha} = \arg\limits_{\v{\alpha}} \max\limits_{\|\v{\alpha}\| = 1} \mathbb{E}\left[ \left\| \mathrm{proj}_{\v{\alpha}} \v{X} \right\|^{2} \right]
= \arg\limits_{\v{\alpha}} \max\limits_{\|\v{\alpha}\| = 1} \mathbb{E}\left[ \dfrac{\left( \v{\alpha}^{\mathrm{T}} \v{X} \right)^{2}}{\v{\alpha}^{\mathrm{T}} \v{\alpha}} \right]
= \arg\limits_{\v{\alpha}} \max\limits_{\|\v{\alpha}\| = 1} \v{\alpha}^{\mathrm{T}} \boldsymbol{R}_{\v{X}} \v{\alpha}
$$

引入 Lagrange 乘子 $\lambda$，构造 Lagrange 函数 
$$
\mathcal{L}(\v{\alpha}, \lambda) = \v{\alpha}^{\mathrm{T}} \boldsymbol{R}_{\v{X}} \v{\alpha} - \lambda (\v{\alpha}^{\mathrm{T}} \v{\alpha} - 1)
$$
对 $\v{\alpha}$ 求梯度并令其为零，有
$$
\nabla_{\v{\alpha}} \mathcal{L}(\v{\alpha}, \lambda) = 2 \boldsymbol{R}_{\v{X}} \v{\alpha} - 2 \lambda \v{\alpha} = 0 \quad \Longrightarrow \quad \boldsymbol{R}_{\v{X}} \v{\alpha} = \lambda \v{\alpha}
$$
因此，$\v{\alpha}$ 必须是 $\boldsymbol{R}_{\v{X}}$ 的**特征向量 (eigenvector)**，$\lambda$ 是对应的**特征值 (eigenvalue)**。而
$$
\v{\alpha}^{\mathrm{T}} \boldsymbol{R}_{\v{X}} \v{\alpha} = \lambda \v{\alpha}^{\mathrm{T}} \v{\alpha} = \lambda
$$
因此应取最大的特征值对应的特征向量。

### 双正交展开 (bi-orthogonal expansion)

#### 随机变量列的双正交展开

在[[#去相关 (decorrelation)]] 中，我们已经知道可以通过线性变换将随机变量列 $\v{X}$ 变为不相关的随机变量列 $\v{Y} = \boldsymbol{Q}^{\mathrm{H}} \v{X}$，其中 $\boldsymbol{Q}$ 是 $\boldsymbol{R}_{\v{X}}$ 的特征向量矩阵。

考虑逆变换
$$
\v{X} = \boldsymbol{Q} \v{Y} = \sum\limits_{i=1}^{n} Y_{i} \v{q}_{i}
$$
其中 $\v{q}_{i}$ 是 $\boldsymbol{Q}$ 的第 $i$ 列，即 $\boldsymbol{R}_{\v{X}}$ 的第 $i$ 个特征向量。显然，

+ $\left< Y_{i}, Y_{j} \right> = \mathbb{E}[Y_{i} Y_{j}^{*}] = 0$，$\forall i \neq j$，即 $\v{Y}$ 的各分量**正交**；
+ $\left< \v{q}_{i}, \v{q}_{j} \right> = \v{q}_{i}^{\mathrm{H}} \v{q}_{j} = 0$，$\forall i \neq j$，即 $\boldsymbol{Q}$ 的各列**正交**。

因此，上面的展开称为**双正交展开 (bi-orthogonal expansion)**。

#### 随机过程的双正交展开

考虑宽平稳随机过程 $X(t)$，我们希望找到一组函数 $\{\phi_{n}(t)\}$ 和一组随机变量 $\{\alpha_{n}\}$，使得
$$
X(t) = \sum\limits_{k=-\infty}^{+\infty} \alpha_{k} \phi_{k}(t)
$$
且 $\{\phi_{n}(t)\}$ 和 $\{\alpha_{n}\}$ 分别**正交**，即
$$
\begin{cases}
\left< \phi_{i}, \phi_{j} \right> = \dint_{-\infty}^{+\infty} \phi_{i}(t) \phi_{j}^{*}(t) \dif t = \delta_{ij}, \\
\left< \alpha_{i}, \alpha_{j} \right> = \mathbb{E}[\alpha_{i} \alpha_{j}^{*}] = \lambda_{i} \delta_{ij}
\end{cases}
$$
其中 $\lambda_{i} \geq 0$。

注意到 $\boldsymbol{R}_{\v{X}}$ 的特征向量 $\left\{  \v{q}_{i}  \right\}$ 是**正交归一化**的，因此可取 $\phi_{i}(t) = q_{i}(t)$，其中 $q_{i}(t)$ 是 $\v{q}_{i}$ 的插值函数，即有
$$
\boldsymbol{R}_{\v{X}} \v{q}_{i} = \left( \sum\limits_{j=1}^{n} R_{X} (k, j) \phi_{i}(j) \right)_{k} = \lambda_{i} \v{q}_{i} = \big( \lambda_{i}\phi_{i}(k) \big) _{k}
$$
取 $n \to \infty$，则可以猜想有
$$
\dint_{-\infty}^{+\infty} R_{X}(t,s) \phi_{i}(s) \dif s = \lambda_{i} \phi_{i}(t)
$$




# 随机过程的平稳性

## 二阶矩随机过程

> [!definition] 随机过程
> **随机过程 (stochastic process)** 是一组随机变量的集合 $\{X(t) \mid t \in T\}$，其中 $T \subset \mathbb{R}$ 通常是时间参数集。
> 一个随机过程可视作同时依赖于**样本空间 $\varOmega$ 中的样本点**和**时间 $t$** 的二元函数，即
> $$
> X(\omega, t): \varOmega \times T \to \mathbb{R} 
> $$
^SuijiGuocheng

若随机过程 $X(t)$ 在每个时刻 $t$ 的二阶矩存在，即 $\mathbb{E}[|X(t)|^2] < +\infty$，则称 $X(t)$ 为**二阶矩随机过程 (second-order moment stochastic process)**。二阶矩过程的均值和方差都存在，是电子技术与通信领域中最常见的随机过程。[^1]

[^1]: [陆大䋮，张颢：《随机过程及其应用》](<file:///E:\Schoolworks\Tsinghua\2025秋\课程\概率论与随机过程（2）\随机过程及其应用 (陆大絟 张颢) (Z-Library).pdf>)，北京：清华大学出版社，2012 年，p. 5。

### 随机过程的相关性

我们考察随机过程 $X(t)$ 在任意两个时刻 $t_{1}$ 和 $t_{2}$ 的统计关系。类比于[[#随机变量的基础概念#^SuijiBianliangXiangguan|随机变量的相关]]，定义

> [!definition] 相关函数
> 对于[[#^SuijiGuocheng|随机过程]] $X(t)$，任取两个时刻 $t_{1}$ 和 $t_{2}$，则 $X(t_{1})$、$X(t_{2})$ 是两个随机变量，其**相关**定义为 $X(t)$ 的**相关函数 (correlation function)**，即
> $$
> R_{X} (t_{1}, t_{2}) = \mathbb{E}\left[X(t_{1}) \overline{ X(t_{2}) }\right]
> $$

显然，
+ 同一时点的相关函数**非负**，即 
$$R_{X}(t,t) = \mathbb{E}\left[|X(t)|^2\right] \geq 0$$
+ 相关函数是**对称**的，即
$$R_{X}(t, s) = \overline{ R_{X}(s, t) }$$

类似可以定义实随机过程的**协方差函数 (covariance function)**
$$
C_{X}(t_{1}, t_{2}) = \mathbb{E} \left[ \big( X(t_{1}) - \mathbb{E}[X(t_{1})] \big) \overline{ \big( X(t_{2}) - \mathbb{E}[X(t_{2})] \big) } \right]
$$
其与相关函数的关系为
$$
C_{X}(t_{1},t_{2}) = R_{X}(t_{1},t_{2}) - \mathbb{E} \left[ X(t_{1}) \right] \overline{ \mathbb{E} \left[ X(t_{2}) \right]  }
$$

> [!definition] 函数的正定性
> 我们称一个函数 $f(t)$ 是**正定 (positive definite)** 的，若对于任意整数 $n$ 和任意实数 $t_{1}, t_{2}, \ldots, t_{n}$，矩阵 $\big( f(t_{i} - t_{j}) \big)_{i,j}$ 是正定的。

我们考虑随机过程 $X(t)$ 的有限维向量 $\v{X} = \big( X(t_{1}), X(t_{2}), \cdots, X(t_{n}) \big)^{\mathrm{T}}$，则
$$
\boldsymbol{R} = \mathbb{E}\left[\v{X} \cdot \v{X}^{\mathrm{H}}\right] 
= \Big(\mathbb{E}\left[ X(t_{i}) \overline{ X(t_{j}) } \right]\Big)_{i,j}
= \big( R_{X}(t_{i}, t_{j}) \big)_{i,j}
$$
而 $\forall \v{x} \in \mathbb{C}^{n}$，
$$
\v{x}^{\mathrm{H}}\boldsymbol{R}\v{x} = \mathbb{E}\left[ \left( \v{x}^{\mathrm{H}}\v{X} \right) \overline{ \left( \v{x}^{\mathrm{H}}\v{X} \right) } \right] = \mathbb{E}\left[ \left|\v{x}^{\mathrm{H}}\v{X}\right|^2 \right] \geq 0
$$
因此 $\boldsymbol{R}$ 是正定的。

> [!theorem] 相关函数的正定性
> 任意二阶矩随机过程 $X(t)$ 的**相关函数 $R_{X}(s,t)$ 是正定的**。
^XiangguanHanshuZhengding

正定性是相关函数的一种特征性质。如果一个二元函数具有正定性，则一定可以构造一个随机过程，使得该函数为其相关函数。

### 随机过程的平稳性

**平稳性 (stationarity)** 描述随机过程在时间平移前后的统计特性变化。若随机过程的任意有限维分布在时间平移后不变，即 $F_{X(t_{1}+\tau), \cdots, X(t_{n}+\tau)} = F_{X(t_{1}), \cdots, X(t_{n})}$，则称该随机过程为**严平稳 (strict-sense stationary)** 随机过程，其各种性质都与绝对时间无关。

严平稳过程要求太高，信号缺少「发挥空间」。下面给出一个**假定**，研究符合下面性质的随机过程：
> [!definition] 宽平稳随机过程
> 若随机过程 $X(t)$ 满足对于任意 $T$，
> 
> + $\mathbb{E}[X(t+T)] = \mathbb{E}[X(t)]$，即**均值与时间无关**；
> + $R_{X}(t_{1}+T, t_{2}+T) = R_{X}(t_{1}, t_{2})$，即**相关函数只与时间差 $t_{2}-t_{1}$ 有关**，
> 
> 则称 $X(t)$ 为**宽平稳 (wide-sense stationary, WSS)** 随机过程。
^KuanpingwenSuijiguocheng

对宽平稳随机过程 $X(t)$，相关函数 $R_{X}(s,t)$ 可简写为 $R_{X}(s - t)$。

#### 宽平稳随机过程的性质

对宽平稳随机过程 $X(t)$，其相关函数有以下性质：
+ 相关函数**共轭对称**，$R_{X}(\tau) = \overline{ R_{X}(-\tau) }$；
+ $|R_{X}(\tau)| \le R_{X}(0)$，且 $R_{X}(0) = \mathbb{E}\left[ |X(t)|^2 \right] \ge |\mathbb{E}[X(t)]|^2$；
+ $R_{X}(\tau)$ 是一元正定函数。

> [!theorem] 宽平稳随机过程的周期性
> 对于宽平稳随机过程 $X(t)$，若存在 $T \neq 0$ 使得 $R_{X}(0) = R_{X}(T)$，则 $R_{X}(t)$ **以 $T$ 为周期**，即
> $$
> \exists T \neq 0, \quad R_{X}(0) = R_{X}(T) \quad \implies \quad 
> \forall \tau, \quad R_{X}(\tau) = R_{X}(\tau + T)
> $$

### 随机过程的均方微积分

《概率论与随机过程（1）》曾介绍过随机变量列的**几乎处处收敛 $X_n \xrightarrow{\text{a.e.}} X$**、**依概率收敛 $X_n \xrightarrow{\mathrm{p}} X$**、**依分布收敛 $X_n \xrightarrow{\mathrm{d}} X$** 等概念。对于二阶矩随机过程 $X(t)$，常使用其在时间 $t$ 上的**均方收敛 (mean-square convergence)**。

> [!definition] 随机变量列**均方收敛**的极限
> 设随机变量列 $\{X_n\}$ 和随机变量 $X$ 都有有限二阶矩，若 $\forall \varepsilon > 0$，$\exists N \in \mathbb{N}$，使得当 $n > N$ 时
> $$
> \sqrt{ \mathbb{E}\left[ |X_n - X|^2 \right] } < \varepsilon
> $$
> 也即 $\lim\limits_{ n \to \infty } \sqrt{ \mathbb{E} \left[ |X_{n} - X|^{2} \right] } = 0$，则称 $\{X_n\}$ **均方收敛**于 $X$，记为 $X_n \xrightarrow{\mathrm{m.s.}} X$，或记为 $\mathop{\mathop{}\textbf{l.i.m}\mathop{}}\limits_{n \to \infty} X_n = X$，其中 **l.i.m** 表示**均方极限 (limit in mean-square)**。

在时间参数集 $T$ 连续的情况下，类似可以用 $\varepsilon$-$\delta$ 语言定义任意时间 $t_{0}$ 处的 $\mathop{\mathop{}\textbf{l.i.m}\mathop{}}\limits_{t \to t_{0}} X(t) = X$，进而可以定义其均方连续、均方可导、均方可积等性质。

#### 均方连续

如果二阶矩随机过程 $X(t)$ 在 $t_{0}$ 处满足
$$
\lim_{ t \to t_{0} } \sqrt{ \mathbb{E}\left[ |X(t) - X(t_{0})|^2 \right] } = 0
$$
即 $\mathop{\mathop{}\textbf{l.i.m}\mathop{}}\limits_{t \to t_{0}} X(t) = X(t_{0})$，则称 $X(t)$ 在 $t_{0}$ 处**均方连续 (mean-square continuous)**。如果 $X(t)$ 在时间参数集 $T$ 的每个点均**均方连续**，则称 $X(t)$ **在 $T$ 上均方连续**。

> [!theorem] 均方连续的充分必要条件
> 对在开区间 $T \subseteq \mathbb{R}$ 上的二阶矩随机过程 $X(t)$，以下命题等价：
> + $X(t)$ 在 $T$ 上均方连续；
> + $R_{X}(t_{1}, t_{2})$ 在 $T \times T$ 上连续；
> + $\forall t \in T$，$R_{X}(t_{1}, t_{2})$ 在 $(t,t)$ 处连续。
> 
> 特别地，对**宽平稳随机过程** $X(t)$，其均方连续的充分必要条件为 **$R_{X}(\tau)$ 在 $\tau = 0$ 处连续**。

#### 均方可导、均方可积

若二阶矩随机过程 $X(t)$ 在 $t_{0}$ 处满足
$$
\mathop{\mathop{}\textbf{l.i.m}\mathop{}}\limits_{h \to 0} \dfrac{ X(t_{0} + h) - X(t_{0}) }{ h } = Y(t_{0})
$$
则称 $X(t)$ 在 $t_{0}$ 处**均方可导 (mean-square differentiable)**，$Y(t_{0})$ 为 $X(t)$ 在 $t_{0}$ 处的**均方导数 (mean-square derivative)**，记为 $X'(t_{0})$、$\cfrac{\dif X(t)}{\dif t}\Bigg|_{t=t_{0}}$ 或 $\dot{X}(t_{0})$。如果 $X(t)$ 在时间参数集 $T$ 的每个点均**均方可导**，则称 $X(t)$ **在 $T$ 上均方可导**。

一般地，确认可导性前具体导数值未知，用这一定义判断均方可导性较为困难。下面给出一个更易用的判定条件。

> [!theorem] 均方可导的充分必要条件
> 随机过程 $X(t)$ 在 $t_{0}$ 处**均方可导**的充分必要条件为 $R_{X}(t_{1}, t_{2})$ 在 $(t_{0}, t_{0})$ 处**二阶广义可微**，即存在极限
> $$
> \lim\limits_{ \substack{h \to \infty \\ k \to \infty }} \dfrac{ R_{X}(t_{0}+h, t_{0}+k) - R_{X}(t_{0}+h, t_{0}) - R_{X}(t_{0}, t_{0}+k) + R_{X}(t_{0}, t_{0}) }{ h k }
> $$

由此得到一个更方便的**充分条件**：若 $\cfrac{ \partial^{2} }{ \partial t_{1} \partial t_{2} }R_{X}(t_{1}, t_{2})$ 在 $(t_{0}, t_{0})$ 的邻域内存在且在 $(t_{0}, t_{0})$ 处连续，则上述极限存在，$X(t)$ 在 $t_{0}$ 处**均方可导**。

对于**宽平稳随机过程** $X(t)$，其均方可导的充分必要条件为 $R_{X}(\tau)$ 在 $\tau = 0$ 处**二阶广义可微**，或者 $\cfrac{ \dif^{2} }{ \dif \tau^{2} } R_{X}(\tau)$ 在 $\tau = 0$ 处存在、有限。

对应地，若二阶矩随机过程 $X(t)$ 及确定性函数 $h(t)$ 满足 $\dint_{a}^{b} \dint_{a}^{b} R_{X}(s,t) h(s) h(t) \dif s \dif t$ 存在，则 $X(t)h(t)$ 在 $[a,b]$ 上**均方可积 (mean-square integrable)**，且其均方积分定义为 Riemann 和的均方极限
$$
\dint_{a}^{b} X(t) h(t) \dif t =
\mathop{\mathop{}\textbf{l.i.m}\mathop{}}\limits_{\substack{n \to \infty \\ \max \{ \Delta t_{i} \} \to 0}} \sum\limits_{i=1}^{n} X(t_{i}^{*}) h(t_{i}^{*}) \Delta t_{i}
$$

#### † 均值遍历

**均值遍历性 (mean ergodicity)** 描述随机过程的时间平均 $\left\langle X(t) \right\rangle$ 和统计平均 $\mathbb{E}[X(t)]$ 之间的关系。若对于随机过程 $X(t)$，其时间平均**以某种方式收敛**于统计平均，则称 $X(t)$ 为**均值遍历**的随机过程。

对于宽平稳随机过程 $X(t)$，通常以**均方收敛**考察均值遍历性，即
$$
\mathop{\mathop{}\textbf{l.i.m}\mathop{}}\limits_{T \to \infty} \dfrac{1}{2T} \dint_{-T}^{T} X(t) \dif t = \mathbb{E}[X(t)] = m_{X}
$$
注意此时左侧的积分不是均方积分，而是沿选中的样本轨道做普通的 Riemann 积分，在 $T \to \infty$ 时才合并样本轨道为均方极限。

对于实数宽平稳过程，以下命题等价：
+ $X(t)$ 是均值遍历的；
+ $\lim\limits_{T \to \infty} \dfrac{1}{T} \dint_{-T}^{T} \left( 1 - \cfrac{|\tau|}{T} \right) C_{X}(\tau) \dif \tau = 0$；
+ $\lim\limits_{T \to \infty} \dfrac{1}{T} \dint_{-T}^{T} C_{X}(\tau) \dif \tau = 0$。

并且，有如下两个推论：
+ 若 $C_{X}(\tau)$ 可积，即 $\dint_{0}^{+\infty} C_{X}(\tau) \dif \tau < +\infty$，则 $X(t)$ 是均值遍历的；
+ 若 $C_{X}(0)$ 有限，而**足够远处 $\lim\limits_{\tau \to \infty} C_{X}(\tau) = 0$**，则 $X(t)$ 是均值遍历的。


## 宽平稳随机过程的谱分析

### 相关函数的谱表示

我们已经知道[[#^XiangguanHanshuZhengding|相关函数的正定性]]，下面考虑如何对给定的正定函数 $R(\tau)$ 构造一个宽平稳随机过程 $X(t)$，使得 $R(\tau)$ 成为其相关函数。

> [!theorem] 正定函数与 Fourier 变换的关系
> 函数 $f(t)$ 是**正定**的，当且仅当其 **Fourier 变换 $\hat{f}(\omega)$ 非负**。
^ZhengdingHanshuYuFourierBianhuanDeGuanxi

> [!proof]- [[#^ZhengdingHanshuYuFourierBianhuanDeGuanxi|「正定函数与 Fourier 变换的关系」]]的证明
> ***Sufficiency***：
> 对 $\e^{\J \omega t}$，显然有
> $$
> \big( \e^{\J\omega (t_{i} - t_{j})} \big)_{i,j} = \v{g} \v{g}^{\mathrm{H}}, \quad \v{g} = \big( \e^{\J\omega t_{1}}, \e^{\J\omega t_{2}}, \cdots, \e^{\J\omega t_{n}} \big)^{\mathrm{T}}
> $$
> 因此 **$\e^{\J \omega t}$ 是正定的**。进而，对任意实函数 $\hat{f}(\omega) \geq 0$，有 **Fourier 逆变换**函数
> $$
> f(t) = \dfrac{1}{2\pi} \int_{-\infty}^{+\infty} \hat{f}(\omega) \e^{\J\omega t} \dif \omega
> $$
> 是**正定**的。
> 
> ***Necessity***：
> 若 $f(t)$ 是正定的，则对任意整数 $n$ 和任意实数 $t_{1}, t_{2}, \cdots, t_{n}$，矩阵 $\big( f(t_{i} - t_{j}) \big)_{i,j}$ 也是正定的。特别地，取定 $\v{x} = \big( \e^{-\J \omega t_{1}}, \e^{-\J\omega t_{2}}, \cdots, \e^{-\J\omega t_{n}}\big)$，则正定性要求
> $$
> \v{x}^{\mathrm{H}} \big( f(t_{i} - t_{j}) \big)_{i,j} \v{x} 
> = \sum\limits_{i=1}^{n} \sum\limits_{j=1}^{n} f(t_{i} - t_{j}) \e^{-\J \omega (t_{i} - t_{j})} \geq 0
> $$
> 进而转换为积分形式，有
> $$
> \dfrac{1}{T} \dint_{-T}^{T} \dint_{-T}^{T} f(t-s) \e^{-\J\omega (t-s)} \dif t  \dif s \ge 0
> $$
> 做变量替换 $u = t-s$，$v = t + s$，Jacobian 行列式为 $\left| \dfrac{ D (t,s) }{ D (u,v) } \right| = \dfrac{1}{2}$，积分区域变为 $|u| \leq 2T$、$|v| \leq 2T - |u|$ 的菱形，因此
> $$
> \begin{align}
> \mathrm{LHS} &= \dfrac{1}{T} \dint_{-2T}^{2T} \dint_{|u| - 2T}^{2T - |u|} f(u) \e^{-\J \omega u} \cdot \frac{1}{2} \dif v \dif u \\
> &= \dfrac{1}{2T} \dint_{-2T}^{2T} f(u) \e^{-\J \omega u} (4T - 2|u|) \dif u 
> = \dint_{-2T}^{2T} \left( 2 - \dfrac{|u|}{T} \right)  f(u) \e^{-\J \omega u} \dif u  \\
> &\xrightarrow[\text{Lebesgue dominated}]{T \to +\infty} 2\dint_{-\infty}^{+\infty} f(u) \e^{-\J \omega u} \dif u \geq 0
> \end{align}
> $$
> 因此，**正定函数 $f(t)$ 的 Fourier 变换**
> $$
> \hat{f}(\omega) = \dint_{-\infty}^{+\infty} f(t) \e^{-\J \omega t} \dif t \geq 0
> $$
> **非负**。
^ZhengdingHanshuYuFourierBianhuanDeGuanxiProof

上述定理启发我们，相关函数的 Fourier 变换非负，而相关函数本身是随机过程的二阶矩，因此这个 Fourier 变换应当与随机过程的**功率—频率**关系有关。下面仿照上述证明过程，定义随机过程的**功率谱**，这样即可认为构造出了一个以给定正定函数 $R(\tau)$ 为相关函数的宽平稳随机过程。

#### 随机过程的功率谱

对于一般的随机过程 $X(t)$，不能保证 $\dint |X(t)| \dif t < \infty$，因此不能直接进行 Fourier 变换。

随机过程的**功率谱 (power spectrum)** 定义为随机过程 $X_{T}(t)$ 的**截断** Fourier 变换 (STFT) 的模平方期望的极限。

> [!definition] 随机过程的功率谱密度
> 对于随机过程 $X(t)$，定义其**功率谱密度 (power spectrum density)** 为
> $$
> S_{X}(\omega) = \lim_{T \to +\infty} \dfrac{1}{2T} \mathbb{E}\left[ \left| \dint_{-T}^{T} X(t) \e^{-\J \omega t} \dif t \right|^2 \right]
> $$
^GonglvpuMidu

显然，$S_{X}(\omega) \geq 0$；展开后，有
$$
\begin{align}
S_{X}(\omega) &= \lim_{T \to +\infty} \dfrac{1}{2T} \mathbb{E}\left[ \left( \dint_{-T}^{T} X(t) \e^{-\J \omega t} \dif t \right) \overline{ \left( \dint_{-T}^{T} X(s) \e^{\J \omega s} \dif s \right) } \right] \\
&= \lim\limits_{ T \to +\infty } \dfrac{1}{2T} \dint_{-T}^{T} \dint_{-T}^{T} \mathbb{E}[X(t) X^{*}(s)] \e^{-\J \omega (t-s)} \dif t \dif s \\
&= \dint_{-\infty}^{+\infty} R_{X}(u) \e^{-\J \omega u} \dif u = \mathscr{F}\{R_{X}(t)\}
\end{align}
$$
其中第 3 个等号与上面[[#^ZhengdingHanshuYuFourierBianhuanDeGuanxiProof|「正定函数与 Fourier 变换的关系」的证明]]类似，用到 $R_{X}(\tau) = \mathbb{E} \left[ X(t+\tau)X(t) \right]$，因此一般需要 $X(t)$ 为**宽平稳随机过程**。

> [!theorem] Wiener-Khinchin 关系
> 宽平稳随机过程 $X(t)$ 的**功率谱密度 $S_{X}(\omega)$ 是其相关函数 $R_{X}(t)$ 的 Fourier 变换**，即
> $$
> S_{X}(\omega) = \mathscr{F}\{R_{X}(t)\} = \dint_{-\infty}^{+\infty} R_{X}(t) \e^{-\J \omega t} \dif t
> $$
> 反之，
> $$
> R_{X}(t) = \mathscr{F}^{-1}\{S_{X}(\omega)\} = \dfrac{1}{2\pi} \dint_{-\infty}^{+\infty} S_{X}(\omega) \e^{\J \omega t} \dif \omega
> $$
^Wiener-Khinchin

常见**相关函数** $R(\tau)$ 与对应**功率谱密度** $S(\omega)$ 有

| 相关函数 $R(\tau)$                                                                                                                                       | 功率谱密度 $S(\omega)$                                                                                                                                                        | 注     |
| :--------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---- |
| $R(\tau) = \e^{-\alpha \vert \tau \vert},\quad \alpha > 0$                                                                                           | $S(\omega) = \cfrac{2\alpha}{\alpha^2 + \omega^2}$                                                                                                                       |       |
| $R(\tau) = \delta(\tau)$                                                                                                                             | $S(\omega) = 1$                                                                                                                                                          | 理想白噪声 |
| $R(\tau) = \cos \omega_0 \tau$                                                                                                                       | $S(\omega) = \pi (\delta(\omega - \omega_0) + \delta(\omega + \omega_0))$                                                                                                | 随机相位  |
| $R(\tau) = \cfrac{\sin \omega_0 \tau}{\omega_0 \tau}$                                                                                                | $S(\omega) = \begin{cases} \cfrac{\pi}{\omega_0}, & \vert \omega \vert \le \omega_0 \\ 0, & \vert \omega \vert > \omega_0 \end{cases}$                                   | 理想低通  |
| $R(\tau) = \begin{cases} 1 - \cfrac{2 \vert \tau \vert}{T}, & \vert \tau \vert \le \cfrac{T}{2} \\ 0, & \vert \tau \vert > \cfrac{T}{2} \end{cases}$ | $S(\omega) = \cfrac{8 \sin^2 \left( \cfrac{\omega T}{4} \right)}{\omega^2 T}$                                                                                            |       |
| $R(\tau) = \e^{-\alpha \vert \tau \vert} \cos \omega_0 \tau,\quad \alpha > 0$                                                                        | $S(\omega) = \cfrac{\alpha}{\alpha^2 + (\omega - \omega_0)^2} + \cfrac{\alpha}{\alpha^2 + (\omega + \omega_0)^2}$                                                        |       |
| $R(\tau) = \e^{-\alpha \tau^2},\quad \alpha > 0$                                                                                                     | $S(\omega) = \sqrt{\cfrac{\pi}{\alpha}} \e^{-\tfrac{\omega^2}{4\alpha}}$                                                                                                 |       |
| $R(\tau) = \e^{-\alpha \tau^2} \cos \beta \tau,\quad \alpha > 0$                                                                                     | $S(\omega) = \cfrac{1}{2} \sqrt{\cfrac{\pi}{\alpha}} \left( \e^{-\tfrac{(\omega - \beta)^2}{4\alpha}} + \e^{-\tfrac{(\omega + \beta)^2}{4\alpha}} \right)$               |       |
| $R(\tau) = \cfrac{2 \sin \left( \cfrac{\Delta \omega}{2} \tau \right)}{\pi \tau} \cos(\omega_0 \tau)$                                                | $S(\omega) = \begin{cases} 1, & \omega_0 - \cfrac{\Delta \omega}{2} \le \vert \omega \vert \le \omega_0 + \cfrac{\Delta \omega}{2} \\ 0, & \text{otherwise} \end{cases}$ | 理想带通  |

对于离散时间的宽平稳随机过程 $X[n]$，Wiener-Khinchin 关系类似，只是变为 **DTFT 关系**，即
$$
S_{X}(\e^{\J \omega}) = \sum\limits_{n=-\infty}^{+\infty} R_{X}[n] \e^{-\J \omega n}, \qquad 
R_{X}[n] = \dfrac{1}{2\pi} \int_{-\pi}^{\pi} S_{X}(\e^{\J \omega}) \e^{\J \omega n} \dif \omega
$$

尽管一般只对**宽平稳**随机过程定义功率谱，但实则只需要满足**相关函数的平稳性**即可有 Wiener-Khinchin 关系。

> [!note] 功率谱的物理意义
> 功率谱描述随机过程**在不同频率上的功率分布**情况。对功率谱 $S_{X}(\omega)$ 在全频域积分，有
> $$
> \dint_{-\infty}^{+\infty} S_{X}(\omega) \dif \omega = 2\pi R_{X}(0) = 2\pi \mathbb{E}\left[|X(t)|^2\right]
> $$
> 此即随机过程 $X(t)$ 的**功率**。

对于**实值宽平稳**随机过程 $X(t)$，相关函数 $R_{X}(\tau) = \mathbb{E}\left[ X(t)X(t + \tau) \right]$ 即为**实值偶函数**，因此
$$
\begin{align}
S_{X}(\omega) &= \dint_{-\infty}^{+\infty} R_{X}(t) \e^{-\J \omega t} \dif t \\
&= \dint_{-\infty}^{+\infty} R_{X}(t) \cos(\omega t) \dif t - \J \dint_{-\infty}^{+\infty} \underbrace{ R_{X}(t) \sin(\omega t) }_{ \text{odd} } \dif t \\
&= \dint_{-\infty}^{+\infty} R_{X}(t) \cos(\omega t) \dif t = S_{X}(-\omega)
\end{align}
$$
功率谱 $S_{X}(\omega)$ 也为**实值偶函数**。

#### † 谱分布函数

功率谱密度 $S_X(\omega)$ 是针对平稳过程的相关函数 $R_X(\tau)$ 做 Fourier 变换得到的。但并非所有随机过程都存在密度函数，更一般的描述是**谱分布函数 (spectral distribution function)** $F_X(\omega)$。

**Bochner-Khinchin 定理**指出，任意的连续一元正定函数 $R(\tau)$ 都可以表示为某个**非减**函数 $F(\omega)$ 的 Fourier-Stieltjes 变换
$$
R(\tau) = \dint_{-\infty}^{+\infty} \e^{\J \omega \tau} \dif F(\omega) 
$$
其中 $F(\omega)$ 即为**谱分布**函数；若进一步满足 $\dint_{-\infty}^{+\infty} |R(\tau)| \dif \tau < \infty$，则 $F(\omega)$ 可导且导数即为功率谱密度 $S(\omega) = \cfrac{\dif F(\omega)}{\dif \omega}$。


### † 随机过程的谱表示

考虑如下的两个空间
$$
\begin{align}
X(t) &\longleftrightarrow \exp(\J \omega t) \\
\mathrm{span}\left\{ X(t) \right\} &\longleftrightarrow L^{2}(\mathbb{R}, \dif F_{X}(\omega))
\end{align}
$$
其中：
+ $\mathrm{span}\left\{ X(t) \right\} = L^{2}(\varOmega, \mathcal{F}, P)$ 是定义在概率空间 $(\varOmega, \mathcal{F}, P)$ 上的二次可积**随机变量**空间，其上 $X(t_{1})$ 与 $X(t_{2})$ 间距离**以均方意义定义**为
$$
d(X(t_{1}), X(t_{2})) = \sqrt{\mathbb{E} \left[ |X(t_{1}) - X(t_{2})|^2 \right]} = \sqrt{2(R_{X}(0) - R_{X}(t_{1} - t_{2}))}
$$
+ $L^{2}(\mathbb{R}, \dif F_{X}(\omega))$ 是定义在实数集 $\mathbb{R}$ 上、以复指数函数 $\exp(\J\omega t)$ 为基底的二次可积**函数**空间，其上 $F(\omega)$ 与 $G(\omega)$ 间距离**以 $\dif F_{X}(\omega)$ 定义**为
$$
\begin{align}
d^{2}(F, G) &= \int_{-\infty}^{\infty} |F(\omega) - G(\omega)|^2 \dif F_{X}(\omega) \\
&= \dfrac{1}{2\pi} \dint_{\infty}^{\infty} S_{X}(\omega) |F(\omega) - G(\omega)|^2 \dif \omega
\end{align}
$$

下面证明，这两个空间构成**等距同构 (isometric isomorphism)**，即
$$
\mathbb{E} \left[ |X(t_{1}) - X(t_{2})|^{2} \right] = \dfrac{1}{2\pi} \dint_{-\infty}^{\infty} S_{X}(\omega) |\exp(\J\omega t_{1}) - \exp(\J\omega t_{2})|^2 \dif \omega
$$
利用欧拉公式 $|\e^{\J\theta_1} - \e^{\J\theta_2}|^2 = 2 - 2\cos(\theta_1 - \theta_2)$，得到
$$
\begin{align} 
\text{RHS}
&= \frac{1}{2\pi} \int_{-\infty}^{+\infty} \left|\e^{\J\omega t_1} - \e^{\J\omega t_2}\right|^2 S_X(\omega) \dif \omega \\
&= \frac{1}{2\pi} \int_{-\infty}^{+\infty} \big( 2 - 2\cos(\omega(t_1-t_2)) \big) S_X(\omega) \dif \omega \\
&= 2 \cdot \underbrace{\frac{1}{2\pi} \int S_X(\omega) \dif \omega}_{R_X(0)} - 2 \cdot \underbrace{\frac{1}{2\pi} \int \cos(\omega(t_1-t_2)) S_X(\omega) \dif \omega}_{R_X(t_1-t_2)} \\
&= 2R_X(0) - 2R_X(t_1-t_2) = \mathbb{E} \left[ |X(t_{1}) - X(t_{2})|^{2} \right] = \text{LHS}
\end{align}
$$
因此，随机过程 $X(t)$ 可以表示为
$$
X(t) = \dfrac{1}{2\pi} \dint_{-\infty}^{+\infty} \e^{\J \omega t} \dif Z(\omega)
$$
其中随机增量过程 $Z(\omega)$ 称为 $X(t)$ 的**谱过程**，满足
+ $\mathbb{E}[\dif Z(\omega)] = 0$；
+ $\mathbb{E}[|\dif Z(\omega)|^2] = S_{X}(\omega) \dif \omega$；
+ 对于 $\omega_{1} \neq \omega_{2}$，$\dif Z(\omega_{1})$ 与 $\dif Z(\omega_{2})$ **不相关**。

### LTI 系统对宽平稳随机过程的作用

以**宽平稳**随机过程 $X(t)$ 作为**线性时不变 (LTI) 系统 $h(t)$** 的输入，输出为随机过程 $Y(t)$，则
$$
Y(t) = X(t) * h(t) = \dint_{-\infty}^{+\infty} X(\tau) h(t - \tau) \dif \tau
$$
因此
$$
\begin{align}
R_{Y}(t, s) &= \mathbb{E} \left[Y(t) \overline{ Y(s) }\right] \\
&= \mathbb{E}\left[ \left( \dint_{-\infty}^{+\infty} X(\tau) h(t - \tau) \dif \tau \right) \overline{ \left( \dint_{-\infty}^{+\infty} X(\sigma) h(s - \sigma) \dif \sigma \right) } \right] \\
&= \dint_{-\infty}^{+\infty} \dint_{-\infty}^{+\infty} h(t - \tau) \overline{ h(s - \sigma) } \mathbb{E} \left[X(\tau) \overline{ X(\sigma) }\right] \dif \tau \dif \sigma \\
&= \dint_{-\infty}^{+\infty} \dint_{-\infty}^{+\infty} h(t - \tau) \overline{ h(s - \sigma) } R_{X}(\tau - \sigma) \dif \tau \dif \sigma
\end{align}
$$
记 $\t{h}(t) = \overline{ h(-t) }$，则
$$
R_{Y}(t, s) = \left( R_{X} * h * \t{h} \right) (t - s) 
$$
因此，**$Y(t)$ 也是宽平稳随机过程**，其**谱**函数为
$$
S_{Y}(\omega) = \mathscr{F} \left\{ R_{X} * h * \t{h} \right\} = S_{X}(\omega) \cdot H(\J\omega) \cdot \t{H}(\J\omega)
$$
而
$$
\t{H}(\J\omega) = \dint_{-\infty}^{+\infty} \overline{ h(-t) } \e^{-\J \omega t} \dif t = \dint_{-\infty}^{+\infty} \overline{ h(u) } \e^{\J \omega u} \dif u = \overline{ H(\J\omega) }
$$
因此
$$
S_{Y}(\omega) = S_{X}(\omega) \cdot H(\J\omega) \cdot \overline{ H(\J\omega) } = \mark{ S_{X}(\omega) |H(\J\omega)|^2 }
$$
其中 $H(\omega)$ 是系统 $h(t)$ 的**频率响应 (frequency response)**。

> [!example] [[例题#L5-1]]：滑动平均积分器对随机过程的作用

> [!example] [[例题#L5-2]]：白噪声通过 LTI 系统。

利用随机过程的谱分布函数，可以更直观地看到 LTI 系统对随机过程的作用。设随机过程 $X(t)$、$Y(t)$ 的谱分布函数分别为 $F_{X}(\omega)$、$F_{Y}(\omega)$，则
$$
\begin{align}
Y(t) &= \dint_{-\infty}^{\infty} h(t-\tau) X(\tau) \dif \tau = \dint_{-\infty}^{\infty} h(t-\tau) \dint_{-\infty}^{\infty} \exp(\J\omega \tau) \dif F_{X}(\omega) \dif \tau \\
&= \dint_{-\infty}^{\infty} \dint_{-\infty}^{\infty} \exp(\J\omega \tau) h(t-\tau) \dif \tau \dif F_{X}(\omega) \\
&= \dint_{-\infty}^{\infty} \dint_{-\infty}^{\infty} \exp(\J\omega (t - \tau')) h(\tau') \dif (t - \tau') \dif F_{X}(\omega) \\
&= \dint_{-\infty}^{\infty} \underbrace{ \left( \dint_{-\infty}^{\infty} \exp(-\J\omega \tau') h(\tau') \dif \tau' \right) }_{ H(\omega) } \exp(\J\omega t) \dif F_{X}(\omega) \\
&= \dint_{-\infty}^{\infty} H(\omega) \exp(\J\omega t) \dif F_{X}(\omega)
\end{align}
$$
对照 $Y(t) = \dint_{-\infty}^{\infty} \exp(\J\omega t) \dif F_{Y}(\omega)$，可见
$$
\dif F_{Y}(\omega) = H(\omega) \dif F_{X}(\omega)
$$
即 LTI 系统**频率响应**直接作用于随机过程的**谱分布函数**。

### 随机过程的互功率谱

对于两个**宽平稳随机过程 $X(t)$ 和 $Y(t)$**，其互相关函数为
$$
R_{XY}(\tau) = \mathbb{E}\left[ X(t + \tau) \overline{ Y(t) } \right],\qquad
R_{YX}(\tau) = \mathbb{E}\left[ Y(t + \tau) \overline{ X(t) } \right]
$$

考虑 $X(t)$ 通过 LTI 系统 $H(\omega)$ 得到输出 $Y(t)$，做谱分解
$$
\begin{align} 
&X(t) = \dint_{-\infty}^{+\infty} \e^{\J \omega t} \dif F_{X}(\omega), \\
&Y(t) = \dint_{-\infty}^{+\infty} \e^{\J \omega t} \dif F_{Y}(\omega) = \dint_{-\infty}^{+\infty} \e^{\J \omega t} H(\omega) \dif F_{X}(\omega)
\end{align}
$$
得到
$$
\begin{align}
R_{XY}(\tau) &= \mathbb{E}\left[ X(t + \tau) \overline{ Y(t) } \right] \\
&= \mathbb{E} \left[ \left( \dint_{-\infty}^{+\infty} \e^{\J \omega_{1} (t + \tau)} \dif F_{X}(\omega_{1}) \right) \left( \dint_{-\infty}^{+\infty} \e^{-\J \omega_{2} t} \overline{ H(\omega_{2}) } \dif \overline{F_{X}(\omega_{2})} \right) \right] \\
&= \dint_{-\infty}^{+\infty} \dint_{-\infty}^{+\infty} \e^{\J \omega_{1} \tau} \overline{ H(\omega_{2}) } \mathbb{E}\left[ \dif F_{X}(\omega_{1}) \dif \overline{F_{X}(\omega_{2})} \right] \\
&= \dfrac{1}{2\pi} \dint_{-\infty}^{+\infty} \e^{\J \omega \tau} \overline{ H(\omega) } S_{X}(\omega) \dif \omega
\end{align}
$$
因此，类比功率谱密度的定义，我们期望有
$$
R_{XY}(\tau) = \dfrac{1}{2\pi} \dint_{-\infty}^{+\infty} \underbrace{ \overline{ H(\omega) } S_{X}(\omega) }_{ S_{XY}(\omega) } \e^{\J \omega \tau} \dif \omega
$$

> [!definition] 随机过程的互功率谱密度
> 对于两个宽平稳随机过程 $X(t)$ 和 $Y(t)$，定义其**互功率谱密度 (cross power spectrum density)** 为
> $$
> S_{XY}(\omega) = \mathscr{F}\{ R_{XY}(\tau) \} = \dint_{-\infty}^{+\infty} R_{XY}(\tau) \e^{-\J \omega \tau} \dif \tau
> $$
> 其中 $R_{XY}(\tau) = \mathbb{E}\left[ X(t + \tau) \overline{ Y(t) } \right]$ 为互相关函数。

于是
$$
S_{XY}(\omega) = \overline{ H(\omega) } S_{X}(\omega), \qquad
S_{YX}(\omega) = \overline{ S_{XY}(\omega) } = H(\omega) S_{X}(\omega)
$$
互功率谱不再描述能量（功率）分布，也就不再一定是实值函数；它描述的是**两个随机过程在不同频率上的相关性**。

## 循环平稳过程

### 循环平稳过程的定义

我们已知**[[#^KuanpingwenSuijiguocheng|宽平稳过程]]** $X(t)$ 满足
$$
\forall T \in \mathbb{R}, \quad \begin{cases}
\mathbb{E} \left[ X(t+T) \right] = \mathbb{E} \left[ X(t) \right]  \\
R_{X}(s+T, t+T) = R_{X}(s,t)
\end{cases}
$$
因此，$R_{X}(s,t)$ 只与时间差 $t-s$ 有关。

类似地，若有随机过程 $X(t)$ 满足
$$
\exists T \neq 0, \quad \begin{cases}
\mathbb{E} \left[ X(t+T) \right] = \mathbb{E} \left[ X(t) \right]  \\
R_{X}(s+T, t+T) = R_{X}(s,t)
\end{cases}
$$
这个随机过程应该也有特殊的概率性质。

> [!definition] 循环平稳过程
> 对随机过程 $X(t)$，如果存在 $T \neq 0$，使得
> + $\mathbb{E} \left[ X(t+T) \right] = \mathbb{E} \left[ X(t) \right]$，即**均值具有周期性**，且
> + $R_{X}(s+T, t+T) = R_{X}(s,t)$，即**相关函数具有周期性**，
> 
> 则称 $X(t)$ 为**循环平稳 (cyclostationary)** 过程，或称为**周期平稳 (periodically stationary)** 过程。

循环平稳过程是典型的**非平稳随机过程**，但它的均值和相关函数都具有周期性，使得其分析相对简单。

### 循环平稳与宽平稳的联系

设有周期为 $T$ 的循环平稳过程 $X(t)$，我们考察其**移位过程**
$$
Y(t) = X(t + \theta)
$$
其中 $\theta \sim U (0, T)$ **独立**于 $X(t)$。则 $Y(t)$ 的相关为
$$
\begin{align}
R_{Y}(t, s) &= \mathbb{E} \left[ Y(t) Y(s) \right] = \mathbb{E} \left[ X(t+\theta) X(s+\theta) \right] \\
&= \mathbb{E}_{\theta} \left[ \mathbb{E}_{X\mid\theta} \left[ X(t + \theta) X(s + \theta) \mid \theta \right]\right]  \\
&= \mathbb{E}_{\theta} \left[ R_{X}(t + \theta, s + \theta) \right]  \\
&= \dfrac{1}{T} \dint_{0}^{T} R_{X}(t + \theta, s + \theta) \dif \theta = \dfrac{1}{T} \dint_{s}^{s+T} R_{X}(t - s + \theta', \theta') \dif \theta' \\
&= \dfrac{1}{T} \dint_{0}^{T} R_{X}(t - s + \theta', \theta') \dif \theta' = R_{Y}(t - s)
\end{align}
$$
可见，**移位过程 $Y(t)$ 是宽平稳过程**。

通过移位操作可以将循环平稳过程转化为宽平稳过程，从而利用宽平稳过程的分析方法研究循环平稳过程的性质。

> [!example] [[例题#L5-3]]：脉冲幅度调制
> 考察随机信号
> $$
> X(t) = \sum\limits_{k=-\infty}^{\infty} \alpha_{k} \phi(t - kT)
> $$
> 其中 $\{\alpha_{k}\}$ 是**平稳**的随机序列，满足
> $$
> \mathbb{E} \left[ \alpha_{k} \right] = 0, \qquad \mathbb{E} \left[ \alpha_{k} \alpha_{k+m} \right] = R_{\alpha}(m)
> $$
> 而 $\phi(t)$ 是一个给定的**基带 (baseband) 脉冲**，其自相关函数为
> $$
> R_{\phi}(\tau) = \dint_{-\infty}^{+\infty} \phi(t) \phi(t + \tau) \dif t
> $$



# † Hilbert 变换

## Hilbert 变换的引入

考虑一个线性滤波器
$$
H(\omega) = -\J \sgn (\omega) = \begin{cases}
-\J, & \omega > 0, \\
0, & \omega = 0, \\
\J, & \omega < 0
\end{cases}
$$
其时域冲激响应为
$$
h(t) = \frac{1}{2\pi} \int_{-\infty}^{+\infty} H(\omega) e^{\J \omega t} \dif \omega = \frac{1}{\pi t}
$$
该滤波器称为 **Hilbert 变换 (Hilbert transform)**，记作 $\mathscr{H}_{\mathrm{h}} \left\{ \cdot \right\}$。

### Hilbert 变换对复指数信号的作用

考虑输入信号为**复指数信号 $x(t) = \e^{\J \omega_{0} t}$**，则其频谱为
$$
\hat{x}(\omega) = 2\pi \delta(\omega - \omega_{0})
$$
不妨假设 $\omega_{0} > 0$，经过 Hilbert 变换后，输出频谱为
$$
\hat{y}(\omega) = H(\omega) \hat{x}(\omega) = -\J \sgn(\omega) \cdot 2\pi \delta(\omega - \omega_{0}) = -\J \cdot 2\pi \delta(\omega - \omega_{0})
$$
因此时域输出信号为
$$
y(t) = \mathscr{H}_{\mathrm{h}} \{ x(t) \} = -\J \e^{\J \omega_{0} t} = \e^{\J \left(\omega_{0} t - \tfrac{\pi}{2}\right)}
$$
若输入信号为**负频率**成分 $x(t) = \e^{-\J \omega_{0} t}$，则类似地可得输出信号为
$$
y(t) = \mathscr{H}_{\mathrm{h}} \{ x(t) \} = \J \e^{-\J \omega_{0} t} = \e^{-\J \left(\omega_{0} t - \tfrac{\pi}{2}\right)}
$$
即 Hilbert 变换将正频率成分的相位延迟了 $\cfrac{\pi}{2}$。

因此，
+ 对余弦输入 $\cos (\omega_{0} t) = \cfrac{1}{2} \left( \e^{\J \omega_{0} t} + \e^{-\J \omega_{0} t} \right)$，Hilbert 变换的输出为
$$
\mathscr{H}_{\mathrm{h}} \{ \cos (\omega_{0} t) \} = \frac{1}{2} \left( -\J \e^{\J \omega_{0} t} + \J \e^{-\J \omega_{0} t} \right) = \sin (\omega_{0} t)
$$
+ 对正弦输入 $\sin (\omega_{0} t) = \cfrac{1}{2\J} \left( \e^{\J \omega_{0} t} - \e^{-\J \omega_{0} t} \right)$，Hilbert 变换的输出为
$$
\mathscr{H}_{\mathrm{h}} \{ \sin (\omega_{0} t) \} = \frac{1}{2\J} \left( -\J \e^{\J \omega_{0} t} - \J \e^{-\J \omega_{0} t} \right) = -\cos (\omega_{0} t)
$$

即 Hilbert 变换**将余弦信号变为正弦信号，将正弦信号变为负余弦信号**，相当于将信号相位延迟 $\cfrac{\pi}{2}$。

### Hilbert 变换对带限调制信号的作用

设输入信号 $x(t)$ 为**带限信号**，其频谱 $\hat{x}(\omega)$ 满足
$$
\hat{x}(\omega) = 0, \qquad |\omega| > \omega_{\mathrm{c}}
$$
其可乘以载波 $\cos(\omega_{0}t)$（$\omega_{0} > \omega_{\mathrm{c}}$）进行调制，频谱迁移为 $\cfrac{1}{2} \left( \hat{x}(\omega - \omega_{0}) + \hat{x}(\omega + \omega_{0}) \right)$。对该调制信号进行 Hilbert 变换，输出频谱为
$$
H(\omega) \cdot \dfrac{1}{2} \left( \hat{x}(\omega - \omega_{0}) + \hat{x}(\omega + \omega_{0}) \right)
= \dfrac{1}{2} \left( -\J \hat{x}(\omega - \omega_{0}) + \J \hat{x}(\omega + \omega_{0}) \right)
$$
因此时域输出信号为
$$
\begin{align}
\mathscr{H}_{\mathrm{h}} \{ x(t) \cos(\omega_{0} t) \} &= \mathscr{F}^{-1} \left\{ \dfrac{1}{2} \left( -\J \hat{x}(\omega - \omega_{0}) + \J \hat{x}(\omega + \omega_{0}) \right) \right\} \\
&= \dfrac{1}{2} \left( -\J x(t) \e^{\J \omega_{0} t} + \J x(t) \e^{-\J \omega_{0} t} \right) \\
&= x(t) \cdot \dfrac{1}{2} (-\J) \left( \e^{\J \omega_{0} t} - \e^{-\J \omega_{0} t} \right) = x(t) \sin(\omega_{0} t)
\end{align}
$$
即 Hilbert 变换将调制信号 $x(t) \cos(\omega_{0} t)$ 转换为 $x(t) \sin(\omega_{0} t)$，相当于将载波信号相位延迟 $\cfrac{\pi}{2}$。

同理，对调制信号 $x(t) \sin(\omega_{0} t)$，Hilbert 变换的输出为
$$
\mathscr{H}_{\mathrm{h}} \{ x(t) \sin(\omega_{0} t) \} = - x(t) \cos(\omega_{0} t)
$$

## 随机过程的 Hilbert 变换

设随机过程 $X(t)$ 有分解
$$
X(t) = \dint_{-\infty}^{\infty} \e^{\J \omega t} \dif F_{X}(\omega)
$$
其中 $F_{X}(\omega)$ 是随机过程 $X(t)$ 的**频率分量随机变量列 (frequency component random variable series)**。 则 Hilbert 变换后的随机过程为
$$
\check{X} (t) = \mathscr{H}_{\mathrm{h}} \{ X(t) \} = \dint_{-\infty}^{\infty} \e^{\J \omega t} \cdot \left( -\J \sgn(\omega) \right) \dif F_{X}(\omega)
$$

### Hilbert 变换对宽平稳随机过程的作用

设随机过程 $X(t)$ 是[[#随机过程的平稳性]]，其均值为 $\mu_{X} = \mathbb{E}[X(t)]$，自相关函数为 $R_{X}(\tau) = \mathbb{E}[X(t) X(t+\tau)]$。则 Hilbert 变换后的随机过程 **$\check{X}(t)$ 也是宽平稳随机过程**，有
$$
\begin{align}
R_{\check{X}}(\tau) &= \mathbb{E} \left[ \check{X}(t+\tau) \overline{\check{X}(t)} \right]  \\
&= \mathbb{E} \left[ \dint_{-\infty}^{\infty} \e^{\J \omega (t+\tau)}  \left( -\J \sgn(\omega) \right) \dif F_{X}(\omega) \cdot \dint_{-\infty}^{\infty} \e^{-\J \omega' t} \left( \J \sgn(\omega') \right) \overline{\dif F_{X}(\omega')} \right] \\
&= \dint_{-\infty}^{\infty} \dint_{-\infty}^{\infty} \e^{\J \omega \tau + \J (\omega - \omega') t} \sgn(\omega) \sgn(\omega') \cdot \mathbb{E} \left[ \dif F_{X}(\omega) \overline{\dif F_{X}(\omega')} \right]  \\
&= \dint_{-\infty}^{\infty} \dint_{-\infty}^{\infty} \e^{\J \omega \tau + \J (\omega - \omega') t} \sgn(\omega) \sgn(\omega') \cdot \dfrac{1}{2\pi} \delta(\omega - \omega') S_{X}(\omega) \dif \omega \dif \omega' \\
&= \dfrac{1}{2\pi} \dint_{-\infty}^{\infty} \e^{\J \omega \tau} \sgn^{2}(\omega) S_{X}(\omega) \dif \omega = \dfrac{1}{2\pi} \dint_{-\infty}^{\infty} \e^{\J \omega \tau} S_{X}(\omega) \dif \omega = R_{X}(\tau)
\end{align}
$$
即 Hilbert 变换**不改变宽平稳随机过程的自相关函数**。

类似地，我们得到
$$
\begin{align}
R_{\check{X} X} (\tau) &= \mathbb{E} \left[ \check{X}(t+\tau) \overline{X(t)} \right]  = \dfrac{1}{2\pi} \dint_{-\infty}^{\infty} \e^{\J \omega \tau} \left( -\J \sgn(\omega) \right) S_{X}(\omega) \dif \omega \\
R_{X \check{X}} (\tau) &= \mathbb{E} \left[ X(t+\tau) \overline{\check{X}(t)} \right]  = \dfrac{1}{2\pi} \dint_{-\infty}^{\infty} \e^{\J \omega \tau} \left( \J \sgn(\omega) \right) S_{X}(\omega) \dif \omega
\end{align}
$$



# Gauss 过程

## Gauss 过程的引入

### 多元 Gauss 分布

对于多维随机变量 $\v{X} = \begin{pmatrix}X_{1} & X_{2} & \cdots & X_{n}\end{pmatrix}^{\mathrm{T}}$，如果 $\mathbb{E} \left[ |X_{k}|^{2} \right] < \infty$，则其**均值向量 (mean vector)** 定义为
$$
\v{\mu} = \mathbb{E}[\v{X}] = \begin{pmatrix} \mathbb{E}[X_{1}] & \mathbb{E}[X_{2}] & \cdots & \mathbb{E}[X_{n}] \end{pmatrix}^{\mathrm{T}}
$$
其**协方差矩阵 (covariance matrix)** 定义为
$$
\boldsymbol{\varSigma} = \mathbb{E} \left[ (\v{X} - \v{\mu})(\v{X} - \v{\mu})^{\mathrm{T}} \right] = \Big( \mathbb{E} \big[ (X_{i} - \mathbb{E} \left[ X_{i} \right] )(X_{j} - \mathbb{E} \left[ X_{j} \right] ) \big]  \Big)_{i,j}
$$

> [!definition] 多元 Gauss 分布
> 设 $\v{X} = \begin{pmatrix}X_{1} & X_{2} & \cdots & X_{n}\end{pmatrix}^{\mathrm{T}}$ 是 $n$ 维随机变量，如果 $\v{X}$ 的联合概率密度函数形如
> $$
> f_{\v{X}}\left( \v{x} \right) = k \exp\left( -\dfrac{1}{2} \left( \v{x} - \v{\mu} \right)^{\mathrm{T}} \boldsymbol{\varSigma}^{-1} \left( \v{x} - \v{\mu} \right) \right)
> $$
> 则称 $\v{X}$ 服从 $n$ 元 **Gauss 分布 (Gaussian distribution)**，记为 $\v{X} \sim N(\v{\mu}, \boldsymbol{\varSigma})$，其中 $k \in \mathbb{R}$，$\v{\mu} \in \mathbb{R}^{n}$，$\boldsymbol{\varSigma} \in \mathbb{R}^{n \times n}$ 对称正定。

#### 多元 Gauss 分布的归一化

由 $\boldsymbol{\varSigma}$ 对称正定，可知 $\boldsymbol{\varSigma}$ 可对角化，即存在正交矩阵 $\boldsymbol{U}$ 和对角矩阵 $\boldsymbol{\varLambda} = \mathrm{diag}(\lambda_{1}, \lambda_{2}, \ldots, \lambda_{n})$，使得
$$
\boldsymbol{\varSigma} = \boldsymbol{U} \boldsymbol{\varLambda} \boldsymbol{U}^{\mathrm{T}}
$$
其中 $\lambda_{1}, \lambda_{2}, \ldots, \lambda_{n} > 0$ 是 $\boldsymbol{\varSigma}$ 的特征值。此处引入
$$
\boldsymbol{B} = \boldsymbol{\varLambda}^{-1/2} \boldsymbol{U}^{\mathrm{T}}
$$
则 $\boldsymbol{\varSigma}^{-1} = \boldsymbol{B} \boldsymbol{B}^{\mathrm{T}}$，进而
$$
\begin{align}
\left( \v{x} - \v{\mu} \right)^{\mathrm{T}} \boldsymbol{\varSigma}^{-1} \left( \v{x} - \v{\mu} \right) &= \left( \v{x} - \v{\mu} \right)^{\mathrm{T}} (\boldsymbol{B} \boldsymbol{B}^{\mathrm{T}}) \left( \v{x} - \v{\mu} \right)  \\
&= \left( \boldsymbol{B} (\v{x} - \v{\mu}) \right)^{\mathrm{T}} \left( \boldsymbol{B} (\v{x} - \v{\mu}) \right)
\end{align}
$$
可做变量替换 $\v{y} = \boldsymbol{B} (\v{x} - \v{\mu}) = \boldsymbol{\varLambda}^{-1/2} \boldsymbol{U}^{\mathrm{T}} (\v{x} - \v{\mu})$，这一变换的 Jacobian 行列式为
$$
\left| \dfrac{ \partial \v{y} }{ \partial \v{x} } \right| = |\det \boldsymbol{B}| = |\det \boldsymbol{\varLambda}|^{-1/2} |\det \boldsymbol{U} | = | \det\boldsymbol{\varSigma}|^{-1/2}
$$

尝试**确定归一化系数 $k$**，归一化条件要求
$$
\begin{align}
1 &= \dint_{\mathbb{R}^{n}} f_{\v{X}}(\v{x}) \dif \v{x} = k \dint_{\mathbb{R}^{n}} \exp\left( -\dfrac{1}{2} \left( \v{x} - \v{\mu} \right)^{\mathrm{T}} \boldsymbol{\varSigma}^{-1} \left( \v{x} - \v{\mu} \right) \right) \dif \v{x} \\
&= k \dint_{\mathbb{R}^{n}} \exp\left( -\dfrac{1}{2} \v{y}^{\mathrm{T}} \v{y} \right) |\det \boldsymbol{\varSigma}|^{1/2} \dif \v{y} \\
&= k |\det \boldsymbol{\varSigma}|^{1/2} \prod\limits_{i=1}^{n} \dint_{-\infty}^{\infty} \exp\left( -\dfrac{1}{2} y_{i}^{2} \right) \dif y_{i} = k |\det \boldsymbol{\varSigma}|^{1/2} (2\pi)^{n/2}
\end{align}
$$
故 $k = (2\pi)^{-n/2} |\det \boldsymbol{\varSigma}|^{-1/2}$，多元 Gauss 分布的概率密度函数为
$$
\mark{ f_{\v{X}}\left( \v{x} \right) = \dfrac{1}{(2\pi)^{n/2} |\det \boldsymbol{\varSigma}|^{1/2}} \exp\left( -\dfrac{1}{2} \left( \v{x} - \v{\mu} \right)^{\mathrm{T}} \boldsymbol{\varSigma}^{-1} \left( \v{x} - \v{\mu} \right) \right) }
$$

特别地，**二维 Gauss 分布**的协方差矩阵常记为 $\boldsymbol{\varSigma} = \begin{pmatrix}\sigma_{1}^{2} & \rho\sigma_{1}\sigma_{2} \\ \rho\sigma_{1}\sigma_{2} & \sigma_{2}^{2}\end{pmatrix}$，其中 $\sigma_{1}^{2} > 0$，$\sigma_{2}^{2} > 0$，$-1 < \rho < 1$，此时其概率密度函数为
$$
\begin{align} 
f_{\v{X}}\left( \v{x} \right) &= \dfrac{1}{2\pi \sigma_{1} \sigma_{2} \sqrt{1 - \rho^{2}}}  \\
&\hspace{1.2em} \cdot \exp\left( -\dfrac{1}{2(1 - \rho^{2})} \left( \dfrac{(x_{1} - \mu_{1})^{2}}{\sigma_{1}^{2}} - \dfrac{2\rho (x_{1} - \mu_{1})(x_{2} - \mu_{2})}{\sigma_{1}\sigma_{2}} + \dfrac{(x_{2} - \mu_{2})^{2}}{\sigma_{2}^{2}} \right) \right) 
\end{align}
$$

#### 多元 Gauss 分布的特征函数

对随机向量 $\v{X} \in \mathbb{R}^{n}$，引入 $\v{\omega} \in \mathbb{R}^{n}$ 的函数
$$
\phi_{\v{X}}(\v{\omega}) = \mathbb{E} \left[ \exp(\J \v{\omega}^{\mathrm{T}} \v{X}) \right]
= \dint_{\mathbb{R}^{n}} \exp(\J \v{\omega}^{\mathrm{T}} \v{x}) f_{\v{X}}(\v{x}) \dif \v{x}
$$
称为 $\v{X}$ 的**特征函数 (characteristic function)**。

对多元 Gauss 分布，有
$$
\begin{align}
\phi_{\v{X}}(\v{\omega}) &= \dint_{\mathbb{R}^{n}} \exp(\J \v{\omega}^{\mathrm{T}} \v{x}) f_{\v{X}}(\v{x}) \dif \v{x} \\
&= \dfrac{1}{(2\pi)^{n/2} |\det \boldsymbol{\varSigma}|^{1/2}} \dint_{\mathbb{R}^{n}} \exp\left( \J \v{\omega}^{\mathrm{T}} \v{x} - \dfrac{1}{2} (\v{x} - \v{\mu})^{\mathrm{T}} \boldsymbol{\varSigma}^{-1} (\v{x} - \v{\mu}) \right) \dif \v{x}
\end{align}
$$
为计算上面积分，首先考虑一元情况，可配方得到
$$
\begin{align}
\J \omega x - \dfrac{1}{2\sigma^{2}} (x - \mu)^{2} &= -\dfrac{1}{2\sigma^{2}} \left( x^{2} - 2(\mu + \J \sigma^{2} \omega) x + \mu^{2} \right) \\
&= -\dfrac{1}{2\sigma^{2}} \left( x - \mu - \J \sigma^{2} \omega \right)^{2} + \J \mu \omega - \dfrac{1}{2} \sigma^{2} \omega^{2}
\end{align}
$$
类似地，对多元情况，有
$$
\begin{align}
&\J \v{\omega}^{\mathrm{T}} \v{x} - \dfrac{1}{2} (\v{x} - \v{\mu})^{\mathrm{T}} \boldsymbol{\varSigma}^{-1} (\v{x} - \v{\mu}) \\
&= -\dfrac{1}{2} \left( \v{x} - \v{\mu} - \J \boldsymbol{\varSigma} \v{\omega} \right)^{\mathrm{T}} \boldsymbol{\varSigma}^{-1} \left( \v{x} - \v{\mu} - \J \boldsymbol{\varSigma} \v{\omega} \right) + \J \v{\mu}^{\mathrm{T}} \v{\omega} - \dfrac{1}{2} \v{\omega}^{\mathrm{T}} \boldsymbol{\varSigma} \v{\omega}
\end{align}
$$
因此
$$
\begin{align}
\phi_{\v{X}}(\v{\omega}) &= \dfrac{1}{(2\pi)^{n/2} |\det \boldsymbol{\varSigma}|^{1/2}} \exp\left( \J \v{\mu}^{\mathrm{T}} \v{\omega} - \dfrac{1}{2} \v{\omega}^{\mathrm{T}} \boldsymbol{\varSigma} \v{\omega} \right) \\
&\hspace{1em}\cdot \dint_{\mathbb{R}^{n}} \exp\left( -\dfrac{1}{2} \left( \v{x} - \v{\mu} - \J \boldsymbol{\varSigma} \v{\omega} \right)^{\mathrm{T}} \boldsymbol{\varSigma}^{-1} \left( \v{x} - \v{\mu} - \J \boldsymbol{\varSigma} \v{\omega} \right) \right) \dif \v{x} \\
&= \exp\left( \J \v{\mu}^{\mathrm{T}} \v{\omega} - \dfrac{1}{2} \v{\omega}^{\mathrm{T}} \boldsymbol{\varSigma} \v{\omega} \right)
\end{align}
$$

综上所述，**多元 Gauss 分布的特征函数**为
$$
\mark{ \phi_{\v{X}}(\v{\omega}) = \exp\left( \J \v{\mu}^{\mathrm{T}} \v{\omega} - \dfrac{1}{2} \v{\omega}^{\mathrm{T}} \boldsymbol{\varSigma} \v{\omega} \right) }
$$
$X_{1}, X_{2}, \cdots, X_{n}$ 相互独立的充分必要条件是协方差矩阵 $\boldsymbol{\varSigma}$ 为对角矩阵，此时
$$
\phi_{\v{X}}(\v{\omega}) = \prod\limits_{i=1}^{n} \exp\left( \J \mu_{i} \omega_{i} - \dfrac{1}{2} \sigma_{i}^{2} \omega_{i}^{2} \right) = \prod\limits_{i=1}^{n} \phi_{X_{i}}(\omega_{i})
$$

#### 多元 Gauss 分布的性质

Gauss 变量的分布**完全由其一、二阶矩 $\v{\mu}$、$\boldsymbol{\varSigma}$ 决定**，因此
+ **高阶矩**均可由 $\v{\mu}$、$\boldsymbol{\varSigma}$ 表示，如零均值 Gauss 变量的四阶矩
$$
\begin{align} 
\mathbb{E} \left[ X_{i} X_{j} X_{k} X_{l} \right] &= \boldsymbol{\varSigma}_{i,j} \boldsymbol{\varSigma}_{k,l} + \boldsymbol{\varSigma}_{i,k} \boldsymbol{\varSigma}_{j,l} + \boldsymbol{\varSigma}_{i,l} \boldsymbol{\varSigma}_{j,k} \\
&= \mathbb{E} \left[ X_{i} X_{j} \right] \mathbb{E} \left[ X_{k} X_{l} \right] + \mathbb{E} \left[ X_{i} X_{k} \right] \mathbb{E} \left[ X_{j} X_{l} \right] + \mathbb{E} \left[ X_{i} X_{l} \right] \mathbb{E} \left[ X_{j} X_{k} \right]
\end{align}
$$
+ **线性变换**对 $\v{\mu}$、$\boldsymbol{\varSigma}$ 的影响是线性的，因而对整个分布的影响也是线性的，如 $\v{Y} = \boldsymbol{A} \v{X} + \v{b}$，则 $\v{Y} \sim \mathscr{N}(\boldsymbol{A} \v{\mu} + \v{b}, \boldsymbol{A} \boldsymbol{\varSigma} \boldsymbol{A}^{\mathrm{T}})$，称为**线性变换不变性**。这是 Gauss 分布的**特征性质**。

### Gauss 过程的定义

> [!definition] Gauss 过程
> 设 $X(t)$ 是定义在概率空间 $(\Omega, \mathcal{F}, P)$ 上的随机过程。如果对于任意正整数 $n$ 和任意时刻 $t_{1}, t_{2}, \cdots, t_{n}$，随机变量组 $\v{X} = \begin{pmatrix}X(t_{1}) & X(t_{2}) & \cdots & X(t_{n})\end{pmatrix}^{\mathrm{T}}$ 都服从 $n$ 元 Gauss 分布 $N\left( \v{\mu},\boldsymbol{\varSigma} \right)$，则称 $X(t)$ 为 **Gauss 过程 (Gaussian process)**。

由定义，Gauss 过程的**有限维分布**都是多元 Gauss 分布，因此多元 Gauss 分布的性质均适用于 Gauss 过程。例如，Gauss 过程 $X(t)$ **通过一般线性系统 $h(t, \tau)$** 得到的**输出 $Y(t)$ 仍然是 Gauss 过程**，且
$$
\begin{align}
&\mathbb{E} \left[ Y(t) \right] = \dint_{-\infty}^{\infty} h(t, \tau) \mathbb{E} \left[ X(\tau) \right] \dif \tau, \\
&\mathrm{Cov} \left[ Y(t_{1}), Y(t_{2}) \right] = \dint_{-\infty}^{\infty} \dint_{-\infty}^{\infty} h(t_{1}, \tau_{1}) h(t_{2}, \tau_{2}) \mathrm{Cov} \left[ X(\tau_{1}), X(\tau_{2}) \right] \dif \tau_{1} \dif \tau_{2}
\end{align}
$$


## Gauss 条件分布

考虑多维随机变量 $\v{X} \in \mathbb{R}^{m}$、$\v{Y} \in \mathbb{R}^{n}$，设其联合服从 $(m+n)$ 元 Gauss 分布 $N\left( \v{\mu}, \boldsymbol{\varSigma} \right)$，其中
$$
\v{\mu} = \begin{pmatrix} \v{\mu}_{X} \\ \v{\mu}_{Y} \end{pmatrix}, \qquad
\boldsymbol{\varSigma} = \begin{pmatrix}
\boldsymbol{\varSigma}_{XX} & \boldsymbol{\varSigma}_{XY} \\
\boldsymbol{\varSigma}_{YX} & \boldsymbol{\varSigma}_{YY} 
\end{pmatrix}
$$
我们考察 **$\v{Y}$ 相对于 $\v{X}$ 的条件分布**，即考察
$$
f_{\v{Y}\mid\v{X}} \left( \v{y} \mid \v{x} \right) = \dfrac{f_{\v{X},\v{Y}}\left( \v{x},\v{y} \right)}{f_{\v{X}}\left( \v{x} \right)}
$$
其中，由 $\v{X}$ 也服从 Gauss 分布，概率密度为
$$
f_{\v{X}}\left( \v{x} \right) = k_{X} \exp\left( -\dfrac{1}{2} \left( \v{x} - \v{\mu} \right)^{\mathrm{T}} \boldsymbol{\varSigma}_{XX}^{-1} \left( \v{x} - \v{\mu} \right) \right)
$$
$\v{X}$ 和 $\v{Y}$ 的联合概率分布为
$$
f_{\v{X},\v{Y}}\left( \v{x},\v{y} \right) = k \exp\left( -\dfrac{1}{2} \begin{pmatrix}
\v{x} - \v{\mu}_{X} \\ \v{y} - \v{\mu}_{Y}
\end{pmatrix}^{\mathrm{T}} \boldsymbol{\varSigma}^{-1} \begin{pmatrix}
\v{x} - \v{\mu}_{X} \\ \v{y} - \v{\mu}_{Y}
\end{pmatrix} \right)
$$
其中 $k$ 和 $k_{X}$ 是归一化系数。

### 条件概率密度的计算

为计算条件概率密度，首先需计算 $\boldsymbol{\varSigma}^{-1}$。如果能够将右上角块 $\boldsymbol{\varSigma}_{XY}$ 和左下角块 $\boldsymbol{\varSigma}_{YX}$ 消去，则可将 $\boldsymbol{\varSigma}^{-1}$ 写成**分块对角矩阵**的形式，从而简化计算。为此，考虑如下初等变换：
$$
\underbrace{ \begin{pmatrix}
\boldsymbol{I}_{m} &  \\
\boldsymbol{B} & \boldsymbol{I}_{n}
\end{pmatrix} \begin{pmatrix}
\boldsymbol{\varSigma}_{XX} & \boldsymbol{\varSigma}_{XY} \\
\boldsymbol{\varSigma}_{YX} & \boldsymbol{\varSigma}_{YY}
\end{pmatrix} }_{ \begin{pmatrix}
\boldsymbol{\varSigma}_{XX} & \boldsymbol{\varSigma}_{XY} \\
\boldsymbol{B} \boldsymbol{\varSigma}_{XX} + \boldsymbol{\varSigma}_{YX} & \boldsymbol{B} \boldsymbol{\varSigma}_{XY} + \boldsymbol{\varSigma}_{YY}
\end{pmatrix} } \begin{pmatrix}
\boldsymbol{I}_{m} & \boldsymbol{A} \\
& \boldsymbol{I}_{n}
\end{pmatrix} = \begin{pmatrix}
\boldsymbol{C} &  \\
& \boldsymbol{D}
\end{pmatrix}
$$
则右上角块为
$$
\boldsymbol{\varSigma}_{XX} \boldsymbol{A} + \boldsymbol{\varSigma}_{XY} = \boldsymbol{O} \implies \boldsymbol{A} = -\boldsymbol{\varSigma}_{XX}^{-1} \boldsymbol{\varSigma}_{XY}
$$
左下角块为
$$
\boldsymbol{B} \boldsymbol{\varSigma}_{XX} + \boldsymbol{\varSigma}_{YX} = \boldsymbol{O} \implies \boldsymbol{B} = -\boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1}
$$
因此，有
$$
\begin{pmatrix}
\boldsymbol{I}_{m} &  \\
-\boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} & \boldsymbol{I}_{n}
\end{pmatrix} \boldsymbol{\varSigma} \begin{pmatrix}
\boldsymbol{I}_{m} & -\boldsymbol{\varSigma}_{XX}^{-1} \boldsymbol{\varSigma}_{XY} \\
& \boldsymbol{I}_{n}
\end{pmatrix} = \begin{pmatrix}
\boldsymbol{\varSigma}_{XX} &  \\
& \boldsymbol{\varSigma}_{YY} - \boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} \boldsymbol{\varSigma}_{XY}
\end{pmatrix}
$$
得
$$
\boldsymbol{\varSigma} = \begin{pmatrix}
\boldsymbol{I}_{m} &  \\
-\boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} & \boldsymbol{I}_{n}
\end{pmatrix}^{-1} \begin{pmatrix}
\boldsymbol{\varSigma}_{XX} &  \\
& \boldsymbol{\varSigma}_{YY} - \boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} \boldsymbol{\varSigma}_{XY}
\end{pmatrix} \begin{pmatrix}
\boldsymbol{I}_{m} & -\boldsymbol{\varSigma}_{XX}^{-1} \boldsymbol{\varSigma}_{XY} \\
& \boldsymbol{I}_{n}
\end{pmatrix}^{-1}
$$
进而
$$
\boldsymbol{\varSigma}^{-1} = \begin{pmatrix}
\boldsymbol{I}_{m} & -\boldsymbol{\varSigma}_{XX}^{-1} \boldsymbol{\varSigma}_{XY} \\
& \boldsymbol{I}_{n}
\end{pmatrix} \begin{pmatrix}
\boldsymbol{\varSigma}_{XX}^{-1} &  \\
& \left( \boldsymbol{\varSigma}_{YY} - \boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} \boldsymbol{\varSigma}_{XY} \right)^{-1}
\end{pmatrix} \begin{pmatrix}
\boldsymbol{I}_{m} &  \\
-\boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} & \boldsymbol{I}_{n}
\end{pmatrix}
$$

这样，**联合概率密度**指数部分中的**二次型**可写成
$$
\begin{align}
&\begin{pmatrix}
    \v{x}^{\mathrm{T}} - \v{\mu}_{X}^{\mathrm{T}} & \v{y}^{\mathrm{T}} - \v{\mu}_{Y}^{\mathrm{T}} 
\end{pmatrix} \boldsymbol{\varSigma}^{-1} \begin{pmatrix}
    \v{x} - \v{\mu}_{X} \\ \v{y} - \v{\mu}_{Y} 
\end{pmatrix} \\
&= {\color{ violet } \begin{pmatrix}
    \v{x}^{\mathrm{T}} - \v{\mu}_{X}^{\mathrm{T}} & \v{y}^{\mathrm{T}} - \v{\mu}_{Y}^{\mathrm{T}} 
\end{pmatrix} \begin{pmatrix}
    \boldsymbol{I}_{m} & -\boldsymbol{\varSigma}_{XX}^{-1} \boldsymbol{\varSigma}_{XY} \\
    & \boldsymbol{I}_{n}
\end{pmatrix} }  \\
&\hspace{1em}\mathop{}\begin{pmatrix}
    \boldsymbol{\varSigma}_{XX}^{-1} &  \\
    & \left( \boldsymbol{\varSigma}_{YY} - \boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} \boldsymbol{\varSigma}_{XY} \right)^{-1}
\end{pmatrix} {\color{ orange } \begin{pmatrix}
    \boldsymbol{I}_{m} &  \\
    -\boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} & \boldsymbol{I}_{n}
\end{pmatrix} \begin{pmatrix}
    \v{x} - \v{\mu}_{X} \\ \v{y} - \v{\mu}_{Y}
\end{pmatrix} } \\
&= {\color{ violet } \begin{pmatrix}
    \v{x}^{\mathrm{T}} - \v{\mu}_{X}^{\mathrm{T}}  &
    \v{y}^{\mathrm{T}} - \v{\mu}_{Y}^{\mathrm{T}} - \left( \v{x}^{\mathrm{T}} - \v{\mu}_{X}^{\mathrm{T}} \right) \boldsymbol{\varSigma}_{XX}^{-1} \boldsymbol{\varSigma}_{XY}
\end{pmatrix} }  \\
&\hspace{1em}\mathop{}\begin{pmatrix}
    \boldsymbol{\varSigma}_{XX}^{-1} &  \\
    & \left( \boldsymbol{\varSigma}_{YY} - \boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} \boldsymbol{\varSigma}_{XY} \right)^{-1}
\end{pmatrix} {\color{ orange } \begin{pmatrix}
    \v{x} - \v{\mu}_{X} \\
    \v{y} - \v{\mu}_{Y} - \boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} \left( \v{x} - \v{\mu}_{X} \right)
\end{pmatrix} } \\
&= \mathop{} \left( \v{x}^{\mathrm{T}} - \v{\mu}_{X}^{\mathrm{T}} \right) \boldsymbol{\varSigma}_{XX}^{-1} \left( \v{x} - \v{\mu}_{X} \right)  \\
    &\hspace{1em} + \left( \v{y}^{\mathrm{T}} - \v{\mu}_{Y}^{\mathrm{T}} - \left( \v{x}^{\mathrm{T}} - \v{\mu}_{X}^{\mathrm{T}} \right) \boldsymbol{\varSigma}_{XX}^{-1} \boldsymbol{\varSigma}_{XY} \right) \left( \boldsymbol{\varSigma}_{YY} - \boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} \boldsymbol{\varSigma}_{XY} \right)^{-1} \\
    &\hspace{2em} \mathop{}\cdot\mathop{} \left( \v{y} - \v{\mu}_{Y} - \boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} \left( \v{x} - \v{\mu}_{X} \right) \right)
\end{align}
$$
于是，**条件概率密度**的指数部分即为
$$
\begin{align}
&\left(  -\dfrac{1}{2} \begin{pmatrix}
\v{x} - \v{\mu}_{X} \\ \v{y} - \v{\mu}_{Y}
\end{pmatrix}^{\mathrm{T}} \boldsymbol{\varSigma}^{-1} \begin{pmatrix}
\v{x} - \v{\mu}_{X} \\ \v{y} - \v{\mu}_{Y}
\end{pmatrix} \right) - \left( -\dfrac{1}{2} \left( \v{x} - \v{\mu}_{X} \right)^{\mathrm{T}} \boldsymbol{\varSigma}_{XX}^{-1} \left( \v{x} - \v{\mu}_{X} \right) \right) \\
&= -\dfrac{1}{2} \left( \v{y}^{\mathrm{T}} - \v{\mu}_{Y}^{\mathrm{T}} - \left( \v{x}^{\mathrm{T}} - \v{\mu}_{X}^{\mathrm{T}} \right) \boldsymbol{\varSigma}_{XX}^{-1} \boldsymbol{\varSigma}_{XY} \right) \\
&\hspace{3em} \mathop{}\cdot\mathop{} \big( \underbrace{ \boldsymbol{\varSigma}_{YY} - \boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} \boldsymbol{\varSigma}_{XY} }_{ \boldsymbol{\varSigma}_{Y\mid X} } \big)^{-1} 
\Big( \v{y} - \Big(\underbrace{ \v{\mu}_{Y} + \boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} \left( \v{x} - \v{\mu}_{X} \right) }_{ \v{\mu}_{Y\mid X} }\Big) \Big) \\
&= -\dfrac{1}{2} \left( \v{y} - \v{\mu}_{Y\mid X} \right)^{\mathrm{T}} \boldsymbol{\varSigma}_{Y\mid X}^{-1} \left( \v{y} - \v{\mu}_{Y\mid X} \right)
\end{align}
$$

> [!thm.] 多元 Gauss 分布各块间的条件分布
> 设多维随机变量 $\v{X} \in \mathbb{R}^{m}$、$\v{Y} \in \mathbb{R}^{n}$ 的联合**服从 $(m+n)$ 元 Gauss 分布 $\mathscr{N}\left( \v{\mu}, \boldsymbol{\varSigma} \right)$**，其中
> $$
> \v{\mu} = \begin{pmatrix} \v{\mu}_{X} \\ \v{\mu}_{Y} \end{pmatrix}, \qquad
> \boldsymbol{\varSigma} = \begin{pmatrix}
> \boldsymbol{\varSigma}_{XX} & \boldsymbol{\varSigma}_{XY} \\
> \boldsymbol{\varSigma}_{YX} & \boldsymbol{\varSigma}_{YY}
> \end{pmatrix}
> $$
> 则 $\v{Y}$ 相对于 $\v{X}$ 的条件分布**仍然服从 Gauss 分布**，概率密度为
> $$
> f_{\v{Y}\mid\v{X}} \left( \v{y} \mid \v{x} \right) = k_{Y\mid X} \exp\left( -\dfrac{1}{2} \left( \v{y} - \v{\mu}_{Y\mid X} \right)^{\mathrm{T}} \boldsymbol{\varSigma}_{Y\mid X}^{-1} \left( \v{y} - \v{\mu}_{Y\mid X} \right) \right)
> $$
> 即 **$\v{Y} \mid \v{X} \sim \mathscr{N}\left( \v{\mu}_{Y\mid X}, \boldsymbol{\varSigma}_{Y\mid X} \right)$**，其中
> $$
> \v{\mu}_{Y\mid X} = \v{\mu}_{Y} + \boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} \left( \v{x} - \v{\mu}_{X} \right), \qquad
> \boldsymbol{\varSigma}_{Y\mid X} = \boldsymbol{\varSigma}_{YY} - \boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} \boldsymbol{\varSigma}_{XY}
> $$

特别地，对二维情形 $\begin{pmatrix}X \\ Y\end{pmatrix} \sim \mathscr{N}\left( \begin{pmatrix}\mu_{X} \\ \mu_{Y}\end{pmatrix}, \begin{pmatrix}\sigma_{X}^2 & \rho \sigma_{X} \sigma_{Y} \\ \rho \sigma_{X} \sigma_{Y} & \sigma_{Y}^2\end{pmatrix} \right)$，则有
$$
\begin{align}
&\mathbb{E} \left[ Y \mid X \right] = \mu_{Y \mid X} = \mu_{Y} + \rho \dfrac{\sigma_{Y}}{\sigma_{X}} (X - \mu_{X}), \\
&\mathrm{Var} \left[ Y \mid X \right] = \sigma_{Y \mid X}^{2} = (1 - \rho^{2}) \sigma_{Y}^{2}
\end{align}
$$

> [!example] [[例题#L10-1]] 至 [[例题#L10-7|L10-7]]：Gauss 条件分布算例
> 设 $X_{1}, X_{2} \stackrel{\text{i.i.d.}}{\sim} \mathscr{N}(0, 1)$，尝试求解以下条件期望。
> + 直接求解：
> 	+ [[例题#L10-1]]　$\mathbb{E} \left[ X_{1}-X_{2}\mid X_{1}+X_{2} \right]$；
> + 利用独立性简化计算：
> 	+ [[例题#L10-2]]　$\mathbb{E} \left[ (X_{1}-X_{2})^{2} \mid X_{1}+X_{2} \right]$；
> 	+ [[例题#L10-3]]　$\mathbb{E} \left[ (X_{1}-X_{2})^{2n} \mid X_{1}+X_{2} \right]$，$n \in \mathbb{N}^{*}$；
> 	+ [[例题#L10-4]]　$\mathbb{E} \left[ X_1^2 + X_2^2 \mid X_1 + X_2 \right]$；
> + 利用特征函数简化计算：
> 	+ [[例题#L10-5]]　$\mathbb{E} \left[ \exp\left( 2X_1 - X_2 \right) \mid X_1 + X_2 \right]$；
> 	+ [[例题#L10-6]]　$\mathbb{E} \left[ \exp(2X_{1}^{2} + X_{2}^{2}) \mid X_{1} - X_{2} \right]$；
> 	+ [[例题#L10-7]]　$\mathbb{E} \left[ \sin (2X_{1} - X_{2}) \mid X_{1} + X_{2} \right]$。

### 条件分布的几何直观

观察条件均值 $\v{\mu}_{Y\mid X}$ 的表达式
$$
\v{\mu}_{Y\mid X} = \v{\mu}_{Y} + \boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} \left( \v{x} - \v{\mu}_{X} \right)
$$
其可视为**对无条件均值 $\v{\mu}_{Y}$ 的修正**，且
+ 修正量与 $\v{X}$ 偏离其均值 $\v{\mu}_{X}$ 的程度 $\left( \v{x} - \v{\mu}_{X} \right)$，即 $\v{X}$ 中的**随机成分**成正比；
+ 修正量与上述随机成分的**比例系数**为 $\boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1}$，其中 $\boldsymbol{\varSigma}_{XX}^{-1}$ 起到「标准化」的作用，而 $\boldsymbol{\varSigma}_{YX}$ 则反映了 $\v{X}$ 和 $\v{Y}$ 之间的**相关性**。

因此，$\v{Y}$ 相对于 $\v{X}$ 的条件分布可看做**依据 $\v{X}$ 的随机成分在 $\v{Y}$ 上的投影 (projection)** 对 $\v{Y}$ 的分布进行调整后的结果。


## Gauss 过程通过非线性系统

### 典型非线性系统下的 Gauss 过程

非线性系统的解析结构通常较为复杂，难以泛泛讨论其对 Gauss 过程的影响，需要具体问题具体分析。

> [!example] [[例题#L11-1]]：Gauss 过程通过理想限幅器
> **理想限幅器 (ideal limiter)** 定义为
> $$
> g(x) = \begin{cases}
> -1, & x < 0, \\
> 1, & x \ge 0
> \end{cases}
> $$

> [!example] [[例题#L11-2]]：Gauss 过程通过全波线性检波器
> **全波线性检波器 (full-wave rectifier)** 定义为
> $$
> g(x) = |x| = \begin{cases}
> -x, & x < 0, \\
> x, & x \ge 0
> \end{cases}
> $$

> [!example] [[例题#L11-3]]：Gauss 过程通过半波线性检波器
> **半波线性检波器 (half-wave rectifier)** 定义为
> $$
> g(x) = \begin{cases}
> 0, & x < 0, \\
> x, & x \ge 0
> \end{cases} = \mathrm{ReLU} (x)
> $$

> [!example] [[例题#L11-4]]：Gauss 过程通过平方律检波器
> **平方律检波器 (square-law detector)** 即 $g(x) = x^{2}$。

### Price 定理

**Price 定理**是分析 Gauss 过程通过非线性系统后输出统计特性的有力工具。

> [!theorem] Price 定理
> 设 $(X, Y)$ 服从二元 Gauss 分布 $\mathscr{N}(\mu_{1}, \mu_{2}, \sigma_{1}^{2}, \sigma_{2}^{2}, \rho)$，$r = \mathrm{Cov}(X, Y) = \rho\sigma_{1}\sigma_{2}$，$g(x,y)$ 是满足一定正则性条件的二元函数，则
> $$
> \dfrac{\partial^{n}}{\partial r^{n}} \mathbb{E} \left[ g(X, Y) \right] = \mathbb{E} \left[ \dfrac{\partial^{2n} g(X, Y)}{\partial x^{n} \partial y^{n}} \right]
> $$
> 特别地，$n=1$ 时即
> $$
> \dfrac{\partial}{\partial \rho} \mathbb{E} \left[ g(X, Y) \right] = \sigma_{1} \sigma_{2} \mathbb{E} \left[ \dfrac{\partial^{2} g(X, Y)}{\partial x \partial y} \right]
> $$

使用 Price 定理的核心是，选取合适的函数 $g(x,y)$，从而**将待求的统计量 $\mathbb{E} \left[ Y(t) Y(s) \right]$ 表示为 $\mathbb{E} \left[ g(X(t), X(s)) \right]$**，以使用 $\mathbb{E} \left[ X(t)X(s) \right]$ 简化计算。通常直接选取 $g(x, y) = g(x)g(y)$，其中 $g(\cdot)$ 为非线性系统的输入输出关系。

Gauss 过程的 **Bussgang 性质 (Bussgang property)** 是 Price 定理的一个重要推论，描述了 Gauss 过程通过非线性系统后输出与输入之间的相关性关系。

> [!theorem] Bussgang 性质
> 设 $(X, Y)$ 服从零均值二元 Gauss 分布，$h(\cdot)$ 为满足一定正则性条件的无记忆非线性函数，则
> $$
> \mathbb{E} \left[ X h(Y) \right] = C \mathbb{E} \left[ XY \right] 
> $$
> 其中 $C$ 是仅依赖于 $Y$ 的常数，具体为 $C = \cfrac{\mathbb{E} \left[ Y h(Y) \right]}{\mathbb{E} \left[ Y^{2} \right]} = \mathbb{E} \left[ \cfrac{\dif}{\dif Y} h(Y) \right]$。

## † 窄带 Gauss 过程

### 二维 Gauss 分布的幅度分布

设 $\begin{pmatrix}X \\ Y\end{pmatrix} \sim \mathscr{N}\left( \v{\mu}, \sigma^{2} \boldsymbol{I} \right)$， 不失一般性地设 $\v{\mu} = \begin{pmatrix}A \cos \phi \\ A \sin \phi\end{pmatrix}$，则联合概率密度为
$$
\begin{align}
f_{X,Y}(x,y) &= \dfrac{1}{2\pi \sigma^{2}} \exp\left( -\dfrac{1}{2\sigma^{2}} \left( (x - A \cos \phi)^{2} + (y - A \sin \phi)^{2} \right) \right) \\
&= \dfrac{1}{2\pi \sigma^{2}} \exp\left( -\dfrac{1}{2\sigma^{2}} \left( x^{2} + y^{2} + A^{2} - 2A (x \cos \phi + y \sin \phi) \right) \right)
\end{align}
$$
转换到**极坐标系 $(R, \varTheta)$**，其中 $R = \sqrt{X^{2} + Y^{2}}$、$\varTheta = \arctan \dfrac{Y}{X}$，则
$$
\begin{align}
f_{R,\varTheta}(r,\theta) &= f_{X,Y}(r \cos \theta, r \sin \theta) \left| \dfrac{ D (x, y) }{ D (r, \theta) }  \right| \\
&= \dfrac{r}{2\pi \sigma^{2}} \exp\left( -\dfrac{1}{2\sigma^{2}} \left( r^{2} + A^{2} - 2A r \cos(\theta - \phi) \right) \right)
\end{align}
$$
对 $\theta$ 积分即得到幅度 $R$ 的概率密度
$$
\begin{align}
f_{R}(r) &= \dint_{0}^{2\pi} f_{R,\varTheta}(r,\theta) \dif \theta  \\
&= \dfrac{r}{2\pi \sigma^{2}} \exp\left( -\dfrac{r^{2} + A^{2}}{2\sigma^{2}} \right) \dint_{0}^{2\pi} \exp\left( \dfrac{A r}{\sigma^{2}} \cos(\theta - \phi) \right) \dif \theta \\
&= \dfrac{r}{\sigma^{2}} \exp\left( -\dfrac{r^{2} + A^{2}}{2\sigma^{2}} \right) I_{0} \left( \dfrac{A r}{\sigma^{2}} \right), \quad r \ge 0
\end{align}
$$
称 $R$ 服从 **Rician 分布**；当 $A=0$ 时，$R$ 的概率密度化为
$$
f_{R}(r) = \dfrac{r}{\sigma^{2}} \exp\left( -\dfrac{r^{2}}{2\sigma^{2}} \right), \quad r \ge 0
$$
称 $R$ 服从 **Rayleigh 分布**，此时 $f_{R, \varTheta}(r, \theta) = \cfrac{f_{R}(r)}{2\pi} = f_{R}(r) f_{\varTheta}(\theta)$，即幅度和相位**统计独立**。

### 零均值窄带 Gauss 过程

设联合平稳的零均值实宽平稳 Gauss 过程 $X(t)$、$Y(t)$ 满足：
+ 相关函数 $R_{X}(\tau) = R_{Y}(\tau)$，$R_{XY}(\tau) = -R_{YX}(\tau)$；
+ $|\omega|\ge \omega_{0}$ 上功率谱密度 $S_{X}(\omega) = S_{Y}(\omega) = 0$。

则可构造 Gauss 过程
$$
Z(t) = X(t) \cos \omega_{\mathrm{c}} t - Y(t) \sin \omega_{\mathrm{c}} t
= V(t) \cos \left( \omega_{\mathrm{c}} t + \varTheta(t) \right)
$$
称为零均值**窄带 Gauss 过程**，其中 $V(t) = \sqrt{X^{2}(t) + Y^{2}(t)}$ 为**包络过程**，$\varTheta(t) = \arctan \cfrac{Y(t)}{X(t)}$ 为**相位过程**，调制频率 $\omega_{\mathrm{c}} \gg \omega_{0}$。

由[[#二维 Gauss 分布的幅度分布]]中的结论立得，**$V(t)$ 服从 Rayleigh 分布**，$\varTheta(t)$ 服从均匀分布，且 $V(t)$ 和 $\varTheta(t)$ 统计独立。

### 非零均值窄带 Gauss 过程

设窄带 Gauss 的非零均值是由**正弦波随机相位过程**叠加引入的，即考虑
$$
\xi(t) = p \sin \left( \omega_{\mathrm{c}} t + \varPhi \right) + Z(t)
$$
其中 $p$ 为常数，$\varPhi$ 为均匀分布在 $[0, 2\pi)$ 上的随机变量，$Z(t)$ 为[[#零均值窄带 Gauss 过程]]。

$\xi(t)$ 可写成
$$
\begin{align}
\xi(t) &= \underbrace{ p \sin \varPhi }_{ \mu_{X} } \cos \omega_{\mathrm{c}} t + \underbrace{ p \cos \varPhi }_{ \mu_{Y} } \sin \omega_{\mathrm{c}} t + X(t) \cos \omega_{\mathrm{c}} t - Y(t) \sin \omega_{\mathrm{c}} t \\
&= \left( X(t) + \mu_{X} \right) \cos \omega_{\mathrm{c}} t - \left( Y(t) - \mu_{Y} \right) \sin \omega_{\mathrm{c}} t \\
&= V_{\xi}(t) \cos \left( \omega_{\mathrm{c}} t + \varTheta_{\xi}(t) \right)
\end{align}
$$
其中
$$
V_{\xi}(t) \cos \varTheta_{\xi}(t) = X(t) + p \sin \varPhi, \qquad
V_{\xi}(t) \sin \varTheta_{\xi}(t) = Y(t) - p \cos \varPhi
$$
则 **$V_{\xi}(t)$ 服从 Rician 分布**，概率密度为
$$
f_{V_{\xi}}(v) = \dfrac{v}{\sigma^{2}} \exp\left( -\dfrac{v^{2} + p^{2}}{2\sigma^{2}} \right) I_{0} \left( \dfrac{p v}{\sigma^{2}} \right), \quad v \ge 0
$$


# Poisson 过程

## Poisson 过程的定义

Poisson 过程是一类**时间连续、状态离散**的随机过程，广泛应用于排队论、可靠性工程、通信系统等领域。它描述了在单位时间内某事件发生的次数，且这些事件是独立且均匀分布的。

### 增量独立性、增量平稳性

一个随机过程 $X(t)$ 如果满足
$$
\forall t_{1} < t_{2} \le t_{3} < t_{4}, \qquad X(t_{2}) - X(t_{1}) \perp X(t_{4}) - X(t_{3})
$$
则称其具有**增量独立性 (independent increments)**。

此外，如果对于任意 $s, t, \tau \ge 0$，都有
$$
X(t + \tau) - X(s + \tau) \stackrel{\text{d}}{=} X(t) - X(s)
$$
其中 $\stackrel{\text{d}}{=}$ 表示**同分布 (equal in distribution)**，即 $X(t) - X(s)$ 的分布只与 $t - s$ 有关，而与具体的时间点无关，则称其具有**增量平稳性 (stationary increments)**。

### 矩母函数

对于具有离散状态取值随机变量 $X(t)$，我们参照 **$z$ 变换**引入其**矩母函数 (moment generating function)**，定义为
$$
G_{X(t)}(z) = \mathbb{E}\left[z^{X(t)}\right]
$$
则 $G_{X(t)}(z)$ 可以展开为
$$
G_{X(t)}(z) = \sum_{k=0}^{\infty} P\left\{ X(t) = k \right\} \cdot z^{k}
$$
即 $X(t)$ 取为每个 $k$ 的概率都对应到**矩母函数相应阶项 $z^{k}$ 的系数**上。

### Poisson 过程的引入

设 $X(t)$ 是一个具有[[#增量独立性、增量平稳性]]的随机过程，我们尝试**构造一个关于其[[#矩母函数]]的微分方程**。

为此，我们求其矩母函数对时间的导数，即
$$
\begin{align} 
\dfrac{\dif}{\dif t} G_{X(t)}(z) &= \lim_{\Delta t \to 0} \dfrac{G_{X(t + \Delta t)}(z) - G_{X(t)}(z)}{\Delta t}
= \lim_{\Delta t \to 0} \dfrac{\mathbb{E}\left[z^{X(t + \Delta t)} - z^{X(t)}\right]}{\Delta t}  \\
&= \lim_{\Delta t \to 0} \dfrac{\mathbb{E}\left[z^{X(t)} \left( z^{X(t + \Delta t) - X(t)} - 1 \right) \right]}{\Delta t}
\end{align}
$$
令**初态 $X(0) = 0$**，则由增量独立性有 $X(t) - X(0)$ 与 $X(t + \Delta t) - X(t)$ 独立，由增量平稳性有 $X(t + \Delta t) - X(t) \stackrel{\text{d}}{=} X(\Delta t)$，因此上式可写为
$$
\begin{align}
\dfrac{\dif}{\dif t} G_{X(t)}(z) &= \lim_{\Delta t \to 0} \dfrac{\mathbb{E}\left[z^{X(t)}\right] \cdot \mathbb{E}\left[z^{X(t + \Delta t) - X(t)} - 1\right]}{\Delta t} \\
&= G_{X(t)}(z) \cdot \lim_{\Delta t \to 0} \dfrac{\mathbb{E}\left[z^{X(\Delta t)} - 1\right]}{\Delta t} \\
&= G_{X(t)}(z) \cdot \lim_{\Delta t \to 0} \dfrac{1}{\Delta t} \left( \sum\limits_{k=0}^{\infty} P\{X(\Delta t) = k\} \cdot z^{k} - 1 \right)
\end{align}
$$
^JumuHanshuDeDaoshu

括号中的因子可展开为
$$
\begin{align}
&\sum\limits_{k=0}^{\infty} P\{X(\Delta t) = k\} \cdot z^{k} - 1 \\
&= \underbrace{ P\{X(\Delta t) = 0\} - 1 }_{ \#1 } + \underbrace{ P\{X(\Delta t) = 1\} \cdot z^{1} }_{ \#2 } + \underbrace{ \sum\limits_{k=2}^{\infty} P\{X(\Delta t) = k\} \cdot z^{k} }_{ \#3 }
\end{align}
$$
分别处理上述三项。

#### Term \#1

注意到
$$
\begin{align}
P\{X(t) = 0\} &= P\{ X(s) = 0, X(t) - X(s) = 0 \} \quad(\forall s \in [0, t]) \\
&= P\{ X(s) = 0 \} \cdot P\{ X(t) - X(s) = 0 \} \\
&= P\{ X(s) = 0 \} \cdot P\{ X(t - s) = 0 \}
\end{align}
$$
因此，$H(t) = P\{X(t) = 0\}$ 满足**函数方程**
$$
H(t) = H(s) \cdot H(t - s)
$$
在**有界**的条件下，唯一解为**指数函数**，即知
$$
P\{X(\Delta t) = 0\} = \e^{-\lambda \Delta t}, \qquad \lambda \ge 0
$$
因此
$$
\lim\limits_{ \Delta t \to 0 } \dfrac{1}{\Delta t} \left( P\{X(\Delta t) = 0\} - 1 \right) = \lim\limits_{ \Delta t \to 0 } \dfrac{ \e^{-\lambda \Delta t} - 1 }{ \Delta t } = -\lambda
$$

#### Term \#2

已知
$$
P \left\{ X(\Delta t) = 0 \right\} + P \left\{ X(\Delta t) = 1 \right\} + P \left\{ X(\Delta t) \ge 2 \right\} = 1
$$
即有
$$
\dfrac{1 - P \left\{ X(\Delta t) = 0 \right\}}{\Delta t} = \dfrac{P \left\{ X(\Delta t) = 1 \right\}}{\Delta t} \left( 1 + \dfrac{P\left\{ X(\Delta t) \ge 2 \right\}}{P\left\{ X(\Delta t) = 1 \right\}} \right)
$$
为了使得上式在 $\Delta t \to 0$ 时有界，必须引入**稀疏性假设 (sparsity assumption)**，即要求
$$
\lim_{\Delta t \to 0} \dfrac{1}{\Delta t} \dfrac{P\left\{ X(\Delta t) \ge 2 \right\}}{P\left\{ X(\Delta t) = 1 \right\}} = 0
$$
^XishuxingJiashe

在此假设下，有
$$
\lim\limits_{ \Delta t \to 0 } \dfrac{1}{\Delta t} P \left\{ X(\Delta t) = 1 \right\} = \lambda
$$

#### Term \#3

我们先考察这个求和项的收敛，有
$$
\begin{align}
\left| \sum\limits_{k=2}^{\infty} P\{X(\Delta t) = k\} \cdot z^{k} \right| &\le \sum\limits_{k=2}^{\infty} P\{X(\Delta t) = k\} \cdot |z|^{k} \\
&= \sum\limits_{k=2}^{\infty} P\{X(\Delta t) = k\} = P\{X(\Delta t) \ge 2\}
\end{align}
$$
因此，在稀疏性假设下，有
$$
\dfrac{\left| \sum\limits_{k=2}^{\infty} P\{X(\Delta t) = k\} \cdot z^{k} \right|}{P \left\{ X(\Delta t) = 1 \right\}} \le \dfrac{P\{X(\Delta t) \ge 2\}}{P \left\{ X(\Delta t) = 1 \right\}} \xrightarrow{\Delta t \to 0} o(\Delta t)
$$
故由夹逼准则知
$$
\lim\limits_{ \Delta t \to 0 } \dfrac{1}{\Delta t} \cdot P\left\{ X(\Delta t) = 1 \right\} \cdot \dfrac{\sum\limits_{k=2}^{\infty} P\{X(\Delta t) = k\} \cdot z^{k}}{P\left\{ X(\Delta t) = 1 \right\}} = 0
$$

综上，将三项结果代入矩母函数的导数表达式中，得到
$$
\dfrac{\dif}{\dif t} G_{X(t)}(z) = G_{X(t)}(z) \cdot \left( -\lambda + \lambda z + 0 \right ) = (-\lambda + \lambda z) G_{X(t)}(z)
$$
该微分方程的初始条件为
$$
G_{X(0)}(z) = \mathbb{E}\left[z^{X(0)}\right] = z^{0} = 1
$$
故解得
$$
G_{X(t)}(z) =  \mark{ \e^{(-\lambda + \lambda z) t} } = \e^{-\lambda t} \cdot \e^{\lambda t z} = \e^{-\lambda t}  \sum\limits_{k=0}^{\infty} \dfrac{(\lambda t)^{k}}{k!}  z^{k}
$$
对比[[#矩母函数]]的定义式，可知
$$
P\{X(t) = k\} = \dfrac{(\lambda t)^{k}}{k!} \e^{-\lambda t} , \qquad k = 0, 1, 2, \cdots
$$
这是一个以 $\lambda t$ 为参数的 **Poisson 分布**。

> [!def.] Poisson 过程
> 设 $N(t)$ 是一个随机过程，满足以下条件：
> 1. $N(t)$ 的取值为非负整数，且**初态 $N(0) = 0$**，
> 2. $N(t)$ 具有**增量独立性**和**增量平稳性**，
> 3. $N(t)$ 满足**稀疏性假设**，即 $\cfrac{P\left\{ N(\Delta t) \ge 2 \right\}}{P\left\{ N(\Delta t) = 1 \right\}} = o(\Delta t)$（$\Delta t \to 0$），
> 
> 则称 $N(t)$ 为 **Poisson 过程 (Poisson process)**，其概率分布为
> $$
> P\{N(t) = k\} = \dfrac{(\lambda t)^{k}}{k!} \e^{-\lambda t} , \qquad k = 0, 1, 2, \cdots
> $$
> 其中 $\lambda > 0$ 称为 Poisson 过程的**强度 (intensity)**。

由增量平稳性，概率分布也写为
$$
P\{N(t) - N(s) = k\} = \dfrac{(\lambda (t - s))^{k}}{k!} \e^{-\lambda (t - s)} , \qquad k = 0, 1, 2, \cdots
$$

## Poisson 过程的基本性质

### 非宽平稳

由 Poisson 过程的概率分布可知
$$
\mathbb{E}[N(t)] = \lambda t, \qquad \mathrm{Var}[N(t)] = \lambda t, \qquad
\mathbb{E} \left[ N^{2}(t) \right] = \lambda t + (\lambda t)^{2}
$$
Poisson 过程的相关函数为
$$
R_{N}(t_{1}, t_{2}) = \mathbb{E}[N(t_{1}) N(t_{2})] = \underbrace{ \lambda \min(t_{1}, t_{2}) }_{ C_{N}(t, s) } + \lambda^{2} t_{1} t_{2}
$$
因此，Poisson 过程既不满足**均值平稳 (mean stationary)**，也不满足**相关平稳 (correlation stationary)**，故 Poisson 过程是一个**非宽平稳**的随机过程，我们需要借助其他方法来分析其性质。

### 条件均值

设 $N(t)$ 是一个 Poisson 过程，且 $0 \le s < t$，则**沿时间方向**有
$$
\begin{align}
\mathbb{E} \left[ N(t) \mathop| N(s) \right] &= \mathbb{E} \left[ N(t) -N(s) + N(s) \mathop| N(s) \right]  \\
&= \mathbb{E} \left[ N(t) - N(s) \mathop| N(s) \right] + \mathbb{E} \left[ N(s) \mathop| N(s) \right] \\
&= \mathbb{E} \left[ N(t) - N(s) \right] + N(s) = \lambda (t - s) + N(s)
\end{align}
$$
即 Poisson 过程的条件期望是**时间线性**的，事件继续发生的速率仍为 $\lambda$。

反过来，我们考虑**逆时间方向**的条件概率分布，有
$$
\begin{align}
P \left\{ N(s) = k \mathop| N(t) = n \right\} &= \dfrac{P \left\{ N(s) = k, N(t) = n \right\}}{P \left\{ N(t) = n \right\}} \\
&= \dfrac{P \left\{ N(s) = k, N(t) - N(s) = n - k \right\}}{P \left\{ N(t) = n \right\}} \\
&= \dfrac{P \left\{ N(s) = k \right\} \cdot P \left\{ N(t) - N(s) = n - k \right\}}{P \left\{ N(t) = n \right\}} \\
&= \cfrac{ \dfrac{(\lambda s)^{k}}{k!} \e^{-\lambda s} \cdot \dfrac{(\lambda (t - s))^{n - k}}{(n - k)!} \e^{-\lambda (t - s)} }{ \dfrac{(\lambda t)^{n}}{n!} \e^{-\lambda t} } \\
&= \binom{n}{k} \left( \dfrac{s}{t} \right)^{k} \left( 1 - \dfrac{s}{t} \right)^{n - k}
\end{align}
$$
即在给定 $N(t) = n$ 的条件下，此前的 $N(s)$ 将转而服从**二项分布** $B\left( n, \cfrac{s}{t} \right)$，从而
$$
\mathbb{E} \left[ N(s) \mathop| N(t) \right] = N(t) \cdot \dfrac{s}{t}
$$
同样也是时间线性的，但不同的是，此时的**系数与 Poisson 过程的强度 $\lambda$ 无关**，因为 Poisson 过程的增量独立性使得过去的信息无法影响未来的分布，但已知的信息可以推测过去的分布。

### 事件间隔

由增量独立性和增量平稳性，我们只需研究从初态开始到第一个事件的间隔 $T_{1}$ 的分布，其定义为
$$
F_{T_{1}}(t) = P\{T_{1} \le t\} = P \left\{ N(t) \ge 1 \right\} = 1 - P \left\{ N(t) = 0 \right\} = 1 - \e^{-\lambda t}
$$
因此
$$
f_{T_{1}}(t) = \dfrac{\dif}{\dif t} F_{T_{1}}(t) = \lambda \e^{-\lambda t}, \qquad t \ge 0
$$
于是事件间隔均服从参数为 $\lambda$ 的**指数分布**，即 $\left\{ T_{k} \right\} \stackrel{\text{i.i.d}}{\sim} \text{Exp}(\lambda)$，有
$$
\mathbb{E}[T_{k}] = \dfrac{1}{\lambda}, \qquad \mathrm{Var}[T_{k}] = \dfrac{1}{\lambda^{2}}
$$

由独立性，容易得到事件间隔 $T_{1}, \cdots, T_{k}$ 的**联合概率密度函数**为
$$
f_{T_{1}, T_{2}, \cdots, T_{k}}(t_{1}, t_{2}, \cdots, t_{k}) = \prod\limits_{i=1}^{k} f_{T_{i}}(t_{i}) = \lambda^{k} \e^{-\lambda \sum\limits_{i=1}^{k} t_{i}}, \qquad t_{i} \ge 0
$$

### 等待时间

#### 等待时间的边缘分布

设第 $n$ 个事件发生的时间为 $S_{n} = \sum\limits_{k=1}^{n} T_{k}$。引入**特征函数 $\phi_{X}(\omega) = \mathbb{E}\left[ \e^{\J \omega X} \right]$**，则由事件间隔的独立性，有
$$
\phi_{T_{k}}(\omega) = \int_{0}^{\infty} \lambda \e^{-\lambda t} \cdot \e^{\J \omega t} \dif t = \dfrac{\lambda}{\lambda - \J \omega}  
\implies
\phi_{S_{n}}(\omega) = \left( \phi_{T_{k}}(\omega) \right)^{n} = \left( \dfrac{\lambda}{\lambda - \J \omega} \right)^{n}
$$
因此可以通过逆变换求得 **$S_{n}$ 的概率密度函数**为
$$
f_{S_{n}}(t) = \dint_{-\infty}^{\infty} \phi_{S_{n}}(\omega) \cdot \e^{-\J \omega t} \dfrac{\dif \omega}{2 \pi}
= \begin{cases}
\dfrac{\lambda (\lambda t)^{n - 1}}{(n - 1)!} \e^{-\lambda t}, & t \ge 0, \\
0, & t < 0
\end{cases}
$$
此为参数为 $(n, \lambda)$ 的 **Erlang 分布 (Erlang distribution)**。

> [!note] 等待时间分布与 Poisson 过程概率分布的转换
> 设 $N(t)$ 是参数为 $\lambda$ 的 Poisson 过程，第 $n$ 个事件发生的时间为 $S_{n}$，则有重要关系
> $$
> P\{ S_{n} \le t \} = P\{ N(t) \ge n \}, \qquad P\{ S_{n} > t \} = P\{ N(t) < n \}
> $$
> 
> 由此关系也可以导出等待时间的概率密度函数，即
> $$
> F_{S_{n}}(t) = P\{ S_{n} \le t \} = P\{ N(t) \ge n \} = \sum\limits_{k=n}^{\infty} P\{ N(t) = k \}
> = \sum\limits_{k=n}^{\infty} \dfrac{(\lambda t)^{k}}{k!} \e^{-\lambda t}
> $$
> $$
> \begin{align}
> f_{S_{n}}(t) = \dfrac{\dif}{\dif t} F_{S_{n}}(t) &= \sum\limits_{k=n}^{\infty} \left( \dfrac{\lambda (\lambda t)^{k-1}}{(k - 1)!} \e^{-\lambda t} - \dfrac{\lambda (\lambda t)^{k}}{k!} \e^{-\lambda t} \right) \\
> &= \dfrac{\lambda (\lambda t)^{n - 1}}{(n - 1)!} \e^{-\lambda t} + \lim\limits_{ n \to \infty } \dfrac{\lambda (\lambda t)^{n}}{n!} \e^{-\lambda t} = \dfrac{\lambda (\lambda t)^{n - 1}}{(n - 1)!} \e^{-\lambda t}
> \end{align}
> $$

为将 $n$ 推广为任意正实数，可引入 **$\boldsymbol{\varGamma}$ 函数 $\varGamma(\alpha) = \dint_{0}^{\infty} t^{\alpha - 1} \e^{-t} \dif t$** 替代阶乘，则 $S_{n}$ 的概率密度函数可写为
$$
f_{S_{n}}(t) = \begin{cases}
\dfrac{\lambda (\lambda t)^{n - 1}}{\varGamma(n)} \e^{-\lambda t}, & t \ge 0, \\
0, & t < 0
\end{cases}
$$
此即参数为 $(n, \lambda)$ 的 **$\boldsymbol{\varGamma}$ 分布 (Gamma distribution)**。

#### 等待时间的联合分布

可以用**微元法**导出 $S_{1},S_{2}, \cdots, S_{k}$ 的联合概率密度函数。设 $0 < t_{1} < t_{2} < \cdots < t_{k}$，并取足够小的正数 $h_{1}, \cdots, h_{k}$，有
$$
\begin{align}
&P \left\{ t_{1} \le S_{1} < t_{1} + h_{1}, t_{2} \le S_{2} < t_{2} + h_{2}, \cdots, t_{k} \le S_{k} < t_{k} + h_{k} \right\} \\
&= P \big\{ N(t_{1}) = 0, N(t_{1} + h_{1}) - N(t_{1}) = 1, N(t_{2}) - N(t_{1} + h_{1}) = 0, \cdots,  \\
&\hspace{2.6em} N(t_{k}) - N(t_{k-1} + h_{k-1}) = 0,N(t_{k} + h_{k}) - N(t_{k}) = 1 \big\} \\
&= P \left\{ N(t_{1}) = 0 \right\} \cdot P \left\{ N(t_{1} + h_{1}) - N(t_{1}) = 1 \right\}  \cdots \\
&\hspace{1.2em} \cdot P \left\{ N(t_{k}) - N(t_{k-1} + h_{k-1}) = 0 \right\} \cdot P \left\{ N(t_{k} + h_{k}) - N(t_{k}) = 1 \right\} \\
&= \e^{-\lambda t_{1}} \cdot (\lambda h_{1} \e^{-\lambda h_{1}}) \cdot \e^{-\lambda (t_{2} - t_{1} - h_{1})} \cdots (\lambda h_{k} \e^{-\lambda h_{k}}) \\
&= \lambda^{k} \e^{-\lambda (t_{k} + h_{k})} \cdot h_{1} h_{2} \cdots h_{k}  \\
&\xrightarrow{h_{i} \to 0} f_{S_{1}, S_{2}, \cdots, S_{k}}(t_{1}, t_{2}, \cdots, t_{k}) \cdot h_{1} h_{2} \cdots h_{k}
\end{align}
$$
因此，得到 **$S_{1}, S_{2}, \cdots, S_{k}$ 的联合概率密度函数**
$$
f_{S_{1}, S_{2}, \cdots, S_{k}}(t_{1}, t_{2}, \cdots, t_{k}) = \begin{cases}
\lambda^{k} \e^{-\lambda t_{k}}, & 0 < t_{1} < t_{2} < \cdots < t_{k}, \\
0, & \text{otherwise}
\end{cases}
$$

#### 等待时间的条件分布

给定 $N(t) = n$，考察前 $n$ 个事件发生时间的条件联合分布。同样由微元法，设 $0 < t_{1} < t_{2} < \cdots < t_{n} < t$，并取足够小的正数 $h_{1}, \cdots, h_{n}$，有
$$
\begin{align}
&P \left\{ t_{1} \le S_{1} < t_{1} + h_{1}, t_{2} \le S_{2} < t_{2} + h_{2}, \cdots, t_{n} \le S_{n} < t_{n} + h_{n} \mid N(t) = n \right\} \\
&= \dfrac{ P \left\{ t_{1} \le S_{1} < t_{1} + h_{1}, t_{2} \le S_{2} < t_{2} + h_{2}, \cdots, t_{n} \le S_{n} < t_{n} + h_{n}, N(t) = n \right\} }{ P \left\{ N(t) = n \right\} } \\
&= \dfrac{ P \left\{ N(t_{1}) = 0, N(t_{1} + h_{1}) - N(t_{1}) = 1, \cdots, N(t) - N(t_{n} + h_{n}) = 0 \right\} }{ P \left\{ N(t) = n \right\} } \\
&= \dfrac{ \lambda^{n} \e^{-\lambda (t_{n} + h_{n})} \cdot h_{1} h_{2} \cdots h_{n} \cdot \e^{-\lambda (t-t_{n} - h_{n})} }{ \dfrac{(\lambda t)^{n}}{n!} \e^{-\lambda t} } 
= \dfrac{ n! }{ t^{n} } \cdot h_{1} h_{2} \cdots h_{n}  \\
&\xrightarrow{h_{i} \to 0} f_{S_{1}, S_{2}, \cdots, S_{n} \mid N(t) = n}(t_{1}, t_{2}, \cdots, t_{n}) \cdot h_{1} h_{2} \cdots h_{n}
\end{align}
$$
即得到**条件联合概率密度函数**
$$
f_{S_{1}, S_{2}, \cdots, S_{n} \mid N(t) = n}(t_{1}, t_{2}, \cdots, t_{n}) = \begin{cases}
\cfrac{ n! }{ t^{n} }, & 0 < t_{1} < t_{2} < \cdots < t_{n} < t, \\
0, & \text{otherwise}
\end{cases}
$$

> [!note] 顺序统计量
> 设 $X_{1}, X_{2}, \cdots, X_{n}$ 是来自某一分布 $F_{X}(x)$ 的 $n$ 个**独立同分布**随机变量，则将它们按从小到大的顺序排列，记为 $Y_{1} \le Y_{2} \le \cdots \le Y_{n}$，即称 $\left\{ Y_{i} \right\}_{i=1}^{n}$ 为 $X_{1}, X_{2}, \cdots, X_{n}$ 的**顺序统计量 (order statistics)**。第 $k$ 顺序统计量 $Y_{k}$ 即为 $X_{1}, X_{2}, \cdots, X_{n}$ 中第 $k$ 小的值。
> 
> 对于两个极端情况，容易得到
> $$
> \begin{align}
> &F_{Y_{n}}(x) = \prod\limits_{i=1}^{n} P\{ X_{i} \le x \} = \left( F_{X}(x) \right)^{n} \\
> &F_{Y_{1}}(x) = 1 - \prod\limits_{i=1}^{n} P\{ X_{i} > x \} = 1 - \left( 1 - F_{X}(x) \right)^{n}
> \end{align}
> $$
> 对于一般的 $Y_{k}$，设有充分小的 $h$ 使得 $x < Y_{k} \le x + h$，即 $k-1$ 个 $X_{i}$ 落在 $(-\infty, x]$，1 个 $X_{i}$ 落在 $(x, x+h]$，其余 $n-k$ 个 $X_{i}$ 落在 $(x+h, +\infty)$，则有
> $$
> \begin{align}
> f_{Y_{k}}(x) &= \lim\limits_{ h \to 0 } \dfrac{ P \left\{ x < Y_{k} \le x + h \right\} }{ h } \\
> &= \lim\limits_{ h \to 0 } \dfrac{1}{h} \binom{n}{k-1} \binom{n - k + 1}{1} \binom{n - k}{n - k} \\
> &\hspace{3em} \cdot \left( F_{X}(x) \right)^{k - 1} \cdot \left( F_{X}(x + h) - F_{X}(x) \right) \cdot \left( 1 - F_{X}(x + h) \right)^{n - k} \\
> &= \binom{n}{k-1} \binom{n - k + 1}{1} ( F_{X}(x) )^{k - 1} ( 1 - F_{X}(x) )^{n - k}  f_{X}(x) \\
> \end{align}
> $$
> 同理，通过微元法拆分，可以得到**顺序统计量的联合概率密度函数**
> $$
> f_{Y_{1}, Y_{2}, \cdots, Y_{n}}(y_{1}, y_{2}, \cdots, y_{n}) = \begin{cases}
> n! \prod\limits_{i=1}^{n} f_{X}(y_{i}), & y_{1} < y_{2} < \cdots < y_{n}, \\
> 0, & \text{otherwise}
> \end{cases}
> $$
> 
> 注意到，$n$ 个在 $(0, t)$ 上**独立同分布**的**均匀分布**随机变量的**顺序统计量**的联合概率密度函数与上述条件联合概率密度函数形式完全相同，因此 **等待时间 $S_{1}, S_{2}, \cdots, S_{n}$ 在条件 $N(t) = n$ 下可视为 $n$ 个在 $(0, t)$ 上独立同分布的均匀分布随机变量的顺序统计量**。这意味着，就**总等待时间**而言，可以将 Poisson 过程视为在时间轴上随机均匀分布的事件集合。

对条件联合概率密度函数进行边缘化，有
$$
\begin{align} 
f_{S_{k} \mid N(t) = n}(s_{k}) &= \dint_{0}^{s_{k}} \dif s_{k-1} \dint_{0}^{s_{k-1}} \dif s_{k-2} \cdots \dint_{0}^{s_{2}} \dif s_{1} \cdot \dint_{s_{k}}^{t} \dif s_{k+1} \cdots \dint_{s_{n-1}}^{t} \dif s_{n} \\
&\hspace{1em} \cdot f_{S_{1}, S_{2}, \cdots, S_{n} \mid N(t) = n}(s_{1}, s_{2}, \cdots, s_{n}) \\
&= \dfrac{n!}{t^{n}} \cdot \dfrac{s_{k}^{k-1}}{(k-1)!} \dfrac{(t - s_{k})^{n - k}}{(n - k)!} \\
&= \dfrac{1}{t} \dfrac{n!}{(k-1)! (n - k)!} \left( \dfrac{s_{k}}{t} \right)^{k-1} \left( 1 - \dfrac{s_{k}}{t} \right)^{n - k},
\quad 0 < s_{k} < t
\end{align}
$$
这即为参数为 $(k, n-k+1, t)$ 的 **Beta 分布 (Beta distribution)**。利用 Beta 函数与 Gamma 函数的关系
$$
B(\alpha, \beta) = \dint_{0}^{1} t^{\alpha - 1} (1 - t)^{\beta - 1} \dif t = \dfrac{\varGamma(\alpha) \varGamma(\beta)}{\varGamma(\alpha + \beta)}
\stackrel{\alpha, \beta \in \mathbb{Z}_{+}}{=\!=\!=\!=\!=} \dfrac{(\alpha - 1)! (\beta - 1)!}{(\alpha + \beta - 1)!}
$$
可得
$$
\begin{align}
&\mathbb{E} \left[ S_{k} \mid N(t) = n \right] = \dfrac{k}{n+1} t, \quad \mathbb{E} \left[ S_{k}^{2} \mid N(t) = n \right] = \dfrac{k (k+1)}{(n+1)(n+2)} t^{2} \\
&\mathrm{Var} \left[ S_{k} \mid N(t) = n \right] = \dfrac{k (n - k + 1)}{(n + 1)^{2} (n + 2)} t^{2}
\end{align}
$$


## Poisson 过程的拓广

### 非齐次 Poisson 过程

对于某些实际问题，事件发生的强度并非恒定不变，而是随着时间变化的。为此，考虑**削弱 Poisson 过程的增量平稳性**，即不再有
$$
\Delta N(t) = N(t + \Delta t) - N(t) \stackrel{\text{d}}{=} N(\Delta t)
$$

此时，[[#^JumuHanshuDeDaoshu|矩母函数的导数式]]中 $N(\Delta t)$ 应全部保留为 $\Delta N(t)$，处理 [[#Term 1]] 时不再有 $P\{\Delta N(t) = 0\} = \e^{-\lambda \Delta t}$，我们引入
$$
\lim\limits_{ \Delta t \to 0 } \dfrac{1}{\Delta t} \left( 1 - P\{\Delta N(t) = 0\} \right) = \lambda(t)
$$
对 [[#Term 2]]，仍有
$$
\dfrac{1 - P \left\{ \Delta N(t) = 0 \right\}}{\Delta t} = \dfrac{P \left\{ \Delta N(t) = 1 \right\}}{\Delta t} \left( 1 + \dfrac{P\left\{ \Delta N(t) \ge 2 \right\}}{P\left\{ \Delta N(t) = 1 \right\}} \right)
$$
且仍保留[[#^XishuxingJiashe|稀疏性假设]]
$$
\lim_{\Delta t \to 0} \dfrac{1}{\Delta t} \dfrac{P\left\{ \Delta N(t) \ge 2 \right\}}{P\left\{ \Delta N(t) = 1 \right\}} = 0
$$
因此有
$$
\lim\limits_{ \Delta t \to 0 } \dfrac{1}{\Delta t} P \left\{ \Delta N(t) = 1 \right\} = \lambda(t)
$$
这也使得 $\lambda(t)$ 可视为**事件发生速率**；类似地，[[#Term 3]] 仍为 0，故得到**关于矩母函数的微分方程**
$$
\dfrac{\dif}{\dif t} G_{N(t)}(z) = (-\lambda(t) + \lambda(t)z) G_{N(t)}(z), \qquad G_{N(0)}(z) = 1
$$
解得
$$
G_{N(t)}(z) = \exp\left( \dint_{0}^{t} \lambda(\tau) \dif \tau \cdot (z-1) \right) = \exp\left( z\dint_{0}^{t} \lambda(\tau) \dif \tau \right) \exp\left( -\dint_{0}^{t} \lambda(\tau) \dif \tau \right)
$$
故得
$$
P\left\{ N(t) = k \right\} = \dfrac{\left( \dint_{0}^{t} \lambda(\tau) \dif \tau \right)^{k}}{k!} \exp\left( - \dint_{0}^{t} \lambda(\tau) \dif \tau \right)
$$
当 $\lambda(t)$「齐次」为 $\lambda(t) \equiv \lambda$ 时，即得到 Poisson 分布的概率分布，故此分布称为**非齐次 Poisson 过程 (non-homogeneous Poisson Process)**。

类似于参数为 $\lambda$ 齐次 Poisson 过程 $N(t)$ 服从**参数为 $\lambda t$ 的 Poisson 分布**，事件发生速率为 $\lambda(t)$ 的非齐次 Poisson 过程 $N(t)$ 服从**参数为 $\dint_{0}^{t} \lambda(\tau) \dif \tau$ 的 Poisson 分布**，有
$$
\mathbb{E} \left[ N(t) \right] = \mathrm{Var} \left[ N(t) \right] = \dint_{0}^{t} \lambda(\tau) \dif \tau
$$

### 复合 Poisson 过程

#### 从事件「效果」引入复合 Poisson 过程

考虑**发生次数服从 Poisson 过程**的随机过程 $X(t) = \sum\limits_{k=1}^{N(t)} X_{k}$，其中单个事件的「效果」$\left\{ X_{k} \right\}_{k=1}^{\infty}$ 独立同分布且独立于 $N(t)$。

已知 $G_{N(t)}(z) = \mathbb{E} \left[ z^{N(t)} \right] = \e^{(-\lambda + \lambda z) t}$，则 $X(t)$ 的矩母函数为
$$
\begin{align}
G_{X(t)} (z) &= \mathbb{E} \left[ z^{X(t)} \right] = \mathbb{E} \left[ z^{\sum_{k=1}^{N(t)}X_{k}} \right] = \mathbb{E}_{N(t)} \left[ \mathbb{E}_{X_{k} \mid N(t)} \left[ z^{\sum_{k=1}^{n}X_{k}} \mathop{\Big|} N(t) = n \right]  \right] \\
&= \mathbb{E} \left[ \left( \mathbb{E} \left[ z^{X_{k}} \right] \right)^{N(t)}  \right] = G_{N(t)}(G_{X_{k}}(z)) = \e^{(-\lambda + \lambda G_{X_{k}}(z)) t}
\end{align}
$$
可见，**$X(t)$ 的矩母函数**（或**特征函数**，若 $\left\{ X_{k} \right\}_{k=1}^{\infty}$ 取值不为非负整数）为 $N(t)$ 的矩母函数与 $\left\{ X_{k} \right\}_{k=1}^{\infty}$ 的矩母函数（或特征函数）的**复合**，因此称为**复合 Poisson 过程 (compound Poisson process)**。

> [!example] [[例题#L14-1]]：Poisson 过程的独立稀释

> [!example] [[例题#L14-2]]：Poisson 过程的和与差

#### 从事件稀疏性引入复合 Poisson 过程

另一方面，对于某些实际问题，时间微元内出现 2 次或以上事件的概率不可忽略，需要考虑**削弱 Poisson [[#^XishuxingJiashe|稀疏性假设]]**，即设定
$$
P\left\{ X(\Delta t) = k \mid X(\Delta t) \ge 1 \right\} \xrightarrow{\Delta t \to 0} p_{k}
$$
这对 [[#Term 1]] 没有影响；对 [[#Term 2]]、[[#Term 3]]，不再需要分开讨论，有
$$
\begin{align}
&\lim_{\Delta t \to 0} \dfrac{1}{\Delta t} \sum\limits_{k=1}^{\infty} P\left\{ X(\Delta t) = k \right\} \cdot z^{k}  \\
&= \lim_{\Delta t \to 0} \dfrac{1}{\Delta t} P\left\{ X(\Delta t) \ge 1 \right\} \cdot \sum\limits_{k=1}^{\infty} P\left\{ X(\Delta t) = k \mid X(\Delta t) \ge 1 \right\} \cdot z^{k} \\
&= \lim_{\Delta t \to 0} \dfrac{1}{\Delta t} (1 - P \left\{ X(\Delta t) = 0 \right\}) \underbrace{ \sum\limits_{k=1}^{\infty} p_{k} z^{k} }_{ P(z) }= \lambda P(z)
\end{align}
$$
即得到**关于矩母函数的微分方程**
$$
\dfrac{\dif}{\dif t} G_{X(t)}(z) = \lambda(P(z) - 1) G_{X(t)}(z), \qquad G_{X(0)}(z) = 1
$$
解得
$$
G_{X(t)}(z) = \exp\left( \lambda t (P(z) - 1) \right) = \exp\left( \lambda t P(z) \right) \exp\left( -\lambda t \right) = G_{N(t)}(P(z))
$$
此即上述复合 Poisson 过程的矩母函数。

### 过滤 Poisson 过程

在复合 Poisson 过程中，若将事件「效果」看作是由 $\left\{ X_{k} \right\}_{k=1}^{\infty}$ 决定的**某个随机系统的输出**，则该过程可视为**过滤 Poisson 过程 (filtered Poisson process)**。设该随机系统的**冲激响应 (impulse response)** 为 $h(t; x)$，则系统输出为
$$
Y(t) = \sum\limits_{k=1}^{N(t)} h(t - S_{k}; X_{k})
$$
其中 $S_{k} = \sum\limits_{i=1}^{k} T_{i}$ 为第 $k$ 个事件发生的时间，$T_{i}$ 为事件间隔。

**$Y(t)$ 的特征函数**为
$$
\begin{align}
\phi_{Y(t)}(\omega) &= \mathbb{E} \left[ \e^{\J \omega Y(t)} \right] = \mathbb{E} \left[ \exp\left( \J \omega \sum\limits_{k=1}^{N(t)} h(t - S_{k}; X_{k}) \right) \right] \\
&= \mathbb{E}_{N(t)} \left[ \mathbb{E}_{\{S_{k}, X_{k}\}} \left[ \exp\left( \J \omega \sum\limits_{k=1}^{n} h(t - S_{k}; X_{k}) \right) \mathop{\Bigg|} N(t) = n \right]  \right] \\
&= \mathbb{E}_{N(t)} \left[ \mathbb{E}_{\{U_{k}, X_{k}\}} \left[ \prod\limits_{k=1}^{n} \e^{ \J \omega h(t - U_{k}; X_{k}) } \mathop{\Bigg|} N(t) = n \right]  \right] \\
&= \mathbb{E}_{N(t)} \left[ \left( \dint_{0}^{t} \mathbb{E}_{X_{k}} \left[ \e^{ \J \omega h(t - u; X_{k}) } \right] \dfrac{1}{t} \dif u \right)^{N(t)}  \right] \\
&\stackrel{\mathbb{E} \left[ z^{N(t)} \right] = \e^{\lambda t (z-1)}}{=\!=\!=\!=\!=\!=\!=\!=\!=} \exp\left( \lambda t \left( \dint_{0}^{t} \mathbb{E} \left[ \e^{ \J \omega h(t - u; X_{k}) } \right] \dfrac{1}{t} \dif u - 1 \right) \right) \\
&= \exp\left( \lambda \dint_{0}^{t} \left( \mathbb{E} \left[ \e^{ \J \omega h(t - u; X_{k}) } \right] - 1 \right) \dif u \right)
\end{align}
$$
其中 $\{U_{k}\}$ 为在 $(0, t)$ 上独立同分布的均匀分布随机变量，其顺序统计量即为条件 $N(t) = n$ 下的 $\{S_{k}\}$，在求和意义下二者等价。

由特征函数，容易得到 $Y(t)$ 的**均值与方差**
$$
\mathbb{E} \left[ Y(t) \right] = \lambda \dint_{0}^{t} \mathbb{E} \left[ h(t - u; X_{k}) \right] \dif u, \quad
\mathrm{Var} \left[ Y(t) \right] = \lambda \dint_{0}^{t} \mathbb{E} \left[ h^{2}(t - u; X_{k}) \right] \dif u
$$
若事件的影响是**因果**的，即 $h(t; x) = 0$ 对 $t < 0$ 成立，则用类似的方法可以计算过滤 Poisson 过程的二维特征函数
$$
\begin{align}
\phi_{Y(t_{1}), Y(t_{2})}(\omega_{1}, \omega_{2}) &= \mathbb{E} \left[ \e^{\J \omega_{1} Y(t_{1}) + \J \omega_{2} Y(t_{2})} \right] \\
&= \exp\left( \lambda \dint_{0}^{\max\{t_{1}, t_{2}\}} \left( \mathbb{E} \left[ \e^{ \J \omega_{1} h(t_{1} - u; X_{k}) + \J \omega_{2} h(t_{2} - u; X_{k}) } \right] - 1 \right) \dif u \right)
\end{align}
$$
从而得到**协方差函数**
$$
C_{Y}(t_{1}, t_{2}) = \lambda \dint_{0}^{\min\{t_{1}, t_{2}\}} \mathbb{E} \left[ h(t_{1} - u; X_{k}) h(t_{2} - u; X_{k}) \right] \dif u
$$

特别地，**波形 $h$ 不具有随机性**时，有
$$
\begin{align}
&\phi_{Y(t)}(\omega) = \exp\left( \lambda \dint_{0}^{t} \left( \e^{ \J \omega h(t - u) } - 1 \right) \dif u \right), \\
&\mathbb{E} \left[ Y(t) \right] = \lambda \dint_{0}^{t} h(t - u) \dif u, \quad \mathrm{Var} \left[ Y(t) \right] = \lambda \dint_{0}^{t} h^{2}(t - u) \dif u, \\
&C_{Y}(t_{1}, t_{2}) = \lambda \dint_{0}^{\min\{t_{1}, t_{2}\}} h(t_{1} - u) h(t_{2} - u) \dif u
\end{align}
$$

# Markov 链

## Markov 链的定义

**Markov 链**是描述**离散时间、离散状态**的随机过程的模型，是具有 [[#Markov 性]]的离散时间离散状态随机过程。

### Markov 性

对一个随机过程 $\left\{ X_{k} \right\}_{k=0}^{\infty}$，**Markov 性**表述为 $\forall n$
$$
P \left\{ X_{n} = x_{n} \mid X_{n-1} = x_{n-1}, \cdots , X_{1} = x_{1} , X_{0} = x_{0} \right\} = P \left\{ X_{n} = x_{n} \mid X_{n-1} = x_{n-1} \right\}
$$

若称 $X_{n-1}$ 为**现在**（$B$），之前的状态为**过去**（$A$），之后的状态为**未来**（$C$），则 **Markov 性**表明了条件之间的独立性
$$
P(CA \mid B) = P(C \mid B) P(A \mid B)
$$
「过去」与「未来」之间的联系，只有通过「现在」建立起来。如果掌握了现在，那么过去的信息对于推测未来不起作用。

「过去」和「未来」均可以复杂化，即
+ 将未来 $X_{n}$ **泛化为集合 $A$**，有
$$
\begin{align} 
&P \left\{ X_{n} \in A \mid X_{n-1} = x_{n-1}, \cdots , X_{1} = x_{1} , X_{0} = x_{0}  \right\}  \\
&= \sum\limits_{x_{n} \in A} P \left\{ X_{n} = x_{n} \mid X_{n-1} = x_{n-1}, \cdots , X_{1} = x_{1} , X_{0} = x_{0} \right\}  \\
&= \sum\limits_{x_{n} \in A} P \left\{ X_{n} = x_{n} \mid X_{n-1} = x_{n-1} \right\} = P \left\{ X_{n} \in A \mid X_{n-1} = x_{n-1} \right\}
\end{align}
$$
仍然保持 Markov 性；
+ 将过去 $(X_{n-2}, \cdots, X_{0})$ **泛化为集合 $B$**，有
$$
\begin{align} 
&P \{ X_{n} = x_{n}, (X_{n-2}, \cdots, X_{0}) \in B \mid X_{n-1} = x_{n-1} \} \\
&= \sum\limits_{\{x_{k}\}_{k=0}^{n-2} \in B} P \{ \underbrace{ X_{n} = x_{n} }_{ \text{「未来」} }, \underbrace{ (X_{n-2}, \cdots, X_{0}) \in (x_{n-2}, \cdots, x_{0}) }_{ \text{「过去」} } \mid \underbrace{ X_{n-1} = x_{n-1} }_{ \text{「现在」} } \} \\
&= \sum\limits_{\{x_{k}\}_{k=0}^{n-2} \in B} P \{ \underbrace{ X_{n} = x_{n} }_{ \text{「未来」} } \mid \underbrace{ X_{n-1} = x_{n-1} }_{ \text{「现在」} } \} \\
&\hspace{4.5em} \cdot P \{ \underbrace{ (X_{n-2}, \cdots, X_{0}) \in (x_{n-2}, \cdots, x_{0}) }_{ \text{「过去」} } \mid \underbrace{ X_{n-1} = x_{n-1} }_{ \text{「现在」} } \} \\
&= P \{ X_{n} = x_{n} \mid X_{n-1} = x_{n-1} \} \cdot P \{ (X_{n-2}, \cdots, X_{0}) \in B \mid X_{n-1} = x_{n-1} \}
\end{align}
$$
即
$$
\begin{align}
&P \{ X_{n} = x_{n} \mid (X_{n-2}, \cdots, X_{0}) \in B, X_{n-1} = x_{n-1} \} \\
&= \dfrac{P \{ X_{n} = x_{n}, (X_{n-2}, \cdots, X_{0}) \in B \mid X_{n-1} = x_{n-1} \}}{P \{ (X_{n-2}, \cdots, X_{0}) \in B \mid X_{n-1} = x_{n-1} \}} 
= P \{ X_{n} = x_{n} \mid X_{n-1} = x_{n-1} \}
\end{align}
$$
仍然保持 Markov 性。

但是，「现在」的复杂化将可能破坏 Markov 性。

### Markov 链的迭代表示

我们考虑 Markov 链的 $n$ 维联合概率分布，有
$$
\begin{align}
P(X_{n}, X_{n-1}, \cdots, X_{0}) &= P(X_{n} \mid X_{n-1}, \cdots, X_{0}) \cdot P(X_{n-1}, \cdots, X_{0}) \\
&= P(X_{n} \mid X_{n-1}) \cdot P(X_{n-1}, \cdots, X_{0}) \\
&= \cdots  \\
&= P(X_{n} \mid X_{n-1})  P(X_{n-1} \mid X_{n-2} ) \cdots P(X_{1} \mid X_{0}) P(X_{0})
\end{align}
$$
即，其决定于一组条件概率
$$
P_{i,j} (m, n) = P \left\{ X_{n} = x_{j} \mid X_{m} = x_{i} \right\}
$$
称为 $n - m$ 步**转移概率 (transition probability)**。

#### 平稳转移概率假设

一般地，一个 $n$ 步的转移概率 $P_{i,j}(m, m+n)$ 与其发生的时刻 $m$ 有关。如果其**与发生时刻无关**，即
$$
\forall m, \qquad
P_{i,j}(m, m+n) \equiv P_{i, j}(n)
$$
则称之为**平稳 (stationary)** Markov 链。

在此假设下，特定步数 $n$ 的转移概率只依赖于转移的**起点状态 $i$** 和**终点状态 $j$**，计算 $P_{i,j}^{(n)}$ 只需对起点与终点之间的每一条路径的概率求和即可，尽管也不是非常简便。

#### Chapman-Kolmogorov 方程

> [!theorem] Chapman-Kolmogorov 方程
> 设 Markov 链的状态空间为 $E$，$i,j,k \in E$，对时刻 $r, s, t$，有
> $$
> P_{i,j}(r, t) = \sum\limits_{k} P_{i,k} (r,s) P_{k,j} (s, t)
> $$
> 在[[#平稳转移概率假设]]下，对时间间隔 $m, n$，有
> $$
> P_{i,j}{(m + n)} = \sum\limits_{k} P_{i,k}{(m)} P_{k,j}{(n)}
> $$
^ChapmanKolmogorovIdentity

[[#^ChapmanKolmogorovIdentity|C-K 方程]]的本质是将路径求和**按照中间时刻 $s$（或中间步数 $m$）的状态 $k$ 分组**，因此显然是一个恒等式。具体地，
$$
\begin{align}
P_{i,j}{(m + n)} &= P \left\{ X_{m + n} = x_{j} \mid X_{0} = x_{i} \right\}  \\
&= \sum\limits_{k} P \left\{ X_{m + n} = x_{j} , X_{m} = x_{k} \mid X_{0} = x_{i} \right\} \\
&= \sum\limits_{k} P \left\{ X_{m + n} = x_{j} \mid X_{m} = x_{k}, X_{0} = x_{i} \right\} P \left\{ X_{m} = x_{k} \mid X_{0} = x_{i} \right\} \\
&= \sum\limits_{k} \underbrace{ P \left\{ X_{m + n} = x_{j} \mid X_{m} = x_{k} \right\} }_{ P_{k,j}{(n)} } \underbrace{ P \left\{ X_{m} = x_{k} \mid X_{0} = x_{i} \right\} }_{ P_{i,k}{(m)} }
\end{align}
$$

容易发现，[[#^ChapmanKolmogorovIdentity|C-K 方程]]的形式类似**矩阵乘法**，由此定义
$$
\boldsymbol{P}(n) = \Big( P_{i,j}{(n)} \Big)_{i,j}
$$
称为 **$n$ 步转移概率矩阵**，则立得
$$
\mark{ \boldsymbol{P}(m + n) = \boldsymbol{P}(m) \boldsymbol{P}(n) }
$$

于是，任意步数 $n$ 的转移概率矩阵为
$$
\boldsymbol{P}(n) = \boldsymbol{P}(n-1) \boldsymbol{P}(1) = \boldsymbol{P}(n-2) (\boldsymbol{P}(1))^{2} = \cdots (\boldsymbol{P}(1))^{n}
$$
因此，只要给定
+ **1 步转移概率矩阵** $\boldsymbol{P}(1) = \Big( P_{i,j}{(1)} \Big)_{i,j}$，不妨**记为 $\boldsymbol{P}$**，以及
+ **初始概率分布 $\big\{ P \left\{ X_{0} = x_{i} \right\} \big\}_{i}$**，

则整个 Markov 链的概率分布就确定了。

## Markov 链的常返性

从 Markov 性的「精神」出发，当转移步数 $n$ 即**时间趋于无穷**时，我们希望 Markov 链达到一个**不依赖初始状态的稳定分布**，即希望有
$$
P_{i,j}{(n)} \quad \xrightarrow{n \to \infty} \quad P_{j}
$$

### Markov 链状态的分类

我们期望深入考察 Markov 链的状态空间结构，为此**将状态值 $x_{i}$ 简记为 $i$**，并给出如下几个定义：
+ 若 $\exists n > 0$，$P_{i,j}(n) > 0$，则称 **$i$ 可达 (reachable) $j$**，记作 $i \to j$；
+ 若 $i \to j$ 且 $j \to i$，则称 **$i$、$j$ 相通 (commutative)**，记作 $i \leftrightarrow j$；
+ 如果对集合 $S \subseteq E$，$\forall i \in S$、$j \not\in S$，$i \not\to j$，则称 $S$ 为**闭集 (closed set)**。 ^ClosedSet

> [!def.] 不可约 Markov 链
> 设 Markov 链的状态空间为 $E$，如果子集 $C \subseteq E$ 仅有一个[[#^ClosedSet|闭集]] $C$ 本身，即**不存在闭的真子集**，则称该子集为**不可约 (irreducible)** 的。
> 
> 如果状态空间 $E$ 本身是不可约的，则称该 Markov 链为**不可约**的。
^Bukeyue

设 $C \subseteq E$ 不可约，我们设 $\forall i \in C$，$A_{i} = \left\{ j \in C \mid i \to j \right\}$ 为 $i$ 可达的状态集合，现在我们证明 $A_{i}$ 是闭集，从而得到 $A_{i} = C$。$\forall j \in A_{i}$，假定 $\exists k \not\in A_{i}$，使得 $j \to k$，则由 $i \to j$ 和 $j \to k$ 可知 $i \to k$，从而 $k \in A_{i}$，与假设矛盾，因此 $A_{i}$ 是闭集，只能有 $A_{i} = C$。因此，**不可约 Markov 链中任意两个状态相通**。

### 常返

设 Markov 链的状态空间为 $E$，对 $i, j \in E$，定义从时刻 $n = 0$ 出发到达状态 $j$ 的**首达时间 (first passage time)** 为
$$
\tau_{j} = \inf \left\{ n \geq 1 \mid X_{n} = j \right\}
$$
经 $n$ 步从状态 $i$ 到状态 $j$ 的**首达概率 (first passage probability)** 为
$$
\begin{align} 
f_{i,j}(n) &= P \left\{ \tau_{j} = n \mid X_{0} = i \right\} \\
&= P \left\{ X_{1} \neq j, X_{2} \neq j, \cdots, X_{n-1} \neq j, X_{n} = j \mid X_{0} = i \right\} 
\end{align}
$$

显然，在哪一步首达的事件之间是互斥的，因此有
$$
f_{i,j} = \sum\limits_{n=1}^{\infty} f_{i,j}(n) \leq 1
$$
$f_{i,j}$ 即为**从状态 $i$ 出发「迟早」到达状态 $j$ 的概率**。

> [!def.] 常返性
> 对 Markov 链的状态空间 $E$ 中的状态 $i$，如果 $f_{i,i} = 1$，则称状态 $i$ 为**常返 (recurrent) 态**；否则，$f_{i,i} < 1$，称为**滑过 (transient) 态**或**非常返态**。
> 
> 从常返态 $i$ 出发，将**以概率 1** 返回到状态 $i$ 一次；而从非常返态 $i$ 出发，**有正的概率**永远不返回状态 $i$。

#### 常返性的判据

我们期望利用转移概率 $P_{i,j}{(n)}$ 来研究 $f_{i,j}(n)$，以判定状态 $i$ 的常返性。

类比于 [[#^ChapmanKolmogorovIdentity|C-K 方程]]的推导，我们可以将 $P_{i,j}(n)$ **按照首达时间 $\tau_{j}$ 分组**，有
$$
\begin{align}
P_{i,j}(n) &= P \left\{ X_{n} = j \mid X_{0} = i \right\} 
= \sum\limits_{k=1}^{n} P \left\{ X_{n} = j, \tau_{j} = k \mid X_{0} = i \right\} \\
&= \sum\limits_{k=1}^{n} P \left\{ X_{n} = j \mid \tau_{j} = k, X_{0} = i \right\} \cdot P \left\{ \tau_{j} = k \mid X_{0} = i \right\} \\
&= \sum\limits_{k=1}^{n} P \left\{ X_{n} = j \mid X_{k} = j \right\} \cdot P \left\{ \tau_{j} = k \mid X_{0} = i \right\} \\
&= \sum\limits_{k=1}^{n} P_{j,j}(n-k) f_{i,j}(k)
\end{align}
$$
即
$$
\mark{ P_{i,j}{(n)} = \sum\limits_{k=1}^{n} P_{j,j}{(n-k)} f_{i,j}(k) }
$$

上式表现出**离散时间索引的卷积**形式，因此可做 **$z$ 变换**，定义其**生成函数**为
$$
\t{P}_{i,j} (z) = \sum\limits_{n=0}^{\infty} P_{i,j}{(n)} z^{n} = \delta_{i,j} + \sum\limits_{n=1}^{\infty} P_{i,j}{(n)} z^{n}, \qquad
F_{i,j} (z) = \sum\limits_{n=1}^{\infty} f_{i,j}(n) z^{n}
$$
则有
$$
\begin{align} 
\t{P}_{i,j} (z) &= \delta_{i,j} + \sum\limits_{n=1}^{\infty} \sum\limits_{k=1}^{n} P_{j,j}{(n-k)} f_{i,j}(k) \cdot  z^{n}  \\
&= \delta_{i,j} + \sum\limits_{k=1}^{\infty} \sum\limits_{n=k}^{\infty} (f_{i,j}(k) z^{k}) (P_{j,j}{(n-k)} z^{n-k}) \\
&= \delta_{i,j} + \left( \sum\limits_{k=1}^{\infty} f_{i,j}(k) z^{k} \right) \left( \sum\limits_{m=0}^{\infty} P_{j,j}{(m)} z^{m} \right) 
= \delta_{i,j} + F_{i,j} (z) \t{P}_{j,j} (z)
\end{align}
$$
即
$$
\mark{ \t{P}_{i,j} (z) = \delta_{i,j} + F_{i,j} (z) \t{P}_{j,j} (z) }
$$

> [!note] Markov 链的分解
> Markov 链有两种**分解**方案：
> + 在**空间**上分解，按照先走 $m$ 步时的中间状态 $k$ 分组，得到
> $$
> P_{i,j}{(n)} = \sum\limits_{k} P_{i,k}{(m)} P_{k,j}{(n - m)}
> \quad\text{OR}\quad
> \boldsymbol{P}{(m + n)} = \boldsymbol{P}{(m)} \boldsymbol{P}{(n)}
> $$
> 即 [[#^ChapmanKolmogorovIdentity|C-K 方程]]；
> + 在**时间**上分解，按照首达时间分组，得到上式
> $$
> P_{i,j}{(n)} = \sum\limits_{k=1}^{n} P_{j,j}{(n-k)} f_{i,j}(k)
> \quad\text{OR}\quad
> \t{P}_{i,j} (z) = \delta_{i,j} + F_{i,j} (z) \t{P}_{j,j} (z)
> $$
^MarkovFenjie

从而，令 $i = j$ 并令 $z \to 1_{-}$，得
$$
\sum\limits_{n=0}^{\infty} P_{i,i}{(n)} = \t{P}_{i,i} (1_{-}) = \dfrac{1}{1 - \sum\limits_{n=1}^{\infty} f_{i,i}(n)} = \dfrac{1}{1 - f_{i,i}}
$$
$f_{i,i}$ 是否为 1 取决于左侧级数 $\sum\limits_{n=0}^{\infty} P_{i,i}{(n)}$ 的敛散性，由此给出常返性的第一判据。

> [!theorem] 常返性判据
> 状态 $i$ 为常返态的**充分必要条件**为级数 $\sum\limits_{n=0}^{\infty} P_{i,i}{(n)}$ 发散。
^RecurrentCriterionI

当 $i \neq j$ 时，令 $z \to 1_{-}$ 则得到
$$
\sum\limits_{n=0}^{\infty} P_{i,j}{(n)} = \t{P}_{i,j} (1_{-}) = F_{i,j} (1_{-}) \t{P}_{j,j} (1_{-}) = f_{i,j} \sum\limits_{n=0}^{\infty} P_{j,j}{(n)}
$$
若 $j$ **不是常返态**，则由[[#^RecurrentCriterionI|判据]]有 $\sum\limits_{n=0}^{\infty} P_{j,j}(n) < \infty$，且由 $f_{i,j} \le 1$ 亦知 $\sum\limits_{n=0}^{\infty} P_{i,j}(n) < \infty$，则二者的通项
$$
P_{j,j}(n) \xrightarrow{n \to \infty} 0, \qquad P_{i,j}(n) \xrightarrow{n \to \infty} 0
$$
^NonRecurrentLimit

这也是我们主要研究常返态的原因。

#### 态的返回次数

对常返态 $i$，定义其**返回次数** $N_{i} = \# \left\{ n \mid X_{n} = i, X_{0} = i \right\}$，则 $N_{i}$ 的**期望**为
$$
\mathbb{E} \left[ N_{i} \right] = \mathbb{E} \left[ \sum\limits_{n=0}^{\infty} \mathbb{1}_{\left\{ X_n = i \mid X_{0} = i \right\}} \right] = \sum\limits_{n=0}^{\infty} \mathbb{E} \left[ \mathbb{1}_{\left\{ X_n = i \mid X_{0} = i \right\}} \right] = \sum\limits_{n=0}^{\infty} P_{i,i}{(n)} = \infty 
$$

记从 $i$ 到达 $j$ 至少 $n$ 次的概率为
$$
g_{i,j}(n) = P \left\{ \#\left\{ k \mid X_{k} = j \right\} \geq n \mid X_{0} = i \right\}
$$
利用 Markov 链的[[#^MarkovFenjie|时间分解]]，可知
$$
\begin{align}
g_{i,j}(n) &= \sum\limits_{m=1}^{\infty} P \left\{ \tau_{j} = m, \#\left\{ k > m \mid X_{k} = j \right\} \geq n - 1 \mid X_{0} = i \right\} \\
&= \sum\limits_{m=1}^{\infty} P \left\{ \tau_{j} = m \mid X_{0} = i \right\} \cdot P \left\{ \#\left\{ k > m \mid X_{k} = j \right\} \geq n - 1 \mid X_{m} = j \right\} \\
&= \sum\limits_{m=1}^{\infty} P \left\{ \tau_{j} = m \mid X_{0} = i \right\} \cdot P \left\{ \#\left\{ k \mid X_{k} = j \right\} \geq n - 1 \mid X_{0} = j \right\} \\
&= \sum\limits_{m=1}^{\infty} f_{i,j}(m) \cdot g_{j,j}(n - 1) = f_{i,j} \cdot g_{j,j}(n - 1)
\end{align}
$$
令 $i = j$，则有**递推关系**
$$
g_{i,i}(n) = f_{i,i} \cdot g_{i,i}(n - 1)
$$
由 $g_{i,i}(0) = 1$ 可得
$$
P \left\{ N_{i} = n \right\} = g_{i,i}(n) = (f_{i,i})^{n} \xrightarrow{n \to \infty} \begin{cases}
1, & \text{if } f_{i,i} = 1, \\
0, & \text{if } f_{i,i} < 1
\end{cases}
$$
因此，**常返态几乎必然无限次返回，而非常返态则几乎必然有限次返回**。

#### 常返性与连通性

下面考虑 **$i \leftrightarrow j$**，即 **$i$、$j$ 相通**的情况。由 $i \to j$，可知 $\exists m$ 使得 $P_{i,j}{(m)} > 0$；由 $j \to i$，可知 $\exists n$ 使得 $P_{j,i}{(n)} > 0$。因此，对于任意 $k$，都有
$$
P_{i,i}{(m + n + k)} \geq P_{i,j}{(m)} P_{j,j}{(k)} P_{j,i}{(n)}
$$
即
$$
\sum\limits_{k=0}^{\infty} P_{i,i}{(m + n + k)} \geq P_{i,j}{(m)} P_{j,i}{(n)} \sum\limits_{k=0}^{\infty} P_{j,j}{(k)}
$$
若 **$j$ 为常返态**，则由[[#^RecurrentCriterionI|判据]]知右侧发散，因此左侧亦发散，从而 $\sum\limits_{k=0}^{\infty} P_{i,i}{(k)}$ 发散，由[[#^RecurrentCriterionI|判据]]知 **$i$ 亦为常返态**，故

> [!theorem] 连通状态的常返性
> Markov 链中连通状态的**常返性相同**。

对**有限状态 Markov 链**，倘若所有状态都非常返态，则取定 $\forall i \in E$ 都有 
$$
\forall j \in E, \quad P_{i,j}{(n)} \xrightarrow{n \to \infty} 0
\quad\Longrightarrow\quad
\sum\limits_{j \in E} P_{i,j}{(n)} \xrightarrow{n \to \infty} 0
$$
但由概率归一性知 $\sum\limits_{j \in E} P_{i,j}{(n)} = 1$，与上式矛盾，因此**有限状态 Markov 链中至少存在一个常返态**。进而，**有限[[#^Bukeyue|不可约]] Markov 链中所有状态均为常返态**。

进一步考察任意 Markov 链（也只剩无限状态的情况了），设其存在一个**常返态 $i$**，则知 $g_{i,i}(\infty) = 1$。对此概率表示的「返回无穷次」的路径加以[[#^MarkovFenjie|空间分解]]，有
$$
\begin{align}
1 = g_{i,i}(\infty) &= \sum\limits_{k \in E} P_{i,k}(m) \cdot P \left\{ \#\left\{ n > m \mid X_{n} = i \right\} = \infty \mid X_{m} = k \right\} \\
&= \sum\limits_{k \in E} P_{i,k}(m) \cdot g_{k,i}(\infty), \qquad \forall m > 0
\end{align}
$$
而知 $\sum\limits_{k \in E} P_{i,k}(m) = 1$，因此 $\sum\limits_{k \in E} P_{i,k}(m) \cdot (1 - g_{k,i}(\infty)) = 0$，这一求和中每一项均非负，故必有
$$
\forall m > 0, \quad \forall k \in E, \quad P_{i,k}(m) \cdot (1 - g_{k,i}(\infty)) = 0
$$
对于 $i$ 的某一可达状态 $j$，由 $i \to j$ 可知 $\exists m$ 使得 $P_{i,j}(m) > 0$，因此 $g_{j,i}(\infty) = 1$，即 **$j \to i$**，从而 **$i \leftrightarrow j$** 且 **$j$ 亦为常返态**。

> [!theorem] 可达状态的常返性
> 若 Markov 链中存在常返态 $i$，则 $i$ 的**所有可达状态**均与 $i$ **相通**，且均为常返态。

## 转移概率的极限行为

### Markov 链的周期性

> [!def.] 周期态
> 对状态 $i$，定义其**周期 (period)** 为
> $$
> d_{i} = \gcd \left\{ n \geq 1 \mid P_{i,i}{(n)} > 0 \right\}
> $$
> 其中 $\gcd$ 表示**最大公约数 (greatest common divisor)**。
> 
> 如果 $d_{i} = 1$，则称状态 $i$ 为**非周期 (aperiodic) 态**；否则，$d_{i} \geq 2$，称为**周期 (periodic) 态**。

**非周期**带来的一个直观性质是
$$
\exists N, \quad \forall n \geq N, \quad P_{i,i}{(n)} > 0
$$

考虑两个相通状态 $i$、$j$，即设 $\exists m$ 使得 $P_{i,j}{(m)} > 0$，同时 $\exists n$ 使得 $P_{j,i}{(n)} > 0$，因此
+ $P_{i,i}(m + n) \ge P_{i,j}(m) P_{j,i}(n) > 0$，故 **$d_{i} \mid (m + n)$**；
+ $\forall k \in \left\{ n \geq 1 \mid P_{j,j}{(n)} > 0 \right\}$，有 $P_{i,i}(m + k + n) \ge P_{i,j}(m) P_{j,j}(k) P_{j,i}(n) > 0$，故 **$d_{i} \mid (m + k + n)$**。

由此，**$\forall k \in \left\{ n \geq 1 \mid P_{j,j}{(n)} > 0 \right\}$，$d_{i} \mid k$**，即 $d_{i}$ 是该集合的一个公约数，故 **$d_{i} \mid d_{j}$**。同理可得 $d_{j} \mid d_{i}$，因此 **$d_{i} = d_{j}$**，即**相通状态的周期性相同**。

这样，在[[#^Bukeyue|不可约 Markov 链]]中，所有状态的周期性均相同。若其中有一个状态为非周期态，则所有状态均为非周期态，称该 Markov 链为**非周期的**，并有
$$
\exists N, \quad \forall n \geq N, \quad \forall i,j \in E, \quad P_{i,j}{(n)} > 0
$$

#### 遍历性

在**非周期**的[[#^Bukeyue|不可约 Markov 链]]中，直接有
$$
\lim_{n \to \infty} P_{i,j}{(n)} = \pi_{j}
$$
称为**遍历性 (ergodicity) 定理**，其中 $\pi_{j}$ 与初始状态 $i$ 无关。

若没有非周期的条件，而是在任意[[#^Bukeyue|不可约 Markov 链]]中任取两个状态 $i$、$j$，有
$$
\lim\limits_{ n \to \infty } \dfrac{1}{n} \sum\limits_{k=1}^{n} P_{i,j}{(k)} = \dfrac{1}{a_{j}}
$$
称为**弱遍历性 (weak ergodicity) 定理**，其中 $a_{j} = \sum\limits_{k=1}^{\infty} f_{i,i}(k)\cdot k$ 为状态 $j$ 的**平均返回时间 (mean return time)**，与初始状态 $i$ 无关。由级数知识知，若存在 $\lim\limits_{n \to \infty} P_{i,j}{(n)} = \pi_{j}$，则 $\cfrac{1}{a_{j}} = \lim\limits_{ n \to \infty } \dfrac{1}{n} \sum\limits_{k=1}^{n} P_{i,j}{(k)} = \pi_{j}$。

另外，此处 $\cfrac{1}{n} \sum\limits_{k=1}^{n} P_{i,j}{(k)}$ 可写成
$$
\begin{align} 
\dfrac{1}{n} \sum\limits_{k=1}^{n} P_{i,j}{(k)} &= \dfrac{1}{n} \sum\limits_{k=1}^{n} \mathbb{E} \left[ \mathbb{1}_{\left\{ X_{k} = j \mid X_{0} = i \right\}} \right] 
= \dfrac{1}{n} \mathbb{E} \left[ \sum\limits_{k=1}^{n} \mathbb{1}_{\left\{ X_{k} = j \mid X_{0} = i \right\}} \right] \\
&= \dfrac{\mathbb{E} \left[ \#\left\{ k \mid X_{k} = j, X_{0} = i, 1\le k \le n \right\} \right] }{n} 
\end{align}
$$
其概率意义是在 $n$ 步转移中**到达状态 $j$ 的平均频率**，即 $n$ 步转移中**状态 $j$ 的平均比例**。

#### 正常返、零常返

考虑上述「平均到达频率」的极限 $\lim\limits_{ n \to \infty } \cfrac{1}{n} \sum\limits_{k=1}^{n} P_{i,j}{(k)}$，其与初始状态无关，因此也可称为「平均返回频率」。由[[#^NonRecurrentLimit|非常返态的性质]]知，若状态 $j$ 为非常返态，则 $P_{i,j}{(n)} \xrightarrow{n \to \infty} 0$，从而 $\lim\limits_{ n \to \infty } \cfrac{1}{n} \sum\limits_{k=1}^{n} P_{i,j}{(k)} = 0$，即**平均返回频率为 0**。

但对于常返态，并不一定有正的平均频率，定义：
+ 若状态 $j$ 的**平均返回时间有限**，即 $a_{j} < \infty$，则 $\lim\limits_{ n \to \infty } \cfrac{1}{n} \sum\limits_{k=1}^{n} P_{i,j}{(k)} = \cfrac{1}{a_{j}} > 0$，称状态 $j$ 为**正常返 (positive recurrent) 态**；
+ 若状态 $j$ 的**平均返回时间无限**，即 $a_{j} = \infty$，则 $\lim\limits_{ n \to \infty } \cfrac{1}{n} \sum\limits_{k=1}^{n} P_{i,j}{(k)} = 0$，称状态 $j$ 为**零常返 (null recurrent) 态**。

> [!example] 零常返的实例
> 考虑[[例题#L19-1]] 的**一维无限制随机游走**，已知当 $p=\cfrac{1}{2}$ 时状态 0（以及其他所有状态）为常返态，但有
> $$
> P(z) = \sum\limits_{n=0}^{\infty} P_{0,0}{(2n)} z^{2n} = \sum\limits_{n=0}^{\infty} \binom{2n}{n} \left( \dfrac{1}{2} \right)^{2n} z^{2n} = \dfrac{1}{\sqrt{1 - z^{2}}}
> $$
> 于是
> $$
> \lim\limits_{ n \to \infty } \dfrac{1}{n} \sum\limits_{k=1}^{n} P_{0,0}{(k)} = \lim\limits_{ z \to 1_{-} } (1 - z) P(z) = \lim\limits_{ z \to 1_{-} } \dfrac{1 - z}{\sqrt{1 - z^{2}}} = 0
> $$
> 因此，**常返态中亦可存在平均返回频率为 0 的情况**。



### 平稳分布

由 [[#^ChapmanKolmogorovIdentity|C-K 方程]]，$\boldsymbol{P}(n)$ 有分解
$$
\boldsymbol{P}(n) = \boldsymbol{P}(n-1) \boldsymbol{P}(1) = \boldsymbol{P}(1) \boldsymbol{P}(n-1)
$$
因此，若**极限 $\lim\limits_{n \to \infty} \boldsymbol{P}(n) = \boldsymbol{\varPi}$ 存在**，则有
$$
\boldsymbol{\varPi} = \boldsymbol{\varPi} \boldsymbol{P},
\qquad\text{and}\qquad
\boldsymbol{\varPi} = \boldsymbol{P} \boldsymbol{\varPi}
$$
其中，
+ $\boldsymbol{\varPi} = \lim\limits_{n \to \infty} \boldsymbol{P}(n)$ 显然应**与初状态无关**，即形如
$$
\boldsymbol{\varPi} = \begin{pmatrix}\pi_{1} & \pi_{2} & \pi_{3} & \cdots \\ \pi_{1} & \pi_{2} & \pi_{3} & \cdots \\ \vdots & \vdots & \vdots & \vdots \\ \pi_{1} & \pi_{2} & \pi_{3} & \cdots \end{pmatrix} = \v{1}^{\mathrm{T}} \begin{pmatrix}\pi_{1} & \pi_{2} & \pi_{3} & \cdots \end{pmatrix} = \v{1}^{\mathrm{T}} \v{\pi}
$$
+ 1 步转移概率矩阵 $\boldsymbol{P} = \boldsymbol{P}(1) = \Big( P_{i,j}{(1)} \Big)_{i,j}$ 的各行表示从各状态出发的概率分布，因此**各行和均为 1**，即 $\boldsymbol{P} \v{1}^{\mathrm{T}} = \v{1}^{\mathrm{T}}$。

由此 $\boldsymbol{\varPi} \equiv \boldsymbol{P} \boldsymbol{\varPi}$ 成为恒等式，而 $\boldsymbol{\varPi} = \boldsymbol{\varPi} \boldsymbol{P}$ 则可展开为
$$
\mark{ \v{\pi} = \v{\pi} \boldsymbol{P} }
$$
注意此处的 $\v{\pi}$ 是行向量。

首先确认 $\v{\pi}$ 非零解的存在性。对（更熟悉的列向量形式的）方程 $(\boldsymbol{P}^{\mathrm{T}} - \boldsymbol{I}) \v{\pi}^{\mathrm{T}} = \v{0}^{\mathrm{T}}$，考虑 $\boldsymbol{P}$ 的特征方程
$$
\det (\boldsymbol{P}^{\mathrm{T}} - \lambda \boldsymbol{I}) = \det (\boldsymbol{P} - \lambda \boldsymbol{I}) = 0
$$
由概率矩阵的性质知 $\boldsymbol{P} \v{1}^{\mathrm{T}} = \v{1}^{\mathrm{T}}$，即 $\lambda = 1$ 是其特征值，$\det (\boldsymbol{P}^{\mathrm{T}} - \boldsymbol{I}) = 0$，从而**齐次线性方程组有非零解**。

进一步，向量中各元素 $\pi_{j} = \sum\limits_{i} \pi_{i} P_{i,j}(1)$。当**初始分布 $P(X_{0} = i)$ 即为 $\pi_{i}$** 时，有
$$
P(X_{1} = j) = \sum\limits_{i} P(X_{0} = i) P_{i,j}(1) = \sum\limits_{i} \pi_{i} P_{i,j}(1) = \pi_{j}
$$
即**经过一步转移后分布不变**，这是称 $\v{\pi}$ 为 Markov 链的**平稳分布 (stationary distribution)** 的原因。

## † 连续时间 Markov 链

设有随机过程 $X(t)$，其状态空间记为 $E = \{1, 2, \cdots \}$，其 **Markov 性**定义为
$$
\begin{align} 
\forall t_{1} \le t_{2} \le \cdots \le t_{n}, \quad &P \left\{ X(t_{n}) = x_{n} \mid X(t_{n-1}) = x_{n-1}, \cdots, X(t_{1}) = x_{1} \right\}  \\
&= P \left\{ X(t_{n}) = x_{n} \mid X(t_{n-1}) = x_{n-1} \right\} 
\end{align}
$$
满足上述性质的随机过程称为**连续时间 Markov 链 (continuous-time Markov chain, CTMC)**。

### 转移概率与生成元矩阵

连续时间 Markov 链的**转移概率**定义为
$$
P_{i,j}(t) = P \left\{ X(t + s) = j \mid X(s) = i \right\}, \quad \forall s, t \geq 0
$$
由于状态离散，与离散时间 Markov 链类似可定义 $\boldsymbol{P}(t) = \big( P_{i,j}(t) \big)_{i,j}$，且同样有 **Chapman-Kolmogorov 方程**
$$
\boldsymbol{P}(t + s) = \boldsymbol{P}(t) \boldsymbol{P}(s)
$$

不同于离散时间 Markov 链，连续时间 Markov 链没有「1 步转移」的概念，其转移概率矩阵 $\boldsymbol{P}(t)$ 随时间 $t$ **连续变化**。因此，我们考察
$$
\begin{align} 
\lim\limits_{\Delta t \to 0} \dfrac{\boldsymbol{P}(t + \Delta t) - \boldsymbol{P}(t)}{\Delta t} 
&= \lim\limits_{\Delta t \to 0} \dfrac{\boldsymbol{P}(t) \boldsymbol{P}(\Delta t) - \boldsymbol{P}(t)}{\Delta t}
= \boldsymbol{P}(t) \cdot \lim\limits_{\Delta t \to 0} \dfrac{\boldsymbol{P}(\Delta t) - \boldsymbol{I}}{\Delta t} \\
&= \lim\limits_{\Delta t \to 0} \dfrac{\boldsymbol{P}(\Delta t) \boldsymbol{P}(t) - \boldsymbol{P}(t)}{\Delta t}
= \lim\limits_{\Delta t \to 0} \dfrac{\boldsymbol{P}(\Delta t) - \boldsymbol{I}}{\Delta t} \cdot \boldsymbol{P}(t) 
\end{align}
$$
定义**生成元矩阵 (generator matrix)** 为
$$
\boldsymbol{Q} = \lim\limits_{\Delta t \to 0} \dfrac{\boldsymbol{P}(\Delta t) - \boldsymbol{I}}{\Delta t}
$$
则有 **Kolmogorov 前向方程与后向方程**
$$
\begin{cases}
\cfrac{\dif}{\dif t} \boldsymbol{P}(t) = \boldsymbol{P}(t) \boldsymbol{Q}  & \text{（前向方程）} \\
\cfrac{\dif}{\dif t} \boldsymbol{P}(t) = \boldsymbol{Q} \boldsymbol{P}(t)  & \text{（后向方程）}
\end{cases} 
$$
于是，$\boldsymbol{P}(t)$ 的演化由 $\boldsymbol{Q}$ 决定，有
$$
\boldsymbol{P}(t) = \boldsymbol{P}(0) \e^{\boldsymbol{Q} t} = \boldsymbol{P}(0) \sum\limits_{n=0}^{\infty} \dfrac{(\boldsymbol{Q} t)^{n}}{n!} = \boldsymbol{P}(0) \sum\limits_{n=0}^{\infty} \dfrac{t^{n}}{n!} \boldsymbol{Q}^{n} 
$$

$\boldsymbol{Q}$ 有以下性质：
+ 其**非对角元非负**，即 $Q_{i,j} \geq 0, \forall i \neq j$，表示单位时间内从状态 $i$ 转移到状态 $j$ 的速率；
+ 其**对角元为负**，保证**行和为 0**，即 $Q_{i,i} = - \sum\limits_{j \neq i} Q_{i,j} \leq 0$，表示单位时间内**离开状态 $i$** 的速率。

> [!example] Poisson 过程的生成元矩阵 
> [[#Poisson 过程]]即是一个典型的连续时间 Markov 链，由[[#Poisson 过程#^XishuxingJiashe|稀疏性假设]]，其在 $\Delta t \to 0$ 间隔内的转移概率为
> $$
> P_{i,j}(\Delta t) = \begin{cases}
> \e^{-\lambda \Delta t} , & j = i, \\
> \lambda \Delta t \cdot \e^{-\lambda \Delta t} , & j = i + 1, \\
> 0 , & \text{otherwise}
> \end{cases}
> $$
> 因此，其生成元矩阵的矩阵元为
> $$
> Q_{i,j} = \lim\limits_{\Delta t \to 0} \dfrac{P_{i,j}(\Delta t) - \delta_{i,j}}{\Delta t} = \begin{cases}
> -\lambda , & j = i, \\
> \lambda , & j = i + 1, \\
> 0 , & \text{otherwise}
> \end{cases}
> $$
> 即生成元矩阵为
> $$
> \boldsymbol{Q} = \begin{pmatrix}
> -\lambda & \lambda \\
> & -\lambda & \lambda \\
> & & -\lambda & \lambda \\
> & & & \ddots & \ddots
> \end{pmatrix}
> $$

### 平稳分布

不同于离散时间 Markov 链，对连续时间 Markov 链，只要**不可约**，则 $P_{i,j}(t)$ 的极限 $\lim\limits_{t \to \infty} P_{i,j}(t) = \pi_{j}$ 总是存在，且与初始状态 $i$ 无关。因此，$\boldsymbol{P}(t)$ 的极限 $\lim\limits_{t \to \infty} \boldsymbol{P}(t) = \boldsymbol{\varPi}$ 亦存在，且形如
$$
\boldsymbol{\varPi} = \begin{pmatrix}
\pi_{1} & \pi_{2} & \pi_{3} & \cdots \\
\pi_{1} & \pi_{2} & \pi_{3} & \cdots \\
\vdots & \vdots & \vdots & \vdots \\
\pi_{1} & \pi_{2} & \pi_{3} & \cdots
\end{pmatrix} = \v{1}^{\mathrm{T}} \v{\pi}
$$
由 Kolmogorov 前向方程知
$$
\boldsymbol{O} = \lim\limits_{t \to \infty} \dfrac{\dif}{\dif t} \boldsymbol{P}(t) = \lim\limits_{t \to \infty} \boldsymbol{P}(t) \boldsymbol{Q} = \boldsymbol{\varPi} \boldsymbol{Q}
\quad \Longrightarrow \quad
\v{\pi} \boldsymbol{Q} = \v{0}
$$
同样需注意此处向量符号默认是**行向量**。

与离散时间 Markov 链类似，$\v{\pi}$ 是连续时间 Markov 链的**平稳分布**，当初始分布为 $\v{\pi}$ 时，经过任意时间 $t$ 的转移后分布仍为 $\v{\pi}$。
