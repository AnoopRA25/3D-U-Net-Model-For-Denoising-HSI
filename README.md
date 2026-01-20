# 3D U-Net Model for Hyperspectral Image (HSI) Denoising

This repository contains an implementation of a **Spectral-Attention based 3D U-Net** model for **Hyperspectral Image (HSI) Denoising**.  
The model performs denoising using **3D convolutions** to capture both **spatial + spectral features**, improving image quality significantly.

---

## 📌 Project Overview

Hyperspectral images contain rich spectral information across multiple bands, but they are highly affected by noise during acquisition.  
This project applies a **3D U-Net architecture with spectral attention** to remove noise while preserving spectral details.

✅ Captures spatial features (x, y)  
✅ Captures spectral features (bands)  
✅ Improves PSNR + SSIM drastically

---

## 📂 Repository Contents

- **Notebook (.ipynb)** → Complete training + validation + inference
- **Result images** stored in `result/` folder:
  - `trainingloss.png` → Training loss curve
  - `validationpsnr.png` → Validation PSNR curve
  - `validationssim.png` → Validation SSIM curve
  - `result.png` → Final denoised output visualization

---

## ⚙️ Workflow

1. Load HSI cube dataset  
2. Split into train/test cube  
3. Extract 3D patches (spatial + spectral cubes)  
4. Train Spectral-Attention 3D U-Net using MSE Loss  
5. Validate PSNR + SSIM at regular epochs  
6. Run full cube inference for final denoised output  

---

## 🧠 Model Architecture

### ✅ Why 3D U-Net?
- HSI has shape: **Height × Width × Bands**
- 3D CNN learns:
  - spatial correlations (height & width)
  - spectral correlations (bands)

### ✅ Spectral Attention
Spectral attention improves performance by focusing more on important spectral bands and reducing noise influence.

---

## 📊 Training Configuration

- Dataset cube size: **(1096, 715, 102)**
- Train cube: **(876, 715, 102)**
- Test cube: **(220, 715, 102)**
- Patch size: **32 × 32 × 32**
- Epochs: **80**
- Training patches: **3000**
- Training time: **96.35 minutes**
- Final full cube inference time: **35.33 seconds**

---

## ✅ Final Test Results

| Metric | Noisy | Denoised |
|-------|-------|----------|
| **PSNR (dB)** | 28.38 | **39.20** |
| **SSIM** | 0.7263 | **0.9671** |

✅ **PSNR improved by +10.82 dB**  
✅ Strong structural similarity improvement

---

## 📉 Training and Validation Graphs

### 🔻 Training Loss Curve
![Training Loss](result/trainingloss.png)

### 📈 Validation PSNR Curve
![Validation PSNR](result/validationpsnr.png)

### 📈 Validation SSIM Curve
![Validation SSIM](result/validationssim.png)

---

## 🖼️ Output Result

### Noisy vs Denoised Comparison
![Result](result/result.png)

---

## 🛠️ How to Run

### Option 1: Run on Google Colab
Upload notebook to Google Colab and run all cells:
- Runtime → Run all

### Option 2: Run locally
Install dependencies:

```bash
pip install numpy matplotlib pandas torch torchvision scikit-image opencv-python
