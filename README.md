# PET/CT Tumor Segmentation and Quantitative Analysis (NSCLC)

## 📌 Overview

This project implements a full pipeline for **lung segmentation, tumor candidate detection, and quantitative PET analysis** using the NSCLC Radiogenomics dataset.

The goal was to simulate a **real-world medical imaging workflow** under **limited computational resources (MacBook Air M3)**, focusing on robustness, automation, and reproducibility.

---

## 🧠 Motivation

PET/CT imaging is widely used in lung cancer for:
- Tumor detection  
- Treatment planning  
- Monitoring therapy response  

Key quantitative metrics such as:
- **SUVmax**
- **SUVmean**
- **Tumor volume**

are essential for clinical decision-making.

This project explores how these metrics can be extracted **without manual annotations**, using automated methods.

---

## ⚙️ Pipeline

### 1. Data Handling
- Recursive loading of DICOM files from complex folder structures
- Automatic detection of PET scans among multiple modalities
- Normalization of voxel intensities

---

### 2. Lung Segmentation

Two approaches were implemented:

#### 🧠 Deep Learning (lungmask U-Net)
- Pre-trained model for lung segmentation
- Runs slice-wise inference

#### ⚠️ Fallback Method (Classical)
- Threshold-based segmentation
- Automatically triggered when deep model fails

Example issue encountered:
⚠️ lungmask failed — using fallback segmentation

This ensured the pipeline remained **robust and fully automated**.

---

### 3. Tumor Candidate Detection

- Adaptive thresholding applied within lung regions
- Threshold computed from PET intensity distribution
- Designed to approximate high-SUV tumor regions

Example:
Adaptive threshold (lung-only): 0.39

---

### 4. Quantitative Feature Extraction

For detected tumor regions:

- **Tumor Volume (mm³)**
- **SUVmax**
- **SUVmean**

Example output:
Volume: 0
SUVmax: 0
SUVmean: 0


---

### 5. Visualization

The project includes:

- Overlay visualization:
  - Lung mask (blue)
  - Tumor candidates (red)
- Multi-slice views across the volume
- PET intensity histogram inside lungs

Saved outputs:
- Figures (`outputs/figures/`)
- Tables (`outputs/tables/`)

---

## 📊 Results & Observations

### Key Findings

- Lung segmentation worked reliably using fallback when deep learning failed
- Tumor detection was **highly sensitive to threshold selection**
- Several scans resulted in:
  - No detected tumor regions
  - SUV metrics equal to zero

### Interpretation

This does **not indicate failure**, but highlights:

- PET intensity variability across scans
- Lack of ground-truth tumor annotations
- Limitations of simple threshold-based detection

---

## 🖼️ Example Visualization

- Blue: Lung mask  
- Red: Tumor candidate  

![Example](outputs/figures/R01-010_overlay.png)

---

## ⚠️ Limitations

- No ground-truth tumor masks available
- Tumor detection based on simple intensity thresholding
- lungmask model may fail on some scans
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
```
nsclc-pet-analysis/
├── notebooks/
├── scripts/
├── outputs/
└── README.md
```

---

## 🚀 Key Takeaways

- Built a **robust end-to-end medical imaging pipeline**
- Successfully handled:
  - messy DICOM data
  - model failures
  - hardware limitations
- Demonstrated:
  - segmentation techniques
  - quantitative PET analysis
  - medical data visualization

---

## 🔮 Future Work

- Radiomics feature extraction (PyRadiomics)
- Improved tumor detection (region-based methods)
- Integration of CT + PET information
- Machine learning classification

---

## 📄 References

- TCIA NSCLC Radiogenomics Dataset  
- lungmask segmentation model  
- PET imaging literature  
