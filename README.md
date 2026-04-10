# NSCLC PET/CT Tumor Analysis

## Overview

This project demonstrates a workflow for **lung and tumor segmentation**, feature extraction, and visualization from the **NSCLC Radiogenomics dataset** (TCIA). It compares classical threshold-based segmentation with deep learning-based segmentation using **pre-trained U-Net / lungmask**.

The goal is to provide a **portfolio-ready Python/Jupyter workflow** for PET/CT analysis in oncology imaging.

---

## 📁 Dataset

- Source: [TCIA NSCLC Radiogenomics](https://www.cancerimagingarchive.net/analysis-result/nsclc-radiogenomics-stanford/)
- Data includes:
  - PET and CT DICOM scans
  - Some clinical and genomic metadata (optional)
- For MacBook Air-friendly workflow, **subset of patients** used (e.g., 5–10)

---

## ⚙️ Pipeline

1. **DICOM Loading**
   - Recursive loading of patient folders
   - Normalization of PET/CT volumes

2. **Segmentation**
   - **Option A: Classical threshold + lung mask**  
     Fallback if lungmask U-Net fails.
   - **Option B: Lungmask pre-trained U-Net**  
     Performs automatic 2D slice-wise lung segmentation.

3. **Tumor Detection**
   - Threshold-based SUV detection inside segmented lungs
   - Computed metrics:
     - Tumor volume (mm³)
     - SUVmax
     - SUVmean

4. **Visualization**
   - Overlay lung and tumor masks on PET slices
   - Representative slices shown per patient

5. **Quantitative Summary**
   - Tabulated metrics per patient
   - Comparison between classical vs. U-Net where applicable

---

## 📊 Example Output

| Patient | Tumor Volume (mm³) | SUVmax | SUVmean | Notes |
|---------|------------------|--------|---------|-------|
| R01-001 | 0                | 0      | 0       | Fallback mask used |

- ⚠️ Lungmask failed for some patients → fallback mask applied
- Volumes/SUVs may be zero if tumor not detected or thresholds too strict

---

## 🛠️ Requirements

- Python 3.10+  
- Packages:
  ```bash
  pip install numpy matplotlib pydicom torch torchvision lungmask SimpleITK pandas ipywidgets