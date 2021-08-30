## Few-shot 3D Point Cloud Semantic Segmentation

_Aug 2021_

- Link: https://openaccess.thecvf.com/content/CVPR2021/papers/Zhao_Few-Shot_3D_Point_Cloud_Semantic_Segmentation_CVPR_2021_paper.pdf

### Overall

#### Problem statement
Few-shot 3D point cloud semantic segmentation task: training on a base classes, then perform per-point semantic classes prediction on novel classes with the support of few or one examples.
#### Application
To estimate the category of each point in the 3D point cloud 
=> real-world applications: autonomous driving, robotics, and augmented/virtual reality.
#### Challenge
- how to extract discriminative knowledge from scarce support that can represent a novel class (which never seen during training).
- how to use these knowledge to perform segmentation.


#### Typical approaches + limitation
#### General idea: 
- Use DGCNN with self-attention to extract embedding features.
- Propose multi prototypes to represent each classes.
- Use transductive inference to assign semantic classes.

### Base
- Transductive learning:
[**Learning with Local and Global Consistency**](https://papers.nips.cc/paper/2003/file/87682805257e619d49b8e0dfdc14affa-Paper.pdf)
- Metric learner: 
[**Prototype Network**]


### Key ideas
![](images/FS3D_arch.png?raw=true)
- Baseline: query and support set:
    ![](images/FS3D_baseline.png?raw=true)
- Embedding Network:
    - Use DGCNN with EdgeConv to extract per-point feature.
    - Propose self-attention network (SAN) to aggregate the global contextual information of the corresponding point cloud.
    ![](images/FS3D_SAN.png?raw=true)
    - Add metric learner (MLP) with bigger LR than the feature extractor for faster adapt.
    - Concatenate the three levels of learned features.
- Multi-prototype Generation: for each of N+1 class (+1 background), generate n prototypes by clustering:
    * Sample n seed points by farthest point sampling.
    * Compute point-to-seed distance and assign points to seeds.
    * For each prototype, calculate the feature vector by average pooling over features of point (hard assigning point to prototype by Euclide distance).
    ![](images/FS3D_multiprototype.png?raw=true)
- Transductive Inference: exploit relationships between the unlabeled query points and the multi-prototypes, among the unlabeled query points.
    * k-NN graph:
        - Vertices: V = n×(N + 1) multiprototypes and T×M query points.
        - construct a sparse affinity matrix A by computing the Gaussian similarity between each node and its k nearest neighbors.
    * Label propagation:
        - Follow [Learning with Local and Global Consistency](https://papers.nips.cc/paper/2003/file/87682805257e619d49b8e0dfdc14affa-Paper.pdf) to find the predicted class of V points.
        - S: symmetric normalized matrix of A, Y: initial label, Z: predicted matrix of V points.
        ![](images/FS3D_labelprop.png?raw=true)

### Detail Implementation:

#### Dataset:
- Use S3DIS (12+1 classes) and ScanNetv2 (20+1 classes).
- Split classes into 2 folds (50-50) as train-val set and use cross validation.
- Divide each scan into blocks of 1x1m (xy-plane) like PointNet
- Random sample 2048 points per block.

#### Episodic task setup:
- for each class in train set, construct a set of episode by finding all blocks which contain at least 100 points of this class. (as a block may contain points from multi classes => the same block can appear in train task and test task but with different class label).
- Training: N-way K-shot
    * Random sample N classes from train set.
    * Random sample support set S and query set Q.
    * Support set: pointcloud + mask (only 0/1 binary mask for indicate single class).
    * Query set: pointcloud + label (multi-class label (same classes with support set)).
    * Modify the label of query set corresponding to the support set classes.
- Testing:
    * Iterate all combinations of N classes of the test set (sampling 100 episode for each iter).

#### Training phase:

- Pretrain: to train the feature extractor (DGCNN) by setup normal segmentation task with all classes in the train set.
    * Add 3-layer MLP to the feature extractor to predict semantic classes of each point.
    * Lr = 0.001 for all params.

- Few-shot train:
    * Load pretrain weight for the feature extractor.
    * set lr of feature extractor = 1/10 lr of metric learner and self-attention module.

### Results
4 baselines:
- Fine-tuning: use the pretrain model, fine-tuning the 3-layer MLP semantic head on support set.
- Prototypical Learning: follow Prototypical Network
    * replace SAN with linear mapper.
    * represent each class by one prototype given by the mean feature of points.
    * assign label of query points by squared Euclidean distance to the prototypes.
- Attention-aware Prototypical Learning: add SAN.
- Multi-prototype Transductive Inference: replace SAN in the proposed arch by linear mapper.
![](images/FS3D_results.png?raw=true)

