# Transporter Networks: Rearranging the Visual World for Robotic Manipulation  
*(Zeng et al., 2020)*, [arxiv](https://arxiv.org/abs/2010.14406)

## Description
Transporter Networks are designed for **learning robotic manipulation policies** from demonstrations, especially pick-and-place tasks. They treat manipulation as a **transport problem**, moving features from a pick location to a place location in an image.

In the basic formulation, a planar picking setup with fixed gripper rotation around z axis is assumed in this paper, which leads to a simplified formulation, in which picking location can be formulated as a "picking pixel" $T_{pick}~(u,v) \in o_t$. Place location may also include a discretized rotation dimension. Extensions to 6 DoF, sequential multi-step tasks and motion-primitive-based manipulation of deformable objects and piles of objects are discussed.

One of the key innovations of the paper is the calculation of the placement location using a convolution between a partial crop $\psi(o_t[T_{pick}])$ of query features with key features $\phi(o_t)$: $Q_{\text{place}}(\tau \mid o_t, T_{\text{pick}}) = \psi\big(o_t[T_{\text{pick}}]\big) \ast \phi(o_t)[\tau]$. In this formulation, the place location is the maximum of this convolution: $T_{\text{place}} = \arg\max_{\tau_i} \; Q_{\text{place}}(\tau_i \mid o_t, T_{\text{pick}})$.

## Architecture
- **Input:** RGB-D image of a tabletop scene.
- **Process:**
  - Encode the scene into a dense feature map.
  - Use cross-correlation between feature patches to generate an **attention map** that predicts where an object should be moved.
- **Output:** Pixel-to-pixel “transport” map that specifies pick → place correspondences.

## Key Innovations
- Reframed manipulation as a spatial transport operation, rather than explicit object modeling.
- Pixel-level learning avoids complex 3D reconstruction or object pose estimation.
- Data-efficient: Learns from relatively few demonstrations.

## Results
- Achieved strong performance on multi-step pick-and-place benchmarks.
- Showed generalization to unseen configurations and tasks.
- Outperformed reinforcement learning and imitation learning baselines in data efficiency.

## Impact
- Provided a practical way to learn **precise manipulation policies**.
- Became a core component in later **vision-language-action models** like [[CLIPort]], where Transporter networks are combined with [[CLIP]] embeddings for language grounding.
