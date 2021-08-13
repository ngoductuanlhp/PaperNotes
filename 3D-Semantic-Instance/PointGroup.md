### PointGroup: Dual-Set Point Grouping for 3D Instance Segmentation

_Aug 2021_

- Link: https://openaccess.thecvf.com/content_CVPR_2020/papers/Jiang_PointGroup_Dual-Set_Point_Grouping_for_3D_Instance_Segmentation_CVPR_2020_paper.pdf

### Overall

Propose a multi-task network with 2 branches: semantic and centroid offset for clustering instances.


### Key ideas
![](images/grouppoint_arch.png?raw=true)

- Backbone: 
    * convert pointcloud into regular grid.
    * apply a 3D Unet-like with Submanifold sparse convolution to extract voxel feature F<sub>voxel</sub>.
- Semantic branch:
    * Use shared MLP for each point features.
- Instance branch:
    * Use shared MLP predict center shift offset (3 offsets from each point to its object's center) based on point features.
- Cluster instances:
    * 2 types of clusters: cluster based on original points (2 nearby instances may failed), cluster based on shifted points (large instances may failed).
    * For each types of point (original points and shifted point): use ball query with fixed radius r to group points. 
    * Union together.
- ScoreNet: use a shared mini 3D Unet (with sparse conv) for each cluster
![](images/grouppoint_scorenet.png?raw=true)
    * Concat position and point features in each cluster, use average pool to voxelize.
    * Use soft label to supervise the score of each cluster.
    * NMS base on the output score (as union original cluster and shifted cluster, need NMS)

### Detail Implementation:

- Process whole frame in a single pass as voxel backbone is lightweight.

### Results


### Notes

- Single-level clustering.
- Need NMS.