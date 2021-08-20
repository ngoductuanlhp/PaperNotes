### SOLQ: Segmenting Objects by Learning Queries

_Aug 2021_

- Link: https://arxiv.org/pdf/2106.02351.pdf

### Overall



### Key ideas
![](images/SOLQ_arch.png?raw=true)
- Multi-scale deformable transformer (like Deformable DETR).

- Unified Query Representation
    * Design a set of learnable queries, each query vector contains feature for: classfication, localization, instance mask.
    * Mask Compression Coding: Principal Component Analysis, Discrete Cosine Transform , or Sparse Coding
        * in training phase: GT mask is encoded then calculate loss with the predicted mask vector (l1 loss)
        * in testing phase: the predicted mask vector is decoded to get the final mask.

    ![](images/SOLQ_UQR.png?raw=true)


### Detail Implementation:


### Results


### Notes