# 3D Semantic Instance Segmentation

## Datasets

1. **ScanNet(v2)**:
    - Paper: https://arxiv.org/pdf/1702.04405.pdf
    - Download: https://github.com/ScanNet/ScanNet
    - Benchmark: http://kaldir.vc.in.tum.de/scannet_benchmark/semantic_instance_3d

2. **S3DIS**:
    - Paper: http://buildingparser.stanford.edu/images/3D_Semantic_Parsing.pdf
    - Download: http://buildingparser.stanford.edu/dataset.html
    - Benchmark: 

## Survey:

- [**Deep Learning for 3D Point Clouds: A Survey**](https://arxiv.org/pdf/1912.12033.pdf) (TPAMI 2020).
- [**Deep Learning based 3D Segmentation: A Survey**](https://arxiv.org/pdf/2103.05423.pdf) (ACM 2020).


## Approaches

![](images/timeline.png?raw=true)

### Proposal-based

- [**Learning Object Bounding Boxes for 3D Instance Segmentation on Point Clouds**](https://arxiv.org/pdf/1906.01140.pdf) (NeurIPS 2019 spotlight). ([Note](3D-BoNet.md))

### Proposal-free

#### Learning Dynamic Kernel

- [**DyCo3D: Robust Instance Segmentation of 3D Point Clouds
through Dynamic Convolution**](https://openaccess.thecvf.com/content/CVPR2021/papers/He_DyCo3D_Robust_Instance_Segmentation_of_3D_Point_Clouds_Through_Dynamic_CVPR_2021_paper.pdf) (CVPR 2021). ([Note](DyCo3D.md))

#### Grouping by centroid offset

- [**Hierarchical Aggregation for 3D Instance Segmentation**](https://arxiv.org/pdf/2108.02350v1.pdf) (ICCV 2021 - SOTA). ([Note](HAIS.md))

- [**PointGroup: Dual-Set Point Grouping for 3D Instance Segmentation**](https://openaccess.thecvf.com/content_CVPR_2020/papers/Jiang_PointGroup_Dual-Set_Point_Grouping_for_3D_Instance_Segmentation_CVPR_2020_paper.pdf) (CVPR 2020). ([Note](PointGroup.md))

#### Grouping by Similarity Matrix of embedding feature

- [**OccuSeg: Occupancy-aware 3D Instance Segmentation**](https://openaccess.thecvf.com/content_CVPR_2020/papers/Han_OccuSeg_Occupancy-Aware_3D_Instance_Segmentation_CVPR_2020_paper.pdf) (CVPR 2020). ([Note](OccuSeg.md))

- [**SGPN: Similarity Group Proposal Network for 3D Point Cloud Instance Segmentation**](https://openaccess.thecvf.com/content_cvpr_2018/papers/Wang_SGPN_Similarity_Group_CVPR_2018_paper.pdf) (CVPR 2018). ([Note](SGPN.md))

#### CRF

- [**JSIS3D: Joint Semantic-Instance Segmentation of 3D Point Clouds with
Multi-Task Pointwise Networks and Multi-Value Conditional Random Fields**](https://arxiv.org/pdf/1904.00699.pdf) (CVPR 2019). ([Note](JSIS3D.md))

### Sampling and assigning

- [**End-to-end 3D Point Cloud Instance Segmentation without Detection**](https://openaccess.thecvf.com/content_CVPR_2020/papers/Jiang_End-to-End_3D_Point_Cloud_Instance_Segmentation_Without_Detection_CVPR_2020_paper.pdf) (CVPR 2020). ([Note](E2E_withoutdetection).md))

