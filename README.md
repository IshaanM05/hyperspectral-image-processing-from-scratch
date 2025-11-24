# GNR401Proj
# Hyperspectral Image Processing: Core & Advanced Algorithms from Scratch

### Project Overview
This project implements fundamental and advanced hyperspectral image processing algorithms applied to the **Indian Pines AVIRIS dataset** (145×145×220 bands). Every algorithm is implemented **entirely from scratch using raw NumPy** — no OpenCV, no scikit-learn, no spectral processing libraries.

### Dataset
**Indian Pines** (AVIRIS sensor): 145×145 pixel scene, 220 spectral bands, 16 land-cover classes.
* Band-averaged grayscale for spatial processing; full spectral cube for classification and unmixing.
* 16-class ground-truth map for validation.

### Implemented Algorithms

#### Core Processing (`GNR401.ipynb`)
1.  **Intensity Transformations** — Log, Gamma, Contrast Stretching, Histogram Equalization
2.  **Spatial Filtering** — Manual 2D convolution with edge-replication padding, Mean filter, Sobel edge detection

#### Advanced Hyperspectral Analysis (`GNR401_advanced.ipynb`)

3.  **Reed–Xiaoli (RX) Anomaly Detector**
    * Per-pixel Mahalanobis distance via full 200×200 inverse covariance estimation
    * Tikhonov-regularised matrix inversion for numerical stability

4.  **Vertex Component Analysis (VCA) — Endmember Extraction**
    * Geometric endmember extraction via iterative orthogonal subspace projection
    * SVD-based dimensionality reduction, null-space vertex selection

5.  **Fully Constrained Linear Spectral Unmixing (FCLS)**
    * Per-pixel constrained optimisation: non-negativity + sum-to-one abundance constraints
    * Lawson–Hanson active-set NNLS solver implemented from scratch
    * Augmented least-squares formulation for sum-to-one enforcement

6.  **Minimum Noise Fraction (MNF) Transform**
    * Noise covariance estimation via spatial shift-difference method
    * Cholesky noise-whitening → eigen-decomposition → SNR-ordered components

7.  **Graph-Based Semi-Supervised Label Propagation**
    * k-NN spectral similarity graph with adaptive Gaussian kernel bandwidth
    * Normalised graph Laplacian iterative diffusion
    * Achieves classification from only 5% labelled pixels via MNF features

8.  **Extended Morphological Attribute Profiles (EMAPs)**
    * Two-pass connected components labeling (union-find with path compression)
    * Area-based attribute opening/closing at multiple thresholds on PCA components
    * Spectral-spatial feature extraction → nearest-centroid classification
