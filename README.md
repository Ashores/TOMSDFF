
# Conveyor-Belt Operational Status Monitoring

This repository contains our end-to-end information-fusion framework based on Mask R-CNN for joint detection and segmentation of conveyor-belt operating states. We integrate three novel modules—MS-DFF, TOM, and BEseg—along with a Dynamic Weighted Hybrid Loss to deliver superior performance in challenging industrial scenarios with widely varying object scales.

## Table of Contents

- [Features](#features)  
- [Installation](#installation)  
- [Dataset](#dataset)  
- [Usage](#usage)  
- [Results](#results)  
- [Citation](#citation)  

## Features

- **Multi-Scale Dynamic Feature Fusion (MS-DFF)**  
  Aggregates and adapts pyramid features for both detection and segmentation in one unified backbone.

- **Task-Oriented Module (TOM)**  
  Dynamically routes fused features to the appropriate task head to improve multi-task collaboration.

- **Boundary Enhanced Segmentation (BEseg)**  
  Reinforces mask boundaries for clearer, more accurate segmentation.

- **Dynamic Weighted Hybrid Loss (DWH Loss)**  
  Automatically balances detection and segmentation losses during training.

## Installation

1. Clone this repository:  
   ```bash
   git clone https://github.com/Ashores/TOMSDFF.git
   cd TOMSDFF/
```

2. Create a Python environment and install dependencies:

   ```bash
   python3 -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```

## Dataset

* **Belt Dataset**

  * Annotated in COCO format
  * Publicly available at: `data/`
  * Contains images and JSON annotation files for conveyor-belt anomalies

## Usage

1. Prepare the dataset following COCO directory structure:

   ```
   data/
     ├── train2017/
     ├── val2017/
     └── annotations/
         ├── instances_train2017.json
         └── instances_val2017.json
   ```
2. Train the model:

   ```bash
   python train.py --config configs/ours_mask_rcnn.yaml
   ```
3. Evaluate on the validation set:

   ```bash
   python evaluate.py --config configs/ours_mask_rcnn.yaml
   ```
4. Visualize results:

   ```bash
   python demo.py --config configs/ours_mask_rcnn.yaml --input path/to/image.jpg
   ```

## Results

| Model         | AP₅₀ (%) ↑ | AP₇₅ (%) ↑ | mAP (%) ↑ | AP₅₀ (%) (Seg) ↑ | AP₇₅ (%) (Seg) ↑ | mAP (%) (Seg) ↑ | FLOPs (Gb) | Params (Mb) |
| ------------- | ---------- | ---------- | --------- | ---------------- | ---------------- | --------------- | ---------- | ----------- |
| Mask-R-CNN    | 97.3       | 64.7       | 66.0      | 54.4             | 40.2             | 39.7            | 142        | 43.99       |
| Cascade-R-CNN | 97.9       | 65.6       | 67.2      | 55.2             | 41.5             | 42.4            | 163        | 77.03       |
| SOLO          | 97.5       | 68.3       | 67.3      | 63.4             | 42.2             | 43.1            | 156        | 36.13       |
| SOLOv2        | 97.9       | 66.4       | 68.0      | 70.1             | 43.6             | 42.7            | 139        | 46.24       |
| HTC           | 97.7       | 67.1       | 67.6      | 56.3             | 42.1             | 41.5            | 162        | 79.97       |
| Yolact        | 98.0       | 66.2       | 66.9      | 60.6             | 43.5             | 42.3            | **61.7**   | 34.75       |
| DynaMask      | 97.8       | 67.7       | 67.8      | 58.7             | 43.1             | 42.8            | 782        | 56.3        |
| OrientedR-CNN | 98.1       | 67.6       | 67.1      | 57.9             | 42.7             | 42.1            | 136        | 51.7        |
| YOLO11-seg    | 98.3       | 67.9       | 68.7      | 65.5             | 44.2             | 43.6            | 123.3      | **22.4**    |
| **Ours**      | **98.4**   | **70.2**   | **69.8**  | **73.5**         | **46.8**         | **45.8**        | 339        | 63.72       |

Our approach achieves the best overall detection and segmentation performance while maintaining a reasonable computational footprint.

## Citation

