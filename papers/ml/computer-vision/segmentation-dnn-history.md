# Segmentation, Semantic Segmentation, and Instance Segmentation

### Segmentation (General)
- **Definition:** Any task that partitions an image into regions based on visual similarity or meaning.
- Can be unsupervised (clustering pixels) or supervised (learning labels).
- Examples:
  - Simple thresholding: foreground vs background.
  - Superpixel segmentation: grouping pixels with similar color/texture.

"Segmentation" is the umbrella term — it doesn’t specify what the regions *mean*.
### Semantic Segmentation
- **Definition:** Assigns a **class label to every pixel** in the image.
- Goal: understand *what category* each pixel belongs to.
- Example: label all pixels as **road, car, pedestrian, tree, sky**.
- **Limitation:** All objects of the same class get the same label, with no distinction between different instances.

Semantic segmentation answers: *“What class is this pixel?”* but not *“Which object is this pixel part of?”*
### Instance Segmentation
- **Definition:** Assigns a **unique mask for each object instance** in the image.
- Goal: differentiate not only the classes but also separate objects of the same class.
- Example: if there are three people in the image:
  - Semantic segmentation → all three labeled “person” with one mask.
  - Instance segmentation → produces **three distinct person masks**, one per individual.
- Combines detection (separating objects) + segmentation (precise shape).

Instance segmentation answers: *“Which object instance does this pixel belong to?”*
# History of Deep Learning–Based Segmentation
## Early CNN Segmentation (2014–2015)
- **Fully Convolutional Networks (FCN, 2014):** First end-to-end CNN for semantic segmentation. Replaced fully connected layers with convolutional ones to output dense per-pixel predictions.
- **U-Net (2015):** Encoder–decoder with skip connections. Became dominant in medical imaging.

**Key contribution:** Showed CNNs can produce dense segmentation maps, not just classification.
## Two-Stage Instance Segmentation (2017)
- **[Mask R-CNN](rcnn-family) (2017):** Extension of Faster R-CNN. Adds:
  - A **parallel mask branch** for per-instance binary masks.
  - **RoIAlign** (replacing RoI Pooling) for pixel-accurate alignment.
- Flexible and extensible (later adapted for keypoints, human pose).

**Impact:** Became the workhorse of instance segmentation.
## Refinements and One-Stage Alternatives (2018–2020)
- **PANet (2018):** Added feature pyramid enhancements and mask information flow to Mask R-CNN.
- **YOLACT (2019):** One-stage real-time instance segmentation using prototype masks + linear combination.
- **SOLO & SOLOv2 (2019–2020):** “Segmenting Objects by Locations” — direct instance segmentation without box proposals.

**Trend:** Shift toward faster, simpler models.
## Transformer Era of Segmentation (2020–2022)
- **DETR (2020):** Introduced transformers for object detection. Set-prediction with bipartite matching; no anchors or NMS.
- **Deformable DETR (2020):** Sparse attention for faster training and better small-object handling.
- **MaskFormer (2021):** Unified semantic + instance segmentation using per-segment embeddings.
- **Mask2Former (2022):** Improved MaskFormer with masked attention; strong across semantic, instance, and panoptic segmentation.

**Impact:** Transformers unify segmentation tasks under a clean set-based formulation.
## DETR Variants and DINO Family (2021–2023)
- **Conditional / DAB-DETR (2021):** Introduced spatially meaningful object queries (anchors).
- **DN-DETR (2022):** Added denoising training for stability.
- **DINO (2022):** Combined DN-DETR and DAB-DETR with iterative refinement and mixed query selection. Stronger performance, faster convergence.
- **Mask DINO (2022):** Added mask prediction; unified detection + segmentation.

**Impact:** Transformer-based models surpassed CNN-based two-stage frameworks.
## Current State of the Art (2024–2025)
- **DI-MaskDINO (2024):** Balanced decoder optimization between detection and segmentation tasks. Improved accuracy on COCO.
- **Large [[ViT]] Backbones (e.g., Swin, DINOv3):** Provide powerful feature encoders for segmentation.
- **SparseInst & Real-Time Models:** Achieve ~40 FPS on COCO with competitive accuracy, important for deployment.

**Summary:**
- Transformers (Mask2Former, Mask DINO, DI-MaskDINO) dominate accuracy benchmarks.
- Specialized lightweight models (SparseInst, YOLACT) target real-time applications.
- Unified frameworks handle **semantic, instance, and panoptic segmentation** in one model.
## Timeline Overview
- **2014:** FCN → first deep segmentation  
- **2015:** U-Net → encoder–decoder revolution  
- **2017:** [Mask R-CNN](rcnn-family) → mainstream instance segmentation  
- **2018–2020:** PANet, YOLACT, SOLO → refinements & one-stage efficiency  
- **2020:** [DETR](DETR.md) → transformers enter detection/segmentation  
- **2021–2022:** MaskFormer, Mask2Former → unified segmentation  
- **2022:** DINO, Mask DINO → strong DETR variants

---

For a broader evolution of transformer-based detectors, see the [DETR family overview](DETR-family.md), and for pre-transformer detection pipelines, see the [R-CNN lineage](rcnn-family.md).

