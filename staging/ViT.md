# Vision Transformer (ViT)

## Description
The Vision Transformer (ViT, Dosovitskiy et al., 2020) was the first model to show that a pure transformer architecture can outperform convolutional networks on large-scale image classification. Instead of convolutions, ViT processes images as sequences of fixed-size patches, treating them similarly to word tokens in NLP.

## Architecture
- An image is divided into non-overlapping patches (e.g., 16×16 pixels).
- Each patch is flattened and linearly projected into a vector embedding.
- A special \[CLS\] token is prepended for classification.
- Positional embeddings are added to preserve spatial information.
- The sequence of patch embeddings is fed into a standard transformer encoder (multi-head self-attention + feed-forward layers).
- The final \[CLS\] embedding is used for classification.

## Innovations
- Reframing vision as a sequence modeling problem, enabling direct transfer of NLP transformer architectures.
- Demonstrated that global self-attention can replace local convolutional inductive biases if enough data is available.
- Introduced patch embeddings as the vision analogue to word embeddings.

## Limitations
- Requires very large datasets (e.g., JFT-300M) to train effectively; struggles on smaller datasets without heavy augmentation or distillation.
- Computationally expensive due to quadratic attention complexity with respect to the number of patches.
- Lacks built-in locality and inductive biases that CNNs provide, making data efficiency lower.

## Impact
- Established transformers as a new backbone for computer vision.
- Inspired numerous follow-ups improving efficiency and data efficiency:
  - DeiT (2020) — trained ViTs on ImageNet-1k with distillation.
  - Swin Transformer (2021) — introduced hierarchical, shifted window attention.
  - DINOv2 (2023) — large-scale self-supervised ViT training for foundation models.
- Provided the architectural foundation for transformer-based detectors (e.g., DETR) and segmentation frameworks (e.g., Mask2Former).

