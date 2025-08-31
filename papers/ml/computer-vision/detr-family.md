# DETR Family: Evolution of Transformer-Based Object Detection and Segmentation
## Pre-DETR (Before 2020): State of the Art in Detection and Segmentation

### 1. Two-Stage Detectors ([R-CNN Lineage](rcnn-family))
- **R-CNN (2014):** CNN features + region proposals (Selective Search).
- **Fast R-CNN (2015):** Shared conv features, RoI Pooling, end-to-end multitask loss.
- **Faster R-CNN (2015):** Introduced Region Proposal Network (RPN), fully learnable pipeline.
- **Mask R-CNN (2017):** Added segmentation branch and RoIAlign for instance masks.
- **Cascade R-CNN (2018):** Multi-stage detector with progressively stricter IoU thresholds.
- **Hybrid Task Cascade (2019):** Joint refinement for detection + segmentation.

**Strengths:** Very accurate, extensible, dominant in research.  
**Weaknesses:** Complex pipelines (anchors, proposals, NMS), relatively slow.

---

### 2. One-Stage Detectors
- **[YOLO](yolo-family) (2016 → v3 in 2018):** Real-time detection by regressing boxes and classes directly on a grid.
- **SSD (2016):** Multi-scale feature maps with default anchor boxes.
- **RetinaNet (2017):** Introduced **Focal Loss** to handle extreme class imbalance, achieving strong accuracy while staying single-stage.

**Strengths:** Fast, simpler than two-stage methods.  
**Weaknesses:** Slightly less accurate than Faster/Mask R-CNN (until RetinaNet closed the gap).

---

### 3. Segmentation Approaches
- **FCN (2014):** First fully convolutional semantic segmentation network.
- **U-Net (2015):** Encoder–decoder with skip connections, huge impact in medical imaging.
- **DeepLab series (2015–2018):** Used atrous/dilated convolutions, CRFs, and later atrous spatial pyramid pooling (ASPP).
- **Mask R-CNN (2017):** Instance segmentation baseline.
- **PANet (2018):** Improved feature pyramids and mask refinement.
- **YOLACT (2019):** One-stage real-time instance segmentation using prototype masks.

**Strengths:** Mature, high-performing segmentation pipelines.  
**Weaknesses:** Still relied on bounding boxes + proposals, complex heuristics.

---

### 4. Common Characteristics Before DETR
- Heavy reliance on **anchors**, **proposals**, and **Non-Maximum Suppression (NMS)**.
- Multi-stage training and complex heuristics.
- CNN-based backbones (ResNet, ResNeXt, FPN) dominated.
- Trade-off: **two-stage = accuracy, one-stage = speed**.
- Segmentation treated as **detection + mask refinement**, not a unified task.

---

### Overall Landscape by 2019
- **Mask R-CNN** → default for instance segmentation.  
- **Faster R-CNN / Cascade R-CNN** → state-of-the-art two-stage detection.  
- **RetinaNet & [YOLOv3](yolo-family)** → strong single-stage detectors.  
- **DeepLabv3+** → state-of-the-art semantic segmentation.  
- **Hybrid Task Cascade, PANet, YOLACT** → refinements and efficiency gains.  

**In short:** By 2019, CNN-based detection and segmentation had matured into very strong, but still **fragmented and heuristic-heavy pipelines**. DETR (2020) disrupted this by introducing **transformers, set prediction, and end-to-end training**, removing the need for anchors, proposals, and NMS.

# DETR family
## 1. [DETR](detr.md) – DEtection TRansformer (Carion et al., 2020)
- **Contribution:** First fully end-to-end object detector with a transformer backbone.
- Replaced anchors, proposals, and NMS with a **set prediction formulation** and **Hungarian matching loss**.
- Showed transformers can unify detection with direct object queries.
- **Limitations:** Very slow convergence (hundreds of epochs), struggled with small objects.

---

## 2. Deformable DETR (Zhu et al., 2020)
- **Contribution:** Introduced **deformable attention**, attending only to a sparse set of key points around a reference.
- Dramatically accelerated convergence (tens vs. hundreds of epochs).
- Improved small-object detection.
- Established deformable attention as a practical fix to vanilla DETR.

---

## 3. Conditional DETR (Meng et al., 2021)
- **Contribution:** Made object queries **spatially aware** by conditioning them on reference points.
- Improved training stability and convergence.
- Reduced query ambiguity.

---

## 4. DAB-DETR – Dynamic Anchor Boxes (Liu et al., 2022)
- **Contribution:** Represented object queries explicitly as **anchor boxes** (center + size).
- Enabled iterative refinement of queries, improved interpretability.
- Better localization accuracy compared to abstract embeddings.

---

## 5. DN-DETR – Denoising DETR (Li et al., 2022)
- **Contribution:** Added **denoising training task**:
  - Injected noisy versions of ground-truth boxes during training.
  - Model learned to denoise them → stabilized Hungarian matching.
- Result: faster convergence and more stable training.

---

## 6. DINO – DETR with Improved Denoising Anchor Boxes (Zhang et al., 2022)
- **Contribution:** Unified ideas from DN-DETR and DAB-DETR.
- Added **mixed query selection** and **look forward twice** strategy for iterative refinement.
- Achieved strong performance and fast convergence.
- Became a strong DETR baseline for detection.

---

## 7. Mask DINO (Li et al., 2022)
- **Contribution:** Extended DINO to **instance and panoptic segmentation**.
- Added a mask prediction branch with **mask embeddings**.
- Unified detection + segmentation under one framework.
- Achieved state-of-the-art results across segmentation tasks.

---
## 8. [DI-MaskDINO](di-mask-dino.md) (2024)
- **Contribution:** Tackled the **imbalance** between detection and segmentation tasks in the transformer decoder.
- Introduced two key innovations:
  - **De-Imbalance (DI) Module:** redistributes gradient flow between detection and segmentation branches, ensuring balanced learning.
  - **Balance-Aware Tokens Optimization (BATO):** reweights query tokens to better calibrate training.
- **Results:**
  - Improved **box AP by +1.2** and **mask AP by +0.9** on COCO compared to Mask DINO.
  - Outperforms other DETR-based models (including Mask2Former).
- **Impact:** Established as the **state-of-the-art** in instance segmentation in the DETR/DINO lineage.


---

## Timeline Summary
- **2020:** DETR → End-to-end detection with transformers.  
- **2020:** Deformable DETR → Faster training, sparse attention.  
- **2021:** Conditional DETR → Spatially aware queries.  
- **2022:** DAB-DETR → Queries as anchor boxes.  
- **2022:** DN-DETR → Denoising task for stability.  
- **2022:** DINO → Combines denoising + anchor boxes + refinements.  
- **2022:** Mask DINO → Unified detection and segmentation. 
- **2024:** DI-MaskDINO → Balanced decoding, SOTA instance segmentation.  

---
By 2019 the field was dominated by two-stage detectors like those in the [R-CNN lineage](rcnn-family.md) and mature segmentation systems; DETR unified detection and later segmentation, as covered in the [segmentation history](segmentation-dnn-history.md).


