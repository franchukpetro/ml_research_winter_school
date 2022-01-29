# Optical Flow Adversarial Attack

This project is motivated by the [Attacking Optical Flow](https://arxiv.org/pdf/1910.10053.pdf) paper.

This paper extends adversarial patch attacks to optical flow networks and shows that such attacks can compromise their performance. The authors show that corrupting a small patch of less than 1% of the image size can significantly affect optical flow estimates.


## Main goal

This project aims to create such an adversarial attack that Optical Flow will be affected a lot.

## Benchmark setup

### Models
RAFT, GMA and Perceiver IO models were tested during this project with some noise corrupting input images. You can find short summaries of these papers in the corresponding folders. For the testing, the original implementation of the methods and checkpoints were used.


### Dataset
Models were tested on the KITTI dataset.


### Noise creation
Models were tested with two types of noise: noise patch (100x100 pixels) and overall Gaussian noise. Every kind of noise was generated only once and added to all images of the KITTI dataset. In such a way, models were benchmarked on the same corrupted images to provide a fair comparison.


### Metric
KITTI dataset has no ground truth data for the test subset. Because of this, it was decided to run the models on the original test set and assume predicted optical flow as a kind of soft ground truth. Then this optical flow was compared to the optical flow predicted on the test set corrupted with the noise using Mean Squared Error (MSE).

## Results

| Method        | Patch Noise   | Overall Gaussian noise  |
| ------------- |:-------------:| -----------------------:|
| RAFT          | 5.88          | 486.60                  |
| GMA           | 3.14          | 612.88                  |
| Perceiver IO  | 46.65         | 6086.99                 |


I assume that Perceiver IO is very sensitive to the noise since it is not task-specific architecture but rather a universal method, which can be applied to different problems. Because of that, the architecture of this network itself is pretty generic and can not fix all edge-cases of the Optical Flow problem.

In the case of the RAFT and GMA models, it is hard to find some pattern. Both are not so sensitive to the patch noise, the same as was stated in the reference paper on adversarial attacks. Actually, the authors of that paper stated that deconvolution layers lead to strong amplification of activations and checkerboard artifacts. Since both RAFT and GMA models don't have deconvolution, patch noise attack affected just small region of the flow. So, I assume that the reason for such effects of adversarial attacks on the Optical Flow models can be some particular layers, which lead to the propagation of the noise in the activation maps.

