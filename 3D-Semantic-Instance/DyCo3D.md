### DyCo3D: Robust Instance Segmentation of 3D Point Clouds through Dynamic Convolution

_Aug 2021_

- Link: https://openaccess.thecvf.com/content/CVPR2021/papers/He_DyCo3D_Robust_Instance_Segmentation_of_3D_Point_Clouds_Through_Dynamic_CVPR_2021_paper.pdf

### Overall

3D instance segmentation by dynamic kernel.

### Base
[**PointGroup: Dual-Set Point Grouping for 3D Instance Segmentation**](https://openaccess.thecvf.com/content_CVPR_2020/papers/Jiang_PointGroup_Dual-Set_Point_Grouping_for_3D_Instance_Segmentation_CVPR_2020_paper.pdf)

[**SOLOv2: Dynamic and Fast Instance Segmentation**](https://arxiv.org/pdf/2003.10152.pdf)


### Key ideas
![](images/dyco3d_arch.png?raw=true)
- Backbone: 
    * apply a 3D Unet-like with sparse convolution.
    * use lighweight transformer between encoder and decoder to enhance longrange interactions.
- Head:
    * semantic head
    * centroid offset head
    * mask head
- Dynamic Weight Generator: insteaf of generating filter for every location on pixel-grid like SOLOv2, they first cluster points into group then generate filter for these groups.
    * use semantic and centroid offset heads to cluster.
    * voxelize each cluster with fixed size g, the feature for each cluster is the mask head from backbone.
    * use MLP to learn convolution weight for dynamic conv.
    * **Note**:
        * Different from PointGroup (treat the clusters as individual instance proposals), the clustering step only uses for generate filters for instances decoding.
    ![](images/dyco3d_dynamicconv.png?raw=true)
- Instance Decoder:
    * position-embedded feature F<sub>z</sub> = concat(F<sub>pos</sub>(3), F<sub>mask</sub>(D)).
    * instance-aware filter: from Dynamic Weight Generator.
    * Use dynamic conv (like SOLOv2) to generate binary masks.

### Detail Implementation:


### Results


### Notes
- Efficient: 0.28s compared with 0.39s for PointGroup.