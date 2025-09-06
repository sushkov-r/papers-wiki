### Notes
*There may be some confusion about the DINO model. Note that there are two papers that named their model DINO, one of them is a variant of DETR [the other](DINO) is a foundation model from Meta.*
# DETR: DEtection TRansformer (Carion et al., 2020)
- **DETR** reframes object detection as a **direct set prediction problem** using a transformer encoder–decoder architecture.
- Pipeline:
  1. **Backbone (ResNet/[[ViT]]):** Extract image features.
  2. **Transformer Encoder:** Applies global self-attention to the feature map.
  3. **Transformer Decoder:** Takes a fixed number of learned **object queries** and predicts class + bounding box for each.
  4. **Hungarian Matching Loss:** One-to-one assignment between predictions and ground truth ensures unique objects.
**Key idea:** No anchors, proposals, or NMS. Detection is end-to-end, learned directly.
## Pre-DETR (Before 2020): State of the Art in Detection and Segmentation
*TODO: move this section to [[segmentation-dnn-history]]*
### Two-Stage Detectors ([R-CNN Family](R-CNN-family.md))
- **R-CNN (2014):** CNN features + region proposals (Selective Search).
- **Fast R-CNN (2015):** Shared conv features, RoI Pooling, end-to-end multitask loss.
- **Faster R-CNN (2015):** Introduced Region Proposal Network (RPN), fully learnable pipeline.
- **Mask R-CNN (2017):** Added segmentation branch and RoIAlign for instance masks.
- **Cascade R-CNN (2018):** Multi-stage detector with progressively stricter IoU thresholds.
- **Hybrid Task Cascade (2019):** Joint refinement for detection + segmentation.

**Strengths:** Very accurate, extensible, dominant in research.  
**Weaknesses:** Complex pipelines (anchors, proposals, NMS), relatively slow.
### One-Stage Detectors
- **[YOLO](YOLO-family.md) (2016 → v3 in 2018):** Real-time detection by regressing boxes and classes directly on a grid.
- **SSD (2016):** Multi-scale feature maps with default anchor boxes.
- **RetinaNet (2017):** Introduced **Focal Loss** to handle extreme class imbalance, achieving strong accuracy while staying single-stage.

**Strengths:** Fast, simpler than two-stage methods.  
**Weaknesses:** Slightly less accurate than Faster/Mask R-CNN (until RetinaNet closed the gap).
### Segmentation Approaches
- **FCN (2014):** First fully convolutional semantic segmentation network.
- **U-Net (2015):** Encoder–decoder with skip connections, huge impact in medical imaging.
- **DeepLab series (2015–2018):** Used atrous/dilated convolutions, CRFs, and later atrous spatial pyramid pooling (ASPP).
- **Mask R-CNN (2017):** Instance segmentation baseline.
- **PANet (2018):** Improved feature pyramids and mask refinement.
- **YOLACT (2019):** One-stage real-time instance segmentation using prototype masks.

**Strengths:** Mature, high-performing segmentation pipelines.  
**Weaknesses:** Still relied on bounding boxes + proposals, complex heuristics.
### Common Characteristics Before DETR
- Heavy reliance on **anchors**, **proposals**, and **Non-Maximum Suppression (NMS)**.
- Multi-stage training and complex heuristics.
- CNN-based backbones (ResNet, ResNeXt, FPN) dominated.
- Trade-off: **two-stage = accuracy, one-stage = speed**.
- Segmentation treated as **detection + mask refinement**, not a unified task.
### Overall Landscape by 2019
- **Mask R-CNN** → default for instance segmentation.  
- **Faster R-CNN / Cascade R-CNN** → state-of-the-art two-stage detection.  
- **RetinaNet & [YOLOv3](YOLO-family.md)** → strong single-stage detectors.  
- **DeepLabv3+** → state-of-the-art semantic segmentation.  
- **Hybrid Task Cascade, PANet, YOLACT** → refinements and efficiency gains.  

**In short:** By 2019, CNN-based detection and segmentation had matured into very strong, but still **fragmented and heuristic-heavy pipelines**. DETR (2020) disrupted this by introducing **transformers, set prediction, and end-to-end training**, removing the need for anchors, proposals, and NMS.
## Key Innovations in DETR
1. **Set Prediction Formulation**
   - Recasts detection as predicting a fixed set of objects (queries ↔ objects).
   - Removes duplicates naturally — no need for Non-Maximum Suppression (NMS).

2. **Hungarian Matching Loss**
   - One-to-one matching between predicted objects and ground truth.
   - Ensures each prediction corresponds to exactly one object (or “no object” class).
   - Prevents duplicate detections, which plagued earlier anchor-based methods.

3. **Object Queries**
   - Learned embeddings that serve as “slots” for different objects.
   - Decoder refines these queries by attending to the image features.
   - Each query outputs exactly one box + class.

4. **End-to-End Pipeline**
   - Unlike [Faster R-CNN](R-CNN-family.md) or [YOLO](YOLO-family.md) (which need anchors, proposals, and NMS), DETR requires only the backbone + transformer + prediction heads.
   - Simplifies the detection pipeline dramatically.
## Relation to Vision Transformer (ViT)
- **[[ViT]] (Dosovitskiy et al., 2020):**
  - Pure transformer for image classification.
  - Splits an image into fixed-size patches, embeds them, and feeds them into a transformer encoder.
  - Outputs a class embedding for classification.
- **DETR:**
  - Uses a CNN backbone (ResNet) for feature extraction (not patches initially).
  - Then flattens the feature map and passes it through a transformer encoder (like ViT).
  - Adds a **decoder** with **object queries**, which ViT does not have.
  - Instead of one global class token (ViT), DETR uses multiple queries to predict multiple objects.

In short: DETR = ViT + decoder + object queries + set prediction loss.  
It’s the *detection counterpart* to ViT’s classification formulation.
# Limitations
## Slow Convergence
- **Problem:** Vanilla DETR needed **500+ epochs** on COCO to converge, compared to ~36 epochs for Faster R-CNN.
- **Why:** 
  - Matching queries to objects from scratch is hard.
  - The bipartite matching (Hungarian loss) makes training unstable early on.
- **Solutions:**
  - **Deformable DETR (2020):** Sparse attention → faster convergence (~50 epochs).
  - **DN-DETR (2022):** Added denoising task to stabilize matching and accelerate learning.
  - **DINO (2022):** Combined denoising + dynamic anchors → strong baseline with fast convergence.
## Poor Small-Object Detection
- **Problem:** DETR struggled with small objects (e.g., faraway people, tiny items).
- **Why:** 
  - Queries distribute attention across the whole image.
  - No explicit multi-scale features in original design.
- **Solutions:**
  - **Deformable DETR:** Multi-scale deformable attention improves small-object handling.
  - **Swin Transformer (2021):** Hierarchical features for multiple scales.
  - **Mask2Former (2022):** Unified segmentation with masked attention at multiple scales.
## Heavy Computation (Quadratic Attention)
- **Problem:** Transformer encoder has **O(N²)** complexity in the number of image tokens.
- **Why:** Full self-attention compares all tokens with all others.
- **Solutions:**
  - **Deformable DETR:** Sparse attention to selected key points.
  - **Swin Transformer:** Shifted window attention reduces complexity to O(N).
  - **Efficient DETR variants (2021–2023):** Explore locality and sparse attention to reduce cost.
## Fixed Number of Queries
- **Problem:** DETR always predicts a fixed number of objects (e.g., 100), padded with “no object”.
- **Why:** Design of Hungarian matching requires a fixed set size.
- **Issues:** Wasteful, and not adaptive to image content.
- **Solutions:**
  - **Dynamic DETR Variants (DAB-DETR, 2022):** Represent queries as anchors, refined iteratively.
  - **Sparse DETR approaches:** Activate only needed queries.
## Generalization / Data Requirements
- **Problem:** ViT-like architectures require **large datasets** to train well.
- **Solutions:**
  - **DeiT (2020):** Showed transformers can be trained on ImageNet-1k with strong augmentation/distillation.
  - **DINOv2 (2023):** Large-scale self-supervised training produced general-purpose visual transformers.
## Segmentation Limitations
- **Problem:** Original DETR was focused on detection, not segmentation.
- **Solutions:**
  - **MaskFormer (2021):** Extended DETR-like design to segmentation via mask embeddings.
  - **Mask2Former (2022):** Unified semantic, instance, panoptic segmentation with masked attention.
  - **Mask DINO (2022):** Added segmentation branch to DINO.

## Impact
- Introduced transformers into object detection.
- Inspired a wave of improved DETRs (Deformable DETR, Conditional DETR, DAB-DETR, DN-DETR, DINO, Mask DINO, DI-MaskDINO).
- Established a clean, general paradigm for detection and segmentation tasks.