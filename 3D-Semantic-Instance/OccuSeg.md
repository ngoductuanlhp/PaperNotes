### OccuSeg: Occupancy-aware 3D Instance Segmentation

_Aug 2021_

- Link: https://openaccess.thecvf.com/content_CVPR_2020/papers/Han_OccuSeg_Occupancy-Aware_3D_Instance_Segmentation_CVPR_2020_paper.pdf

### Overall

Propose a Occupancy-prediction to cluster instances.

### Key ideas
![](images/occuseg_arch.png?raw=true)

- Backbone: 
    * convert pointcloud into regular grid.
    * apply a 3D Unet-like with sparse convolution to extract voxel feature F<sub>voxel</sub>.
    * besides semantic feature, embedding feature (Spatial Term, Feature term, Covariance Term), the backbone also extract instace occupancy (the number of voxels
occupied by each instance)

- Embedding learning: 

    * Spacial term: regress to the object center.
    * Feature term: use discriminative loss function.
        ![](images/occuseg_discri.png?raw=true)
        * feature of voxel is similar with feature of its instance.
        * feature of different instances must be far away.
        * regularization of voxel features.
    * Covariance Term

- Instance Clustering:
    * use [**efficient graph-based segmentation**](http://cs.brown.edu/people/pfelzens/papers/seg-ijcv.pdf) scheme to group voxel to super-voxel.
    * construct a weighted undirect graph with verteces is super-voxels, weight between two vertices measures how similar these super-voxels are.
    * loop: choose the largest edge (most similar), if weight > threshold: merge vertices then recalculate new weights.
    ![](images/occuseg_weightgraph.png?raw=true)



### Detail Implementation:

- Use sparse conv in [**Realtime semantic 3d perception for immersive augmented reality**](https://conferences.computer.org/vr-tvcg/2020/content/TVCG/assets/pdfs/tvcg-fang-2973477-x.pdf) 4x faster than submanifold sparse conv.

### Results


### Notes

- The super-voxel segmentation step is most time-consuming (perform in CPU).