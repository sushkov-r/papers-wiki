# DETR Family: Evolution of Transformer-Based Object Detection and Segmentation

## 1. DETR – DEtection TRansformer (Carion et al., 2020)
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


