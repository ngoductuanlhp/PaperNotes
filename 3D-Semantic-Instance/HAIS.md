### Hierarchical Aggregation for 3D Instance Segmentation

_Aug 2021_

- Link: https://arxiv.org/pdf/2108.02350v1.pdf

### Overall

Propose a hierarchical aggregation to cluster pointcloud into instances

### Base
[**PointGroup: Dual-Set Point Grouping for 3D Instance Segmentation**](https://openaccess.thecvf.com/content_CVPR_2020/papers/Jiang_PointGroup_Dual-Set_Point_Grouping_for_3D_Instance_Segmentation_CVPR_2020_paper.pdf)

### Key ideas
![](images/hais_arch.png?raw=true)

- Backbone: 
    * convert pointcloud into regular grid.
    * apply a 3D Unet-like with Submanifold sparse convolution to extract voxel feature F<sub>voxel</sub>.
    * propagrate F<sub>voxel</sub> back to pointcloud to become point features F<sub>point</sub>. How to assign back the point feature ??? (maybe use interpolate)
- Semantic branch:
    * Use shared MLP for each point features.
- Instance branch:
    * Use shared MLP predict center shift offset (3 offsets from each point to its object's center) based on point features. 
- Point aggregation:
    * Shift each point based on its center shift.
    * Establish group of points with a fixed spatial radius.
    * ignore background points.
- Set aggregation: As point aggregation contains many fragments (false positive groups)
    * instead of hard thresholding small groups, use a cluster algo to combine primary instance and fragment
    * use a dynamic clustering bandwidth for cluster.
- Intra-instance Prediction Network (like ScoreNet in PointGroup method):
    * crop instance point cloud patches and use 3D sparse conv to extract feature of instances.
    * use shared MLP to learn per-point fore/background mask.
    * filter out background point, use shared MLP for foreground feature to learn confidence/certainty score (supervised by the IOU score with GT instance).
![](images/hais_intra_instance_network.png?raw=true)


### Detail Implementation:

- Process whole frame in a single pass as voxel backbone is lightweight.

### Results

- SOTA on both ScanNet(v2) and S3DIS.

- Time:
![](images/hais_time.png?raw=true)

### Notes

- Fast, efficient.
- Many SOTA on 3D detection (Waymo, KITTI) also use voxel-based backbone (with 3D sparse conv). Maybe better than PointNet-based backbone.
- Train an IOU confidence for each instance. The IOU supervised head for confidence/certain score is very trendy on 3D detection.