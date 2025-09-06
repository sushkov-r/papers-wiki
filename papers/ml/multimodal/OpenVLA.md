# OpenVLA: An Open-Source Vision-Language-Action Model
# TODO
- add prismatic: https://arxiv.org/pdf/2402.07865

## Overview
OpenVLA (2024) is a fully open-source Vision-Language-Action model for robotics. It takes images and natural language instructions as input and predicts robot actions, enabling tasks like pick-and-place, sorting, and object rearrangement. Unlike earlier systems such as RT-2 (proprietary) or Octo (heavy, multi-institution infrastructure), OpenVLA emphasizes reproducibility: the training data, code, pretrained checkpoints, and evaluation protocols are all openly released.

## How It Works
- **Inputs:**  
  - RGB images of the robot’s environment.  
  - Natural language instructions.  

- **Model architecture:**  
  - Visual encoder (frozen [DINOv2](DINO#DINOv2) backbone) extracts dense tokens from the image.  
  - Text encoder (frozen language model, [Llama](Requests#Llama)) encodes the instruction.  
  - Tokens are concatenated and fed into a multimodal transformer.  
  - The transformer autoregressively predicts action tokens.  

- **Outputs:**  
  - Discrete action tokens representing 6-DoF end-effector deltas (position + orientation) and gripper state.  
  - These tokens are decoded back into robot actions for execution.  

- **Training:**  
  - Supervised imitation learning on **RT-X**, a large aggregation of robot demonstration datasets.  
  - Training objective is sequence prediction: predict the next action tokens given the current state and instruction.  

- **Evaluation:**  
  - Benchmarked on VLAsim (a standardized evaluation suite) and several real robot tasks.  
  - Success measured as task completion accuracy.  

## Key Contributions
- **Openness and reproducibility**: complete training recipes, model weights, and evaluation protocols are available.  
- **Standardized action representation**: continuous robot actions are discretized into a token space that can be learned by a transformer.  
- **Baseline for comparison**: establishes a community reference point similar to ImageNet for vision or GLUE for language.  

## Challenges and Open Questions
- **Action discretization**: Mapping continuous robot control into discrete tokens is central. The bins must be fine enough for precision, but coarse enough for efficient learning and generalization.  
- **Grounding instructions**: The model fuses language and vision simply by concatenating token embeddings. The challenge is ensuring that the language actually modulates the visual grounding, rather than being ignored by the policy. This depends heavily on dataset diversity.  
- **Generalization limits**: OpenVLA generalizes to some novel combinations of objects and instructions, but its capabilities are still bounded by the coverage of RT-X. Moving beyond imitation learning to broader reasoning or compositional generalization remains an open problem.  

## Summary
OpenVLA is the first fully open, reproducible VLA model trained at scale on real robot data. It provides a transparent reference for the field, enabling researchers to study and extend VLA architectures without relying on proprietary systems. Its architecture closely follows the RT-1/RT-2 design (transformer over vision and language tokens predicting action tokens), but its openness makes it a practical foundation for further work.
