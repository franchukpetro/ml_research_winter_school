# RAFT

[Arxiv](https://arxiv.org/pdf/2003.12039v3.pdf)

[Code](https://github.com/princeton-vl/RAFT)


This paper introduces Recurrent All-Pairs Field Transforms (RAFT), a new deep network architecture for optical flow. RAFT enjoys the following strengths: SOTA accuracy on KITTI and Sintel dataset, strong generalization from synthetic to real-world data and high efficiency during training and inference.


RAFT consists of three main components: (1) a feature encoder that extracts a feature vector for each pixel; (2) a correlation layer that produces a 4D correlation volume for all pairs of pixels, with subsequent pooling to produce lower resolution volumes; (3) a recurrent GRU-based update operator that retrieves values from the correlation volumes and iteratively updates a flow field initialized at zero.

![alt text](https://github.com/franchukpetro/ml_research_winter_school/blob/main/images/RAFT.png)


RAFT maintains and updates a single fixed flow field at high resolution. This is different from the prevailing coarse-to-fine design in prior work, where flow is first estimated at low resolution and upsampled and refined at high resolution.


## Robustness to the Adversarial Attacks

| Attack                      | MSE           |
| ----------------------------|:-------------:| 
| Noise patch                 | 100           | 
| Overall Gaussian noise      | 100           |
