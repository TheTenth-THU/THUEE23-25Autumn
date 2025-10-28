## DTFT 的定义

### DTFT 的引入

已知连续时间信号 $f(t)$ 的 **Fourier 变换 (FT)** 定义为
$$
F(\J\varOmega) = \dint_{-\infty}^{\infty} f(t) \e^{-\J \varOmega t} \dif t
$$
以间隔 $T$ 对其进行冲激采样，得到
$$
f_{\mathrm{s}}(t) = f(t) \sum_{n=-\infty}^{\infty} \delta(t - nT) = \sum_{n=-\infty}^{\infty} f(nT) \delta(t - nT)
$$
则采样信号的 Fourier 变换为
$$
F_{\mathrm{s}}(\J\varOmega) = \dint_{-\infty}^{\infty} f_{\mathrm{s}}(t) \e^{-\J \varOmega t} \dif t = \sum_{n=-\infty}^{\infty} f(nT) \e^{-\J \varOmega nT}
$$
类比于此，考虑离散时间信号 $x[n] = f(nT)$，记采样得到的离散信号频率为 $\omega = \varOmega T$，可以定义**离散时间 Fourier 变换 (DTFT)** 如

> [!definition] 离散时间 Fourier 变换 (DTFT)
> 离散时间信号 $x[n]$ 的 **离散时间 Fourier 变换 (Discrete-Time Fourier Transform, DTFT)** 定义为
> $$
> X(\omega) = \sum_{n=-\infty}^{\infty} x[n] \e^{-\J \omega n}
> $$
> 其**逆变换 (Inverse DTFT)** 为
> $$
> x[n] = \dfrac{1}{2\pi} \dint_{-\pi}^{\pi} X(\omega) \e^{\J \omega n} \dif \omega
> $$

### DTFT 与其它变换的关系

#### DTFT 与 Fourier 变换的关系

由 [[#DTFT 的引入]]可知，离散时间信号 $x[n]$ 的 DTFT 可以看作是其对应的连续时间信号 $f(t)$ 的采样信号频谱 $F_{\mathrm{s}}\left( \J\varOmega \right)$ 在频点 $\varOmega = \dfrac{\omega}{T}$ 处的取值，即
$$
X(\omega) = F_{\mathrm{s}}(\J\varOmega) \Big|_{\varOmega = \omega / T}
$$
由于以 $T$ 为周期的冲激采样会使频谱发生 $\dfrac{2\pi}{T}$ 的周期性重复，因此 DTFT 是周期为 $2\pi$ 的周期函数。

#### DTFT 与 $z$ 变换的关系

注意到 $x[n]$ 的 $z$ 变换为
$$
X(z) = \sum_{n=-\infty}^{\infty} x[n] z^{-n}
$$
则 DTFT 可以看作是 **$z$ 变换在单位圆 $z = \e^{\J \omega}$ 上的取值**，即
$$
X(\omega) = X(z) \Big|_{z = \e^{\J \omega}}
$$

### DTFT 的线性代数解释

将离散时间信号 $x[n]$ 看作是**无限维空间** $\ell^{2}$ 中的一个向量 $\v{x}$，其 DTFT $X(\omega)$ 可以看作是该向量在**另一组单位基底** $\left\{ \vu{\phi}_{\omega} \right\} = \left\{ \phi_{\omega}[n] \right\} = \{ \e^{\J \omega n} \}$ 上的**投影系数**，即
$$
X(\omega) = \left\langle  \v{x}, \vu{\phi}_{\omega}  \right\rangle = \sum_{n=-\infty}^{\infty} x[n] \e^{-\J \omega n}
$$

### 典型信号的 DTFT

一些典型离散时间信号及其 DTFT 如下表所示：

| 信号类型    | 信号 $x[n]$                                                                      | DTFT 频谱 $X(\omega)$                                                                                 |
| :------ | :----------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------- |
| 单位样值序列  | $\delta[n]$                                                                    | $\e^{-\J \omega \cdot 0} = 1$                                                                       |
| 矩形窗序列   | $\begin{cases} 1, & \vert n \vert \le M, \\ 0, & \text{otherwise} \end{cases}$ | $\dfrac{\sin \cfrac{(2M + 1) \omega}{2}}{\sin \cfrac{\omega}{2}}$                                   |
| 全 1 序列  | 1                                                                              | $\sum\limits_{n=-\infty}^{\infty} \e^{\J\omega n} = 2\pi \delta(\omega)$                            |
| 复指数序列   | $\e^{\J \omega_{0} n}$                                                         | $2\pi \delta(\omega - \omega_{0})$                                                                  |
| 余弦序列    | $\cos \omega_{0}n$                                                             | $\pi \big( \delta(\omega - \omega_{0}) + \delta(\omega + \omega_{0}) \big)$                         |
| sinc 序列 | $\dfrac{\sin \omega_{\mathrm{c}}n}{\pi n}$                                     | $\begin{cases} 1, & \vert \omega \vert < \omega_{\mathrm{c}}, \\ 0, & \text{otherwise} \end{cases}$ |

## DTFT 的性质

### 基本性质

+ **线性**：$a x_{1}[n] + b x_{2}[n] \xrightarrow{\text{DTFT}} a X_{1}(\omega) + b X_{2}(\omega)$
+ **周期性**：$X(\omega)$ 是 $2\pi$ 周期函数，即 $X(\omega) = X(\omega + 2k\pi),\ k \in \mathbb{Z}$
+ **时移**：$x[n - n_{0}] \xrightarrow{\text{DTFT}} \e^{-\J \omega n_{0}} X(\omega)$
+ **频移**：$\e^{\J \omega_{0} n} x[n] \xrightarrow{\text{DTFT}} X(\omega - \omega_{0})$
+ **时域差分**：$x[n] - x[n - 1] \xrightarrow{\text{DTFT}} (1 - \e^{-\J \omega}) X(\omega)$
+ **频域微分**：$\J n x[n] \xrightarrow{\text{DTFT}} \dfrac{\dif X(\omega)}{\dif \omega}$

> [!note] DTFT 性质的应用
> 可以利用离散时间信号的**离散特性**简化部分过程，例如**序列解调**中，要将中心频率为 $\omega_{0}$ 的信号变换到基带，连续时间信号中需要乘以 $\cos(\omega_{0} n)$ 再进行低通滤波，而**数字下变频 (DDC)** 任务中限定 $\omega_{0} = \dfrac{\pi}{2}$ 时只需依次**乘以 $\e^{-\J\pi n/2} = (-\J)^{n}$** 即可。
> 
> 此外，也可以利用 DTFT 频谱的**连续性**补足信号序列离散的不足，如在**延时估计**中，可以通过发射波形 $s[n]$ 和接收信号 $r[n] = s[n-n_{0}]$ 的 DTFT 频谱相差 $\e^{-\J\omega n_{0}} = \dfrac{R(\omega)}{S(\omega)}$ 中拟合得到**非整数延时 $n_{0}$**。



