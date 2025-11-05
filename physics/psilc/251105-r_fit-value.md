# 251105-R\_fit value

***

### 📘 理论推导：二维高斯模板下的振幅误差

观测模型：

\$$\
\mathbf d = a,\mathbf t + \mathbf n,\
\$$

其中噪声为零均值高斯随机场，协方差矩阵为 $C$。

广义最小二乘（GLS）最优估计：

\$$\
\hat a = \frac{\mathbf t^\top C^{-1}\mathbf d}{\mathbf t^\top C^{-1}\mathbf t}, \qquad\
\mathrm{Var}(\hat a) = \frac{1}{\mathbf t^\top C^{-1}\mathbf t}.\
\$$

***

#### 白噪声极限

若噪声为白噪声（$C = \sigma\_{\rm pix}^2 I$）：

\$$\
\mathrm{Var}(\hat a)\
\= \frac{\sigma\_{\rm pix}^2}{\int t^2(\mathbf r), d^2r}.\
\$$

二维高斯模板（峰值归一化）：

\$$\
t(r) = e^{-r^2 / (2\sigma^2)}.\
\$$

在有限半径 $R$ 内的平方积分：

\$$\
\int\_{r\<R} t^2, d^2r = \pi\sigma^2 \left( 1 - e^{-R^2 / \sigma^2} \right).\
\$$

因此振幅误差的理论表达式为：

\$$\
\sigma\_a(R)\
\= \frac{\sigma\_{\rm pix}\sqrt{\Delta A\}}\
{\sqrt{\pi\sigma^2!\left( 1 - e^{-R^2 / \sigma^2} \right)\}}.\
\$$

定义相对误差（相对于无限大区域）：

\$$\
\boxed{\
\frac{\sigma\_a(R)}{\sigma\_a(\infty)} =\
\frac{1}{\sqrt{1 - e^{-(R/\sigma)^2\}}}.\
}\
\$$

***

#### 按 FWHM 表示

高斯半高全宽为：

\$$\
\mathrm{FWHM} = 2\sqrt{2\ln 2},\sigma \approx 2.355,\sigma.\
\$$

若拟合半径 $R = n \times \mathrm{FWHM}$，则：

\$$\
\frac{R}{\sigma} = 2.355,n,\
\qquad\
\frac{\sigma\_a(R)}{\sigma\_a(\infty)} =\
\frac{1}{\sqrt{1 - \exp\[-(2.355n)^2]\}}.\
\$$

***

### 📊 理论预测 vs 实测结果（仅白噪声）

实验测得的振幅误差（无 CMB，仅白噪声）：

|   拟合半径   |   理论相对误差  | 理论误差（以 2.5×FWHM 的 10.7548 为基准） |     实测误差    |
| :------: | :-------: | :----------------------------: | :---------: |
| 0.5×FWHM |  1.15466  |             12.418             |  **12.479** |
| 1.0×FWHM |  1.00196  |             10.776             | **10.7745** |
| 1.5×FWHM | 1.0000019 |             10.7548            | **10.7548** |
| 2.0×FWHM | 1.0000000 |             10.7548            | **10.7548** |
| 2.5×FWHM | 1.0000000 |             10.7548            | **10.7548** |

***

### ✅ 总结

* 理论结果：\
  \$$\
  \frac{\sigma\_a(R)}{\sigma\_a(\infty)} = \frac{1}{\sqrt{1 - e^{-(R/\sigma)^2\}}}.\
  \$$
* 当半径达到约 $R \gtrsim 1\times\mathrm{FWHM}$ 时，误差已基本饱和；
* 1.5×FWHM 之后增大区域几乎不再改善误差；
* 实测结果与理论预言高度一致（差异 <0.5%），验证了二维高斯 + 白噪声模型的正确性；
* 在存在相关噪声时，平台位置会略向右移（约 1.5–2×FWHM），但白噪声下的理论仍是良好的基准。

***

是否希望我帮你把这个版本导出成一份带渲染效果的 `.ipynb`（Jupyter Notebook）或 `.md` 文件？那样你直接 commit 到 GitHub 仓库里就能即看即用。



<figure><img src="../../.gitbook/assets/Screenshot 2025-11-05 193146.png" alt=""><figcaption></figcaption></figure>

