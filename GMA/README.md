# GMA

[Arxiv](https://arxiv.org/pdf/2104.02409v3.pdf)

[Code](https://github.com/zacjiang/GMA)


In this paper, the authors argue that the occlusion problem can be better solved in the two-frame case by modelling image self-similarities. They introduce a global motion aggregation module, a transformer-based approach to find long-range dependencies between pixels in the first image, and perform global aggregation on the corresponding motion features.


Network design is based on the successful RAFT architecture. From this architecture were used all-pairs correlation volumes and GRU decoder. Here is the overall architecture of the proposed method: 

![alt text](https://github.com/franchukpetro/ml_research_winter_school/blob/main/images/GMA.png)


Authors hypothesize that the network will be able to find points with similar motions by looking for points with similar appearance in the reference frame. This is motivated by the observation that the motions of points on a single object are often homogeneous.  This statistical bias can be used to propagate motion information from non-occluded pixels, with high (implicit) confidence, to occluded pixels, with low confidence. With these ideas, authors take inspiration from transformer networks, which are known for their ability to model long-range dependencies. 

Unlike the self-attention mechanism in transformers, where query, key, and value come from the same feature vectors, authors use a generalized attention variant. Query and key features are projections of the context feature map, which are used to model the appearance self-similarities in frame 1. The value features are projections of the motion features, which themselves are an encoding of the 4D correlation volume. The attention matrix computed from the query and key features is used to aggregate the value features which are hidden representations of motions.


Authors name this a Global Motion Aggregation (GMA) module. The aggregated motion features are concatenated with the local motion features and the context features, which are to be decoded by the GRU.

![alt text](https://github.com/franchukpetro/ml_research_winter_school/blob/main/images/GMA_module.png)


The proposed method showed SOTA performance compared to previous top-performance methods, such as RAFT, VCN, MaskFlowNet and FlowNet2 on both Sintel and KITTI datasets. Also, the authors found that the relative improvement of their method compared to RAFT is predominantly attributable to better predictions of the flow for occluded points.

## Robustness to the Adversarial Attacks

| Attack                      | MSE           |
| ----------------------------|:-------------:| 
| Noise patch                 | 3.14          | 
| Overall Gaussian noise      | 612.88        |
