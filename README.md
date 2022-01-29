# Optical Flow Adversarial Attack

This project is motivated by the [Attacking Optical Flow](https://arxiv.org/pdf/1910.10053.pdf) paper.

This paper extends adversarial patch attacks to optical flow networks and shows that such attacks can compromise their performance. The authors show that corrupting a small patch of less than 1% of the image size can significantly affect optical flow estimates.


## Main goal

The goal of this project is to create such adversarial attack that Optical Flow was affected a lot.

## Benchmark setup

### Models
During this project, RAFT, GMA and Perceiver IO models were tested with some noise. You can find short summaries of these papers in the corresponding folders. For the testing, original implementation of the methods and checkpoints were used.


### Dataset
Models were tested on the KITTI dataset.


### Noise creation
Models were tested with two types of noise: noise patch (100x100 pixels) and overall Gaussian noise. Each type of the noise was generated only once, and added to all images of the KITTI dataset. In such way, models were benchmarked on the same corrupted images to provide fair comparison.


### Metric
KITTI dataset has no ground thruth data for the test subset. Because of the, it was decided to run the models on the original test set, and assume predicted optical flow as kind of soft ground thruth. Then this optical flow was compared to the optical flow predicted on the test set corrupted with the noise using Mean Squared Error (MSE).

## Results

| Method        | Patch Noise   | Overall Gaussian noise  |
| ------------- |:-------------:| -----------------------:|
| RAFT          | 5.88          | 486.60                  |
| GMA           | 3.14          | 612.88                  |
| Perceiver IO  | 46.65         | 6086.99                 |


