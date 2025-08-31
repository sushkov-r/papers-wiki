# Vision-Language-Action (VLA) Models

## Description
Vision-Language-Action (VLA) models extend vision-language architectures by grounding perception and reasoning in **action spaces**. These models connect what they **see** (vision), what they **understand/describe** (language), and what they can **do** (actions in an environment). They are key steps toward embodied AI, robotics, and interactive agents.
## Models

- **[[CLIPort]] (2021)**  
  Combined CLIP-style visual-language embeddings with affordance-based manipulation policies. Used in tabletop pick-and-place tasks.

- **SayCan (Google, 2022)**  
  Paired a large language model with visual grounding to plan high-level goals, then delegated execution to low-level robot skills. Demonstrated robots executing language commands in real-world kitchens.

- **PaLM-SayCan (2022)**  
  Extended SayCan using PaLM LLM. Provided better reasoning for task decomposition and grounding in affordance functions.

- **RT-1 (Google, 2022)**  
  A transformer-based robot policy trained on large-scale data of robot interactions. Input: images + language command. Output: low-level robot actions. Introduced the concept of **robotic transformer policies**.

- **RT-2 (Google DeepMind, 2023)**  
  Vision-Language-Action model trained on both internet-scale vision-language data and robot action data. Enabled robots to generalize from web knowledge to novel real-world tasks (e.g., "throw away the trash if it’s banana peel").

- **Octo (2023–2024)**  
  Open-source generalist VLA model trained across many robot platforms and datasets. Focused on reproducibility and community use.

- **OpenVLA (2024)**  
  Open-source alternative to RT-2, built to unify vision-language-action datasets into a generalist policy.
## Applications

- **Robotics**  
  Instruction-following for manipulation, navigation, cleaning, cooking, and other household or industrial tasks.

- **Embodied AI and Simulation**  
  Agents in simulated environments (e.g., Habitat, MineDojo) that take natural language commands and act.

- **Interactive Agents**  
  Virtual assistants and avatars that can perceive images, reason with language, and interact with environments through action APIs.

- **Autonomous Systems**  
  Vehicles, drones, and multi-modal decision-making systems benefiting from natural language grounding.
## Timeline

- **2021:** [[CLIPort]] demonstrates combining CLIP embeddings with robotic actions for manipulation.  
- **2022:** SayCan introduces LLM planning + robot skills; PaLM-SayCan scales this with a larger LLM.  
- **2022:** RT-1 proposes Robotic Transformer trained on large robot datasets.  
- **2023:** RT-2 integrates internet-scale vision-language pretraining with robot actions, enabling generalization from web knowledge.  
- **2023–2024:** Octo released as open-source large-scale VLA model.  
- **2024:** OpenVLA consolidates datasets into a reproducible, open VLA model.  
- **2025+:** Research expands into foundation VLA models combining massive web-scale data with diverse embodied robot experiences.
## Summary
- Vision-Language-Action models unify **perception, reasoning, and control**.  
- They evolved from combining CLIP with robot affordances ([[CLIPort]]), to **LLM-guided planning** (SayCan, PaLM-SayCan), to **transformer-based generalist robot policies** (RT-1, RT-2, Octo, OpenVLA).  
- Applications range from **robotics and embodied AI** to **interactive agents** and **autonomous systems**.  
- The trajectory mirrors NLP and vision: moving from **task-specific models** toward **foundation models** for action in the physical world.
