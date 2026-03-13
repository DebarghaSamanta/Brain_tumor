# 🧠 Brain Tumor Intelligence: Dual-Stage Classification & Segmentation

This repository implements a **high-precision medical imaging pipeline** designed to assist in the **automated diagnosis of brain tumors from MRI scans**.  

The system follows a **two-stage deep learning architecture**:

1. **Diagnostic Screening (Classification)** – Determines whether a tumor is present.
2. **Precise Isolation (Segmentation)** – Identifies and outlines the tumor region at the pixel level.

This approach mirrors real-world clinical workflows by **first detecting abnormality and then precisely localizing it**.

---

# 📊 Key Performance Metrics

- **Classification Accuracy:** **94.8%** using a fine-tuned **VGG16**
- **Segmentation Dice Score:** **0.87** using a **custom U-Net**
- **Latency:** Optimized for **rapid diagnostic feedback**

---

# 🏗 Technical Architecture

## 1️⃣ Diagnostic Screening (Classification)

The first stage performs **binary classification** to determine whether an MRI scan contains a tumor.

### Model
- **Base Architecture:** **VGG16**
- **Pretraining:** ImageNet
- **Approach:** Transfer Learning

### Fine-Tuning Strategy
Custom dense layers were added on top of the VGG16 backbone:

- Fully connected layers for MRI feature extraction
- **Dropout (0.5)** to reduce overfitting
- Specialization toward **medical texture patterns**

### Preprocessing
MRI scans are processed using **OpenCV**:

- **Intensity normalization**
- **Resizing to 224 × 224**
- Standardization for CNN input

---

## 2️⃣ Precise Isolation (Semantic Segmentation)

If a scan is classified as **tumor-positive**, the pipeline activates a **U-Net segmentation model** to isolate the tumor region.

### Encoder (Contracting Path)

Captures **global contextual features** through:

- Repeated **convolution layers**
- **Max pooling** for spatial compression
- Hierarchical feature extraction

### Decoder (Expanding Path)

Restores spatial resolution for **precise tumor localization**:

- **Upsampling layers**
- **Skip connections** with encoder features
- High-resolution feature reconstruction

### Optimization Techniques

- **Batch Normalization** for stable training
- **Hybrid Loss Function** to address **class imbalance** between healthy tissue and tumor pixels

---

# 🚀 Pipeline Overview

MRI Scan  
⬇  
**VGG16 Classifier** → Detect Tumor Presence  
⬇  
If Positive  
⬇  
**U-Net Segmentation** → Generate Tumor Mask  
⬇  
Pixel-level Tumor Localization
