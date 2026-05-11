# License Plate Detection — Full Preprocessing Pipeline

**CS383 — Image Processing | Final Project**

A complete image preprocessing pipeline for automatic license plate detection and character enhancement, implemented in Python using OpenCV and scikit-image on Google Colab.

---

## Overview

This project applies a multi-stage preprocessing pipeline to car images, progressively isolating and enhancing license plate characters for downstream OCR or detection tasks.

The pipeline is divided into three main sections:

| Section | Techniques |
|---------|-----------|
| A — Filtering | Gaussian, Laplacian, Sobel, Sharpening |
| B — Transformations | Image Inverse, Gamma Correction, Log Transform, Histogram Equalization, Contrast Stretching |
| C — Plate Zoom & Enhancement | Auto-detect (Canny + Contours), Crop, Zoom ×3, Denoise, Sharpen, Adaptive Threshold, CLAHE |

---

## Pipeline Stages

### Section A — Filtering
- **Gaussian Filter** — reduces noise with sigma=1 smoothing
- **Laplacian Filter** — highlights plate edges and boundaries
- **Sobel Filter** — directional edge detection (X, Y, and combined magnitude)
- **Sharpening Filter** — enhances plate characters and fine details using a 3×3 kernel

### Section B — Transformations
- **Image Inverse** — pixel negation (`255 - pixel`), useful for white plates on dark backgrounds
- **Gamma Correction** — brightness adjustment (γ=1.5 by default)
- **Log Transformation** — reveals hidden detail in dark plate regions
- **Histogram Equalization** — redistributes pixel intensities for better contrast
- **Contrast Stretching** — scales pixel values to the full [0, 255] range

### Section C — Plate Zoom & Character Enhancement
1. **Auto Detect** — Canny edge detection + contour approximation to locate the plate
2. **Crop** — isolates the plate region (falls back to the full image if no plate is found)
3. **Zoom ×3** — upscales with `INTER_CUBIC` interpolation
4. **Denoise** — `fastNlMeansDenoising` to remove noise before thresholding
5. **Sharpen** — sharpening kernel to clarify each character
6. **Adaptive Threshold** — `ADAPTIVE_THRESH_GAUSSIAN_C` to separate characters from background
7. **CLAHE** — local contrast enhancement with `clipLimit=3.0`, `tileGridSize=(4,4)`

---

## Requirements

```
opencv-python-headless
scikit-image
matplotlib
numpy
```

Install with:

```bash
pip install opencv-python-headless scikit-image matplotlib numpy
```

> The notebook is designed to run on **Google Colab**. It mounts Google Drive and reads the dataset from a ZIP file.

---

## Dataset

The dataset is loaded from Google Drive:

```
/content/drive/MyDrive/Automatic-License-Plate-Detection-main(2).zip
```

It contains car images from which 6 random samples are selected per run for visualization.

---

## Usage

1. Open `License_Plate_Preprocessing_FINAL.ipynb` in Google Colab.
2. Upload the dataset ZIP to your Google Drive at the path above.
3. Run all cells in order — each cell is labeled with its section and step.
4. Outputs include side-by-side comparison grids for all 6 sample images across every preprocessing stage.

The final cell (Cell 16) renders a complete 14-step pipeline summary for a single image in one grid.

---

## File Structure

```
├── License_Plate_Preprocessing_FINAL.ipynb   # Main notebook
└── CS383_License_Plate_Report.docx           # Project report
```
