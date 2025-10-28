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

尝试确定归一化系数 $k$，归一化条件要求
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

综上所述，多元 Gauss 分布的特征函数为
$$
\mark{ \phi_{\v{X}}(\v{\omega}) = \exp\left( \J \v{\mu}^{\mathrm{T}} \v{\omega} - \dfrac{1}{2} \v{\omega}^{\mathrm{T}} \boldsymbol{\varSigma} \v{\omega} \right) }
$$

### Gauss 过程的定义

> [!definition] Gauss 过程
> 设 $X(t)$ 是定义在概率空间 $(\Omega, \mathcal{F}, P)$ 上的随机过程。如果对于任意正整数 $n$ 和任意时刻 $t_{1}, t_{2}, \cdots, t_{n}$，随机变量组 $\v{X} = \begin{pmatrix}X(t_{1}) & X(t_{2}) & \cdots & X(t_{n})\end{pmatrix}^{\mathrm{T}}$ 都服从 $n$ 元 Gauss 分布 $N\left( \v{\mu},\boldsymbol{\varSigma} \right)$，则称 $X(t)$ 为 **Gauss 过程 (Gaussian process)**。

由定义，对


## Gauss 条件分布

### 多元 Gauss 分布各块间的条件分布

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

#### 条件概率密度的计算

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
&\hspace{1em} \mathop{}+\mathop{} \left( \v{y}^{\mathrm{T}} - \v{\mu}_{Y}^{\mathrm{T}} - \left( \v{x}^{\mathrm{T}} - \v{\mu}_{X}^{\mathrm{T}} \right) \boldsymbol{\varSigma}_{XX}^{-1} \boldsymbol{\varSigma}_{XY} \right) \left( \boldsymbol{\varSigma}_{YY} - \boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} \boldsymbol{\varSigma}_{XY} \right)^{-1} \\
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
> 其中
> $$
> \v{\mu}_{Y\mid X} = \v{\mu}_{Y} + \boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} \left( \v{x} - \v{\mu}_{X} \right), \qquad
> \boldsymbol{\varSigma}_{Y\mid X} = \boldsymbol{\varSigma}_{YY} - \boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} \boldsymbol{\varSigma}_{XY}
> $$

#### 条件分布的几何直观

观察条件均值 $\v{\mu}_{Y\mid X}$ 的表达式
$$
\v{\mu}_{Y\mid X} = \v{\mu}_{Y} + \boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1} \left( \v{x} - \v{\mu}_{X} \right)
$$
其可视为**对无条件均值 $\v{\mu}_{Y}$ 的修正**，且
+ 修正量与 $\v{X}$ 偏离其均值 $\v{\mu}_{X}$ 的程度 $\left( \v{x} - \v{\mu}_{X} \right)$，即 $\v{X}$ 中的**随机成分**成正比；
+ 修正量与上述随机成分的**比例系数**为 $\boldsymbol{\varSigma}_{YX} \boldsymbol{\varSigma}_{XX}^{-1}$，其中 $\boldsymbol{\varSigma}_{XX}^{-1}$ 起到「标准化」的作用，而 $\boldsymbol{\varSigma}_{YX}$ 则反映了 $\v{X}$ 和 $\v{Y}$ 之间的**相关性**。

因此，$\v{Y}$ 相对于 $\v{X}$ 的条件分布可看做**依据 $\v{X}$ 的随机成分在 $\v{Y}$ 上的投影 (projection)** 对 $\v{Y}$ 的分布进行调整后的结果。
