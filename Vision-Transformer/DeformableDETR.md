### Deformable Detr: Deformable Transformers For End-to-end Object Detection

_Aug 2021_

- Link: https://arxiv.org/pdf/2010.04159.pdf

### Overall

Improve DETR with deformable multi-scale transformer layer.

### Key ideas
![](images/deformdetr_arch.png?raw=true)

- Deformable Attention Module
    ![](images/deformdetr_deform.png?raw=true)
    * Multi-head attention (original DETR): ![](images/deformdetr_multiheadatt.png?raw=true)
    * Deformable attention: ![](images/deformdetr_deformatt.png?raw=true)
        - Instead of weighting all element (HxW), get a small keys K (K << HxW) with deformable offsets.
    * Multi-scale Deformable attention: ![](images/deformdetr_multiscaledeformatt.png?raw=true)
        - sample LxK points from L multi-scale feature maps.
- Deformable Transformer Encoder:
    ![](images/deformdetr_multiscale.png?raw=true)
    * take multi-scale feature maps as input (do not need FPN).
    * add scale-level embedding (random initialized) and positional embedding (fixed encoding) to the feature representation.
- Deformable Transformer Decoder:
    * use a set of object queries (like DETR).
    * replace cross-attention by multi-scale deformable attention.
- Additional improvement:
    * Iterative Bounding box refinement.
    * Two-Stage Deformable DETR.


### Detail Implementation:


### Results
![](images/deformdetr_results.png?raw=true)

### Notes