# 251105-R\_fit value

下面给出**二维高斯模板下振幅误差 (\sigma\_a)** 的从头推导。区分两种常见“模板归一化”方式，并给出有限半径 (R) 的闭式结果（白噪声情形），最后给出相关噪声的一般化公式。

***

## 1. 观测模型与最优估计

设在一块像素区域上观测到\
\[\
\mathbf d = a,\mathbf t + \mathbf n,\
]\
其中 (\mathbf t) 为已知模板（向量，分量是各像素上的模板值），(\mathbf n\sim\mathcal N(0,,C)) 为高斯噪声，协方差 (C)。

广义最小二乘（GLS）/matched filter 的无偏最优振幅估计与方差是\
\[\
\hat a=\frac{\mathbf t^\top C^{-1}\mathbf d}{\mathbf t^\top C^{-1}\mathbf t},\qquad\
\mathrm{Var}(\hat a)=\left(\mathbf t^\top C^{-1}\mathbf t\right)^{-1}.\
\tag{1}\
]

***

## 2. 白噪声极限（像素方差 (\sigma\_{\rm pix}^2)）

白噪声：(C=\sigma\_{\rm pix}^2,I\Rightarrow C^{-1}=\sigma\_{\rm pix}^{-2}I)。代入(1)得\
\[\
\mathrm{Var}(\hat a)=\frac{\sigma\_{\rm pix}^2}{\sum\_i t\_i^2}.\
\tag{2}\
]

将像素求和写成连续极限。设像素面积为 (\Delta A)，则\
\[\
\sum\_i t\_i^2\ \approx\ \frac{1}{\Delta A}\int t^2(\boldsymbol r),d^2r,\
]\
故\
\[\
\mathrm{Var}(\hat a)\ \approx\ \sigma\_{\rm pix}^2,\frac{\Delta A}{\int t^2(\boldsymbol r),d^2r},\qquad\
\sigma\_a\equiv\sqrt{\mathrm{Var}(\hat a)}=\frac{\sigma\_{\rm pix},\sqrt{\Delta A\}}{\sqrt{\int t^2,d^2r\}}.\
\tag{3}\
]

接下来只需算 (\int t^2,d^2r)。

***

## 3. 二维高斯模板与两种归一化

常见有两种约定（请注意你拟合参数 (a) 的物理意义与所选归一化一致）：

### 3.1 “峰值归一化”（peak = 1）

\[\
t(r)=\exp!\Big(-\frac{r^2}{2\sigma^2}\Big)\quad(\text{顶峰为 }1).\
]\
在半径 (R) 的圆盘内：\
\[\
\int\_{r\<R} t^2,d^2r\
\=\int\_0^R e^{-r^2/\sigma^2},2\pi r,dr\
\=\pi\sigma^2\left(1-e^{-R^2/\sigma^2}\right).\
\tag{4}\
]\
代回(3)：\
\[\
\boxed{\ \sigma\_a(R)=\frac{\sigma\_{\rm pix},\sqrt{\Delta A\}}{\sqrt{\pi\sigma^2\left(1-e^{-R^2/\sigma^2}\right)\}}\ }.\
\tag{5}\
]\
当 (R\to\infty)：\
\[\
\boxed{\ \sigma\_a(\infty)=\frac{\sigma\_{\rm pix},\sqrt{\Delta A\}}{\sqrt{\pi},\sigma}\ }.\
\tag{6}\
]

把 FWHM 与 (\sigma) 的关系 ( \mathrm{FWHM}=2\sqrt{2\ln 2},\sigma\simeq2.355,\sigma ) 代入即可按 FWHM 表达半径。

### 3.2 “积分归一化”（unit integral；常用于把 (a) 解释为总通量/总强度）

\[\
t(r)=\frac{1}{2\pi\sigma^2}\exp!\Big(-\frac{r^2}{2\sigma^2}\Big),\quad \int t,d^2r=1.\
]\
此时\
\[\
\int t^2,d^2r\
\=\int\_0^\infty \frac{1}{4\pi^2\sigma^4}e^{-r^2/\sigma^2},2\pi r,dr\
\=\frac{1}{4\pi\sigma^2}\quad (R!\to!\infty).\
]\
有限 (R) 时有同样的截断因子 (1-e^{-R^2/\sigma^2})。于是\
\[\
\boxed{\ \sigma\_a(R)=\frac{\sigma\_{\rm pix},\sqrt{\Delta A\}}{\sqrt{(1-e^{-R^2/\sigma^2})/(4\pi\sigma^2)\}}=\sigma\_{\rm pix},\sqrt{\Delta A},\sqrt{4\pi\sigma^2},\frac{1}{\sqrt{1-e^{-R^2/\sigma^2\}}}\ }.\
\tag{7}\
]\
极限 (R\to\infty)：\
\[\
\boxed{\ \sigma\_a(\infty)=\sigma\_{\rm pix},\sqrt{\Delta A},\sqrt{4\pi},\sigma\ }.\
\tag{8}\
]\
（注意：这里的 (a) 是“总通量”参数，因而量纲和数值与 3.1 的“峰值振幅”不同，二者不应混淆。）

> 实务上你更常用 3.1（峰值归一）来讨论“振幅”的相对误差随 (R) 的变化；我们之前用到的\
> (\sigma\_a(R)\propto 1/\sqrt{1-e^{-R^2/\sigma^2\}}) 就来自(5)。

***

## 4. 为什么半径增大后误差很快饱和？

由(5)或(7)可见，半径只通过因子 (1-e^{-R^2/\sigma^2}) 进入。\
当 (R\gtrsim 3.5,\sigma) 时，(e^{-R^2/\sigma^2}\ll 10^{-5})，因此\
\[\
\sigma\_a(R)\approx \sigma\_a(\infty)\times\left(1+ \tfrac{1}{2}e^{-R^2/\sigma^2}+\cdots\right),\
]\
改进几乎不可见——这就是你用白噪声时看到的快速平台化。

***

## 5. 相关噪声的一般化（给结论形式）

若噪声是平稳相关的，(C) 在傅里叶空间对角化，功率谱为 (P\_n(\boldsymbol k))。令模板的傅里叶变换为 (\tau(\boldsymbol k))。则(1)连续极限给出\
\[\
\boxed{\ \mathrm{Var}(\hat a)^{-1}\ =\ \int \frac{|\tau(\boldsymbol k)|^2}{P\_n(\boldsymbol k)},\frac{d^2k}{(2\pi)^2}\ }.\
\tag{9}\
]\
白噪声 (P\_n(\boldsymbol k)=\text{常数}) 即退化回(3)。

***

### 小结（峰值归一、白噪声、半径 (R)）

\[\
\boxed{\ \sigma\_a(R)=\frac{\sigma\_{\rm pix},\sqrt{\Delta A\}}{\sqrt{\pi\sigma^2\left(1-e^{-R^2/\sigma^2}\right)\}}\ ,\quad\
\mathrm{FWHM}=2\sqrt{2\ln2},\sigma\ }.\
]\
这个式子正是你数值实验（白噪声下随半径迅速平台）所验证的“二维理论公式”。

下面演示**如何用公式一步步算出“理论误差 vs 拟合半径”**，并和你给的数值对上。

***

## 公式与步骤

我们用的是（二维高斯模板、白噪声、峰值归一）：\
\[\
\sigma\_a(R)\ \propto\ \frac{1}{\sqrt{\int\_{r\<R} t^2,d^2r\}}\
\=\frac{1}{\sqrt{\pi\sigma^2\bigl(1-e^{-R^2/\sigma^2}\bigr)\}},\
]\
因此**相对误差**（与“很大半径的极限”相比）为\
\[\
\boxed{\ \frac{\sigma\_a(R)}{\sigma\_a(\infty)}=\frac{1}{\sqrt{1-e^{-(R/\sigma)^2\}}}\ }.\
]

把半高全宽换成 (\sigma)：\
\[\
\mathrm{FWHM}=2\sqrt{2\ln2},\sigma \approx 2.355,\sigma\
\quad\Rightarrow\quad\
\frac{R}{\sigma} = \bigl(\text{半径是 }n\times\mathrm{FWHM}\bigr)\ \Rightarrow\ n\times 2.355.\
]

**计算步骤（任意 (n\times\mathrm{FWHM})）：**

1. 先算 (u=(R/\sigma)^2=(n\times2.355)^2)；
2. 算 (S=1-e^{-u})；
3. 相对误差因子 (=\ 1/\sqrt{S})。

***

## 代入几个你用到的半径

* **0.5×FWHM**：(R/\sigma=0.5\times2.355=1.1775)\
  (u=1.1775^2=1.386)；(,S=1-e^{-1.386}\approx 0.750)\
  (\Rightarrow\ \sigma\_a/\sigma\_a(\infty)=1/\sqrt{0.750}=**1.15466**)
* **1.0×FWHM**：(R/\sigma=2.355)\
  (u=5.551)；(S\simeq 0.99612)\
  (\Rightarrow\ \sigma\_a/\sigma\_a(\infty)=**1.00196**)
* **1.5×FWHM**：(R/\sigma=3.5325)\
  (u=12.47)；(S\simeq 0.9999962)\
  (\Rightarrow\ 1/\sqrt{S}=**1.00000190**)
* **2.0×FWHM**：(R/\sigma=4.71)\
  (u=22.18)；(S\simeq 0.9999999998)\
  (\Rightarrow\ **≈1.00000000**)
* **2.5×FWHM**：(R/\sigma=5.8875)\
  (u=34.65)；(S\to 1)\
  (\Rightarrow\ **≈1.00000000**)

> 这些是**相对误差因子**；常数（像素噪声、像素面积、(\pi\sigma^2)）在比值里都消掉了。

***

## 和你给的“绝对误差”对比

你这组（白噪声，无 CMB）：

```
[12.4791273, 10.7745043, 10.7548005, 10.75477918, 10.75477899]
对应半径: 0.5, 1.0, 1.5, 2.0, 2.5 ×FWHM
```

把 **2.5×FWHM** 当作“极限”（基准）：

* 理论预测 = 基准 × 上述“相对误差因子”。\
  用 2.5×FWHM 的 10.75477899 作为基准，可得
  * 0.5×FWHM：(10.75477899 \times 1.15465977 \approx \mathbf{12.4181})
  * 1.0×FWHM：(\approx \mathbf{10.77583})
  * 1.5×FWHM：(\approx \mathbf{10.7547995})
  * 2.0×FWHM：(\approx \mathbf{10.7547790})
  * 2.5×FWHM：(\approx \mathbf{10.7547790})

和你的数值逐项对齐：

* 0.5×FWHM：**12.4181（理） vs 12.4791（实）**，相差 \~0.5%
* 1.0×FWHM：**10.7758 vs 10.7745**，差 \~0.013%
* 1.5×FWHM、2.0×FWHM、2.5×FWHM：基本完全一致

> 这说明你的白噪声实验与二维理论非常吻合；0.5×FWHM 的微小偏差通常来自像素化/采样或数值因素。

***

### 一句总结

用\
\[\
\boxed{\ \frac{\sigma\_a(R)}{\sigma\_a(\infty)}=\frac{1}{\sqrt{1-e^{-(n\times2.355)^2\}}}\ }\
]\
直接就能把“半径 = (n\times)FWHM” 的**理论相对误差**算出来，再乘上你任取的基准（如 2.5×FWHM 的实测误差）即可得到**理论绝对误差**，与实测高度一致。



