**半经典分布**和**可区分粒子分布**统称为 **Boltzmann 分布**，以此为基础的统计理论称为 **Boltzmann 统计理论**。

## 配分函数

### 配分函数的引入

考虑 Boltzmann 分布 $n_i = g_i \e^{-\alpha -\beta \varepsilon_i}$，其中 $\alpha$ 和 $\beta$ 是待定参数。由此可得到**总粒子数**和**总能量**分别为
$$
\begin{align}
&N = \sum_i n_i = \e^{-\alpha} \sum_i g_i \e^{-\beta \varepsilon_i} \\
&E = \sum_i n_i \varepsilon_i = \e^{-\alpha} \sum_i g_i \varepsilon_i \e^{-\beta \varepsilon_i} = -\e^{-\alpha} \frac{\partial}{\partial \beta} \sum_i g_i \e^{-\beta \varepsilon_i}
\end{align}
$$
可见，计算 Boltzmann 分布宏观量的关键在于计算**配分函数**
$$
z = \sum_i g_i \e^{-\beta \varepsilon_i}
$$

这样，通过量子力学计算出单粒子态的能级 $\varepsilon_i$ 及其简并度 $g_i$，即可计算配分函数 $z$，进而得到系统的各宏观量。

### 用配分函数计算宏观量

由配分函数 $z$，可将总粒子数和总能量表示为
$$
N = \e^{-\alpha} z, \qquad 
E = -\e^{-\alpha} \frac{\partial z}{\partial \beta}
$$
即，$\alpha$ 可由总粒子数 $N$ 和配分函数 $z$ 确定
$$
\alpha = \ln \frac{z}{N}
$$

#### 能量平均值

对近独立粒子体系，能量平均值为
$$
\begin{align}
\overline{E} &= \sum_i \overline{ n }_i \varepsilon_i \approx \sum_i n_i \varepsilon_i &\hspace{-5em}\text{（最可几值近似）} \\
&= \e^{-\alpha} \sum_i \varepsilon_i \e^{-\beta \varepsilon_i} g_i = -\e^{-\alpha} \sum\limits_i g_i \frac{\partial}{\partial \beta} \e^{-\beta \varepsilon_i} \\
&= -\e^{-\alpha} \frac{\partial}{\partial \beta} \sum_i g_i \e^{-\beta \varepsilon_i} = -\dfrac{N}{z} \frac{\partial z}{\partial \beta} = -N\dfrac{\partial \ln z}{\partial \beta}
\end{align}
$$

#### 微观状态数

对 Boltzmann 分布，在**半经典 (semi-classical, s)** 近似下取**最可几 (most probable, m)** 值，系统的微观状态数为
$$
W_{\mathrm{sm}}\{n_{i}\} = \prod\limits_i \dfrac{g_i^{n_i}}{n_i!} \Bigg|_{n_i = g_i \e^{-\alpha - \beta \varepsilon_i}}
$$
取对数并用 Stirling 公式 $\ln n! \approx n \ln n - n$ 近似，有
$$
\begin{align}
\ln W_{\mathrm{sm}}\{n_{i}\} &= \sum_i \left( n_i \ln g_i - \ln n_i! \right) \Big|_{n_i = g_i \e^{-\alpha - \beta \varepsilon_i}} \\
&\approx \sum_i \left( n_i \ln g_i - n_i \ln n_i + n_i \right) \Big|_{n_i = g_i \e^{-\alpha - \beta \varepsilon_i}} \\
&= \sum_i n_i \left( \ln \dfrac{g_{i}}{n_{i}} + 1 \right) \Bigg|_{\frac{g_{i}}{n_{i}} = \e^{\alpha + \beta \varepsilon_{i}}} \\
&= \sum\limits_i n_i (\alpha + \beta \varepsilon_i + 1) = N(\alpha + 1) + \beta \overline{ E }
\end{align}
$$
由 $\alpha = \ln \dfrac{z}{N}$ 和 $\overline{ E } = -N \dfrac{ \partial \ln z }{ \partial \beta }$，进一步得到
$$
\ln W_{\mathrm{sm}}\{n_{i}\} = N \left( \ln \dfrac{z}{N} + 1 - \beta \dfrac{ \partial \ln z }{ \partial \beta } \right) = N \left( \ln z - \beta\dfrac{ \partial \ln z }{ \partial \beta } \right) + N \left( 1 - \ln N \right)
$$
以下将看到，这个结果与[[#配分函数#熵|熵]]密切相关。

#### 压强

首先考虑单粒子态的**能级 $\varepsilon_i$ 随「容器」体积 $V$ 的变化**。以三维无限深方势阱模型为例，单粒子态能级为
$$
\varepsilon_{n_x, n_y, n_z} = \dfrac{h^2}{8m} \left( \dfrac{n_x^2}{L^2} + \dfrac{n_y^2}{L^2} + \dfrac{n_z^2}{L^2} \right)
= A_{n_x, n_y, n_z} L^{-2} = A_{n_x, n_y, n_z} V^{-2/3}
$$
其中 $L$ 为立方体边长，$V = L^3$ 为体积，$A_{n_x, n_y, n_z} = \dfrac{h^2}{8m} (n_x^2 + n_y^2 + n_z^2)$ 是与体积无关的常数。则 **$\varepsilon_{i}$ 关于体积 $V$ 的变化率**为
$$
\dfrac{\partial \varepsilon_i}{\partial V} = -\dfrac{2}{3} A_i V^{-2/3 - 1} = -\dfrac{2}{3} \dfrac{\varepsilon_i}{V}
$$

我们从粒子对「容器」壁的「虚功」出发计算压强。设系统体积变化 $\dif V$，则粒子对壁做的「虚功」为
$$
\dj W_{i} = p_{i} \dif V = - \dif \varepsilon_i
$$
因而粒子在单粒子态 $\psi_i$ 上时对壁的压强贡献为
$$
p_{i} = - \dfrac{\dif \varepsilon_i}{\dif V}
$$
在 Boltzmann 分布下，系统的**总压强**为
$$
\begin{align}
p &= \sum_i n_i p_i = - \sum_i n_i \dfrac{\partial \varepsilon_i}{\partial V} = - \e^{-\alpha} \sum_i g_i \e^{-\beta \varepsilon_i} \dfrac{\partial \varepsilon_i}{\partial V} \\
&= - \e^{-\alpha} \sum\limits_i g_i \cdot \left( - \dfrac{1}{\beta} \dfrac{ \partial }{ \partial V } \e^{-\beta \varepsilon_{i}} \right) \\
&= \dfrac{1}{\beta} \e^{-\alpha} \dfrac{\partial}{\partial V} \sum_i g_i \e^{-\beta \varepsilon_i} = \dfrac{1}{\beta} \dfrac{N}{z} \dfrac{\partial z}{\partial V} = \dfrac{N}{\beta} \dfrac{\partial \ln z}{\partial V}
\end{align}
$$

> [!note] 公式的适用范围
> 上述宏观公式 $\overline{E} = - N \cfrac{ \partial \ln z }{ \partial \beta }$ 和 $p = \cfrac{N}{\beta} \cfrac{ \partial \ln z }{ \partial V }$ 均基于 Boltzmann 分布，适用于**半经典分布**和**可区分粒子分布**的近独立粒子系统；而由微观量计算宏观量的 $\overline{E} = \sum\limits_i \overline{ n }_i \varepsilon_i$ 和 $p = - \sum\limits_i \overline{ n }_i \dfrac{ \partial \varepsilon_i }{ \partial V }$ 则适用于所有近独立粒子系统，包括 Bose 系统和 Fermi 系统。
> 
> 特别地，压强与内能之间有关系
> $$
> p = - \sum\limits_{i} \overline{ n }_i \dfrac{ \partial \varepsilon_i }{ \partial V } = - \sum\limits_{i} \overline{ n }_i \cdot \left( - \dfrac{2}{3} \dfrac{ \varepsilon_i }{ V } \right) = \dfrac{2}{3} \dfrac{ \overline{E} }{ V }
> $$
> 同样适用于所有近独立（非相对论）粒子系统。

#### 热量

已知在无穷小准静态过程中，
$$
\dj W = -p \dif V = \sum\limits_i \overline{ n }_i \dfrac{ \dif \varepsilon_i }{ \dif V } \dif V = \sum\limits_{i} n_{i} \dif \varepsilon_{i}
$$
而由 $\overline{ E } = \sum\limits_{i} n_{i} \varepsilon_{i}$，可得系统内能的微小变化为
$$
\dif \overline{E} = \sum_i \left( \varepsilon_i \dif n_i + n_i \dif \varepsilon_i \right)
$$
由热力学第一定律，应有
$$
\dj Q = \dif \overline{E} - \dj W = \sum_i \varepsilon_i \dif n_i
$$
即，准静态过程中**系统从外界吸收的热量**等于粒子**在各个能级重新分布**所增加的内能，这个过程通过跃迁实现。

借助已经给出的 $\overline{ E }$ 和 $p$ 的表达式，可计算无穷小准静态过程中系统吸收的热量为
$$
\begin{align}
\dj Q &= \dif \overline{E} - (- p \dif V) = \dif \left( -N \dfrac{ \partial \ln z }{ \partial \beta } \right) + \dfrac{N}{\beta} \dfrac{ \partial \ln z }{ \partial V } \dif V \\
&= \dfrac{N}{\beta} \left( \dfrac{ \partial \ln z }{ \partial V } \dif V - \beta \dif\left( \dfrac{ \partial \ln z }{ \partial \beta } \right) \right) \\
&= \dfrac{N}{\beta} \left( \dfrac{ \partial \ln z }{ \partial V } \dif V + \dfrac{ \partial \ln z }{ \partial \beta } \dif \beta - \dfrac{ \partial \ln z }{ \partial \beta } \dif \beta - \beta \dif\left( \dfrac{ \partial \ln z }{ \partial \beta } \right) \right) \\
&= \dfrac{N}{\beta} \left( \dif \ln z - \dif\left( \beta \dfrac{ \partial \ln z }{ \partial \beta } \right) \right) = \dfrac{N}{\beta} \dif \left( \ln z - \beta \dfrac{ \partial \ln z }{ \partial \beta } \right)
\end{align}
$$
即可以写成**全微分**的形式
$$
\beta \dj Q = N \dif \left( \ln z - \beta \dfrac{ \partial \ln z }{ \partial \beta } \right)
$$

#### 熵

已知对无穷小准静态过程，有 $\cfrac{\dj Q}{T} = \dif S$。与上述热量的全微分形式对比，可知 **$\beta$ 与 $\cfrac{1}{T}$ 都是 $\dj Q$ 的积分因子**，我们首先建立二者之间的联系。

不妨记 $\beta \dj Q = \dif S'$，则 $\dif S' = \beta T \dif S$。视 $S'$ 为 $S$ 和 $T$ 的函数，有
$$
\dif S' = \dfrac{ \partial S' }{ \partial S } \dif S + \dfrac{ \partial S' }{ \partial T }  \dif T = \beta T \dif S
$$
比较系数可得
$$
\dfrac{ \partial S' }{ \partial S } = \beta T, \qquad \dfrac{ \partial S' }{ \partial T } = 0
$$
由第二式可知 $S'$ 与 $T$ 无关，即 $S' = S'(S)$，进而 $\beta T = \cfrac{ \partial S'(S) }{ \partial S }$ 也与 $T$ 无关，因此只能取为常数，记为 $\cfrac{1}{k}$，即
$$
\beta = \dfrac{1}{kT}
$$
后面的推导中，我们将证明常数 $k$ 即为 **Boltzmann 常数**。

由 $\beta = \cfrac{1}{kT}$ 和热量的全微分形式，立得
$$
\dif S = Nk \dif \left( \ln z - \beta \dfrac{ \partial \ln z }{ \partial \beta } \right)
$$
由前述[[#配分函数#微观状态数|最可几分布下的微观状态数]]之值，可知
$$
\dif S = k \cdot \dif (\ln W_{\mathrm{sm}}\{n_{i}\})
$$
不妨**定义绝对熵为 $S = k \ln W_{\mathrm{sm}} \left\{ n_{i} \right\}$**，即
$$
S = Nk \left( \ln z - \beta \dfrac{ \partial \ln z }{ \partial \beta } \right) + Nk (1 - \ln N)
= Nk \left( \ln \dfrac{\e z}{N} - \beta \dfrac{ \partial \ln z }{ \partial \beta } \right)
$$

> [!theorem] Boltzmann 关系
> 熵 $S$ 与微观状态数 $W$ 之间的关系为
> $$
> S = k \ln W \left\{ n_{i} \right\}
> $$
> 称为 **Boltzmann 关系**，其中常数 $k$ 称为 **Boltzmann 常数**，其数值约为 $k \approx 1.38 \times 10^{-23} \rmu{J/K}$。

> [!note] 熵的统计意义
> Boltzmann 关系揭示了熵的统计意义：
> + 熵是系统微观状态数的对数，**以指数级别反映系统的无序程度**；微观状态数越多，系统的熵越大，表示系统的无序程度越高。 
> + 熵的零点对应于系统仅有 1 个微观状态的情况。
> 
> 孤立系统在平衡态时 $W$ 达到最大值，熵 $S$ 也达到最大值，即孤立系统自发趋向平衡态的过程就是**自发趋向无规则和无秩序**的过程。
> 
> 在平衡态下，每个可能微观态**出现的概率**为 $\rho \left\{ n_{i} \right\} = \cfrac{1}{W \left\{ n_{i} \right\}}$，而一般情况下 $\rho$ 更能代表系统的分布状态，因此更一般地重新定义熵为
> $$
> S = - k \overline{ \ln \rho } = - k \sum\limits_{s} \rho_{s} \ln \rho_{s}
> $$

#### 自由能与化学势

由于有 $\varepsilon_{i}$ 与 $V$、$\beta$ 与 $T$ 的关系，$z$ 已经成为 $T,V$ 的函数，因此考虑特性函数 **Helmholtz 自由能 $F(T,V) = \overline{ E } - TS$**，有
$$
\begin{align}
F(T,V) &= \overline{ E } - TS = -N\dfrac{\partial \ln z}{\partial \beta} - T \cdot Nk \left( \ln \dfrac{\e z}{N} - \beta \dfrac{ \partial \ln z }{ \partial \beta } \right) \\
&= - NkT \ln \dfrac{\e z(T,V)}{N}
\end{align}
$$
以 $F$ 可求出**化学势**为
$$
\mu = \left( \dfrac{ \partial F }{ \partial N }  \right)_{\!T,V} = -kT (1 + \ln z) + kT (\ln N + 1) = -kT \ln \dfrac{z}{N}
$$

注意到 $\alpha = \ln \cfrac{z}{N}$，因此 $\alpha$ 决定于化学势 $\mu$，有
$$
\alpha = - \dfrac{\mu}{kT}
$$
至此，Boltzmann 分布的**最可几粒子数分布**可写为
$$
n_i = g_i \e^{\tfrac{\mu - \varepsilon_i}{kT}}
$$
