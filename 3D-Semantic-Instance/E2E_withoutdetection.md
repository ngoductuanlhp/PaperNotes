### End-to-end 3D Point Cloud Instance Segmentation without Detection

_Aug 2021_

- Link: https://openaccess.thecvf.com/content_CVPR_2020/papers/Jiang_End-to-End_3D_Point_Cloud_Instance_Segmentation_Without_Detection_CVPR_2020_paper.pdf

### Overall

Propose a proposal-free sampling-assigning method for instance segmentation.

### Base: [**SGPN: Similarity Group Proposal Network for 3D Point Cloud Instance Segmentation**](https://openaccess.thecvf.com/content_cvpr_2018/papers/Wang_SGPN_Similarity_Group_CVPR_2018_paper.pdf)

Use embbeding features of points to calculate similarity matrix then grouping together.

### Key ideas

- Backbone:
    * Use PointNet to extract multi-type feature: semantic feature, instance-aware feature, centroid-aware feature, centroid-distance feature.
    * Concat semantic, instance-aware, centroid-aware features to form refined feature

- Sampling instance:
    * use farthest point sampling to sample fixed K instances (K is large enought to cover all instances).
    * 


### Detail Implementation:


### Results


### Notes