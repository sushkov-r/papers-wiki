# Key Tasks in Pick-and-Place Beyond Detection and Segmentation

Pick-and-place in robotics involves a **full perception-to-action pipeline**. Besides detection and segmentation, several other tasks are critical:

## Pose Estimation (6D Object Pose)
- **Goal:** Estimate the 3D position and orientation of objects to enable grasp planning.
- **Representative Papers:**
  - **PoseCNN** (Xiang et al., 2018) — CNN-based 6D pose estimation.
  - **DenseFusion** (Wang et al., 2019) — RGB-D dense fusion for 6D object pose.
  - **PVNet** (Peng et al., 2019) — Keypoint-based 6D pose estimation.
  - **GDR-Net** (Wang et al., 2021) — Geometry-guided direct regression for 6D pose.

## Grasp Detection / Grasp Pose Estimation
- **Goal:** Predict feasible grasp configurations (positions, orientations, gripper widths).
- **Representative Papers:**
  - **GraspNet-1Billion** (Fang et al., 2020) — Large-scale dataset and benchmark for grasp pose detection.
  - **PointNetGPD** (Liang et al., 2019) — Grasp detection using PointNet on point clouds.
  - **Contact-GraspNet** (Sundermeyer et al., 2021) — Generalizable 6-DoF grasp detection from depth images.
  - **GraspFormer** (Jiang et al., 2021) — Transformer-based grasp generation.

## Object Tracking
- **Goal:** Track objects over time for moving conveyors, dynamic bins, or human-robot collaboration.
- **Representative Papers:**
  - **Deep SORT** (Wojke et al., 2017) — Tracking-by-detection with deep appearance descriptors.
  - **CenterTrack** (Zhou et al., 2020) — Joint object detection and tracking.
  - **FairMOT** (Zhang et al., 2020) — Unified object detection + multi-object tracking.

## Motion Planning and Control
- **Goal:** Plan collision-free, efficient motions for the robot arm to execute the grasp and place actions.
- **Representative Papers:**
  - **CHOMP** (Ratliff et al., 2009) — Covariant Hamiltonian optimization for motion planning.
  - **TrajOpt** (Schulman et al., 2014) — Trajectory optimization with constraints.
  - **RRT* / BIT*** (Karaman & Frazzoli, 2011; Gammell et al., 2015) — Sampling-based motion planning.
  - **MoveIt! Framework** (2012+) — Widely used open-source motion planning library in robotics.

## Manipulation of Deformable Objects
- **Goal:** Handle flexible items (cloth, cables, bags, food items).
- **Representative Papers:**
  - **Nair et al., 2017** — Combining self-supervision and deep learning for cloth folding.
  - **Deep Deformable Grasping** (Sanchez et al., 2018) — Learning to manipulate deformable objects.
  - **DiffCloth** (Liang et al., 2022) — Differentiable cloth simulation for manipulation.

## Object Affordance Detection
- **Goal:** Identify actionable regions on objects (handles, flat surfaces).
- **Representative Papers:**
  - **AffordanceNet** (Do et al., 2018) — End-to-end affordance detection for manipulation.
  - **UOIS-Net** (Xiang et al., 2020) — Unseen object instance segmentation with affordance reasoning.

## Scene Understanding and Reasoning
- **Goal:** Understand occlusion, stacking, and task-specific constraints in cluttered environments.
- **Representative Papers:**
  - **MVPNet** (Han et al., 2019) — Multi-view point network for 3D scene understanding.
  - **TOTO: Topological Object Rearrangement** (Liu et al., 2022) — Task-oriented rearrangement planning.
  - **[[CLIPort]]** (Shridhar et al., 2021) — Language-conditioned manipulation with CLIP embeddings.

## Summary
Besides segmentation and detection, pick-and-place relies on:
- **Pose estimation** (where objects are in 3D),
- **Grasp detection** (how to pick them up),
- **Object tracking** (for dynamic scenes),
- **Motion planning/control** (how to move the robot),
- **Deformable manipulation** (for flexible objects),
- **Affordance detection** (where to grasp),
- **Scene reasoning** (understanding context, occlusions, task goals).

Each of these has produced influential papers that extend the perception-action pipeline toward reliable real-world robotic manipulation.
