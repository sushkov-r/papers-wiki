# CLIPort
[arxiv](https://arxiv.org/abs/2109.12098)

## Description
CLIPort (Shridhar et al., 2021) is a **[vision-language-action model](Vision-Language-Action-Models.md) for robotic manipulation**. It combines **[[CLIP]]-style vision-language embeddings** with **[transport-based manipulation policies](TransporterNetworks)** to execute language-conditioned pick-and-place tasks. The system enables robots to understand and execute commands like *"place the red block on the blue block"* in cluttered scenes, without task-specific training.

## Architecture
- **Input:**  
  - RGB-D observations of a tabletop scene.  
  - Natural language instruction (e.g., "stack the green cube on the yellow cylinder").  

- **Core components:**  
  - **CLIP backbone:** Aligns vision and language into a shared embedding space. This grounds visual perception in natural language.  
  - **Transporter Network:** Learns spatial pick-and-place affordances by predicting pixel-to-pixel "transport" maps from source (pick) to target (place) locations.  
  - **Fusion:** Language embeddings from CLIP modulate the transporter network, conditioning action predictions on the instruction.  

- **Output:**  
  - A **pick location** and **place location** in the scene, represented as 3D coordinates relative to the robot.  

## Key Innovations
- **Language grounding with CLIP:**  
  Uses pre-trained CLIP embeddings to enable zero-shot generalization to unseen instructions.  

- **Transporter policy architecture:**  
  Efficiently learns spatial manipulation policies by modeling pick → place as pixel transport, well-suited to pick-and-place actions.  

- **Zero-shot generalization:**  
  Can perform novel combinations of tasks and objects described in natural language, without retraining for every new command.  

## Fusion of semantic and spatial streams
Fusion of the CLIP and Transporter networks is the key innovation in this paper. The following embeddings are fused:
- $v_t$: the embedding up until the penultimate layer of the CLIP's visual ResNet of the size 7x7x2048 is upsampled to match the Transporter shape ($h \times w \times C$),
- $g_t$: CLIP sentence encoder (embedding of the length 1024) is downsampled down to C and then tiled ($h \times w \times C$) to match the shape of the transporter layer
- $l_t$: Transporter embedding layers of the shape $h \times w \times C$.

The semantic (ventral) embeddings are combined through an element-wise product $v_t \odot g_t$. We are allowed to do this because these embeddings are aligned:
- **Final-layer alignment:** CLIP’s contrastive loss guarantees that the **final projected embeddings** (image 1024-d vs. text 1024-d) are aligned in a common space.
- **Penultimate layer features:** Those conv features (7×7×2048 from ResNet, or patch tokens from ViT) aren’t strictly aligned with text, but because they feed into the final aligned projection, they already encode semantically meaningful structure (objectness, color, shape).
- **Projection layers in CLIPort:** Before fusion, both vision features and text embeddings are passed through additional learned projections. These do two things:
    1. **Shape normalization** (so dimensions match, e.g. down to d=64).
    2. **Re-alignment** (fine-tune so that element-wise operations actually mix compatible channels).
Fusion of the semantic and the spatial (dorsal) embeddings is performed by concatenating these embeddings, which increases the number of channels  ($w \times h \times C_v + C_d$), followed by the 1x1 convolution, which reduces the number 

## Results
- Outperformed baselines on multi-task robotic manipulation benchmarks.  
- Demonstrated **compositional generalization**, e.g., handling tasks with new object combinations or instructions not seen during training.  

## Impact
- One of the first practical demonstrations of **vision-language-action grounding** for robotic manipulation.  
- Inspired subsequent **VLA models** such as SayCan, RT-1/RT-2, and OpenVLA.  
- Highlighted the potential of leveraging large pre-trained vision-language models (like CLIP) in robotics.
