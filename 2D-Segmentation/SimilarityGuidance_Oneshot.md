### SG-One: Similarity Guidance Network for One-Shot Semantic Segmentation

_Aug 2021_

- Link: https://arxiv.org/pdf/1810.09091.pdf

### Overall

Propose one-shot semantic segmentation by calculate feature similarity between query and support images.

### Key ideas
![](images/sg_one_arch.png?raw=true)

- Support and query images have same type of semantic mask.
- use a shared CNN (stem) to extract feature from support and query. 
- similarity branch:
    - Masked Average Pooling:
        * resize the feature map of support image to the same size as the mask Y via bilinear interpolation.
        * use average pooling to get the feature representing the semantic.
        ![](images/sg_one_avepool_supportfeature.png?raw=true)
    - Similarity Guidance:
        * use the average feature vector of support image to compare with feature map of query image.
        * consine similarity:
        * ouput similarity map.
        ![](images/sg_one_cosine_similar.png?raw=true)
- semantic branch:
    * encoder-decoder arch.
    * point-wise multiply similarity map with feature of encoder.
    * decoder: upsampling to get final mask.
- Loss: cross-entropy of query output

 
### Detail Implementation:


### Results


### Notes