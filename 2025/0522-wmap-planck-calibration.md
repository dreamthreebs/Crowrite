# 0522-WMAP-PLANCK calibration

下面是**CMB 实验中的绝对标定（absolute calibration）** 的完整总结，重点聚焦于 **WMAP 和 Planck 的标定策略**，包括 **solar dipole 与 orbital dipole 的作用与关系**：

***

## 🌌 CMB 绝对标定总结：以 WMAP 与 Planck 为例

***

### 📌 1. 什么是绝对标定？

**绝对标定**是指将 CMB 探测器输出的原始信号（单位为 V、counts、ADU 等）转换为物理温度单位（如 μK），以便：

* 正确估计 CMB 的功率谱 CℓC\_\ell；
* 执行宇宙学参数推断（如 AsA\_s、σ8\sigma\_8、rr 等）。

***

### 📡 2. 标定信号的来源：两种 dipole

| Dipole 类型          | 来源                 | 振幅        | 是否可预测    | 用途                  |
| ------------------ | ------------------ | --------- | -------- | ------------------- |
| **Solar dipole**   | 太阳系质心相对于 CMB 静止系运动 | \~3365 µK | ❌ 否，需要测量 | **最常用的绝对标定源**       |
| **Orbital dipole** | 卫星围绕太阳系质心轨道运动调制    | \~270 µK  | ✅ 是，非常精确 | **高精度标定参考（Planck）** |

***

### 🔹 3. WMAP 的标定方式：Solar Dipole 为主

* 使用 WMAP 自己或早期 COBE 测得的 Solar dipole；
* 每年的扫描策略保证可以独立拟合 dipole，获得增益；
* 得益于 Solar dipole 振幅大（SNR 高）；
* 缺点是需要假设 Solar dipole 的**真实方向与振幅是已知的或需自测**。

***

### 🔹 4. Planck 的标定方式转变：从 Solar 到 Orbital

#### 📍 Planck 2013：

* 初期依然使用 WMAP 测得的 Solar dipole（COBE → WMAP → Planck）；
* 用于为 HFI/LFI 的增益提供初始标定。

#### 📍 Planck 2015+：

* 开始完全依赖 **轨道偶极（orbital dipole）进行 self-calibration**；
* 利用已知的卫星轨道速度，构建理论 dipole 模板；
*   假设：

    ΔTorb(n^,t)=TCMB⋅v⃗orb(t)⋅n^c\Delta T\_{\text{orb\}}(\hat{n}, t) = T\_{\text{CMB\}} \cdot \frac{\vec{v}\_{\text{orb\}}(t) \cdot \hat{n\}}{c}
*   这里的 TCMBT\_{\text{CMB\}} 来自 **COBE-FIRAS 测量**：

    TCMB=2.7255±0.0006 KT\_{\text{CMB\}} = 2.7255 \pm 0.0006\\, \text{K}

***

### 🔍 5. 使用 orbital dipole 做标定时的技术关键

* 轨道速度 v⃗orb\vec{v}\_{\text{orb\}} 来自精密星历（误差极小）；
* orbital dipole 年周期调制，容易从 TOD 中提取；
* 但其振幅较小（\~270 μK），需要**极高的仪器灵敏度**；
* Planck 满足这一条件，能以 orbital dipole 为主完成 photometric calibration。

***

### ⚠️ 6. CMB 温度 TCMBT\_{\text{CMB\}} 的作用

* orbital dipole 是 ΔT/T\Delta T / T，需要用 FIRAS 的 TCMBT\_{\text{CMB\}} 转换为实际温度单位（µK）；
* 因此，**标定精度最终受限于我们对 CMB 温度的了解**；
*   Planck 在文献中明确使用：

    > _“Using a CMB temperature of TCMB=2.7255 KT\_{\text{CMB\}} = 2.7255\\, \text{K}, we predict the orbital dipole…”_

***

### 🧪 7. 标定完成后可以反推出 Solar dipole

* Planck 通过 orbital dipole 标定后，反过来从校准后的 sky map 中**拟合 Solar dipole**；
* 得到目前最精确的 Solar dipole 参数（方向精度优于 0.01°）；
* 比 WMAP 更稳定，也成为后续实验的参考。

***

### ✅ 总结表

| 实验           | 标定主策略                            | 使用的 dipole 类型 | 是否使用 FIRAS TCMBT\_{\text{CMB\}} |
| ------------ | -------------------------------- | ------------- | ------------------------------- |
| WMAP         | Solar dipole                     | 直接用于标定        | ❌（自测 dipole）                    |
| Planck 2013  | Solar dipole（WMAP 参考）            | 用于初期标定        | ✅（隐式使用）                         |
| Planck 2015+ | Orbital dipole（self-calibration） | 主标定源          | ✅（用于归一化 orbital dipole）         |

***

