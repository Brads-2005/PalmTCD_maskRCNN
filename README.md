# 🌴 Palm Tree Crown Detection Using Mask R-CNN (PyTorch)

This repository implements a palm tree crown segmentation pipeline using a PyTorch-based Mask R-CNN model. The work closely follows the approach described in the paper:

> **[Apricot Tree Detection from UAV Images Using Mask R-CNN and U-Net](https://www.researchgate.net/publication/367767781_Apricot_Tree_Detection_from_UAV-Images_Using_Mask_R-CNN_and_U-Net)**  
> _(Paper used TensorFlow Mask R-CNN, but this repo adapts it to PyTorch due to compatibility and flexibility reasons.)_

## 🎯 Objective

To accurately detect and segment **individual palm tree crowns** from high-resolution drone (UAV) imagery using an instance segmentation approach.

---

## 📦 Dataset Overview

The dataset was sourced from Kaggle (not included in this repo due to size constraints) and preprocessed to follow the method used in the research paper.

### 🗺️ Input Format

- **Orthophotos**: High-resolution RGB drone images (`.jpg`)
- **Masks**: Binary mask images (`.png`), where:
  - White = Tree Crown  
  - Black = Background

---

## 🔧 Preprocessing Steps

### 1. **Manual Annotation**
- Annotated tree crowns using [LabelMe](https://github.com/wkentaro/labelme)
- Converted to binary masks (1 tree per mask area)

### 2. **Tree Isolation**
- Applied `cv2.connectedComponents()` to isolate individual trees

### 3. **Patch Extraction**
- Extracted **512×512** patches with tree crowns centered
- Accepted some background/empty space for realism
- Ensured one tree per image patch

### 4. **COCO Annotation Format**
- Created a `coco_annotations.json` file with:
  - **Images**: ID, file name, dimensions
  - **Annotations**: Segmentation, bounding box, area
  - **Category**: `{"id": 1, "name": "tree"}`

---
## 🧠 Model & Training

- **Model Used**: PyTorch `maskrcnn_resnet50_fpn` (from `torchvision`)
- **Training Details**:
  - Trained on single-tree patches
  - Used COCO-formatted annotations
  - Mixed precision and frozen backbone options available

---

## 🔬 Key Advantages

- Each image contains exactly **one centered tree**, improving segmentation focus.
- Clean separation of crowns helps avoid occlusion and overlapping issues.
- Compatible with Mask R-CNN pipelines (PyTorch-based).
  
---

## ⚠️ Limitations

- Current dataset focuses only on **palm trees** and may **not generalize** to other species or regions.
- Performance drops observed in diverse or mixed forest imagery.


## 📝 Citation (for reference)

> *Apricot Tree Detection from UAV Images Using Mask R-CNN and U-Net*  
> [ResearchGate Link](https://www.researchgate.net/publication/367767781_Apricot_Tree_Detection_from_UAV-Images_Using_Mask_R-CNN_and_U-Net)

---

## 📌 Note

The dataset used in this project is not included in this repository due to GitHub file size constraints.

---


