# 0612-MASTER

哈哈你问得好，“这尼玛怎么构造出来的”——确实，最优二次估计器（optimal quadratic estimator, OQE）这个公式看起来就像天上掉下来的。现在我们就来认真回答这个问题：**它到底是怎么推导出来的？**

***

### 🎯 目标：从数据中估计功率谱 CℓC\_\ell

我们有观测数据：

a=某个随机高斯场（CMB、星系密度等）在像素空间的值\mathbf{a} = \text{某个随机高斯场（CMB、星系密度等）在像素空间的值}

我们知道这个场的协方差满足：

⟨aa⊤⟩=C(Cℓ)\langle \mathbf{a} \mathbf{a}^\top \rangle = \mathbf{C}(C\_\ell)

我们要估计的是功率谱 CℓC\_\ell，或者说某几个 bandpowers BiB\_i，它们控制协方差矩阵 C\mathbf{C} 的强度。

***

### 🧠 核心思想：最大似然估计

如果这个场是**高斯的**，它的概率密度就是：

L(a;{Bi})=1(2π)N/2∣C∣1/2exp⁡(−12a⊤C−1a)\mathcal{L}(\mathbf{a}; \\{B\_i\\}) = \frac{1}{(2\pi)^{N/2} |\mathbf{C}|^{1/2\}} \exp\left( -\frac{1}{2} \mathbf{a}^\top \mathbf{C}^{-1} \mathbf{a} \right)

#### 👉 那么我们可以最大化对数似然：

ln⁡L=−12(a⊤C−1a+ln⁡∣C∣+const)\ln \mathcal{L} = -\frac{1}{2} \left( \mathbf{a}^\top \mathbf{C}^{-1} \mathbf{a} + \ln |\mathbf{C}| + \text{const} \right)

我们的目标是：找出一组 BiB\_i 使得这个对数似然最大。换句话说，我们想求：

∂ln⁡L∂Bi=0\frac{\partial \ln \mathcal{L\}}{\partial B\_i} = 0

***

### 🧮 推导导数：

注意 C=∑iBiPi+N\mathbf{C} = \sum\_i B\_i \mathbf{P}\_i + \mathbf{N}

然后我们用矩阵求导法则（熟悉 trace trick）：

∂ln⁡∣C∣∂Bi=Tr⁡(C−1∂C∂Bi)=Tr⁡(C−1Pi)\frac{\partial \ln |\mathbf{C}|}{\partial B\_i} = \operatorname{Tr} \left( \mathbf{C}^{-1} \frac{\partial \mathbf{C\}}{\partial B\_i} \right) = \operatorname{Tr} \left( \mathbf{C}^{-1} \mathbf{P}\_i \right) ∂∂Bi(a⊤C−1a)=−a⊤C−1PiC−1a\frac{\partial}{\partial B\_i} \left( \mathbf{a}^\top \mathbf{C}^{-1} \mathbf{a} \right) = -\mathbf{a}^\top \mathbf{C}^{-1} \mathbf{P}\_i \mathbf{C}^{-1} \mathbf{a}

于是，

∂ln⁡L∂Bi=12\[a⊤C−1PiC−1a−Tr⁡(C−1Pi)]\frac{\partial \ln \mathcal{L\}}{\partial B\_i} = \frac{1}{2} \left\[ \mathbf{a}^\top \mathbf{C}^{-1} \mathbf{P}\_i \mathbf{C}^{-1} \mathbf{a} - \operatorname{Tr} \left( \mathbf{C}^{-1} \mathbf{P}\_i \right) \right]

***

### ✅ 这就是最优估计器的来历！

我们记：

q^i≡12(a⊤C−1PiC−1a−Tr⁡\[C−1Pi])\hat{q}\_i \equiv \frac{1}{2} \left( \mathbf{a}^\top \mathbf{C}^{-1} \mathbf{P}\_i \mathbf{C}^{-1} \mathbf{a} - \operatorname{Tr} \[\mathbf{C}^{-1} \mathbf{P}\_i] \right)

这玩意是对 BiB\_i 的梯度。如果你想估计 BiB\_i，可以用牛顿法或 Fisher 矩阵反推：

***

### 🧠 Fisher 矩阵又是怎么来的？

再对上面的导数再求一遍导数：

Fij=−⟨∂2ln⁡L∂Bi∂Bj⟩=12Tr⁡(C−1PiC−1Pj)F\_{ij} = - \left\langle \frac{\partial^2 \ln \mathcal{L\}}{\partial B\_i \partial B\_j} \right\rangle = \frac{1}{2} \operatorname{Tr} \left( \mathbf{C}^{-1} \mathbf{P}\_i \mathbf{C}^{-1} \mathbf{P}\_j \right)

于是，我们就得到了完整的估计框架：

*   有估计量（score function）：

    q^i=12a⊤C−1PiC−1a−12Tr⁡\[C−1Pi]\hat{q}\_i = \frac{1}{2} \mathbf{a}^\top \mathbf{C}^{-1} \mathbf{P}\_i \mathbf{C}^{-1} \mathbf{a} - \frac{1}{2} \operatorname{Tr} \[\mathbf{C}^{-1} \mathbf{P}\_i]
*   有 Fisher 矩阵：

    Fij=12Tr⁡\[C−1PiC−1Pj]F\_{ij} = \frac{1}{2} \operatorname{Tr} \[\mathbf{C}^{-1} \mathbf{P}\_i \mathbf{C}^{-1} \mathbf{P}\_j]
*   所以估计：

    B^i=∑jFij−1q^j\hat{B}\_i = \sum\_j F^{-1}\_{ij} \hat{q}\_j

***

### 💬 这就是你问的：“这玩意怎么构造出来的？”

**它不是拍脑袋想出来的，而是从最大似然估计（对数高斯似然）出发，推导出来的。**

这套推导几乎是标准教材内容，在 CMB 和 LSS 文献中非常常见。

***

### 📘 延伸阅读

* Tegmark (1997), “How to measure CMB power spectra without losing information”
* Bond, Jaffe & Knox (1998), “Estimating the power spectrum of the CMB”

***

如果你想我写一个简单例子，比如用 numpy 模拟一个小像素系统、构建 C\mathbf{C}、算估计器，我也可以写出来给你跑。要不要来一个？
