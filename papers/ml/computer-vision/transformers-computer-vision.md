# History of Transformers in Computer Vision

## Origins: Attention and NLP (2017–2019)
- **Transformer (Vaswani et al., 2017):** Introduced self-attention for sequence modeling (NLP).
- **Key idea:** Replacing recurrence and convolution with self-attention.
- Set the foundation for adapting transformers to visual tasks.

---

## First CV Applications (2019–2020)
- **Image Transformer (Parmar et al., 2018):** Applied self-attention for image generation (small patches).
- **ViT – Vision Transformer (Dosovitskiy et al., 2020):**
  - Broke image into fixed-size patches, fed into standard transformer encoder.
  - Trained on large datasets (JFT-300M), achieved strong classification results.
  - Showed transformers can replace CNNs for image classification.
- **DETR – DEtection TRansformer (Carion et al., 2020):**
  - Applied transformer encoder–decoder to object detection.
  - Introduced set prediction, object queries, Hungarian matching.
  - First fully end-to-end detector without anchors or NMS.

---

## Early Variants and Efficiency Improvements (2020–2021)
- **DeiT (Touvron et al., 2020):** Data-efficient ViT, trained on ImageNet-1k without massive external data.
- **Deformable DETR (Zhu et al., 2020):** Sparse attention to speed up DETR training and improve small-object detection.
- **Conditional DETR (Meng et al., 2021):** Spatially aware object queries.
- **Swin Transformer (Liu et al., 2021):**
  - Hierarchical vision transformer with shifted windows.
  - Scalable backbone for detection, segmentation, classification.
  - Became a new standard vision backbone (like ResNet before).

---

## Expansion to Segmentation and Dense Prediction (2021–2022)
- **MaskFormer (Cheng et al., 2021):**
  - Unified segmentation via mask embeddings (semantic + instance).
- **Mask2Former (Cheng et al., 2022):**
  - Improved with masked attention.
  - Strong results across semantic, instance, panoptic segmentation.
- **DAB-DETR (Liu et al., 2022):**
  - Queries represented as anchor boxes, refined progressively.
- **DN-DETR (Li et al., 2022):**
  - Denoising task to stabilize training.
- **DINO (Zhang et al., 2022):**
  - Combined DAB and DN ideas.
  - Strong DETR baseline with faster convergence.
- **Mask DINO (Li et al., 2022):**
  - Extended DINO for segmentation.
  - Unified detection + segmentation under transformer decoder.

---

## Large-Scale Pretraining and Foundation Models (2022–2023)
- **CLIP (Radford et al., 2021, OpenAI):**
  - Vision-language transformer trained with contrastive learning.
  - Enabled open-vocabulary recognition and zero-shot transfer.
- **BEiT (Bao et al., 2021):** Masked image modeling for ViTs, inspired by BERT.
- **DINOv2 (Oquab et al., 2023):**
  - Self-supervised training of ViTs on massive data.
  - General-purpose backbone for many CV tasks.
- **Segment Anything (SAM, Kirillov et al., 2023):**
  - Promptable foundation model for segmentation.
  - Trained on SA-1B (largest segmentation dataset).
  - Transformer-based architecture, supports zero-shot interactive segmentation.

---

## Current SOTA and Specialization (2023–2025)
- **DI-MaskDINO (2024):**
  - Tackled decoder imbalance in detection vs. segmentation.
  - Introduced DI module + Balance-Aware Tokens Optimization (BATO).
  - State-of-the-art in instance segmentation.
- **YOLO-World (2024):**
  - Brought open-vocabulary detection to YOLO using CLIP embeddings.
- **Vision-Language-Action Models (2023–2025):**
  - Integrate vision transformers with LLMs (e.g., Flamingo, Kosmos, GPT-4V).
  - Move toward **multi-modal, multi-task perception and reasoning**.

---

## Timeline Overview
- **2017:** Transformer (NLP)  
- **2018:** Image Transformer (generation)  
- **2020:** ViT (classification), DETR (detection)  
- **2021:** DeiT (efficient ViT), Swin Transformer (hierarchical backbone)  
- **2021–22:** MaskFormer/Mask2Former (segmentation), DAB/Deformable/DN DETR variants  
- **2022:** DINO, Mask DINO  
- **2023:** CLIP/DINOv2 (foundation models), Segment Anything  
- **2024:** DI-MaskDINO (SOTA segmentation), YOLO-World (vision-language detection)  
- **2025+:** Vision-language-action models, unified multimodal transformers

---

## Summary
- **ViT** proved transformers work for image classification.  
- **DETR** brought them to object detection with set prediction.  
- **Swin** and **Mask2Former** generalized them to dense prediction tasks.  
- **CLIP, SAM, DINOv2** scaled transformers to foundation models with massive data.  
- **DI-MaskDINO** represents the current SOTA in segmentation, while multimodal models push into reasoning and interaction.  
