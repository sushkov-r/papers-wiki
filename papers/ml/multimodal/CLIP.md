# CLIP: Learning Transferable Visual Models From Natural Language Supervision  
*(Radford et al., 2021)*, [arxiv](https://arxiv.org/abs/2103.00020)

## Description
CLIP (Contrastive Language–Image Pre-training) is a vision-language model trained on **400M image–text pairs** from the internet. It learns a shared embedding space for images and natural language, enabling **zero-shot transfer** to a wide variety of visual recognition tasks without task-specific training.

## Architecture
- **Image encoder:** Vision Transformer ([[ViT]]) or ResNet.
- **Text encoder:** Transformer-based language model.
- **Training objective:** Contrastive learning.
  - Align image and text embeddings so that matching pairs have high similarity, and mismatched pairs have low similarity.
  - Loss: Symmetric InfoNCE loss over large batches.

## Key Innovations
- Showed that **natural language is an effective supervision signal** for learning transferable visual features.
- Unified vision and language into a common embedding space.
- Enabled **zero-shot classification** by turning class names into prompts (e.g., “a photo of a dog”).

## Results
- Strong performance on >30 benchmark datasets with no fine-tuning.
- Outperformed supervised baselines on many tasks by using text prompts.
- Demonstrated **open-vocabulary recognition**, generalizing to unseen categories.

## Impact
- Widely adopted in computer vision, robotics, and multimodal AI.
- Provided foundation for downstream models like CLIPort (robotics), Flamingo (vision-language), and Stable Diffusion (text-to-image).
