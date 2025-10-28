## Schrödinger 方程的引入

### 波动参量的物理意义

根据波函数的表示 $\varPsi(\v{r},t) = A \e^{-\I (E t - \v{p} \cdot \v{r}) / \hbar}$，可以得到以下两个重要的关系：
+ 对时间 $t$ 求偏导，得到 $\dfrac{\partial\varPsi}{\partial t} = -\I \dfrac{E}{\hbar} A \e^{-\I (E t - \v{p} \cdot \v{r}) / \hbar}$，即
$$
\I \hbar \dfrac{\partial\varPsi}{\partial t} = E \varPsi
$$
$E\varPsi$ 表征了波函数的**时间变化率**，能量 $E$ 对应着波函数的时间变化性质。
+ 对空间坐标 $\v{r}$ 求梯度，得到 $\nabla \varPsi = \I \dfrac{\v{p}}{\hbar} A \e^{-\I (E t - \v{p} \cdot \v{r}) / \hbar}$，即
$$
-\I \hbar \nabla \varPsi = \v{p} \varPsi
$$
$\v{p}\varPsi$ 表征了波函数的**空间变化率**，动量 $\v{p}$ 对应着波函数的空间变化性质。

### 单粒子 Schrödinger 方程的建立

由上，引入**动量算符**
$$
\hat{\v{p}} = -\I \hbar \nabla
$$
和**能量算符**
$$
\hat{E} = \I \hbar \dfrac{\partial}{\partial t}
$$
则动量 $\v{p}$、能量 $E$ 在波函数上的作用分别于上面两个算符相当。

对**自由粒子**，能量和动量之间的关系为 $E = \dfrac{p^{2}}{2m}$，因此
$$
\I \hbar \dfrac{\partial\varPsi}{\partial t} = \hat{E} \varPsi = \dfrac{\hat{\v{p}}^{2}}{2m} \varPsi = -\dfrac{\hbar^{2}}{2m} \nabla^{2} \varPsi
$$
若粒子处在**势场 $V(\v{r})$** 中，则能量和动量的关系为 $E = \dfrac{p^{2}}{2m} + V$，因此
$$
\I \hbar \dfrac{\partial\varPsi}{\partial t} = \hat{E} \varPsi = \left( \dfrac{\hat{\v{p}}^{2}}{2m} + V \right) \varPsi = -\dfrac{\hbar^{2}}{2m} \nabla^{2} \varPsi + V(\v{r}) \varPsi
$$

> [!theorem] Schrödinger 方程
> 外势场 $V(\v{r})$ 中粒子的波函数 $\varPsi(\v{r},t)$ 满足
> $$
> \I \hbar \dfrac{\partial\varPsi}{\partial t} = -\dfrac{\hbar^{2}}{2m} \nabla^{2} \varPsi + V(\v{r}) \varPsi
> $$
> 这个方程称为 **Schrödinger 波动方程**，简称 **Schrödinger 方程**。

^f53f7b

Schrödinger 方程是量子力学的基本方程，描述了粒子波函数的时空演化规律。通过解 Schrödinger 方程，可以得到粒子的波函数，从而预测粒子的行为和性质。

### 概率守恒定律

定义**概率密度**为
$$
w(\v{r},t) = |\varPsi(\v{r},t)|^{2} = \varPsi^{*}(\v{r},t) \varPsi(\v{r},t)
$$
概率密度的变化率为
$$
\begin{align}
\dfrac{\partial w}{\partial t} &= \varPsi^{*} \dfrac{\partial \varPsi}{\partial t} + \varPsi \dfrac{\partial \varPsi^{*}}{\partial t} \\
&= \varPsi^{*} \left( \dfrac{1}{\I \hbar} \left( -\dfrac{\hbar^{2}}{2m} \nabla^{2} \varPsi + V \varPsi \right) \right) + \varPsi \left( -\dfrac{1}{\I \hbar} \left( -\dfrac{\hbar^{2}}{2m} \nabla^{2} \varPsi^{*} + V \varPsi^{*} \right) \right) \\
&= \dfrac{\I \hbar}{2m} \left( \varPsi^{*} \nabla^{2} \varPsi - \varPsi \nabla^{2} \varPsi^{*} \right) \\
&= \dfrac{\I \hbar}{2m} \left( \varPsi^{*} \nabla^{2} \varPsi + \nabla \varPsi^{*} \cdot \nabla \varPsi - \nabla \varPsi^{*} \cdot \nabla \varPsi - \varPsi \nabla^{2} \varPsi^{*} \right)  \\
&= \dfrac{\I \hbar}{2m} \nabla \cdot \left( \varPsi^{*} \nabla \varPsi - \varPsi \nabla \varPsi^{*} \right)
\end{align}
$$
类比电荷的连续性方程 $\dfrac{ \partial q }{ \partial t } + \nabla \cdot \v{J} = 0$，引入**概率流密度 (probability current density)** 定义为
$$
\v{J} = -\dfrac{\I \hbar}{2m} \left( \varPsi^{*} \nabla \varPsi - \varPsi \nabla \varPsi^{*} \right)
= \mathfrak{Re} \left\{ \varPsi^{*} \dfrac{\hat{\v{p}}}{m} \varPsi \right\}
= \mathfrak{Re} \left\{ \varPsi^{*} \hat{\v{v}} \varPsi \right\}
$$
其中 $\hat{\v{p}} = -\I \hbar \nabla$ 为动量算符，$\hat{\v{v}} = \dfrac{\hat{\v{p}}}{m} = -\dfrac{\I \hbar}{m} \nabla$ 为速度算符。

> [!theorem] 概率守恒定律（微分形式）
> 概率密度 $w(\v{r},t)$ 和概率流密度 $\v{J}(\v{r},t)$ 满足**连续性方程**
> $$
> \dfrac{\partial w}{\partial t} + \nabla \cdot \v{J} = 0
> $$

对任意体积 $V$ 积分，得到
$$
\dfrac{\dif}{\dif t}W_{V} = \dfrac{\dif}{\dif t} \dint_{V} w \dif \tau 
= - \dint_{V} \nabla \cdot \v{J} \dif \tau 
= - \oint_{S} \v{J} \cdot \dif \v{S}
$$
其中 $W_{V} = \dint_{V} w \dif \tau$ 为体积 $V$ 内粒子出现的概率，$S$ 为体积 $V$ 的边界面。

> [!theorem] 概率守恒定律（积分形式）
> 体积 $V$ 内粒子出现的概率 $W_{V}$ 和概率流密度 $\v{J}(\v{r},t)$ 满足
> $$
> \dfrac{\dif}{\dif t}W_{V} = - \oint_{S} \v{J} \cdot \dif \v{S}
> $$
> 其中 $S$ 为体积 $V$ 的边界面。

这里所论及的「概率」是由 Born 对波函数引入的概率诠释，而其守恒性质完全由 Schrödinger 方程的数学形式所决定，与经典世界中的概率守恒并无直接联系，这恰恰证明 **Schrödinger 方程与 Born 的概率诠释是相容的**。

特别地，对整个空间积分，由于真实波函数在无穷远处趋于零，概率流密度 $\v{J}$ 也趋于零，因此
$$
\dfrac{\dif}{\dif t}W_{\infty} = - \oint_{\infty} \v{J} \cdot \dif \v{S} = 0
$$
即**全空间总概率守恒**，这也说明**波函数归一化条件在时间上保持不变**。[^1]

[^1]: 光子是极端相对论粒子，波函数的含义与 Schrödinger 波函数不同，不能直接套用这一结论。

> [!example] 平面波的概率流密度
> 对于自由粒子的平面波 $\varPsi(\v{r},t) = A \e^{\I (\v{k} \cdot \v{r} - \omega t)}$，其概率流密度为
> $$
> \begin{align}
> \v{J} &= -\dfrac{\I \hbar}{2m} \left( \varPsi^{*} \nabla \varPsi - \varPsi \nabla \varPsi^{*} \right) \\
> &= -\dfrac{\I \hbar}{2m} \left( A \e^{-\I \left( \v{k} \cdot \v{r} - \omega t \right)} \I \v{k} A \e^{\I \left( \v{k} \cdot \v{r} - \omega t \right)} - A \e^{\I \left( \v{k} \cdot \v{r} - \omega t \right)} \left( -\I \v{k} \right) A \e^{-\I \left( \v{k} \cdot \v{r} - \omega t \right)} \right) \\
> &= -\dfrac{\I \hbar}{2m} \cdot 2\I \v{k} |A|^{2} = \dfrac{\hbar \v{k}}{m} |A|^{2}
> \end{align}
> $$
> 而概率密度为 $w = |\varPsi|^{2} = |A|^{2}$，速度算符为 $\hat{\v{v}} = \dfrac{\hat{\v{p}}}{m} = \dfrac{\hbar \v{k}}{m}$，因此
> $$
> \v{J} = w \hat{\v{v}}
> $$

## Schrödinger 方程的求解

### 分离变量法解 Schrödinger 方程

一般地，Schrödinger 方程可写为
$$
\I \hbar \dfrac{\partial\varPsi}{\partial t} = \hat{H} \varPsi
$$
假设 $\hat{H}$ 不含 $t$（即 $V(\v{r})$ 暂不是时间的函数），则可以先求**分离变量形式**的所有特解。设单粒子 $\varPsi(\v{r},t) = f(t)\psi(\v{r})$，则代入得
$$
\I \hbar \dfrac{\dif f}{\dif t} \psi(\v{r}) = f(t) \hat{H} \psi(\v{r})
\quad\Longrightarrow\quad
\dfrac{\I \hbar}{f(t)} \dfrac{\dif f}{\dif t} = \dfrac{1}{\psi(\v{r})} \hat{H} \psi(\v{r})
$$
左侧只含 $t$，右侧只含 $\v{r}$，因此两侧均等于某个常数 $E$，即
$$
\begin{cases}
\dfrac{\dif f}{\dif t} = - \dfrac{\I}{\hbar} E f(t) & \text{（时间部分）} \\
\hat{H} \psi(\v{r}) = E \psi(\v{r}) & \text{（空间部分）} 
\end{cases}
$$
其中，
+ 时间部分可直接解出 $f(t) = \e^{- \I E t/\hbar}$，与 de Broglie 波函数的时间部分一致，可知常数 $E$ 即为**粒子的能量**；
+ 空间部分的方程显然是算符 $\hat{H} = -\dfrac{\hbar^{2}}{2m} \nabla^{2} + V(\v{r})$ 的**本征值方程**，由于能量具有确定值 $E$，其称为**定态 Schrödinger 方程**。

> [!definition] 定态 Schrödinger 方程
> **Hamiltonian 算符** $\hat{H} = -\dfrac{\hbar^{2}}{2m} \nabla^{2} + V(\v{r})$ 的本征值方程
> $$
> \hat{H} \psi(\v{r}) = E \psi(\v{r})
> $$
> 称为**定态 Schrödinger 方程**，其中 $E$ 为**本征值**，$\psi(\v{r})$ 为对应的**本征函数**。

完整的**定态波函数**即为
$$
\varPsi(\v{r},t) = \psi(\v{r}) \e^{-\I E t/\hbar}
$$
其**初态** $\varPsi(\v{r},0) = \psi(\v{r})$ 为定态 Schrödinger 方程的解，而完整的 $\varPsi(\v{r}, t)$ 即为 **Schrödinger 方程**的特解。一般地，定态 Schrödinger 方程有无穷多个本征值 $E_{n}$ 和对应的本征函数 $\psi_{n}(\v{r})$，因此 **Schrödinger 方程的通解**可写为
$$
\varPsi(\v{r},t) = \sum\limits_{n} c_{n} \psi_{n}(\v{r}) \e^{-\I E_{n} t/\hbar}
$$


### 定态的性质

每个本征值 $E_{n}$ 对应一个**定态 (stationary state)**，其波函数为
$$
\varPsi_{n}(\v{r},t) = \psi_{n}(\v{r}) \e^{-\I E_{n} t/\hbar}
$$
其中 $\psi_{n}(\v{r})$ 为定态 Schrödinger 方程的本征函数。

#### 定态的概率密度

定态的概率密度为
$$
w_{n}(\v{r},t) = |\varPsi_{n}(\v{r},t)|^{2} = |\psi_{n}(\v{r})|^{2}
$$
概率密度流为
$$
\begin{align}
\v{J}_{n} &= -\dfrac{\I \hbar}{2m} \left( \varPsi_{n}^{*} \nabla \varPsi_{n} - \varPsi_{n} \nabla \varPsi_{n}^{*} \right) \\
&= -\dfrac{\I \hbar}{2m} \left( \psi_{n}^{*} \e^{\I E_{n} t/\hbar} \nabla \left( \psi_{n} \e^{-\I E_{n} t/\hbar} \right) - \psi_{n} \e^{-\I E_{n} t/\hbar} \nabla \left( \psi_{n}^{*} \e^{\I E_{n} t/\hbar} \right) \right) \\
&= -\dfrac{\I \hbar}{2m} \left( \psi_{n}^{*} \nabla \psi_{n} - \psi_{n} \nabla \psi_{n}^{*} \right)
\end{align}
$$
由于定态的概率密度 $w_{n}(\v{r},t)$ 不随时间变化，因此称为**定态**。定态的概率流 $\v{J}_{n}$ 也不随时间变化。

#### 定态的动量

考虑自由粒子平面波 $\varPsi\left( \v{r},t \right) = A \e^{-\I \left( Et - \v{p}\cdot \v{r} \right)/\hbar} = A \e^{-\I Et / \hbar} \e^{\I\v{p}\cdot \v{r}/\hbar}$，尝试代入定态 Schrödinger 方程，得
$$
\begin{align}
\hat{H} \psi(\v{r}) &= -\dfrac{\hbar^{2}}{2m} \nabla^{2} \left( A \e^{\I \v{p}\cdot \v{r}/\hbar} \right) + V(\v{r}) A \e^{\I \v{p}\cdot \v{r}/\hbar} \\
&= \dfrac{p^{2}}{2m} A \e^{\I \v{p}\cdot \v{r}/\hbar} + V(\v{r}) A \e^{\I \v{p}\cdot \v{r}/\hbar} \\
&= \left( \dfrac{p^{2}}{2m} + V(\v{r}) \right) \psi(\v{r})
\end{align}
$$
对自由粒子，$V(\v{r}) = 0$，因此 $\hat{H} \psi(\v{r}) = \dfrac{p^{2}}{2m} \psi(\v{r})$，即能量本征值 $E = \dfrac{p^{2}}{2m}$，与经典力学一致，因此**平面波是自由粒子的定态**。

自由粒子的同一定态只能确定能量 $E$，而不能确定动量 $\v{p}$ 的方向，因此存在**动量简并**。

## 一维 Schrödinger 方程解的分析

### 一维束缚态

> [!definition] 束缚态
> 粒子不可达无穷远处，即 $\psi(\pm \infty) = 0$ 的状态称为**束缚态 (bound state)**。

假定势场 $V(x)$ 在无穷远处有确定的极限 $V(+\infty)$ 和 $V(-\infty)$，则
+ 若 $E < \min\{ V(+\infty), V(-\infty) \}$，则 $\psi(x)$ 在无穷远处指数衰减，粒子被束缚在有限空间内，即处于**束缚态**；
+ 若 $E > \min\{ V(+\infty), V(-\infty) \}$，则 $\psi(x)$ 在（至少一侧）无穷远处振荡，粒子可以到达无穷远处，称其处于**散射态 (scattering state)**。

#### 态的简并

由于能量本征值 $E_{n}$ 仅与量子数 $n$ 有关，而与动量方向无关，因此必然存在**简并**。

> [!definition] 简并
> 如果对一个给定的能量 $E$，只有一个线性独立的波函数存在（即只有一个状态），即不存在 $\psi_{1}$、$\psi_{2}$ 满足 
> $$
> \begin{align}
> &\hat{H}\psi_{1} = E \psi_{1} \\
> \text{AND}\quad
> &\hat{H}\psi_{2} = E \psi_{2} \\
> \text{AND}\quad
> &c_{1}\psi_{1} + c_{2}\psi_{2} \neq 0, \quad \forall c_{1}, c_{2} \in \mathbb{C}^{*}
> \end{align}
> $$
> 则称该能级是**非简并**的，否则称它是**简并  (degeneracy)** 的，其线性独立的波函数的个数称为它的**简并度**。

一维情形下，同一定态方程的两个解 $\psi_{1}$ 和 $\psi_{2}$ 具有相同能量，其 **Wronskian 行列式** $\begin{vmatrix}\psi_{1}' & \psi_{2}' \\ \psi_{1} & \psi_{2}\end{vmatrix}$ 为常数 $c$，且 **$\psi_{1}$ 与 $\psi_{2}$ 线性相关当且仅当 $c = 0$**。[^2]

[^2]: 这称为 **Wronskian 定理**。

在[[#一维无限深势阱问题]]中，边界条件 $\psi(\pm a) = 0$ 导致常数 $c = 0$，因此 $\psi_{1}$ 与 $\psi_{2}$ 线性相关，即不存在简并。更一般地，对任意一维束缚态问题，边界条件 $\psi(\pm \infty) = 0$ 都会导致不存在简并。

> [!theorem] 不简并定理
> 一维**束缚态**必是**非简并态**。

考虑一维束缚态 $\psi$ 是复函数 $\psi_{\mathrm{r}} + \I\psi_{\mathrm{i}}$，则由 $\hat{H} = - \dfrac{\hbar^{2}}{2m} \dfrac{\dif^{2}}{\dif x^{2}} + V(x)$ 的线性性可知 $\psi_{\mathrm{r}}$ 和 $\psi_{\mathrm{i}}$ 也都是能量 $E$ 的本征函数，因此由不简并定理，**$\psi_{\mathrm{r}}$ 和 $\psi_{\mathrm{i}}$ 线性相关**，即 $\psi$ 可写为实函数与**复常数**的乘积。因而，**一维束缚态波函数的相位必是常数**，也即一维束缚态问题的解可以取为实函数。

#### 态的宇称

> [!definition] 宇称
> 若波函数 $\psi(x)$ 满足 $\psi(-x) = \pm \psi(x)$，则称其具有**宇称 (parity)**，其中 
> + $\psi(-x) = \psi(x)$ 称为**偶宇称 (even parity)** 或**正宇称 (positive parity)**；
> + $\psi(-x) = -\psi(x)$ 称为**奇宇称 (odd parity)** 或**负宇称 (negative parity)**。

考虑势场 $V(-x) = V(x)$ 的情形，Hamiltonian 算符也将满足
$$
\hat{H}(-x) = - \dfrac{\hbar^{2}}{2m} \dfrac{\dif^{2}}{\dif (-x)^{2}} + V(-x) = -\dfrac{\hbar^{2}}{2m} \dfrac{\dif^{2}}{\dif x^{2}} + V(x) = \hat{H}(x)
$$
于是对任意定态 Schrödinger 方程的解 $\psi(x)$，都有
$$
\hat{H}(-x) \psi(-x) = \hat{H}(x) \psi(-x) = E \psi(-x)
$$
因此 $\psi(-x)$ 也是能量 $E$ 的本征函数。由不简并定理，$\psi(-x)$ 与 $\psi(x)$ 线性相关，即 $\psi(-x) = c \psi(x)$，其中 $c$ 为某个常数。再由 $\psi(-(-x)) = \psi(x)$，可知 $c^{2} = 1$，即 $c = \pm 1$。因此，**势场关于原点对称时，定态波函数必具有宇称**。

> [!theorem] 宇称定理
> 若一维势场 $V(x)$ 关于原点对称，即 $V(-x) = V(x)$，则 $V(x)$ 中的**一维束缚态波函数必有确定的宇称**。

^651420

### 一维无限深势阱问题

考虑一维无限深势阱，势能 $V(x)$ 定义为
$$
V(x) = \begin{cases}
0, & -a < x < a, \\
+\infty, & \text{otherwise}
\end{cases}
$$
粒子只能存在于 $-a < x < a$ 的区域内，波函数 $\psi(x)$ 在该区域外必须为零，即 $\psi(x) = 0$，$|x| \geq a$，**连续性**要求边界处 $\psi(-a) = \psi(a) = 0$。

在势阱内，定态 Schrödinger 方程为
$$
\dfrac{\dif^{2} \psi(x)}{\dif x^{2}} + \dfrac{2mE}{\hbar^{2}} \psi(x) = 0
$$
记 $k^{2} = \dfrac{2mE}{\hbar^{2}}$，二阶齐次线性常微分方程的通解为
$$
\psi(x) = A \cos k(x + a) + B \sin k(x + a)
$$
应用边界条件 $\psi(-a) = 0$，得 $A = 0$，因此 $\psi(x) = B \sin k(x + a)$；应用边界条件 $\psi(a) = 0$，得 $k = \dfrac{n \pi}{2a}$，$n = 1, 2, 3, \cdots$，而**能量本征值**即为
$$
\mark{ E_{n} = \dfrac{\hbar^{2} k^{2}}{2m} = \dfrac{n^{2} \pi^{2} \hbar^{2}}{8 m a^{2}}, } \quad n = 1, 2, 3, \cdots
$$
用待定系数 $B$ 归一化，得**一维无限深势阱中的能量本征函数**为
$$
\mark{ \psi_{n}(x) = \begin{cases}
\sqrt{\dfrac{1}{a}} \sin \dfrac{n \pi (x + a)}{2a}, & -a < x < a, \\
0, & \text{otherwise},
\end{cases} }\quad n = 1, 2, 3, \cdots
$$

### 一维线性谐振子问题

经典力学下，受到回复力 $F = -kx$  的谐振子势能为 $V(x) = \dfrac{1}{2} kx^{2}$，产生谐振的角频率为 $\omega = \sqrt{\dfrac{k}{m}}$；类似地，给定势场 $V(x) = \dfrac{1}{2} \mu \omega^{2} x^{2}$，考察其中的波函数。

定态 Schrödinger 方程为
$$
\dfrac{\dif^{2} \psi(x)}{\dif x^{2}} + \dfrac{2\mu}{\hbar^{2}} \left( E - \dfrac{1}{2} \mu \omega^{2} x^{2} \right) \psi(x) = 0
$$
定义**无量纲变量 $\xi = \sqrt{\dfrac{\mu \omega}{\hbar}} x$，$\lambda = \dfrac{2E}{\hbar \omega}$**，则方程化为
$$
\dfrac{\dif^{2} \psi(\xi)}{\dif \xi^{2}} + \left( \lambda - \xi^{2} \right) \psi(\xi) = 0
$$

> [!note] 线性谐振子方程解的试探
> 线性谐振子方程中，$\lambda$ 是与能量 $E$ 相关的参量。下面的例子显示，$\lambda(E)$ 只能取一系列特殊的**分立值**，才能保证方程具有**有限**的解。
> 
> 
> ![[一维线性谐振子 lambda=1.png|$\lambda = 1$ 附近一维线性谐振子方程数值求解结果]]

观察到 $\xi \to \pm \infty$ 时，方程近似为 $\dfrac{\dif^{2} \psi(\xi)}{\dif \xi^{2}} - \xi^{2} \psi(\xi) = 0$，其通解为 
$$
\psi(\xi) = A \e^{-\xi^{2}/2} + B \e^{\xi^{2}/2}
$$
由于 $\e^{\xi^{2}/2}$ 在无穷远处发散，因此**有限性**要求 $B = 0$，即取渐近解 $\psi(\xi) \sim \e^{-\xi^{2}/2}$。

设方程的一般解为 $\psi(\xi) = \e^{-\xi^{2}/2} H(\xi)$，回代得到
$$
\dfrac{\dif^{2}}{\dif \xi^{2}} H(\xi) - 2 \xi \dfrac{\dif}{\dif \xi} H(\xi) + (\lambda - 1) H(\xi) = 0
$$
这是 **Hermite 方程**，其解 $H(\xi)$ 称为 **Hermite 多项式**。设 $H(\xi)$ 可展为幂级数 $\sum\limits_{\nu=0}^{\infty} a_{\nu} \xi^{\nu}$，代入得到
$$
\sum\limits_{\nu=0}^{\infty} (\nu + 2) (\nu + 1) a_{\nu+2} \xi^{\nu} - 2 \sum\limits_{\nu=0}^{\infty} \nu a_{\nu} \xi^{\nu} + (\lambda - 1) \sum\limits_{\nu=0}^{\infty} a_{\nu} \xi^{\nu} = 0
$$
比较各幂次项系数，得到**递推关系**
$$
a_{\nu+2} = \dfrac{2\nu - \lambda + 1}{(\nu + 1)(\nu + 2)} a_{\nu},\quad \nu = 0, 1, 2, \cdots
$$

$\xi \to \infty$ 时，$H$ 一般**发散**，且由于 $\lim\limits_{ \nu \to \infty } \dfrac{a_{\nu+2}}{a_{\nu}} = \dfrac{2}{\nu}$，因此 $H(\xi)$ 的**渐近行为为 $\e^{\xi^{2}}$**，从而 $\psi(\xi)$ 的渐近行为为 $\e^{\xi^{2}/2}$，与有限性要求矛盾。无穷级数解总是发散，因此必须考虑退化为**有限级数**，即在某一项 $v = n$ 处，递推关系中分子为零，即 $2n - \lambda + 1 = 0$，从而有**量子化条件**
$$
\lambda = 2n + 1, \quad n = 0, 1, 2, \cdots
$$
根据[[#^651420|宇称定理]]，势场 $V(x) = \dfrac{1}{2} \mu \omega^{2} x^{2}$ 关于原点对称，则 $\psi(\xi)$ 应**有确定的宇称**，因此 $H(\xi)$ 也应有确定的宇称。由递推关系可知，$a_{0}$ 和 $a_{1}$ 可任意取值，因而
+ $a_{0}$ 不为零时，$a_{1} = 0$，表达式为
$$
H_{n}(\xi) = a_{0} + a_{2}\xi^{2} + a_{4}\xi^{4} + \cdots + a_{n} \xi^{n}
$$
此时 $n$ 为偶数，$\psi_{n}(\xi)$ 呈**偶宇称**；
+ $a_{1}$ 不为零时，$a_{0} = 0$，表达式为
$$
H_{n}(\xi) = a_{1}\xi + a_{3}\xi^{3} + a_{5}\xi^{5} + \cdots + a_{n} \xi^{n}
$$
此时 $n$ 为奇数，$\psi_{n}(\xi)$ 呈**奇宇称**。

适当选取最低阶系数，得到 **Hermite 多项式**表示为
$$
\mark{ H_{n} (\xi) = (-1)^{n} \e^{\xi^{2}} \dfrac{\dif^{n}}{\dif \xi^{n}} \e^{-\xi^{2}}, } \quad n = 0, 1, 2, \cdots
$$
而波函数 $\psi_{n}(\xi) = \e^{-\xi^{2}/2} H_{n}(\xi)$，**归一化**后得到**一维线性谐振子中的能量本征函数**
$$
\mark{ \psi_{n}(x) = N_{n} H_{n}(\alpha x) \e^{-\alpha^{2}x^{2}/2}, } \quad n = 0, 1, 2, \cdots
$$
其中 $N_{n} = \left( \dfrac{\alpha}{\sqrt{\pi} 2^{n} n!} \right)^{1/2}$，$\alpha = \sqrt{\dfrac{\mu \omega}{\hbar}}$；对应的**能量本征值**为
$$
\mark{ E_{n} = \left( n + \dfrac{1}{2} \right) \hbar \omega, } \quad n = 0, 1, 2, \cdots
$$

常用的一维谐振子波函数有：
+ $n = 0$，称**基态**，能量 $E_{0} = \cfrac{1}{2} \hbar \omega$，波函数为
$$
\psi_{0}(x) = \left( \dfrac{\alpha}{\sqrt{ \pi }} \right)^{1/2} \e^{-\alpha^{2} x^{2}/2}
$$
^53837c
+ $n = 1$，称**第一激发态**，能量 $E_{1} = \dfrac{3}{2} \hbar \omega$，波函数为
$$
\psi_{1}(x) = \left( \dfrac{2\alpha}{\sqrt{\pi}} \right)^{1/2} \alpha x \e^{-\alpha^{2} x^{2}/2}
$$
+ $n = 2$，称**第二激发态**，能量 $E_{2} = \dfrac{5}{2} \hbar \omega$，波函数为
$$
\psi_{2}(x) = \left( \dfrac{\alpha}{2\sqrt{ \pi }} \right)^{1/2} (2\alpha^{2} x^{2} - 1) \e^{-\alpha^{2} x^{2}/2}
$$

> [!note] 谐振子相干态
> 将上述一维谐振子基态波包 $\psi_{0}(x) = \dfrac{\alpha^{1/2}}{\pi^{1/4}} \e^{-\alpha^{2}x^{2}/2}$ 平移到 $x = x_{0}$ 处，得到
> $$
> \psi(x) = \dfrac{\alpha^{1/2}}{\pi^{1/4}} \e^{-\alpha^{2} (x - x_{0})^{2}/2}
> $$
> 此即**相干态波包**初始时刻状态。可以由含时薛定谔方程证明，这一波包运动中形状保持不变，只是**波包中心周期性振荡**，与经典粒子的运动很相似，如
> $$
> |\varPsi(x, t)|^{2} = | \psi_{0} (x - x_{0} \cos\omega t) |^{2}
> $$

### 一维散射问题

考虑一维势场 $V(x)$，其在某一区域内非零，在无穷远处趋于零，如下图所示：



设例子从左侧入射，入射波函数为 $\varPsi_{\mathrm{i}}(x,t) = A \e^{\I kx}$，反射波函数为 $\varPsi_{\mathrm{r}}(x,t) = B \e^{-\I kx}$，透射波函数为 $\varPsi_{\mathrm{t}}(x,t) = C \e^{\I kx}$，其中 $k = \sqrt{\dfrac{2mE}{\hbar^{2}}}$。转化为**概率流密度**，分别表示为
$$
J_{\mathrm{i}} = |A|^{2} \dfrac{\hbar k}{m}, \qquad J_{\mathrm{r}} = -|B|^{2} \dfrac{\hbar k}{m}, \qquad J_{\mathrm{t}} = |C|^{2} \dfrac{\hbar k}{m}
$$
定义**反射系数** $R$ 和**透射系数** $D$ 为
$$
R = \dfrac{|J_{\mathrm{r}}|}{|J_{\mathrm{i}}|} = \dfrac{|B|^{2}}{|A|^{2}}, \qquad D = \dfrac{J_{\mathrm{t}}}{J_{\mathrm{i}}} = \dfrac{|C|^{2}}{|A|^{2}}
$$

#### 一维方势垒的贯穿

具体地，考虑一维方势垒，势能 $V(x)$ 定义为
$$
V(x) = \begin{cases}
V_{0}, & 0 < x < a, \\
0, & \text{otherwise}
\end{cases}
$$
则在各区域的定态 Schrödinger 方程分别为
$$
\begin{cases}
\dfrac{\dif^{2} \psi(x)}{\dif x^{2}} + \dfrac{2mE}{\hbar^{2}} \psi(x) = 0, & x < 0 \text{ OR } x > a, \\
\dfrac{\dif^{2} \psi(x)}{\dif x^{2}} + \dfrac{2m(E - V_{0})}{\hbar^{2}} \psi(x) = 0, & 0 < x < a, \\
\end{cases}
$$

+ **当 $0 < E < V_0$ 时**：
记 $\alpha = \dfrac{\sqrt{ 2 m (V_{0} - E) }}{\hbar}$，则各区域的波函数可分别解为
$$
\psi(x) = \begin{cases}
A \e^{\I kx} + B \e^{-\I kx}, & x < 0, & \text{（势垒左侧）} \\
F \e^{\alpha x} + G \e^{-\alpha x}, & 0 < x < a, & \text{（势垒内部）} \\
C \e^{\I kx}, & x > a, & \text{（势垒右侧）}
\end{cases}
$$
波函数在 $x = 0$ 和$x = a$ 处连续，且其导数也连续，因此
$$
\begin{cases}
\psi(0^{-}) = \psi(0^{+}), \\
\psi'(0^{-}) = \psi'(0^{+}), \\
\psi(a^{-}) = \psi(a^{+}),  \\
\psi'(a^{-}) = \psi'(a^{+}), 
\end{cases}
\quad\Longrightarrow\quad
\begin{cases}
A + B = F + G, \\
\I k (A - B) = \alpha (F - G), \\
F \e^{\alpha a} + G \e^{-\alpha a} = C \e^{\I k a},  \\
\alpha (F \e^{\alpha a} - G \e^{-\alpha a}) = \I k C \e^{\I k a}
\end{cases}
$$
消去 $\begin{cases} F = \dfrac{A+B + \I \dfrac{k}{\alpha}(A-B)}{2}, \\ G = \dfrac{A+B - \I \dfrac{k}{\alpha}(A-B)}{2} \end{cases}$，解得
$$
\begin{cases}
\dfrac{B}{A} = \dfrac{\left( k^{2} + \alpha^{2} \right) \sinh(\alpha a)}{\left( k^{2} - \alpha^{2} \right) \sinh(\alpha a) + 2\I k\alpha \cosh(\alpha a)}, \\
\dfrac{C}{A} = \dfrac{2\I k\alpha \e^{-\I k a}}{\left( k^{2} - \alpha^{2} \right) \sinh(\alpha a) + 2\I k\alpha \cosh(\alpha a)}
\end{cases}
$$
因此反射系数和透射系数分别为
$$
\begin{align}
&R = \dfrac{|B|^{2}}{|A|^{2}} = \dfrac{\left( k^{2} + \alpha^{2} \right)^{2} \sinh^{2}(\alpha a)}{\left( k^{2} + \alpha^{2} \right)^{2} \sinh^{2}(\alpha a) + 4 k^{2} \alpha^{2}},  \\
&D = \dfrac{|C|^{2}}{|A|^{2}} = \dfrac{4 k^{2} \alpha^{2}}{\left( k^{2} + \alpha^{2} \right)^{2} \sinh^{2}(\alpha a) + 4 k^{2} \alpha^{2}}
\end{align}
$$

+ **当 $E > V_0$ 时**：
记 $\t{k} = \dfrac{\sqrt{ 2 m (E - V_{0}) }}{\hbar}$，则各区域的波函数可分别解为
$$
\psi(x) = \begin{cases}
A \e^{\I kx} + B \e^{-\I kx}, & x < 0, & \text{（势垒左侧）} \\
F \e^{\I \t{k} x} + G \e^{-\I \t{k} x}, & 0 < x < a, & \text{（势垒内部）} \\
C \e^{\I kx}, & x > a, & \text{（势垒右侧）}
\end{cases}
$$
直接利用 $0 < E < V_0$ 的结果，令 $\alpha = \I \t{k}$，并利用 $\sinh(\I x) = \I \sin x$，$\cosh(\I x) = \cos x$，得到
$$
\begin{cases}
\dfrac{B}{A} = \dfrac{\left( k^{2} - \t{k}^{2} \right) \sin(\t{k} a)}{\left( k^{2} + \t{k}^{2} \right) \sin(\t{k} a) + 2 \I k \t{k} \cos(\t{k} a)}, \\
\dfrac{C}{A} = \dfrac{2\I k \t{k} \e^{-\I k a}}{\left( k^{2} + \t{k}^{2} \right) \sin(\t{k} a) + 2 \I k \t{k} \cos(\t{k} a)}
\end{cases}
$$
因此反射系数和透射系数分别为
$$
\begin{align}
&R = \dfrac{|B|^{2}}{|A|^{2}} = \dfrac{\left( k^{2} - \t{k}^{2} \right)^{2} \sin^{2}(\t{k} a)}{\left( k^{2} + \t{k}^{2} \right)^{2} \sin^{2}(\t{k} a) + 4 k^{2} \t{k}^{2} \cos^{2}(\t{k} a)}, \\
&D = \dfrac{|C|^{2}}{|A|^{2}} = \dfrac{4 k^{2} \t{k}^{2}}{\left( k^{2} + \t{k}^{2} \right)^{2} \sin^{2}(\t{k} a) + 4 k^{2} \t{k}^{2} \cos^{2}(\t{k} a)}
\end{align}
$$

+ **当 $E = V_0$ 时**：
此时 $\t{k} = 0$，势垒内部的定态 Schrödinger 方程为 $\dfrac{\dif^{2} \psi(x)}{\dif x^{2}} = 0$，则各区域的波函数可分别解为
$$
\psi(x) = \begin{cases}
A \e^{\I kx} + B \e^{-\I kx}, & x < 0, & \text{（势垒左侧）} \\
F x + G, & 0 < x < a, & \text{（势垒内部）} \\
C \e^{\I kx}, & x > a, & \text{（势垒右侧）}
\end{cases}
$$
波函数在 $x = 0$ 和$x = a$ 处连续，且其导数也连续，因此
$$
\begin{cases}
\psi(0^{-}) = \psi(0^{+}), \\
\psi'(0^{-}) = \psi'(0^{+}), \\
\psi(a^{-}) = \psi(a^{+}),  \\
\psi'(a^{-}) = \psi'(a^{+}), 
\end{cases}
\quad\Longrightarrow\quad
\begin{cases}
A + B = G, \\
\I k (A - B) = F, \\
F a + G = C \e^{\I k a},  \\
\I k C \e^{\I k a} = F
\end{cases}
$$
消去 $\begin{cases} F = \I k (A - B), \\ G = A + B \end{cases}$，解得
$$
\begin{cases}
\dfrac{B}{A} = \dfrac{\I k a - 1}{\I k a + 1}, \\
\dfrac{C}{A} = \dfrac{2 \I k \e^{-\I k a}}{\I k a + 1}
\end{cases}
$$


