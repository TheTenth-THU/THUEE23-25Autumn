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
\begin{align} 
G_{X(t)}(z) &= \e^{(-\lambda + \lambda z) t} = \e^{-\lambda t} \cdot \e^{\lambda t z} = \e^{-\lambda t}  \sum\limits_{k=0}^{\infty} \dfrac{(\lambda t)^{k}}{k!}  z^{k}
\end{align}
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
\mathbb{E}[N(t)] = \lambda t, \qquad \mathrm{Var}(N(t)) = \lambda t
$$
Poisson 过程的相关函数为
$$
R_{N}(t_{1}, t_{2}) = \mathbb{E}[N(t_{1}) N(t_{2})] = \lambda \min(t_{1}, t_{2}) + \lambda^{2} t_{1} t_{2}
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
即 Poisson 过程的条件期望是时间线性的。

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

### 事件间隔与等待时间

#### 事件间隔分布

由增量独立性和增量平稳性，我们只需研究从初态开始到第一个事件的间隔 $T_{1}$ 的分布，其定义为
$$
F_{T_{1}}(t) = P\{T_{1} \le t\} = P \left\{ N(t) \ge 1 \right\} = 1 - P \left\{ N(t) = 0 \right\} = 1 - \e^{-\lambda t}
$$
因此
$$
f_{T_{1}}(t) = \dfrac{\dif}{\dif t} F_{T_{1}}(t) = \lambda \e^{-\lambda t}, \qquad t \ge 0
$$
于是事件间隔均服从参数为 $\lambda$ 的**指数分布**，即 $\left\{ T_{k} \right\} \stackrel{\text{i.i.d}}{\sim} \text{Exp}(\lambda)$。

#### 等待时间分布

设第 $n$ 个事件发生的时间为 $S_{n} = \sum\limits_{k=1}^{n} T_{k}$。引入**特征函数 $\phi_{X}(\omega) = \mathbb{E}\left[ \e^{\J \omega X} \right]$**，则由事件间隔的独立性，有
$$
\begin{align} 
&\phi_{T_{k}}(\omega) = \int_{0}^{\infty} \lambda \e^{-\lambda t} \cdot \e^{\J \omega t} \dif t = \dfrac{\lambda}{\lambda - \J \omega}  \\
\Longrightarrow\quad & \phi_{S_{n}}(\omega) = \left( \phi_{T_{k}}(\omega) \right)^{n} = \left( \dfrac{\lambda}{\lambda - \J \omega} \right)^{n}
\end{align}
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
类似地，[[#Term 3]] 仍为 0，故得到**关于矩母函数的微分方程**
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

