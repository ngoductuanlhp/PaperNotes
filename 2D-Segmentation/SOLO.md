### SOLO: Segmenting Objects by Locations

_Aug 2021_

- Link: https://arxiv.org/pdf/1912.04488.pdf

### Overall

Direct instance segmentation by instance mask generation.


### Key ideas
![](images/SOLO_arch.png?raw=true)
- Divide image feature map into uniform grid SxS (interpolate).
- 2 parallel branches:
    * Semantic branch: 
        - semantic class probability of each grid.
        - Focal loss.
    * Instance mask branch: 
        - each instance mask at each grid is represented as a channel.
        - output a tensor HxWxSxS (grid (i,j) corresponds to channel k = i*S + j)
        - "CoordConv": for position sensitive => concat a tensor (channel = 2) of coordinate (normalized to [-1,1]).
        - Dice loss.
![](images/SOLO_head.png?raw=true)

### Detail Implementation:


### Results


### Notes