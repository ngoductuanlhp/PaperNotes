### End-to-End Object Detection with Transformers

_Aug 2021_

- Link: https://arxiv.org/pdf/2005.12872.pdf

### Overall

Single-shot object detection with transformer network and object queries set.

### Key ideas
![](images/detr_arch.png?raw=true)

- Object detection set prediction loss: find optimal bipartite matching between predicted and ground truth objects by Hungarian algorithm.
    * ![](images/detr_hungarian_assign.png?raw=true)
    * Hungarian Loss: matching cost + box loss.
    ![](images/detr_hungarian_loss.png?raw=true)
    * Bounding box loss: IoU loss + l1 loss.

- Architecture:
    * Backbone: a typical CNN backbone to extract single scale feature F of CxHxW.
    * Transformer encoder:
        ![](images/detr_trans.png?raw=true)
        - Flatten F to CxHW.
        - Add positional encoding to every encoder layer.
    * Transformer decoder:
        - a set of N learnable object queries.
        - decode N objects in parallel: N output embedding.
        - Add positional encoding to every decoder layer.
    * Prediction feed-forward networks (FFNs):
        - shared MLP to predict class, bbox from N output embedding.
        - Auxiliary decoding losses: add FFNs and Hungarian loss after each decoder layer.

- Panoptic segmentation:
    ![](images/detr_seg.png?raw=true)
    - add a mask head on top of the decoder outputs.
    - provide a binary mask for each of the predicted boxes.
    - use FPN-like arch to increase resolution.
    - pixel-wise argmax N binary mask to produce final mask.
    


### Detail Implementation:


### Results
![](images/detr_results.png?raw=true)

### Notes