### Learning Object Bounding Boxes for 3D Instance Segmentation on Point Clouds

_Aug 2021_

- Link: https://arxiv.org/pdf/1906.01140.pdf

### Overall

Propose a proposal network to detect 3D bounding box (anchor free), and a parallel branch for point-level mask for each instance

### Key ideas
![](images/3dbonet_arch.png?raw=true)

- PointNet++ to learn global feature and local feature.
    * Use global feature for bounding box proposal network.
    * Predefine number of box (H = 20).
    * Use Hungarian algo to assign predicted and gt box based on multi-criteria: Euclidean Distance between Vertices, Soft Intersection-over-Union on
Points (differentiable), Cross-Entropy Score.
![](images/3dbonet_bbox_proposal.png?raw=true)
- Point Mask Prediction: use shared MLP to learn confidence score of fore/background.
    * concatenate local features, global feature, box feature ( estimated vertices and score)
- Train a parallel SCN network to learning per-point semantic label.

### Detail Implementation:

- Divive scene to block of 1x1 m, 4096 points/sample for train, full points for test.
- Use block merging to merge samples to full scene.

### Results


### Notes

- Long inference time bce of processing multiple sample (1x1m blocks).
- Different network for semantic and instance tasks.
- Can a single global feature vector regress multiple bboxes in this sample ???