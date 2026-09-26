# Hyperspectral Image Processing: Core & Advanced Algorithms from Scratch

Course project for **GNR401 (Advanced Methods in Image Processing)** applying classical and advanced hyperspectral remote-sensing algorithms to the **Indian Pines AVIRIS dataset** (145×145 pixels, 220 spectral bands, 16 land-cover classes). Every algorithm — from histogram equalization to constrained spectral unmixing — is implemented **entirely from scratch in raw NumPy**, with no OpenCV, scikit-learn, or spectral-processing libraries, to demonstrate the underlying linear algebra and signal processing rather than call a library function.

## Why from scratch

Hyperspectral pipelines are usually built on top of libraries like `spectral` or `scikit-image` that hide the numerics. This project instead implements the math directly — manual convolution, hand-rolled NNLS solvers, custom eigendecomposition-based transforms — to show a working understanding of what those library calls are actually doing.

## Dataset

**Indian Pines** (AVIRIS sensor): a 145×145 pixel agricultural scene with 220 contiguous spectral bands and a 16-class ground-truth land-cover map, one of the standard benchmarks in hyperspectral image analysis.

## What's implemented

### Core processing (`GNR401.ipynb`)
- **Intensity transformations** — log transform, gamma correction, contrast stretching, histogram equalization
- **Spatial filtering** — manual 2D convolution with edge-replication padding, mean filter, Sobel edge detection

### Advanced hyperspectral analysis (`GNR401_advanced.ipynb`)
- **Reed–Xiaoli (RX) anomaly detector** — per-pixel Mahalanobis distance via full 200×200 inverse covariance estimation, with Tikhonov-regularized matrix inversion for numerical stability
- **Vertex Component Analysis (VCA)** — geometric endmember extraction via iterative orthogonal subspace projection and SVD-based dimensionality reduction
- **Fully Constrained Linear Spectral Unmixing (FCLS)** — per-pixel constrained optimization enforcing non-negativity and sum-to-one abundance constraints, solved with a from-scratch Lawson–Hanson active-set NNLS solver
- **Minimum Noise Fraction (MNF) transform** — noise covariance estimation via spatial shift-difference, Cholesky noise-whitening, and SNR-ordered eigendecomposition
- **Graph-based semi-supervised label propagation** — k-NN spectral similarity graph with adaptive Gaussian kernel bandwidth and normalized graph Laplacian diffusion, achieving classification from only 5% labelled pixels using MNF features
- **Extended Morphological Attribute Profiles (EMAPs)** — two-pass connected-components labeling (union-find with path compression) and area-based attribute opening/closing on PCA components for spectral-spatial feature extraction

## Repo layout

```
GNR401.ipynb           # core intensity/spatial algorithms
GNR401_advanced.ipynb  # RX, VCA, FCLS, MNF, label propagation, EMAPs
Indian_pines*.mat      # dataset (raw, corrected, ground truth)
outputs/                # rendered figures from the notebooks
```

## Running it

```bash
pip install numpy scipy matplotlib jupyter
jupyter notebook GNR401.ipynb
```

No other dependencies — every transform and solver is implemented directly on top of NumPy/SciPy's linear algebra primitives.
