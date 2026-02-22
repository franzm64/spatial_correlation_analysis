# Spatial Correlation Analysis of 2D Random Fields

*A minimal, reproducible framework for multi-scale spatial structure characterization*

## Motivation

Spatial organization is a defining feature of many natural systems. In quantitative microscopy, spatial patterns of intensity or density (e.g., chromatin organization within the nucleus) encode structural information that must be extracted from noisy, finite-resolution measurements.

A central question is:

> How can we quantitatively characterize spatial structure and correlation length in two-dimensional intensity fields?

This repository provides a minimal, self-contained implementation of:

- Simulation of spatially correlated 2D random fields
- Estimation of spatial autocorrelation functions
- Spectral (Fourier-based) analysis
- Radial averaging of power spectra
- Correlation length estimation

The goal is not biological interpretation, but demonstration of mathematically transparent and reproducible spatial analysis methods that are directly applicable to quantitative imaging data.

## Mathematical Background

**1. Gaussian Random Fields**

We generate stationary, isotropic Gaussian random fields $u(x,y)$ with prescribed covariance structure:

$$
C(r) = \sigma^2 \exp⁡ \left(-\frac{r}{l} \right),
$$

where

- $r = \sqrt(x^2+y^2)$
- $\ell$ is the correlation length
- $\sigma^2$ is the variance

Alternative covariance models (e.g., squared exponential) can be substituted.

---

**2. Spectral Representation**

By the [Wiener–Khinchin theorem](https://en.wikipedia.org/wiki/Wiener%E2%80%93Khinchin_theorem), the power spectral density 
$S(k)$ is the Fourier transform of the autocovariance function:

$$
S(k) = \mathcal{F}\{ C(r)\}
$$

We generate correlated fields via spectral synthesis:

1. Sample white noise in Fourier space
2. Scale by $\sqrt{S(k)}$
3. Apply inverse FFT

This ensures correct second-order statistics.

---

**3. Autocorrelation Estimation**

Given a simulated field $u(x,y)$, we estimate the empirical autocorrelation:

$$
R(\Delta x, \Delta y) = \mathbb{E} \left[ u(x,y)u(x+\Delta x, y + \Delta y)\right]
$$

computed efficiently using FFT-based convolution.

Radial averaging produces an isotropic correlation function $R(r)$.

---

**4. Correlation Length Estimation**

We estimate correlation length via:

- Exponential fit to radial autocorrelation decay
- Spectral slope analysis
- Characteristic scale extraction from power spectrum

Sensitivity to noise and grid resolution is analyzed.

---

# Example Workflow

1. Generate correlated field
2. Compute 2D autocorrelation
3. Compute power spectral density
4. Radially average spectrum
5. Estimate correlation length
6. Perform sensitivity analysis

The demonstration Jupyter notebook reproduces all figures.

---

# Reproducibility

- Fixed random seeds
- Deterministic FFT pipeline
- Explicit parameter control
- Modular, testable code

---

# Conceptual Relevance to Quantitative Imaging

In microscopy-derived intensity fields, spatial organization reflects underlying structural constraints.

Methods implemented here provide:

- Quantitative measures of spatial clustering or dispersion
- Multi-scale characterization of structural organization
- Robust estimation of correlation length
- Diagnostic tools to assess noise influence

While demonstrated on synthetic fields, the methods are directly transferable to:

- Chromatin density maps
- Nuclear organization imaging
- Spatial transcriptomics intensity fields
- Any 2D stationary spatial dataset

---

# Limitations

- Assumes stationarity and isotropy
- Limited to second-order statistics
- No biological modeling included

The focus is methodological clarity rather than domain-specific interpretation.

Author

Franz M. Krumenacker
Vienna, Austria
franz.m.krumenacker@gmail.com
