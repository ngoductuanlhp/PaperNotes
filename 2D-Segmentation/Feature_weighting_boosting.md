### Feature Weighting and Boosting for Few-Shot Segmentation

_Aug 2021_

- Link: https://openaccess.thecvf.com/content_ICCV_2019/papers/Nguyen_Feature_Weighting_and_Boosting_for_Few-Shot_Segmentation_ICCV_2019_paper.pdf

### Overall

Improve k-shot semantic segmentation with feature weighting and boosting (inference).

### Base

[**SG-One: Similarity Guidance Network for One-Shot Semantic Segmentation**](https://arxiv.org/pdf/1810.09091.pdf)

### Key ideas
- Feature Weighting:
![](images/FWB_featureweighting.png?raw=true)
    * Instead of using average pooling of foreground feature (like SG-One), calculate weight vector r:
        - vector of feature differences phi: signed sum of feature across feature map. Intuition: channel of foreground: value +, channel of background: value -.
        - the weight vector r must maximize the inner product of phi and r. Intuition: r must have bigger coor for foreground channel and smaller for background ~ maximize this inner product (amplify position value (fore) with big coor and minimize negative value (back) with small coor).
        ![](images/FWB_relevance.png?raw=true)
    * Weighted cosin similarity:
        ![](images/FWB_weighted_cosin_similar.png?raw=true)
- Boosting (inference):
![](images/FWB_boosting.png?raw=true)
    * Instead of using single feature of support image, calculate N (10 in exp) features.
        - Features are sequentially calculated by gradient-descent base
        - use N features vector to predict N support masks. 
        - Calculate IoU score p between each predicted support mask with GT support mask.
    * Generate N query predictions.
    * Ensemble query predictions by weight sum with IoU score p.


### Detail Implementation:


### Results


### Notes