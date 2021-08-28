### Few-shot 3D Point Cloud Semantic Segmentation

_Aug 2021_

- Link: https://openaccess.thecvf.com/content/CVPR2021/papers/Zhao_Few-Shot_3D_Point_Cloud_Semantic_Segmentation_CVPR_2021_paper.pdf

### Overall

Few-shot 3D semantic segmentation by proposing attention-aware multi-prototype and transductive learning.

### Base
- Transductive learning:
[**Learning with Local and Global Consistency**](https://papers.nips.cc/paper/2003/file/87682805257e619d49b8e0dfdc14affa-Paper.pdf)


### Key ideas
![](images/FS3D_arch.png?raw=true)
- Baseline: query and support set:
    ![](images/FS3D_baseline.png?raw=true)
- Embedding Network:
    - Use DGCNN with EdgeConv to extract per-point feature.
    - Propose self-attention network (SAN) to aggregate the global contextual information of the corresponding point cloud.
    - Add metric learner (MLP) with bigger LR than the feature extractor for faster adapt.
    - Concatenate the three levels of learned features.
- Multi-prototype Generation: for each of N+1 class (+1 background), generate n prototypes by clustering:
    * Sample n seed points by farthest point sampling.
    * Compute point-to-seed distance and assign points to seeds.
    * Calculate multi-prototype feature vector by average pooling:
    ![](images/FS3D_multiprototype.png?raw=true)
- Transductive Inference:
    * k-NN graph:
        - Vertices: V = n×(N + 1) multiprototypes and T×M query points.
        - construct a sparse affinity matrix A by computing the Gaussian similarity between each node and its k nearest neighbors.
    * Label propagation:
        - Follow [Learning with Local and Global Consistency](https://papers.nips.cc/paper/2003/file/87682805257e619d49b8e0dfdc14affa-Paper.pdf) to find the predicted class of V points.
        - S: symmetric normalized matrix of A, Y: initial label, Z: predicted matrix of V points.
        ![](images/FS3D_labelprop.png?raw=true)

### Detail Implementation:


### Results


### Notes
- Efficient: 0.28s compared with 0.39s for PointGroup.