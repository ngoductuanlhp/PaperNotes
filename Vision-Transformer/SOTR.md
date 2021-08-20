### SOTR: Segmenting Objects with Transformers

_Aug 2021_

- Link: https://arxiv.org/pdf/2108.06747.pdf

### Overall



### Key ideas
![](images/SOTR_arch.png?raw=true)
- Backbone: use FPN arch.
- Transformer
    * Twin Attention:
        - Split self-attention into vertical and horizontal scales.
        ![](images/SOTR_twin_attention.png?raw=true)
    * Twin Attention at multi-scale (FPN):
        - For feature map F<sub>i<sub> at layer i of size HxWxC, split it into P<sub>i<sub> of size NxNxC (billinear interpolate).
        - Apply twin attention to produce output of size NxNxC (apply from P2 to P6).
    * Functional Heads: each transformer output at each layer follows 2 parallel heads: 
        - Class head: output NxNxM (M: num classes)
        - Kernel head: output NxNxD (D: size of weight for dynamic conv (like SOLOv2)).

- Mask:
    - Use P2-P4 from FPN, output of transformer at layer P5.
    - bilinear upsample P3-P5 (2x,4x,8x) to reso H/4 x W/4.
    - Add P2-P5, point-wise conv, upsample to provide mask feature HxWxC
    - Final mask predict = dynamic conv of mask feature (HxWxC) and kernel (NxNxD)
    ![](images/SOTR_dynamic_conv.png?raw=true)



### Detail Implementation:


### Results


### Notes