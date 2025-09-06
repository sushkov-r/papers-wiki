# Emerging Properties in Self-Supervised Vision Transformers (DINO)
### Notes
*Not to be confused with [DINO (a variant of DETR)](DETR.md).*

## Overview
DINO introduced a simple but powerful self-supervised learning approach for [Vision Transformers (ViTs)](ViT.md). The method trains a student network to predict the output of a teacher network, without any labels, by aligning their representations of different augmented views of the same image. Remarkably, DINO shows that ViTs trained this way learn highly semantic and interpretable features.

## Key Innovations
- **Self-distillation without labels**: The model trains a student network to match the teacher’s soft predictions, with no ground-truth supervision.
- **EMA teacher update**: The teacher is an exponential moving average (EMA) of the student, ensuring stable training targets.
- **Multi-crop augmentation**: Student sees both global and local crops, teacher sees only global crops. This asymmetry forces invariance across scales and viewpoints.
- **Collapse prevention**: Introduced two mechanisms:
  - **Centering** of teacher outputs (subtracting a running mean).  
  - **Sharpening** with a low softmax temperature to avoid trivial constant outputs.

## How Self-Distillation Works
1. **Input views**: From an input image, generate several augmentations:
   - Global crops (large image regions).
   - Local crops (smaller patches).
	Multiple local crops and two global crops are generated for each image.
1. **Teacher network**: Processes only global crops. Produces a probability distribution from the \[CLS\] token after a projection head.
2. **Student network**: Processes all crops. Must match its distribution to the teacher’s, even when seeing only local patches.
3. **Loss**: Cross-entropy between student predictions and teacher’s distribution for corresponding views.
4. **Teacher update**: Teacher parameters are updated as an EMA of the student’s, not by gradients. EMA teacher essentially performs a form of model ensembling similar to Polyak-Ruppert averaging with an exponential decay.

This forces the student to align local and global views into a shared representation space, leading to semantically meaningful features.

## Results
- DINO-trained ViTs achieve strong linear probe accuracy on ImageNet (>75% top-1 without labels).
- Features are highly **semantic and interpretable**:
  - Attention heads correspond to meaningful object parts.
  - Features cluster naturally into object categories.
- Outperformed prior self-supervised methods (BYOL, SimCLR) on several benchmarks.

## Impact
- Showed that **ViTs + self-distillation** can learn semantic representations without labels.
- Provided a foundation for later self-supervised ViT approaches (e.g., DINOv2, MAE).
- Popularized the use of ViT features for transfer learning and downstream tasks.

# DINOv2

## Data
- **DINO (2021):** Trained on ImageNet without labels (1.3M images).  
- **DINOv2 (2023):** Trained on a **curated dataset of 142M images** (from a pool of 1.2B).  
  - Applied **automatic filtering, deduplication, and quality control** to remove noisy web data.  
  - This scaling of both size and quality is a key driver of performance.

## Architecture
- **DINO:** Experiments mostly with ViT-Small and ViT-Base.  
- **DINOv2:** Trained **much larger ViTs** (up to ViT-G/14 with ~1B parameters).  
  - Showed clear **scaling laws** for self-supervised vision transformers.

## Training Recipe
- **DINO:** Introduced self-distillation (student–teacher EMA, centering, sharpening) but relatively unstable at large scale.  
- **DINOv2:** Refined recipe:  
  - Improved **teacher sharpening schedule** (temperature tuning).  
  - Better **normalization and loss scaling**.  
  - More robust multi-crop strategy.  
  - Enabled training of giant ViTs without collapse.

## Features and Transferability
- **DINO:** Learned semantic features useful for linear probing on ImageNet (~75% top-1 with ViT-B).  
- **DINOv2:** Produces **foundation-model-level features**:  
  - Stronger linear probe results (86.8% top-1 with ViT-L, 88.1% with ViT-G).  
  - Features transfer seamlessly to downstream tasks (detection, segmentation) without fine-tuning.  
  - Introduced **scale-invariant features** (same embedding regardless of image size/resolution).  

## Overall
- **DINO was a proof of concept**: self-distillation works for ViTs and yields semantic representations.  
- **DINOv2 is a foundation model**:  
  - Trained on huge curated data.  
  - Uses stabilized training recipe.  
  - Scales to very large models.  
  - Produces universal, robust features for many tasks.
