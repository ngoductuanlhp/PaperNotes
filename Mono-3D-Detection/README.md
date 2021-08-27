# Monocular 3D Object Detection

Detect 3D object's bounding box (position, dimension, orientation) in real-world coordinate using only RGB image/stereo image.

## Datasets

1. **KITTI**:
    - Paper: http://www.cvlibs.net/publications/Geiger2012CVPR.pdf
    - Download: http://www.cvlibs.net/datasets/kitti/
    - Benchmark: http://www.cvlibs.net/datasets/kitti/eval_object.php?obj_benchmark=3d

## Survey:

- [**Survey blog by Patrick Liu on Medium**](https://medium.com/m/global-identity?redirectUrl=https%3A%2F%2Ftowardsdatascience.com%2Fmonocular-3d-object-detection-in-autonomous-driving-2476a3c7f57e).

## Approaches

### Representation Transform

- [**Categorical Depth Distribution Network for Monocular 3D Object Detection**](https://openaccess.thecvf.com/content/CVPR2021/papers/Reading_Categorical_Depth_Distribution_Network_for_Monocular_3D_Object_Detection_CVPR_2021_paper.pdf) (CVPR 2021).

### Anchor-based

- [**Geometry-based Distance Decomposition for Monocular 3D Object Detection**](https://arxiv.org/pdf/2104.03775.pdf)

- [**Learning Depth-Guided Convolutions for Monocular 3D Object Detection**](https://openaccess.thecvf.com/content_CVPRW_2020/papers/w60/Ding_Learning_Depth-Guided_Convolutions_for_Monocular_3D_Object_Detection_CVPRW_2020_paper.pdf) (CVPR 2020).

- [**M3D-RPN: Monocular 3D Region Proposal Network for Object Detection**](https://openaccess.thecvf.com/content_ICCV_2019/papers/Brazil_M3D-RPN_Monocular_3D_Region_Proposal_Network_for_Object_Detection_ICCV_2019_paper.pdf) (ICCV 2019).

### Anchor-free

- [**Objects are Different: Flexible Monocular 3D Object Detection**](https://openaccess.thecvf.com/content/CVPR2021/papers/Zhang_Objects_Are_Different_Flexible_Monocular_3D_Object_Detection_CVPR_2021_paper.pdf) (CVPR 2021).

- [**Monocular 3D Object Detection: An Extrinsic Parameter Free Approach**](https://openaccess.thecvf.com/content/CVPR2021/papers/Zhou_Monocular_3D_Object_Detection_An_Extrinsic_Parameter_Free_Approach_CVPR_2021_paper.pdf) (CVPR 2021).

- [**Monocular 3D Detection with Geometric Constraints
Embedding and Semi-supervised Training**](https://arxiv.org/pdf/2009.00764.pdf) (IEEE Robotics & Automation letter).

- [**RTM3D: Real-time Monocular 3D Detection from Object Keypoints for
Autonomous Driving**](https://arxiv.org/pdf/2001.03343.pdf) (ECCV 2020).

- [**SMOKE: Single-Stage Monocular 3D Object Detection via Keypoint Estimation**](https://openaccess.thecvf.com/content_CVPRW_2020/papers/w60/Liu_SMOKE_Single-Stage_Monocular_3D_Object_Detection_via_Keypoint_Estimation_CVPRW_2020_paper.pdf) (CVPR 2020).