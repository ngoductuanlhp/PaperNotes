# Deep Set Prediction Networks

_Sep 2021_

- Link: https://arxiv.org/pdf/1906.06565.pdf

### Overall

Novel algorithm to predict set outputs

### Key ideas
![](images/set_pred_algo.png?raw=true)

- Predicted output as set format (ex: obj detection: list of bbox)

- 2 type of inputs:
    * set inputs (ex: auto-encoder)
    * a single feature vector (ex: extracted vector from CNN backbone)
- Intuition: to regress a good set prediction from a latent z, guess an initial value Y and use an encoder to encode its, compare loss with latent z and use gradient descent to correct the Y.

- 2 loop:
    * inner loop: regress set prediction Y based on gradient descent
    ![](images/set_pred_decode.png?raw=true)
    * outer loop: learn the encoder to encode a good latent z
    ![](images/set_pred_outer_loss.png?raw=true)

### Detail Implementation:

### Results


### Notes