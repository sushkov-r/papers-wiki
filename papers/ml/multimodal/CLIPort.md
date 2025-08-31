# CLIPort
[arxiv](https://arxiv.org/abs/2109.12098)

## Description
CLIPort (Shridhar et al., 2021) is a **[vision-language-action model](Vision-Language-Action-Models.md) for robotic manipulation**. It combines **[[CLIP]]-style vision-language embeddings** with **transport-based manipulation policies** to execute language-conditioned pick-and-place tasks. The system enables robots to understand and execute commands like *"place the red block on the blue block"* in cluttered scenes, without task-specific training.

---

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

---

## Key Innovations
- **Language grounding with CLIP:**  
  Uses pre-trained CLIP embeddings to enable zero-shot generalization to unseen instructions.  

- **Transporter policy architecture:**  
  Efficiently learns spatial manipulation policies by modeling pick → place as pixel transport, well-suited to pick-and-place actions.  

- **Zero-shot generalization:**  
  Can perform novel combinations of tasks and objects described in natural language, without retraining for every new command.  

---

## Applications
- **Robotics:**  
  Tabletop manipulation (stacking, sorting, arranging objects) conditioned on language.  

- **Embodied AI:**  
  Serves as a foundation for integrating internet-scale language-vision understanding with robot skills.  

---

## Results
- Outperformed baselines on multi-task robotic manipulation benchmarks.  
- Demonstrated **compositional generalization**, e.g., handling tasks with new object combinations or instructions not seen during training.  

---

## Impact
- One of the first practical demonstrations of **vision-language-action grounding** for robotic manipulation.  
- Inspired subsequent **VLA models** such as SayCan, RT-1/RT-2, and OpenVLA.  
- Highlighted the potential of leveraging large pre-trained vision-language models (like CLIP) in robotics.

---
