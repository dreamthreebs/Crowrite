# 251017-copolar and crosspolar

### 一、探测器偏振方向的物理意义

在偏振探测器中，每个通道对电场的某一线偏振方向最敏感。\
例如，一个偏振敏感的吸收膜、天线或偏振片，\
对与自身**偏振轴**平行的电场响应最强，对垂直方向理应没有响应。

但真实探测器不完美，对垂直方向仍然存在少量响应。\
这就是：

* **Co-polar（共偏振）**：探测器“主方向”上的理想响应；
* **Cross-polar（交叉偏振）**：垂直方向上的泄漏响应。

***

### 二、形式定义

在波束覆盖的天空上某个方向 $\hat{r}\_b$，\
定义两个响应函数：

\$$\
P\_{\parallel}(\hat{r}_b) \quad\text{(co-polar)}, \qquad_\
&#xNAN;_&#x50;_{\perp}(\hat{r}\_b) \quad\text{(cross-polar)}.\
\$$

二者分别表示：

* 探测器对与偏振轴**平行**的电场分量的响应；
* 探测器对与偏振轴**垂直**的电场分量的响应。

通常有：\
\$$\
P\_{\parallel}(\hat{r}_b) + P_{\perp}(\hat{r}\_b) \approx 1.\
\$$

***

### 三、定义偏振响应比 (P(\hat{r}\_b, \hat{p}\_t))

为了描述波束在不同方向上对偏振的**净响应**，\
定义归一化量：

\$$\
P(\hat{r}\_b, \hat{p}_t)_\
&#xNAN;_= \frac{P_{\parallel}(\hat{r}_b) - P_{\perp}(\hat{r}_b)}_\
&#xNAN;_{P_{\parallel}(\hat{r}_b) + P_{\perp}(\hat{r}\_b)}.\
\$$

其取值范围为 $\[-1,1]$，代表了探测器的偏振效率：

| 情况      | 含义                        |
| ------- | ------------------------- |
| $P = 1$ | 理想偏振响应（无交叉偏振泄漏）           |
| $P < 1$ | 存在 cross-polar 泄漏，偏振测量受污染 |
| $P = 0$ | 对两个正交方向响应相等 → 无偏振敏感性      |

***

### 四、偏振权重向量中的体现

在偏振测量的观测方程中，权重向量为：

\$$\
\mathbf{W}(\hat{r}\_b, \hat{p}\_t)
----------------------------------

\begin{pmatrix}\
1 \\\
\gamma , P(\hat{r}\_b, \hat{p}\_t)\cos 2\psi\_t \\\
\gamma , P(\hat{r}\_b, \hat{p}\_t)\sin 2\psi\_t\
\end{pmatrix},\
\$$

其中：

* $\gamma = \dfrac{1-\epsilon}{1+\epsilon}$ 表示偏振效率；
* $\epsilon$ 是交叉偏振泄漏比例；
* $\psi\_t$ 是该时刻探测器偏振轴相对于局部子午线的角度。

***

### 五、在观测方程中的角色

观测到的信号为：

\$$\
d\_t\
\= \int b(\hat{r}\_b, \hat{p}\_t)\
\Big\[\
I(\hat{r}\_b)

* \gamma , P(\hat{r}\_b, \hat{p}\_t)\
  \big(Q(\hat{r}\_b)\cos 2\psi\_t + U(\hat{r}\_b)\sin 2\psi\_t\big)\
  \Big]\
  , d\Omega.\
  \$$

这说明：

* $I$ 通道不受 cross-polar 影响；
* $Q,U$ 通道的权重随 $P(\hat{r}\_b, \hat{p}\_t)$ 缩放；
* 若 cross-polar 泄漏大，则偏振灵敏度降低，系统误差增大。

***

### 六、在偏振有效波束中的出现

在偏振有效波束定义中，\
偏振权重矩阵 $\mathbf{W}$ 出现在卷积核中：

\$$\
B\_{ij}
-------

\left\[\sum\_t A\_{tp} \mathbf{w}\_t \mathbf{w}_t^{T}\right]^{-1}_\
&#xNAN;_\sum\_t A_{ti} ,\
b(\hat{r}\_j, \hat{p}\_t) ,\
\mathbf{w}\_t \mathbf{W}^{T}(\hat{n}\_j, \hat{p}\_t).\
\$$

这里的 $\mathbf{W}$ 就包含了 $P(\hat{r}\_b,\hat{p}\_t)$，\
因此偏振波束的 co-/cross-polar 差异会影响到最终的\
$Q,U$ 卷积核形状与泄漏特性。

***

### 七、实际实验中的典型数值

| 实验                  | 仪器类型                            | Cross-polar 比例 | 备注             |
| ------------------- | ------------------------------- | -------------- | -------------- |
| **Planck LFI/HFI**  | corrugated feedhorn + bolometer | < 0.5%         | 可忽略            |
| **ACTPol / SPTPol** | lenslet + antenna array         | ≈ 1%           | 在仿真中建模修正       |
| **LiteBIRD**        | HWP + TES bolometer             | ≪ 1%           | 通过 HWP 调制平均化泄漏 |

***

### 八、直观理解（图像比喻）

想象天空上的一个偏振波束：

* **Co-polar 模式**：主敏感方向的响应分布；
* **Cross-polar 模式**：垂直方向的微弱泄漏分布。

二者的差值刻画了偏振纯度：

\$$\
P(\hat{r}_b)_\
&#xNAN;_= \frac{P_{\parallel} - P\_{\perp\}}{P\_{\parallel} + P\_{\perp\}}.\
\$$

如果 $P\_{\perp}$ 很小，说明 cross-polar 泄漏可忽略；\
若两者接近，则说明探测器几乎“失去了偏振方向性”。

***

### 九、总结

> * **Co-polar（共偏振）**：探测器主偏振方向上的理想响应；
> * **Cross-polar（交叉偏振）**：与主偏振方向垂直的泄漏响应；
> * 二者共同决定探测器的偏振纯度；
> * 它们的差值归一化后定义为：\
>   \$$\
>   P = \frac{P\_{\parallel} - P\_{\perp\}}{P\_{\parallel} + P\_{\perp\}},\
>   \$$\
>   并出现在偏振权重向量与有效波束矩阵中；
> * Cross-polar 是偏振观测系统误差的主要来源之一，\
>   特别是在高精度 $B$ 模测量中。

***

是否希望我在这一节后面再补一张 **co-/cross-polar 响应模式的示意图（带偏振轴方向）**？\
可以生成一张干净的灰度或伪彩色图，用来放在笔记里。
