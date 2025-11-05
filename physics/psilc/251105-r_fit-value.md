# 251105-R\_fit value

当然可以。下面是一个你可以直接放在 GitHub README 或文档里的版本（公式用 `$$...$$`，如果你想在本地或 Jupyter Notebook 中看，会正常渲染；在 GitHub 上可改成我前面提到的图片链接方式）。

***

### 📘 理论推导：二维高斯模板下的振幅误差

观测模型：\
\$$\
\mathbf d = a,\mathbf t + \mathbf n,\
\$$\
其中噪声为零均值高斯随机场，协方差矩阵为 ( C )。

广义最小二乘（GLS）最优估计为：\
\$$\
\hat a = \frac{\mathbf t^\top C^{-1}\mathbf d}{\mathbf t^\top C^{-1}\mathbf t},\
\qquad\
\mathrm{Var}(\hat a) = \frac{1}{\mathbf t^\top C^{-1}\mathbf t}.\
\$$

***

#### 白噪声极限

白噪声：( C = \sigma\_{\rm pix}^2 I )，于是

\$$\
\mathrm{Var}(\hat a)\
\= \frac{\sigma\_{\rm pix}^2}{\int t^2(\mathbf r), d^2r}.\
\$$

对于峰值归一化的二维高斯模板\
\$$\
t(r) = e^{-r^2/(2\sigma^2)},\
\$$\
有限半径 ( R ) 内的平方积分为\
\$$\
\int\_{r\<R} t^2, d^2r = \pi\sigma^2 \bigl(1 - e^{-R^2/\sigma^2}\bigr).\
\$$

因此得到振幅误差的理论公式：

\$$\
\boxed{\
\sigma\_a(R)\
\= \frac{\sigma\_{\rm pix}\sqrt{\Delta A\}}{\sqrt{\pi\sigma^2\left(1 - e^{-R^2/\sigma^2}\right)\}}\
}\
\$$

相对误差（相对于无限大视场）：

\$$\
\boxed{\
\frac{\sigma\_a(R)}{\sigma\_a(\infty)} =\
\frac{1}{\sqrt{1 - e^{-(R/\sigma)^2\}}}.\
}\
\$$

***

#### 按 FWHM 表示

高斯的半高全宽：\
\$$\
\mathrm{FWHM} = 2\sqrt{2\ln 2},\sigma \approx 2.355,\sigma,\
\$$\
所以对于半径 ( R = n\times\mathrm{FWHM} )，有\
\$$\
\frac{R}{\sigma} = 2.355,n.\
\$$

***

### 📊 理论预测 vs 实测结果（白噪声）

实验中测得的拟合误差（无 CMB，仅白噪声）：

|    半径    |   理论相对误差  | 理论误差（以 2.5×FWHM 的 10.7548 为基准） |     实测误差    |
| :------: | :-------: | :----------------------------: | :---------: |
| 0.5×FWHM |  1.15466  |             12.418             |  **12.479** |
| 1.0×FWHM |  1.00196  |             10.776             | **10.7745** |
| 1.5×FWHM | 1.0000019 |             10.7548            | **10.7548** |
| 2.0×FWHM | 1.0000000 |             10.7548            | **10.7548** |
| 2.5×FWHM | 1.0000000 |             10.7548            | **10.7548** |

***

### ✅ 总结

* 理论预测来自\
  \$$\
  \frac{\sigma\_a(R)}{\sigma\_a(\infty)} = \frac{1}{\sqrt{1 - e^{-(R/\sigma)^2\}}}.\
  \$$
* 当半径 ≥ 1×FWHM 后，误差已基本饱和；
* 实测与理论完全吻合（相差 <0.5%），验证了二维高斯 + 白噪声模型的正确性；
* 因此在无相关噪声情况下，取 ( R \gtrsim 1.5\times\mathrm{FWHM} ) 即可达到最优精度；
* 任何更大的拟合区域都不会明显降低振幅误差。

***

是否希望我帮你把这一版改成 **GitHub 100% 可预览版（公式转为 SVG 链接）**？那样你直接放 README 里也能看到渲染好的公式。



