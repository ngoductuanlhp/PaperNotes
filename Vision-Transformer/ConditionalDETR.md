### Conditional DETR for Fast Training Convergence

_Aug 2021_

- Link: https://arxiv.org/pdf/2108.06152.pdf

### Overall

Improve DETR (especially faster convergence) by proposing conditional spacial query in cross-attetion of decoder.

### Key ideas

- Cross-attention in decoder:
    ![](images/CDETR_decoder.png?raw=true)
    * Notations:
        - content key c<sub>k</sub> (content embedding output from the encoder).
        - spatial key p<sub>k</sub> (positional embedding of normalized 2D coordinate).
        - content query c<sub>q</sub> (embedding output from the decoder self-attention).
        - spatial query p<sub>q</sub> (obj query o<sub>q</sub>).
    * In DETR:
        - Add content and spatial key/query then dot product:
        ![](images/CDETR_origin_attention.png?raw=true)
    * In Conditional DETR:
        ![](images/CDETR_condition_attention.png?raw=true)
        - Separate by concatenate.
        - Propose spatial query p<sub>q</sub> by encoding reference point s by 256-dimensional sinusoidal positional embedding and learn a linear projection T.
        ![](images/CDETR_spatialquery.png?raw=true)


### Detail Implementation:
- Only 50/108 epoches training (500 for DETR)

### Results
![](images/CDETR_results.png?raw=true)
![](images/CDETR_vis.png?raw=true)

### Notes