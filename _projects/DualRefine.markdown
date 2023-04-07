---
layout: page
title: DualRefine
description: "DualRefine: Self-Supervised Depth and Pose Estimation Through Iterative Epipolar Sampling and Refinement Toward Equilibrium"
img: https://dl.dropboxusercontent.com/s/7zpf026iwnc5vt9/DualRefine.PNG
importance: 1
category: Research
---
## Abstract

<span style="font-size:0.9em;">
Self-supervised multi-frame depth estimation achieves high accuracy by computing matching costs of pixel correspondences between adjacent frames, injecting geometric information into the network. These pixel-correspondence candidates are computed based on the relative pose estimates between the frames. Accurate pose predictions are essential for precise matching cost computation as they influence the epipolar geometry. Furthermore, improved depth estimates can, in turn, be used to align pose estimates.

Inspired by traditional structure-from-motion (SfM) principles, we propose the DualRefine model, which tightly couples depth and pose estimation through a feedback loop. Our novel update pipeline uses a deep equilibrium model framework to iteratively refine depth estimates and a hidden state of feature maps by computing local matching costs based on epipolar geometry. Importantly, we used the refined depth estimates and feature maps to compute pose updates at each step. This update in the pose estimates slowly alters the epipolar geometry during the refinement process. Experimental results on the KITTI dataset demonstrate competitive depth prediction and odometry prediction performance surpassing published self-supervised baselines.
</span>
<p style="margin: 0 auto; font-size:0.9em; text-align:left ; " markdown="1">
\[[Paper]()\] &nbsp; \[[Code](https://github.com/antabangun/DualRefine)\] 
  </p>

<br>


## Contributions

- <span style="font-size:0.9em;">We introduce an iterative update module that is based on epipolar geometry and direct alignment.</span>
- <span style="font-size:0.9em;">These updates refine theinitial estimates made by the single-frame model.</span>
- <span style="font-size:0.9em;">The model is designed within a deep equilibrium framework, which allows the model to converge to a fixed point.</span>

## Overall architecture
<p align="center">
  <img src="https://dl.dropboxusercontent.com/s/zwko0467yua2wab/Overall.gif" title="DualRefine overall architecture" data-zoomable width="50%">
  <p style="margin: 0 auto; font-size:0.8em; text-align:center ; max-width: 70%;">
  Given a pair of source and target images, the teacher model predicts an initial depth D0 and pose T0, as well as
initial hidden states that will be updated. DEQ-based alignments are then performed to find the fixed point and output the final predictions.</p>
</p>


## Experiments
### Comparison with state-of-the-art methods
<p align="center">
  <img src="https://dl.dropboxusercontent.com/s/7183l0l14pt2o9v/DualRefineComparisonTable.PNG" title="Comparison with state-of-the-art" data-zoomable>
  <p style="margin: 0 auto; font-size:0.8em; text-align:center ; max-width: 70%;">
  A comparative evaluation of the DualRefine model with recent leading self-supervised multi-frame depth estimation methods using the KITTI Eigen test split dataset.
  </p>
</p>

### Significance of pose refinement
<p align="center">
  <img src="https://dl.dropboxusercontent.com/s/vtwwak9fqyqubu3/DualRefinePoseTable.PNG" title="Pose ablation" data-zoomable width="30%">
  <p style="margin: 0 auto; font-size:0.8em; text-align:center ; max-width: 70%;">
  The model trained without pose refinement exhibit the poorest performance. In contrast, models employing pose refinement with learned per-pixel weights and refined pose for computing consistency masks achieve the best results overall. This highlights the crucial role of pose refinement in enhancing the accuracy of depth estimation.
  </p>
</p>

### Depth per iteration
<p align="center">
  <img src="https://dl.dropboxusercontent.com/s/zdc8bsz85mqcvk8/Iters.PNG" title="Depth error per iteration" data-zoomable width="30%">
  <p style="margin: 0 auto; font-size:0.8em; text-align:center ; max-width: 70%;">
  The depth error per iteration for the DualRefine model. The model converges to a fixed point after 6 iterations.
  </p>


<p align="center">
  <video width="960" height="540" controls>
    <source src="https://dl.dropboxusercontent.com/s/omnpmdoqkhdybci/Iterations.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
  <p style="margin: 0 auto; font-size:0.8em; text-align:center ; max-width: 70%;">
    On the left shows the initial depth estimates and on the right is the refined depth at each iteration. Note that the speed is slowed down for visualization purposes.
    Actual speed on our device with an RTX 3090 is around 15 fps.
  </p>
</p>
