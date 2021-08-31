## DyCo3D: Robust Instance Segmentation of 3D Point Clouds through Dynamic Convolution

_Aug 2021_

- Link: https://openaccess.thecvf.com/content/CVPR2021/papers/He_DyCo3D_Robust_Instance_Segmentation_of_3D_Point_Clouds_Through_Dynamic_CVPR_2021_paper.pdf

### Overall
#### Problem statement
3D instance segmentation: provide per-point semantic classes and instance level.
#### Application
Real-world applications: autonomous driving, robotics, and augmented/virtual reality.
#### Challenge
- Irregularity and sparsity of the pointcloud data format.
- Diversity of objects and scenes.
#### Typical approaches + limitation
- Top-down approaches: detect proposals then predict mask in each proposals.
- Bottom-up approaches: learning per-point embedding feature then grouping
    * sensitive to parameter for clustering (need fine-tune).
    * complex post-processing steps.
- Dynamic Conv (ex: SOLOv2, CondInst):
    * large amount of computation.
    * limited receptive field and representation of sparse conv.
#### General idea: 
- Sparse Conv with Transformer for feature extractor.
- Learn dynamic kernel for each proposal group to refine the instances via dynamic convolution.

### Base
[**PointGroup: Dual-Set Point Grouping for 3D Instance Segmentation**](https://openaccess.thecvf.com/content_CVPR_2020/papers/Jiang_PointGroup_Dual-Set_Point_Grouping_for_3D_Instance_Segmentation_CVPR_2020_paper.pdf)

[**SOLOv2: Dynamic and Fast Instance Segmentation**](https://arxiv.org/pdf/2003.10152.pdf)


### Key ideas
![](images/dyco3d_arch.png?raw=true)
- Backbone: 
    * apply a 3D Unet-like with sparse convolution.
    * use lighweight transformer between encoder and decoder to enhance longrange interactions:
        - positional encoding: mean of the pairwise direction vector or relative position.
- Head:
    * semantic head
    * centroid offset head
    * mask head
- Dynamic Weight Generator: insteaf of generating filter for every location on pixel-grid like SOLOv2, they first cluster points into group then generate filter for these groups.
    * use semantic and centroid offset heads to cluster.
    * voxelize each cluster with fixed size g, the feature for each cluster is the mask head from backbone.
    * Weight Generator network: sparse conv + global pool + MLP
    * **Note**:
        * Different from PointGroup (treat the clusters as individual instance proposals), the clustering step only uses for generate filters for instances decoding.
    ![](images/dyco3d_dynamicconv.png?raw=true)
- Instance Decoder:
    * For each point, position-embedded feature F<sub>z</sub> = concat(F<sub>pos</sub>(3), F<sub>mask</sub>(D)).
    * instance-aware filter: from Dynamic Weight Generator.
    * For each dynamic filter, apply dynamic conv (like SOLOv2) to all points with same semantic label of cluster which generates the filter to create binary masks:


### Detail Implementation:
- Loss:
    ![](images/dyco3d_loss.png?raw=true)
- NMS on the instance binary masks, scored by semantic score of foreground points. IoU thresh = 0.3, ignore cluster < 50 points.
- Voxelize with size 0.02m and 0.05m for ScanNetv2 and S3DIS.
- First 12k iters: train only seg loss and centroid loss, next 38k iters: all losses.


### Results
![](images/dyco3d_resultsval.png?raw=true)

### Notes
- Efficient: 0.28s compared with 0.39s for PointGroup.