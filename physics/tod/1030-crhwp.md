# 1030-CRHWP

好的，下面是一个**结构化、简洁且专业的笔记版本**，包括关键原理、公式和符号定义，适合直接放入科研笔记或论文附录中。

***

### 🌀 Principle of the Continuously Rotating Half-Wave Plate (CRHWP)

A **Continuously Rotating Half-Wave Plate (CRHWP)** is used in CMB polarization experiments to modulate and separate the Stokes parameters (I, Q, U).\
It enables a **single polarization-sensitive detector** to measure all components and **suppresses 1/f noise** and systematics arising from detector mismatch.

***

#### **1. Polarization modulation by HWP**

A **half-wave plate (HWP)** rotates the polarization angle of incident radiation by twice its birefringent axis angle.\
If the incoming polarization angle is (\theta\_{\text{in\}}) and the HWP axis is at angle (\theta\_{\text{HWP\}}), then after transmission:

\[\
\theta\_{\text{out\}} = 2\theta\_{\text{HWP\}} - \theta\_{\text{in\}}.\
]

When the HWP rotates continuously with angular velocity (\omega\_{\text{HWP\}}),\
the polarization angle is modulated as:

\[\
2\theta\_{\text{HWP\}}(t) = 2\omega\_{\text{HWP\}} t.\
]

In terms of Stokes parameters:

\[\
Q\_{\text{out\}}(t) - iU\_{\text{out\}}(t)\
\= \[Q\_{\text{in\}}(t) + iU\_{\text{in\}}(t)] , m(t),\
]\
where the **modulation function**\
\[\
m(t) \equiv e^{-i\omega\_{\text{mod\}} t}, \quad \omega\_{\text{mod\}} = 4\omega\_{\text{HWP\}}.\
]

The factor of 4 arises because linear polarization is a **spin-2** quantity — a rotation of the optical element by (\theta\_{\text{HWP\}}) causes a (4\theta\_{\text{HWP\}}) phase shift in the polarization signal.

***

#### **2. Detector timestream with modulation**

The signal measured by a polarization-sensitive detector is:

\[\
d\_m(t) =\
\delta I\_{\text{in\}}(t)

* \varepsilon , \mathrm{Re}!\left{\
  \[Q\_{\text{in\}}(t) + iU\_{\text{in\}}(t)] ,\
  m(t) , e^{-2i\theta\_{\text{det\}}}\
  \right}
* N\_m(t),\
  \tag{2.2}\
  ]

where

* (\delta I\_{\text{in\}}(t) = I\_{\text{in\}}(t) - \langle I\_{\text{in\}}\rangle) is the fluctuating intensity,
* (\varepsilon) is the polarization modulation efficiency,
* (\theta\_{\text{det\}}) is the detector orientation angle,
* (N\_m(t)) is the white noise.

Only the **fluctuating component** (\delta I\_{\text{in\}}) is measurable; the absolute baseline is typically filtered out.

***

#### **3. Demodulation process**

If the HWP rotation frequency is higher than the scan speed divided by the beam size, the intensity and polarization signals can be separated by **frequency-domain demodulation**:

\[\
\bar{d}_m(t) \equiv \mathrm{FLPF}{d\_m(t)}_\
&#xNAN;_= \delta I_{\text{in\}}(t) + \bar{N}\_m(t),\
\tag{2.3}\
]

\[\
\bar{d}_d(t) \equiv_\
&#xNAN;_\mathrm{FLPF}{d\_m(t) , 2m^\*(t)e^{2i\theta_{\text{det\}}\}}\
\= \varepsilon\[Q\_{\text{in\}}(t) + iU\_{\text{in\}}(t)]

* N\_{\bar{d\}}^{(\mathrm{Re})}(t)
* iN\_{\bar{d\}}^{(\mathrm{Im})}(t),\
  \tag{2.4}\
  ]

where

* **FLPF** denotes a low-pass filter (cutoff ≈ rotation frequency or its double),
* (m^\*(t)) is the complex conjugate of (m(t)),
* (\bar{d}\_m(t)) and (\bar{d}\_d(t)) are the recovered **intensity** and **polarization** signals, respectively.

Noise decomposition satisfies:

\[\
\langle \[N\_{\bar{d\}}^{(\mathrm{Re})}]^2 \rangle\
\= \langle \[N\_{\bar{d\}}^{(\mathrm{Im})}]^2 \rangle\
\= 2 \langle \[\bar{N}\_m]^2 \rangle \equiv 2N.\
]

***

#### **4. Physical picture**

* The CRHWP continuously modulates the sky polarization at (4f\_{\text{HWP\}}), shifting (Q, U) signals to a higher frequency band where 1/f noise is minimal.
* The total intensity (I) remains at DC (unmodulated).
* Demodulation recovers (Q, U) from the modulated timestream using the known reference function (m(t)).
* In real systems, optical non-idealities and detector nonlinearity cause **intensity-to-polarization (I→P) leakage** and **instrumental polarization**, which must be characterized and corrected.

***

Would you like me to add a small schematic explanation (text version) — e.g. how frequency spectra look before and after modulation (I at DC, Q/U at 4fₕwₚ)? It’s useful if this note is going into a presentation or documentation.
