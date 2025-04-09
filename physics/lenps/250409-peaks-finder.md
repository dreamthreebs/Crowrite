# 250409-peaks finder

**connected objects** (or "blobs")

### 1. peak finder

* tips: maybe find peak after denoise is better?
* todo: implement spherical peak finder maybe better?

### 2. denoise

### 🌀 Needlet-Based Denoising for CMB Maps

#### 📌 Overview

Needlets are spherical wavelets localized in both harmonic and pixel space. Denoising in needlet space leverages their multiscale nature to suppress noise without overly smoothing the signal.

***

### 🔹 Hard/Soft Thresholding in Needlet Space

#### 1. **Needlet Transform**

Decompose the map $T(\hat{n})$ into needlet coefficients:

$$
\beta_{jk} = \int_{S^2} T(\hat{n}) \, \psi_{jk}(\hat{n}) \, d\Omega
$$

#### 2. **Thresholding Rules**

**Hard Thresholding**

$$
\tilde{\beta}_{jk} =
\begin{cases}
\beta_{jk}, & \text{if } |\beta_{jk}| > \lambda_j \\
0, & \text{otherwise}
\end{cases}
$$

**Soft Thresholding**

$$
\tilde{\beta}_{jk} =
\begin{cases}
\text{sign}(\beta_{jk}) (|\beta_{jk}| - \lambda_j), & \text{if } |\beta_{jk}| > \lambda_j \\
0, & \text{otherwise}
\end{cases}
$$

> Threshold $\lambda\_j$ is often chosen based on the noise level at scale $j$, e.g.,
>
> $$
> \lambda_j = \sigma_j \sqrt{2 \log N_j}
> $$

#### 3. **Reconstruction**

$$
\tilde{T}(\hat{n}) = \sum_{j,k} \tilde{\beta}_{jk} \, \psi_{jk}(\hat{n})
$$

***

### 🔹 Bayesian Shrinkage in Needlet Space

#### Model Setup

Assume noisy coefficients:

$$
\beta_{jk}^{\text{obs}} = \beta_{jk}^{\text{true}} + \epsilon_{jk}, \quad \epsilon_{jk} \sim \mathcal{N}(0, \sigma_{jk}^2)
$$

With prior:

$$
\beta_{jk}^{\text{true}} \sim \mathcal{N}(0, \tau_j^2)
$$

#### Posterior Mean (Shrinkage Estimator)

$$
\tilde{\beta}_{jk} = \frac{\tau_j^2}{\tau_j^2 + \sigma_{jk}^2} \, \beta_{jk}^{\text{obs}}
$$

This is equivalent to Wiener filtering in needlet space.

***

### ✅ Comparison Summary

| Method             | Thresholding  | Local Adaptivity | Bayesian | Continuous Output |
| ------------------ | ------------- | ---------------- | -------- | ----------------- |
| Hard Thresholding  | Yes           | Yes              | No       | No                |
| Soft Thresholding  | Yes           | Yes              | No       | Yes               |
| Bayesian Shrinkage | No (implicit) | Yes              | Yes      | Yes               |
