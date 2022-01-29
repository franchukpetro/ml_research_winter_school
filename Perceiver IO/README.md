# Perceiver IO

[Arxiv](https://arxiv.org/pdf/2107.14795v2.pdf)

[Code](https://github.com/deepmind/deepmind-research/tree/master/perceiver)


The Perceiver IO model builds on the Perceiver architecture, which achieved its cross-domain generality by assuming that its input is a simple 2D byte array: a set of elements (which might be pixels or patches in vision, characters or words in language, or some form of embedding, learned or otherwise), each described by a feature vector. The model then encodes information about the input array using a smaller number of latent feature vectors, using Transformer-style attention, followed by iterative processing and a final aggregation down to a category label. Rather than output a single category, Perceiver IO aims to have the same level of generality with respect to its outputs as the Perceiver has with respect to its inputs: that is, it should produce arbitrary output arrays. The key insight is that we can predict each element of the output array using another attention module, by simply querying the latent array using a query feature vector unique to the desired output element. In other words, we define a query array with the same number of elements as the desired output.

The encode and processing stages re-use the basic structure of the original Perceiver.2 The encoder consists of a single attention module, where the queries are learned and have shapes independent of the input data. Because the queries do not depend on the input, this module has a complexity linear in the input size. The processor is composed of a stack of several attention modules: it is essentially a latent-space Transformer. The decoder works similarly to the encoder, but instead of mapping inputs to latents, it maps latents to outputs. It uses latents as inputs to its keys and value networks and passes an output query array to its query network. The resulting output has the same number of elements as the decoder query array.



![alt text](https://github.com/franchukpetro/ml_research_winter_school/blob/main/images/Perceiver_model.png)

Following the design of the Perceiver, authors implement each of the architecture’s components using Transformer-style attention modules. Each of these modules applies a global query-key-value (QKV) attention operation followed by a multi-layer perceptron (MLP). 


Also, Perceiver IO, in contrast to usual attention-based networks, uses attention non-homogeneously, first using it to map inputs to a latent space, then using it to process in that latent space, and finally using it to map to an output space. The resulting architecture has no quadratic dependence on the input or output size: encoder and decoder attention modules depend linearly on the input and output size (respectively), while latent attention is independent of both input and output sizes. Because of this structure, and the corresponding reduction in compute and memory requirements, Perceivers scale to much larger inputs and outputs.

Here you can see the results of the evaluation of Perceiver IO on the Optical Flow task:

![alt text](https://github.com/franchukpetro/ml_research_winter_school/blob/main/images/Perceiver_results.png)

As you can see, there is a slight boost in performance on the Sintel dataset compared to RAFT and PWCNet methods. However, Perceiver IO shows worse performance on the KITTI dataset compared to the RAFT architecture. I assume this could be because Perceiver IO architecture is not very task-specific and can probably fail on some complex cases of the Optical Flow task.


## Robustness to the Adversarial Attacks

| Attack                      | MSE           |
| ----------------------------|:-------------:| 
| Noise patch                 | 46.65         | 
| Overall Gaussian noise      | 6086.99       |

