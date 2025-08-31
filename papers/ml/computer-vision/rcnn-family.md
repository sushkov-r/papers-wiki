# R-CNN Lineage: Evolution of Region-Based CNN Detectors

The R-CNN family began in 2014 with R-CNN, which used region proposals (Selective Search) and CNNs for classification. It proved that deep nets could outperform traditional detectors like HOG + DPM (Deformable Part Models), but it was slow and multi-stage.

Fast R-CNN (2015) sped things up by sharing convolutional features and introducing RoI Pooling, but still relied on Selective Search.

Faster R-CNN (2015) solved this by adding the Region Proposal Network (RPN), creating a unified, end-to-end trainable detector. This architecture became the gold standard for detection through the late 2010s.

Mask R-CNN (2017) extended Faster R-CNN with RoIAlign and a parallel mask head, making instance segmentation practical and also extensible to keypoints and pose tasks.

The lineage surpassed older hand-crafted pipelines (HOG, DPM, sliding windows) and set the bar for accuracy. Over time, however, it was superseded by one-stage detectors ([YOLO](yolo-family), RetinaNet) for speed, and later by transformer-based models ([DETR](detr.md), Mask2Former, Mask DINO) for end-to-end training and unified segmentation frameworks.

## 1. R-CNN (2014)
- **Pipeline:**
  - Region proposals from *Selective Search* (~2000 per image).
  - Each proposal cropped, warped, passed through CNN (AlexNet/VGG).
  - Features classified with SVMs, boxes refined with linear regression.
- **Contributions:**
  - Showed ImageNet-pretrained CNNs can transfer to detection.
  - Introduced bounding box regression.
- **Drawbacks:** Very slow (thousands of forward passes), multi-stage training.

---

## 2. Fast R-CNN (2015)
- **Pipeline:**
  - Compute a single CNN feature map for the whole image.
  - Use *RoI Pooling* to extract fixed-size features per region proposal.
  - Train end-to-end with a multitask loss (softmax + Smooth L1 bbox reg).
- **Contributions:**
  - Shared computation across RoIs → huge speedup.
  - End-to-end single-stage training.
- **Drawbacks:** Still relied on external proposal methods (Selective Search).

---

## 3. Faster R-CNN (2015)
- **Pipeline:**
  - Introduced *Region Proposal Network (RPN)*: predicts objectness + bbox offsets from anchors.
  - Shared CNN backbone between RPN and detection head.
  - RoI Pooling for per-proposal features → classification + bbox regression.
- **Contributions:**
  - Replaced Selective Search with a learned, efficient RPN.
  - Unified detection pipeline, fully trainable end-to-end.
- **Impact:** Became the standard for two-stage detectors.

---

## 4. Mask R-CNN (2017)
- **Pipeline:**
  - Built on Faster R-CNN (backbone + RPN).
  - Replaced RoI Pooling with *RoIAlign* (no quantization, bilinear interpolation).
  - Added a parallel FCN-based branch for predicting segmentation masks.
- **Contributions:**
  - Enabled instance segmentation in a clean, modular way.
  - RoIAlign improved spatial accuracy for fine-grained tasks.
  - Framework easily extended to keypoints and pose estimation.

---

## 5. Beyond Mask R-CNN (2018 →)
- **PANet (2018):** Feature pyramid enhancements, mask info flow.
- **Cascade R-CNN (2018):** Multi-stage refinement of boxes.
- **Hybrid Task Cascade (2019):** Integrated detection + segmentation refinement.
- **DetectoRS, Libra R-CNN (2019):** Architecture/training improvements.
- **Transition to Transformers (2020+):** DETR, Mask2Former, Mask DINO superseded region-based designs.

---

## Timeline Overview
- **2014:** R-CNN → proof of CNN-based detection.
- **2015:** Fast R-CNN → shared features, faster.
- **2015:** Faster R-CNN → learned proposals via RPN.
- **2017:** Mask R-CNN → added segmentation, RoIAlign.
- **2018+:** Cascade R-CNN, PANet, HTC → refinements.
- **2020+:** [DETR family](detr-family.md) → shift to transformers, anchor-free, set-based detection.

---

For segmentation milestones and the transition to unified mask prediction, see the [segmentation history](segmentation-dnn-history.md).
