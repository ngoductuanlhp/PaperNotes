# SGPN: Similarity Group Proposal Network for 3D Point Cloud Instance Segmentation

_Aug 2021_

- Link: https://openaccess.thecvf.com/content_cvpr_2018/papers/Wang_SGPN_Similarity_Group_CVPR_2018_paper.pdf

### Overall

Pioneer in 3D sematic instance segmentation. The paper proposes a similarity matrix to group proposal, then a per-point classification for class segmentation.

### Key ideas
![](images/sgpn_arch.png?raw=true)

- Backbone: Pointnet/PointNet++
- Similarity Matrix: NxN matrix for similarity of N points in high-dimension feature space. Propose 3 levels of semantic instance level and train with Double-Hinge Loss
![](images/sgpn_hingerloss.png?raw=true)
- Similarity Confidence: confidence score for foreground/background.

### Detail Implementation:

- Divive scene to block of 1x1 m, 4096 points/sample for train, full points for test.
- Use block merging to merge samples to full scene.

### Results


### Notes

- Long inference time bce of processing multiple sample (1x1m blocks).
- Size of similarity matrix => hard to scale to large number of points.