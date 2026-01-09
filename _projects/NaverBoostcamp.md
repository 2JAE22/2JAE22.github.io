---
title: "Naver AI Tech 7th"
featured_image: "images/projects/Naver_boostcamp/naverai_1.png"
start_date: '2024-08-05'
end_date: '2025-02-12'
last_modified_at: '2026-01-06 21:00:00'
---

![NaverBoostcamp Logo](../images/projects/Naver_boostcamp/naverai_2.png)

<br/>

## Overview
During the **Naver AI Tech 7th (Computer Vision Track)**, I conducted four major projects ranging from image classification to segmentation. Through this intensive curriculum, I developed expertise in **Data-Centric AI**, **Model Optimization**, and **MLOps tools** (WandB, Poetry).

Below is a summary of the key projects and my specific contributions.

<br/>

---
### 1. Sketch Image Classification (ImageNet-Sketch) 
👉 [Code](https://github.com/2JAE22/level1-imageclassification-cv-02)

<div style="
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 24px;
  margin: 24px 0;
">
  <div style="text-align: center;">
    <div style="
      height: 260px;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
      border-radius: 10px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
      background: #fff;
    ">
      <img src="../images/projects/Naver_boostcamp/Sketch_data_1.png"
           alt="Global SHAP Analysis"
           style="
             width: 100%;
             height: 100%;
             object-fit: contain;
           ">
    </div>
    <p style="
      margin-top: 8px;
      font-size: 0.9rem;
      color: #555;
    ">
      SketchDataSet_Example1
    </p>
  </div>

  <div style="text-align: center;">
    <div style="
      height: 260px;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
      border-radius: 10px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
      background: #fff;
    ">
      <img src="../images/projects/Naver_boostcamp/Sketch_data_2.png"
           alt="Local SHAP Explanation"
           style="
             width: 100%;
             height: 100%;
             object-fit: contain;
           ">
    </div>
    <p style="
      margin-top: 8px;
      font-size: 0.9rem;
      color: #555;
    ">
      SketchDataSet_Example2
    </p>
  </div>
</div>

**Objective** Build a robust baseline image classification model on the ImageNet-Sketch dataset, focusing on improving generalization performance through data-centric strategies.

<br/>

🎯 **My Role**:
- Led **dataset analysis and data-centric optimization**, identifying performance bottlenecks caused by dataset structure rather than model capacity
- Designed and validated **data cleaning policies** for duplicate and ambiguous samples
- Implemented and evaluated **augmentation and preprocessing strategies** tailored to sketch-style images
- Managed experiments and hyperparameter searches using **Weights & Biases**

<br/>

**Approach & Key Solutions**

🛠️ **Methods**:

![Sketch_method](../images/projects/Naver_boostcamp/Sketch_Method_1.png)

- **Exploratory Data Analysis (EDA)**
  - Analyzed image count per class and class imbalance
  - Identified near-duplicate sketches caused by flips and rotations
  - Examined object placement and background patterns to guide preprocessing decisions

- **Data Cleaning**
  - Removed near-duplicate samples dominating certain classes
  - Pruned ambiguous samples between visually overlapping classes (e.g., baseball icon vs. baseball player)
  - Verified that simple removal outperformed synthetic data generation approaches

- **Targeted Augmentation (Albumentations)**
  - Avoided Flip/Rotate-heavy augmentations already present in the dataset
  - Applied controlled **ShiftScaleRotate (wrap mode)** to improve spatial robustness
  - Used **GaussianBlur** to reduce overfitting to repeated line patterns
  - Empirically confirmed that aggressive augmentations (e.g., CoarseDropout, GridShuffle) degraded performance

- **Grayscale-aware Preprocessing**
  - Identified that ImageNet-Sketch images are inherently grayscale
  - Compared:
    1. Replicating grayscale to 3-channel input
    2. Modifying pretrained Conv2D weights for single-channel input
  - Computed dataset-specific mean and standard deviation for grayscale normalization

- **Experiment Management**
  - Tracked experiments and metrics using **WandB**
  - Performed hyperparameter optimization via **WandB Sweeps**
  - Compared CNN-based and ViT-based models from an inductive bias perspective 

<br/>

📊 **Result**:

![Sketch_Result](../images/projects/Naver_boostcamp/Sketch_Result_1.png)

- Achieved up to **~0.92 classification accuracy**, outperforming naive augmentation baselines
- Demonstrated that **dataset de-duplication and ambiguity removal** provided larger gains than architectural changes
- Confirmed that indiscriminate augmentation **degrades performance** on already-distorted sketch data

<br/>

**Key Insight** For sketch-based image classification, **data quality and class clarity matter more than model complexity**.
Removing misleading samples consistently improved generalization, while indiscriminate augmentation led to performance collapse.

---

### 2. Trash Object Detection
👉 [Code](https://github.com/2JAE22/objectdetection-cv-02)
👉 [Report](../images/projects/Naver_boostcamp/TrashDetection_WrapupReport.pdf)

![Trash_overview](../images/projects/Naver_boostcamp/Trash_overview_1.png)

**Objective**: Detect and classify trash in high-resolution (1024x1024) images into 10 categories.
* 🔍 **EDA**: ① Box ② Class ③ Color
<!-- 🔍 EDA Visualization (3x3 Grid) -->
<div style="
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
  margin: 20px 0 30px 0;
">

  <!-- 1 -->
  <div style="
    height: 220px;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    border-radius: 8px;
    background: #fff;
    box-shadow: 0 3px 6px rgba(0,0,0,0.08);
  ">
    <img src="../images/projects/Naver_boostcamp/Trash_EDA_1_1.png"
         style="width:100%; height:100%; object-fit: contain;">
  </div>

  <!-- 2 -->
  <div style="height:220px; display:flex; align-items:center; justify-content:center;
              overflow:hidden; border-radius:8px; background:#fff;
              box-shadow:0 3px 6px rgba(0,0,0,0.08);">
    <img src="../images/projects/Naver_boostcamp/Trash_EDA_1_2.png"
         style="width:100%; height:100%; object-fit: contain;">
  </div>

  <!-- 3 -->
  <div style="height:220px; display:flex; align-items:center; justify-content:center;
              overflow:hidden; border-radius:8px; background:#fff;
              box-shadow:0 3px 6px rgba(0,0,0,0.08);">
    <img src="../images/projects/Naver_boostcamp/Trash_EDA_1_3.png"
         style="width:100%; height:100%; object-fit: contain;">
  </div>

  <!-- 4 -->
  <div style="height:220px; display:flex; align-items:center; justify-content:center;
              overflow:hidden; border-radius:8px; background:#fff;
              box-shadow:0 3px 6px rgba(0,0,0,0.08);">
    <img src="../images/projects/Naver_boostcamp/Trash_EDA_2_1.png"
         style="width:100%; height:100%; object-fit: contain;">
  </div>

  <!-- 5 -->
  <div style="height:220px; display:flex; align-items:center; justify-content:center;
              overflow:hidden; border-radius:8px; background:#fff;
              box-shadow:0 3px 6px rgba(0,0,0,0.08);">
    <img src="../images/projects/Naver_boostcamp/Trash_EDA_2_2.png"
         style="width:100%; height:100%; object-fit: contain;">
  </div>

  <!-- 6 -->
  <div style="height:220px; display:flex; align-items:center; justify-content:center;
              overflow:hidden; border-radius:8px; background:#fff;
              box-shadow:0 3px 6px rgba(0,0,0,0.08);">
    <img src="../images/projects/Naver_boostcamp/Trash_EDA_2_3.png"
         style="width:100%; height:100%; object-fit: contain;">
  </div>

  <!-- 7 -->
  <div style="height:220px; display:flex; align-items:center; justify-content:center;
              overflow:hidden; border-radius:8px; background:#fff;
              box-shadow:0 3px 6px rgba(0,0,0,0.08);">
    <img src="../images/projects/Naver_boostcamp/Trash_EDA_2_3.png"
         style="width:100%; height:100%; object-fit: contain;">
  </div>

  <!-- 8 -->
  <div style="height:220px; display:flex; align-items:center; justify-content:center;
              overflow:hidden; border-radius:8px; background:#fff;
              box-shadow:0 3px 6px rgba(0,0,0,0.08);">
    <img src="../images/projects/Naver_boostcamp/Trash_EDA_3_1.png"
         style="width:100%; height:100%; object-fit: contain;">
  </div>

  <!-- 9 -->
  <div style="height:220px; display:flex; align-items:center; justify-content:center;
              overflow:hidden; border-radius:8px; background:#fff;
              box-shadow:0 3px 6px rgba(0,0,0,0.08);">
    <img src="../images/projects/Naver_boostcamp/Trash_EDA_3_2.png"
         style="width:100%; height:100%; object-fit: contain;">
  </div>

</div>

* 🎯 **My Role**:
    * **YOLO Implementation**: Experimented with **YOLOv11 (s, l, xl)** models to verify the performance of 1-stage detectors compared to 2-stage models.
    * **Ensemble Strategy**: Contributed to the final ensemble by combining YOLO predictions with the team's Cascade R-CNN and DINO models.
* 🛠️ **Methods**:
    * **Augmentation**: Applied Mosaic, MixUp, and RandomCrop to handle object scale variations.
    * **Ensemble**: Used **WBF (Weighted Boxes Fusion)** and Soft-NMS to merge bounding boxes effectively.
* 📊 **Result**: Achieved Public Score **0.6714** / Private Score **0.6558**.
<br>
You can find the detailed experimental results below.
<iframe
  src="https://wandb.ai/leejken530-kyungpook-national-university/recycling/reports/curves/Recall-Confidence(B)?embed=true"
  width="100%"
  height="600"
  frameborder="0"
></iframe>

<div style="
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 16px;
  margin: 20px 0 30px 0;
">

  <!-- 1 -->
  <div style="
    height: 220px;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    border-radius: 8px;
    background: #fff;
    box-shadow: 0 3px 6px rgba(0,0,0,0.08);
  ">
    <img src="../images/projects/Naver_boostcamp/Trash_result_1.png"
         style="width:100%; height:100%; object-fit: contain;">
  </div>

  <!-- 2 -->
  <div style="height:220px; display:flex; align-items:center; justify-content:center;
              overflow:hidden; border-radius:8px; background:#fff;
              box-shadow:0 3px 6px rgba(0,0,0,0.08);">
    <img src="../images/projects/Naver_boostcamp/Trash_result_2.png"
         style="width:100%; height:100%; object-fit: contain;">
  </div>

  <!-- 3 -->
  <div style="height:220px; display:flex; align-items:center; justify-content:center;
              overflow:hidden; border-radius:8px; background:#fff;
              box-shadow:0 3px 6px rgba(0,0,0,0.08);">
    <img src="../images/projects/Naver_boostcamp/Trash_result_3.png"
         style="width:100%; height:100%; object-fit: contain;">
  </div>

  <!-- 4 -->
  <div style="height:220px; display:flex; align-items:center; justify-content:center;
              overflow:hidden; border-radius:8px; background:#fff;
              box-shadow:0 3px 6px rgba(0,0,0,0.08);">
    <img src="../images/projects/Naver_boostcamp/Trash_result_4.png"
         style="width:100%; height:100%; object-fit: contain;">
  </div>
</div>
<br/>

* **Summary**
> **Conducted large-scale object detection experiments using YOLOv11 and multi-model ensembles (Cascade R-CNN, DINO), achieving Public 0.6714 / Private 0.6558 through optimized augmentation and bounding-box fusion strategies.**

---

### 3. Data-Centric: Multilingual Receipt OCR
👉 [Code](https://github.com/2JAE22/datacentric-cv-02)
👉 [Report](../images/projects/Naver_boostcamp/DataCentricOCR_WrapupReport.pdf)

<div style="
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 24px;
  margin: 24px 0;
">

  <!-- Left image -->
  <div style="text-align: center;">
    <div style="
      height: 260px;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
      border-radius: 10px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
      background: #fff;
    ">
      <img src="../images/projects/Naver_boostcamp/DataCentric_Example1.jpg"
           alt="OCR Example1"
           style="
             width: 100%;
             height: 100%;
             object-fit: contain;
           ">
    </div>
    <p style="
      margin-top: 8px;
      font-size: 0.9rem;
      color: #555;
    ">
      OCR_Example1
    </p>
  </div>

  <!-- Right image -->
  <div style="text-align: center;">
    <div style="
      height: 260px;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
      border-radius: 10px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
      background: #fff;
    ">
      <img src="../images/projects/Naver_boostcamp/DataCentric_Example2.jpg"
           alt="OCR Example2"
           style="
             width: 100%;
             height: 100%;
             object-fit: contain;
           ">
    </div>
    <p style="
      margin-top: 8px;
      font-size: 0.9rem;
      color: #555;
    ">
      OCR Example2
    </p>
  </div>

</div>

**Objective**: Improve OCR performance for multilingual receipts (Chinese, Japanese, Thai, Vietnamese) purely through **Data Preprocessing** (Model architecture fixed).
* **Metrics**: DetEval (F1 Score)
* **🎯 My Role**:
    * **Data Labeling & Cleaning**: Manually corrected orientation issues and removed noise from the Ground Truth labels to improve data quality.
    * **Visualization**: Developed a **Streamlit** dashboard to visualize data distribution and augmentation effects for the team.
* **🛠️ Methods**:
    * **Dataset Expansion**: Integrated external datasets (ICDAR, CORD).
    * **Augmentation**: Applied Perspective Transform and various noise injections (Gaussian, Salt & Pepper).
* **📊 Result**: Achieved **F1 Score 0.8100** (Public) / 0.8078 (Private).

* **Performance Comparison (Before vs. After Ensemble)**

| Stage      | Model / Setting          | Epoch | Precision | Recall    | F1 Score                                   | Key Configuration                                                    |
| ---------- | ------------------------ | ----- | --------- | --------- | ------------------------------------------ | -------------------------------------------------------------------- |
| **Before** | Version 1                | 150   | –         | –         | –                                          | translate (50%), salt & pepper (50%), add line (50%)                 |
|            | Version 2                | 150   | 0.7734    | 0.7032    | 0.7366                                     | translate (50%), gaussian (50%), add line (50%)                      |
|            | Version 3                | 150   | 0.5503    | 0.5088    | 0.5288                                     | translate (50%), salt & pepper (35%), gaussian (35%), add line (50%) |
|            | Version 4                | 150   | 0.6855    | 0.6681    | 0.6767                                     | rotate 90°                                                           |
| **After**  | **Final Ensemble Model** | –     | **0.81+** | **0.80+** | **0.8100 (Public)** / **0.8078 (Private)** | Hard Voting Ensemble (Optimized IoU & Vote Thresholds)               |

* **Summary**

> **After applying an optimized ensemble strategy, the F1 score improved from a maximum of 0.7366 (single model) to 0.8100 (Public) and 0.8078 (Private), demonstrating a balanced improvement in both precision and recall.**



<br/>

---

### 4. Bone Segmentation
👉 [Code](https://github.com/2JAE22/semanticsegmentation-cv-16-lv3)
👉 [Report](../images/projects/Naver_boostcamp/HandBone_Image Segmentation_WrapupReport.pdf)

<div style="text-align:center; margin: 24px 0;">
  <img src="../images/projects/Naver_boostcamp/Handbone_Example.gif"
       alt="Commemorative Animated GIF"
       style="max-width: 800px; width:100%; border-radius:10px; box-shadow:0 2px 8px rgba(0,0,0,0.08);">
  <p style="font-size:0.9rem; color:#555; margin-top:8px;">
    This Streamlit app was developed to provide detailed, step-by-step visualization of hand bone segmentation examples.
  </p>
</div>

**Objective**: Develop a segmentation model to precisely identify bone areas in medical X-ray images.
* **Metrics**: Dice Score
* **🎯 My Role & Technical Approach**:
    * **Library Comparison & Data Workflow**: Conducted analysis of folder structures and performed detailed data EDA, then refactored the pipeline for efficient data preprocessing and augmentation using various libraries.
    * **Encoder Experiments**: Analyzed performance differences between Transformer-based encoders and CNN-based encoders.
    * **Troubleshooting**: Resolved weight initialization errors (`encoder_weights: None`) and decoder compatibility issues.
* **🛠️ Methods**:
    * **Model Architecture**: Found that **U-Net** provided more stable performance on medical data compared to DeepLabV3+ or U-Net++.
    * **Hyperparameter Tuning**: Optimized Image Size and Epochs using WandB Sweeps.

* **📊 Result**:
![HandBone Result](../images/projects/Naver_boostcamp/HandBone_Result_1.png)

Finally, the best result was obtained <strong>by combining high-resolution inputs with attention-enhanced decoding and a soft ensemble strategy</strong>, achieving a <strong>Dice score of 0.9751</strong> on the test set.

### 📸 Commemorative Photos


<div style="
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 16px;
  margin: 16px 0 32px 0;
  justify-items: center;
">

  <figure style="text-align:center;">
    <img src="../images/projects/Naver_boostcamp/Commemorative_Photos1.jpg"
         alt="Commemorative Photo 1"
         style="width:100%; max-width:320px; aspect-ratio:4/5;
                object-fit:cover; border-radius:10px;">
    <figcaption style="margin-top:8px; font-size:0.9rem; color:#555;">
      First Team Commemorative Photo
    </figcaption>
  </figure>

  <figure style="text-align:center;">
    <img src="../images/projects/Naver_boostcamp/Commemorative_Photos2.jpg"
         alt="Commemorative Photo 2"
         style="width:100%; max-width:320px; aspect-ratio:4/5;
                object-fit:cover; border-radius:10px;">
    <figcaption style="margin-top:8px; font-size:0.9rem; color:#555;">
      Second Team Commemorative Photo
    </figcaption>
  </figure>

</div>
