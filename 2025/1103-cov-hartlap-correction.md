# 1103-COV hartlap correction

非常好的问题 👍。

我们来仔细说明一下为什么\*\*样本协方差矩阵（sample covariance matrix）\*\*在求逆时会产生 bias。

***

### 🧩 1️⃣ 背景：什么是样本协方差

假设我们有 (N\_s) 个独立样本 (\mathbf{d}\_k)（每个是维度为 (p) 的向量），它们来自某个真实协方差为 (\mathbf{C}) 的高斯分布：\
\[\
\mathbf{d}\_k \sim \mathcal{N}(0, \mathbf{C})\
]

我们用常规方式估计协方差：\
\[\
\widehat{\mathbf{C\}} = \frac{1}{N\_s - 1} \sum\_{k=1}^{N\_s}\
(\mathbf{d}\_k - \bar{\mathbf{d\}})(\mathbf{d}\_k - \bar{\mathbf{d\}})^{!\top}\
]\
其中 (\bar{\mathbf{d\}}) 是样本均值。

这个 (\widehat{\mathbf{C\}}) 是对 (\mathbf{C}) 的**无偏估计量**，即：\
\[\
\mathbb{E}\[\widehat{\mathbf{C\}}] = \mathbf{C}.\
]\
到这里一切正常。

***

### 🧩 2️⃣ 问题出现在求逆时

我们通常需要用到**精度矩阵（precision matrix）** (\mathbf{\Psi} = \mathbf{C}^{-1})，\
但在实际中只能用样本协方差的逆 (\widehat{\mathbf{C\}}^{-1}) 近似它。\
这一步才是 bias 的来源。

原因是 (\widehat{\mathbf{C\}}) 本身是一个随机矩阵，它服从 **Wishart 分布**：\
\[\
\widehat{\mathbf{C\}} \sim \frac{1}{N\_s - 1} \mathcal{W}\_p(\mathbf{C}, N\_s - 1),\
]\
其中 (p) 是维度，(N\_s-1) 是自由度。

Wishart 分布的数学性质告诉我们：\
\[\
\mathbb{E}\[\widehat{\mathbf{C\}}^{-1}] \neq \mathbf{C}^{-1}.\
]

更精确地说：\
\[\
\mathbb{E}\[\widehat{\mathbf{C\}}^{-1}] =\
\frac{N\_s - 1}{N\_s - p - 2},\mathbf{C}^{-1},\
\quad \text{当 } N\_s > p + 2.\
]\
也就是说，(\widehat{\mathbf{C\}}^{-1}) **系统性地偏小（即低估协方差的逆）**。

***

### 🧩 3️⃣ Hartlap 校正因子

为了消除这种偏差，通常引入一个缩放系数：\
\[\
\alpha\_H = \frac{N\_s - p - 2}{N\_s - 1},\
]\
然后使用：\
\[\
\mathbf{\Psi} = \alpha\_H ,\widehat{\mathbf{C\}}^{-1}.\
]\
这个修正是由 **Hartlap, Simon & Schneider (2007, A\&A 464, 399)** 提出的，被广泛用于宇宙学参数估计（Planck、DES、KiDS、ACT 等都在用）。

***

### 🧩 4️⃣ 直观理解

你可以这样理解：

* 我们用有限样本估计协方差 → 有统计波动；
* 对于多维分布，这种波动会“放大”在矩阵逆的操作中；
* 结果是：(\widehat{C}^{-1}) 平均值偏大于真值；
* Hartlap 因子通过缩放修正这个偏差。

***

### 🧩 5️⃣ 举例

如果：

* 模拟数 (N\_s = 200)，
* bandpower 维度 (p = 10)，

则：\
\[\
\alpha\_H = \frac{200 - 10 - 2}{199} \approx 0.94.\
]\
也就是说，不校正时 (\widehat{C}^{-1}) 会高估真实的 (\mathbf{C}^{-1}) 约 6%。

***

### ✅ 总结

| 项目                               | 是否无偏                                                        |
| -------------------------------- | ----------------------------------------------------------- |
| 样本协方差 (\widehat{C})              | ✅ 无偏 ((\mathbb{E}\[\widehat{C}] = C))                       |
| 样本逆协方差 (\widehat{C}^{-1})        | ❌ 有偏 ((\mathbb{E}\[\widehat{C}^{-1}] \neq C^{-1}))          |
| 校正后 (\alpha\_H \widehat{C}^{-1}) | ✅ 期望无偏 ((\mathbb{E}\[\alpha\_H \widehat{C}^{-1}] = C^{-1})) |

***

是否希望我帮你画一张简单的图（比如 1D 或 2D 示例）展示这个 bias 的数值差异？那样可以在回复或补充材料里直观展示 “为何要 Hartlap 修正”。
