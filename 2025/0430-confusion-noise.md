# 0430-confusion noise

以下是你刚刚系统学习的 **关于 confusion noise（混淆噪声）** 的完整总结，涵盖了其定义、来源、两种判据、物理机制，以及在强度和偏振观测中的表现：

***

### 🧠 一、什么是 Confusion Noise？

> **混淆噪声**是指：由于天区内未被单独分辨出的离散天体（如点源）随机叠加所造成的背景亮度波动。

* 本质是：**天体是离散分布的，但仪器分辨率有限，无法全部 resolve**
* 表现为：即使仪器噪声为零，图像中仍有随机背景“噪声”

***

### 📐 二、两种判据（Confusion Limit Criteria）

| 判据名                          | 核心物理                             | 数学定义                                                                            | 适用场景                      |
| ---------------------------- | -------------------------------- | ------------------------------------------------------------------------------- | ------------------------- |
| **Photometric criterion**    | **测光不准**：faint sources 背景波动影响源测量 | Slim=qphot⋅σtotS\_{\text{lim\}} = q\_{\text{phot\}} \cdot \sigma\_{\text{tot\}} | 高分辨率 / 稀疏天区（如 Planck、SPT） |
| **Source density criterion** | **分不清源**：beam 中源太密分不开            | n(>Slim)⋅Ωbeam<0.1n(>S\_{\text{lim\}}) \cdot \Omega\_{\text{beam\}} < 0.1       | 低分辨率 / 源密集场（如 Herschel）   |

> 二者物理不同，是**两种独立机制下的 confusion 限制**，没有必然数值等价。

***

### 🌌 三、来源分解：三种组成成分

σconf2=σSN,rad2+σSN,ir2+σclus2\sigma\_{\mathrm{conf\}}^2 = \sigma\_{\mathrm{SN,rad\}}^2 + \sigma\_{\mathrm{SN,ir\}}^2 + \sigma\_{\mathrm{clus\}}^2

| 项                                 | 含义               | 来源        | 是否泊松型 | 是否可随分辨率改善 |
| --------------------------------- | ---------------- | --------- | ----- | --------- |
| σSN,rad\sigma\_{\mathrm{SN,rad\}} | 射电点源 shot noise  | AGN 等     | ✅ 是   | ❌ 否       |
| σSN,ir\sigma\_{\mathrm{SN,ir\}}   | DSFG shot noise  | 尘埃星系      | ✅ 是   | ❌ 否       |
| σclus\sigma\_{\mathrm{clus\}}     | clustering noise | DSFG 结构聚集 | ❌ 否   | ✅ 是       |

***

### 🔁 四、与分辨率的关系

* **Shot noise ≠ 随 beam size 变化**：只和是否 mask 掉点源有关
* **Map-domain RMS 会随 beam 缩小下降**，但 Cl 恒定
* **Clustering noise 可随分辨率改善被 resolve**

***

### 🔬 五、偏振观测中的 Confusion Noise

* 在偏振图中，未被强度图中 mask 掉的 DSFG 贡献一个背景偏振噪声：

σPconf=σconf⋅⟨ΠIR⟩（假设 σQ=σU）\sigma\_P^{\mathrm{conf\}} = \sigma\_{\mathrm{conf\}} \cdot \langle \Pi\_{\mathrm{IR\}} \rangle \quad\text{（假设 }\sigma\_Q = \sigma\_U\text{）}

* 通常采用固定偏振分数（如 ⟨ΠIR⟩=1.4%\langle \Pi\_{\mathrm{IR\}} \rangle = 1.4\\%）
* 200、350 μm 观测可能在长时间积分后达到极限 → 成为 ISM 深度偏振巡天的限制因素

***

### 📊 六、关键结论与实验对比

| 实验                        | 主导 confusion 成分        | 是否达混淆极限 |
| ------------------------- | ---------------------- | ------- |
| **Planck**                | CMB 波动主导               | 是（尤其高频） |
| **Herschel SPIRE**        | DSFG shot + clustering | 是（严重）   |
| **SPICA B-POP 200/350μm** | DSFG shot noise        | 是（深巡天）  |
| **SPICA 100μm**           | DSFG 少，偏振度低            | 否（不达极限） |

***

### ✅ 总结一句话：

> **Confusion noise 是观测深度的物理极限**，它来自无法分辨或未被去除的 faint 源。\
> 它在 total intensity 和 polarisation 中表现不同，有不同主导成分和判据，必须结合具体实验参数（分辨率、波段、mask策略）来评估是否构成实质性限制。

***
