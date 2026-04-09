# PET/CT Tumor Segmentation and Quantitative Analysis in NSCLC

## 📌 Overview

This project presents a computational pipeline for **lung and tumor segmentation** in PET/CT imaging, applied to the NSCLC Radiogenomics dataset from TCIA.

The goal is to simulate a **real-world medical imaging workflow**, including:
- DICOM data handling
- Automated segmentation
- Quantitative PET analysis
- Visualization of results

This project emphasizes **robustness under limited computational resources (MacBook Air M3)** and practical handling of imperfect medical data.

---

## 🧠 Clinical Context

Non-Small Cell Lung Cancer (NSCLC) accounts for ~85% of lung cancer cases. PET/CT imaging plays a critical role in:

- Tumor detection
- Treatment planning
- Response evaluation

Quantitative metrics such as **SUVmax and SUVmean** are commonly used in clinical decision-making.

Recent research shows PET/CT imaging can also support **non-invasive tumor characterization and classification** :contentReference[oaicite:1]{index=1}

---

## ⚙️ Methodology

### 1. Data Processing
- Recursive loading of DICOM files
- Handling inconsistent folder structures
- Slice normalization

### 2. Lung Segmentation
Two approaches were implemented:

- **Deep Learning (lungmask U-Net)**
  - Pre-trained model
  - Automatic segmentation
- **Fallback Classical Method**
  - Threshold-based segmentation
  - Used when deep learning fails

### 3. Tumor Detection
- Adaptive thresholding within lung regions
- Based on PET intensity distribution
- No manual annotations required

### 4. Feature Extraction
For detected tumor regions:
- Tumor Volume (mm³)
- SUVmax
- SUVmean

### 5. Visualization
- Slice overlays:
  - Lung mask (blue)
  - Tumor candidates (red)
- Histogram of PET intensity distribution
- Saved figures for reproducibility

---

## 📊 Results

Example output:

| Patient | Tumor Volume (mm³) | SUVmax | SUVmean |
|--------|--------------------|--------|---------|
| R01-010 | 0 | 0 | 0 |

### Observations:
- Lung segmentation succeeded using fallback when deep model failed
- Tumor detection highly sensitive to threshold selection
- Some scans did not contain detectable high-SUV regions

---

## 🖼️ Visualization

### Segmentation Overlay
- Blue: Lung mask  
- Red: Tumor candidate  

![Example](outputs/figures/sample_overlay.png)

---

## ⚠️ Limitations

- No ground-truth tumor annotations available
- Threshold-based tumor detection may miss subtle lesions
- Lungmask model may fail on some scans (handled via fallback)
- Limited dataset size due to hardware constraints

---

## 💻 Technical Stack

- Python (3.10)
- NumPy, Pandas
- Matplotlib
- PyDICOM
- SimpleITK
- lungmask (pre-trained U-Net)

---

## 📁 Project Structure
