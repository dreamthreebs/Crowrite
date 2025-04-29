# 0428-Radio galaxy

明白了！你的要求很专业：\
——不仅总结blazar建模，还要把今天讲过的**shot noise、radio point sources、CIB、DSFG贡献**也系统总结进去。

这很合理，因为今天确实跨了两个主线：**源的物理建模** + **它们在CMB前景里的贡献方式**。

好的，我来帮你补充并整理一版**更完整、更结构化**的总结：\
（直接是适合保存或复习的笔记版）

***

## 📚 今天完整学习总结（Blazar建模 + 射电源与CIB前景贡献）

***

### 1. 基本概念：射电源（Radio Point Sources）和DSFG（尘埃星形成星系）

| 类别                                | 主要源          | 主要波段                   | 特点              | CMB前景贡献类型                         |
| --------------------------------- | ------------ | ---------------------- | --------------- | --------------------------------- |
| 射电源（Radio Point Sources）          | FSRQ, BL Lac | GHz–低毫米波（\~30–150 GHz） | 点状、离散、强偏振、数量较稀疏 | shot noise主导                      |
| DSFG（Dusty Star-Forming Galaxies） | 高红移星系        | 亚毫米波（\~150–1000 GHz）   | 大量、暗弱、有聚集性、弱偏振  | shot noise + clustering (CIB各向异性) |

***

### 2. 什么是 Shot Noise？

* **Shot noise**：源的**离散性**导致的不可避免亮度涨落。
* 在功率谱上表现为一条**常数平坦谱（Cℓ flat）**。
* 来源：
  * 少量极亮的离散源（radio source dominated）
  * 大量暗弱的未分辨源（DSFG dominated）

**Shot noise功率公式：**

Cℓshot=∫0ScutS2dNdSdSC\_\ell^{\mathrm{shot\}} = \int\_0^{S\_{\mathrm{cut\}}} S^2 \frac{dN}{dS} dS

其中：

* SS：源流量；
* dN/dSdN/dS：单位流量源数密度；
* ScutS\_{\mathrm{cut\}}：流量剪切（mask掉明亮源后的剩余部分）。

***

### 3. 为什么需要 flux cut？

* 射电源的shot noise**极度敏感**于流量剪切（亮源贡献大）。
* DSFG的shot noise**对flux cut不敏感**（因为暗源贡献主导）。
* **实际操作**：
  * 去掉S>ScutS>S\_{\mathrm{cut\}}的亮源以降低射电shot noise；
  * 剩下的shot noise由暗源构成。

***

### 4. CIB（Cosmic Infrared Background）贡献

CIB功率谱可以分为两部分：

CℓCIB=Cℓ1h+Cℓ2hC\_\ell^{\mathrm{CIB\}} = C\_\ell^{\mathrm{1h\}} + C\_\ell^{\mathrm{2h\}}

| 成分            | 描述             | 特点    |
| ------------- | -------------- | ----- |
| One-halo term | 同一个暗晕内星系之间的相关  | 小尺度主导 |
| Two-halo term | 不同暗晕星系之间的大尺度相关 | 大尺度主导 |

* **CIB shot noise** ≈ 极大量未分辨DSFG源的离散涨落；
* **CIB clustering** ≈ DSFG沿着宇宙大尺度结构（filaments, walls）排列。

***

### 5. Blazar (Radio Source) 频谱建模

* 低频（GHz）用平谱（α∼0\alpha \sim 0）；
* 高频（>10–100 GHz）出现**spectral steepening**（谱变陡）。

谱断点（break frequency νM\nu\_M）：

νM∝δ B1/5 l−4/5(1+z)−1\nu\_M \propto \delta \\, B^{1/5} \\, l^{-4/5} (1+z)^{-1}

其中：

* δ\delta：都卜勒因子
* BB：磁场
* ll：发射区大小
* zz：红移

不同blazar种群的谱断点特性：

| 类别     | 典型谱断点νM\nu\_M | 发射区大小 rMr\_M        |
| ------ | ------------- | ------------------- |
| FSRQ   | 10–100 GHz    | 0.3–10 pc           |
| BL Lac | >100>100 GHz  | 0.0025–0.05 pc（更新后） |

***

### 6. 更新版C2Ex模型的主要调整

| 变量                                                | 旧版          | 更新版            | 物理意义             |
| ------------------------------------------------- | ----------- | -------------- | ---------------- |
| BL Lac的rMr\_M                                     | 0.01–0.3 pc | 0.0025–0.05 pc | 发射区更致密，延迟到更高频才变陡 |
| 高频谱指数 ⟨αst⟩\langle \alpha\_{\mathrm{st\}} \rangle | -0.8        | -0.7           | 辐射下降更慢，高频数量计数增加  |

* **改善**了在95/150 GHz频段、20–60 mJy流量区间与SPT/ACT观测数据的拟合。
* 使得整体拟合χ2\chi^2接近1，预测更准确。

***

## 📈 总结今天重点的公式

1. **Shot noise功率谱**：

Cℓshot=∫0ScutS2dNdSdSC\_\ell^{\mathrm{shot\}} = \int\_0^{S\_{\mathrm{cut\}}} S^2 \frac{dN}{dS} dS

2. **频谱外推（考虑断点）**：

Sν=Sν0×{(νν0)α1,ν<νM(νMν0)α1(ννM)α2,ν>νMS\_{\nu} = S\_{\nu\_0} \times \begin{cases} \left( \frac{\nu}{\nu\_0} \right)^{\alpha\_1}, & \nu < \nu\_M \\\ \left( \frac{\nu\_M}{\nu\_0} \right)^{\alpha\_1} \left( \frac{\nu}{\nu\_M} \right)^{\alpha\_2}, & \nu > \nu\_M \end{cases}

其中α1∼0\alpha\_1 \sim 0，α2∼−0.7\alpha\_2 \sim -0.7（更新后）。

3. **谱断点频率与物理量关系**：

νM∝δ B1/5 l−4/5(1+z)−1\nu\_M \propto \delta \\, B^{1/5} \\, l^{-4/5} (1+z)^{-1}

***

## ✏️ 最后整体小总结

> 今天你系统掌握了：
>
> * 射电点源（FSRQ/BL Lac）和尘埃星系（DSFG）对CMB前景的贡献方式；
> * shot noise、flux cut、clustering的本质物理来源；
> * 频谱在高频出现断点，并且blazar两类族群（FSRQ vs BL Lac）需要不同建模；
> * 如何通过调节rMr\_M和αst\alpha\_{\mathrm{st\}}来精准拟合SPT/ACT/Planck观测，提升CMB foreground modeling的准确性。

***

