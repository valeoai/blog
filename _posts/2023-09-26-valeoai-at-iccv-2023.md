---
toc: false
layout: post
description: "Gilles Puy, Tuan-Hung Vu, Oriane Siméoni, Matthieu Cord, Cédric Rommel, Andrei Bursuc"
categories: [3d perception, multi-sensor, limited supervision, reliability, domain-adaptation]
title: "valeo.ai at ICCV 2023"
hide: true
image: images/posts/2023_iccv/iccv_logo.svg
---


The [IEEE / CVF International Conference on Computer Vision (ICCV)](https://iccv2023.thecvf.com/) is a landmark event for the increasingly large and diverse community of researchers in computer vision and machine learning. This year, ICCV takes place in Paris, home of the [valeo.ai](https://ptrckprz.github.io/valeoai/) team. From interns to senior researchers, the valeo.ai team will participate in mass at ICCV and will be looking forward to welcoming you and talking about the exciting progress and ideas in the field.

At ICCV 2023 we will present 5 papers in the main conference and 3 in the workshops. We are also organizing 2 tutorials with 2 challenges ([BRAVO](https://valeoai.github.io/bravo/) and [UNCV](https://uncv2023.github.io/)) and a tutorial ([Many Faces of Reliability](https://abursuc.github.io/many-faces-reliability/)).
Take a quick view of our papers in the conference and come meet us at the posters, at our booth or on the hallways.




## Using a Waffle Iron for Automotive Point Cloud Semantic Segmentation
#### Authors: Gilles Puy, Alexandre Boulch, Renaud Marlet


<h4 align="center"> [<a href="https://arxiv.org/abs/2301.10100">Paper</a>] &nbsp;&nbsp; [<a href="https://github.com/valeoai/WaffleIron">Code</a>] &nbsp;&nbsp; [<a href="https://valeoai.github.io/blog/publications/waffleiron/">Project page</a>]</h4>



Semantic segmentation of point clouds delivered by lidars permits autonomous vehicles to make sense of their 3D surrounding environment. Sparse convolutions have become a de-facto tool to process these large outdoor point clouds. The top performing methods on public benchmarks, such SemanticKITTI or nuScenes, all leverage sparse convolutions. Nevertheless, despite their undeniable success and efficiency, these convolutions remain available in a limited number of deep learning frameworks and hardware platforms. In this work, we propose an alternative backbone built with tools broadly available (such as 2D and 1D convolutions) but that still reaches the level of performance of the top methods on automotive datasets.


We propose a point-based backbone, called WaffleIron, which is essentially built using standard MLPs and dense 2D convolutions, both readily available in all deep learning frameworks thanks to their wide use in the field of computer vision. The architecture of this backbone is illustrated in the figure below. It is inspired by the recent MLP-Mixer. It takes as input a point cloud with a token associated to each point. All these point tokens are then updated by a sequence of layers, each containing a token-mixing step (made of dense 2D convolutions) and a channel-mixing step (made of a MLP shared across points).


![waffle_overview]({{ site.baseurl }}/images/posts/2023_iccv/waffleiron.png){:height="80%" width="80%"}
<div class="caption">The WaffleIron backbone takes as input point tokens, provided by an embedding layer (not represented), and updates these point representations L times via a point token-mixing layer (containing the WI block) followed by a channel-mixing layer. The WI block consists of a 2D projection along one of the main axes, a feed-forward network (FFN) with two dense channel-wise 2D convolutions with a ReLU activation in the hidden layer, and a simple copy of the 2D features to the 3D points. The channel-mixing layer contains a batch-norm, a MLP shared across each point, and a residual connection. The WaffleIron backbone is free of any point downsampling or upsampling layer, farthest point sampling, nearest neighbor search, or sparse convolution.
</div>

WaffleIron has three main hyperparameters to tune: the depth L, the width F and the resolution of the 2D grid. We show that these parameters are easy to tune: the performance increases with the network width F and depth L, until an eventual saturation; we observe stable results over a wide range of values for the resolution of the 2D grid.

In our paper, we also provide many details on how to train WaffleIron to reach the performance of top-entries on two autonomous driving benchmarks: SemanticKITTI and nuScenes.

<hr>



## PØDA: Prompt-driven Zero-shot Domain Adaptation
#### Authors: Mohammad Fahes, Tuan-Hung Vu, Andrei Bursuc, Patrick Pérez, Raoul de Charette


<h4 align="center"> [<a href=" https://arxiv.org/abs/2212.03241">Paper</a>] &nbsp;&nbsp; [<a href="https://github.com/astra-vision/PODA ">Code</a>] &nbsp;&nbsp; [<a href="https://www.youtube.com/watch?v=kataxQoPuSE">Video</a>]  &nbsp;&nbsp; [<a href="https://astra-vision.github.io/PODA/ ">Project page</a>]</h4>



Domain adaptation has been vastly investigated in computer vision but still requires access to target images at train time, which might be intractable in some uncommon conditions. In this paper, we propose the task of ‘Prompt-driven Zero-shot Domain Adaptation’, where we adapt a model trained on a source domain using only a general description in natural language of the target domain, i.e., a prompt. First, we leverage a pre-trained contrastive vision-language model (CLIP) to optimize affine transformations of source features, steering them towards the target text embedding while preserving their content and semantics. To achieve this, we propose Prompt-driven Instance Normalization (PIN). Second, we show that these prompt-driven augmentations can be used to perform zero-shot domain adaptation for semantic segmentation. Experiments demonstrate that our method significantly outperforms CLIP-based style transfer baselines on several datasets for the downstream task at hand, even surpassing one-shot unsupervised domain adaptation. A similar boost is observed on object detection and image classification 

![poda_overview]({{ site.baseurl }}/images/posts/2023_iccv/poda.png){:height="100%" width="100%"}
<div class="caption">We perform zero-shot adaptation with natural language prompts. PØDA enables the adaptation of a segmenter model (here, DeepLabv3+ trained on the source dataset Cityscapes) to unseen conditions with only a prompt. Source-only predictions are shown as smaller segmentation masks to the left or right of the test images.
</div>

<hr>

## You Never Get a Second Chance To Make a Good First Impression: Seeding Active Learning for 3D Semantic Segmentation
#### Authors: Nermin Samet, Oriane Siméoni, Gilles Puy, Georgy Ponimatkin, Renaud Marlet, Vincent Lepetit

<h4 align="center"> [<a href="https://arxiv.org/abs/2304.11762">Paper</a>] &nbsp;&nbsp; [<a href="https://github.com/nerminsamet/seedal">Code</a>]</h4>


We are interested in the efficient annotation of sparse 3D point clouds (as captured indoors by depth cameras or outdoors by automotive lidars) for semantic segmentation. Active Learning (AL) iteratively selects relevant data fractions to annotate within a given budget, but requires a first fraction of the dataset (a ’seed’) to be already annotated to estimate the benefit of annotating other data fractions. We show that the choice of the seed can significantly affect the performance of many AL methods and propose a method, named SeedAL, for automatically constructing a seed that will ensure good performance for AL. Assuming that images of the point clouds are available, which is common, our method relies on powerful unsupervised image features to measure the diversity of the point clouds. It selects the point clouds for the seed by optimizing the diversity under an annotation budget, which can be done by solving a linear optimization problem. Our experiments demonstrate the effectiveness of our approach compared to random seeding and existing methods on both the S3DIS and SemanticKitti datasets.


![seedal_overview]({{ site.baseurl }}/images/posts/2023_iccv/seedal.png){:height="65%" width="65%"}
<div class="caption"><b>Impact of active learning seed on performance. </b>We show the variability of results obtained with 20 different random seeds (blue dashed lines), within an initial annotation budget of 3% of the dataset, when using various active learning methods for 3D semantic segmentation of S3DIS. We compare it to the result obtained with our seed selection strategy (solid red line), named SeedAL, which performs better or on par with the best (lucky) random seeds among 20, and “protects” from very bad (unlucky) random seeds.</div>



<hr>


## eP-ALM: Efficient Perceptual Augmentation of Language Models 
#### Authors: Guillaume Couairon, Marlène Careil, Matthieu Cord, Stéphane Lathuilière, Jakob Verbeek


<h4 align="center"> [<a href="https://arxiv.org/abs/2306.13754">Paper</a>] &nbsp;&nbsp; [<a href="https://github.com/mshukor/eP-ALM">Code</a>]  &nbsp;&nbsp; [<a href="https://mshukor.github.io/eP-ALM.github.io/">Project page</a>]</h4>

eP-ALM aims to augment large language models (LLMs) with perception. While most existing approaches train a large number of parameters and rely on extensive multimodal pre-training, we investigate the minimal computational effort required to adapt unimodal models to multimodal tasks. We show that by freezing more than 99% of total parameters, training only one linear projection layer and prepending only one trainable token, our approach (dubbed eP-ALM) significantly outperforms other baselines on VQA and captioning for image, video and audio modalities.


![epalm_overview]({{ site.baseurl }}/images/posts/2023_iccv/ep-alm.png){:height="80%" width="80%"}
<div class="caption"><b> Illustration of the adaptation mechanism in eP-ALM.</b> he perceptual input (image/video/audio) is fed to the perceptual encoder E (e.g., ViT) and the corresponding text to the LM (e.g., OPT), which then generates a text conditioned on the perceptual input. The multimodal interaction is done via the [CLS] tokens acting as Perceptual Prompt, and are extracted from the last layers of the encoder, then injected in the last layers of LM, after passing by the Linear Connection C. The previous [CLS] token is replaced by the new one coming from a deeper layer, keeping the number of tokens fixed. The first layers (grayed) of each model are kept intact without any modality interaction. We ease the adaptation with a Soft Prompt that is prepended to the input of LM.
</div>


<hr>


## Zero-shot spatial layout conditioning for text-to-image diffusion models
#### Authors: Guillaume Couairon, Marlène Careil, Matthieu Cord, Stéphane Lathuilière, Jakob Verbeek


<h4 align="center"> [<a href="https://arxiv.org/abs/2306.13754v.org/abs/2306.13754">Paper</a>]</h4>

Large-scale text-to-image diffusion models have considerably improved the state of the art in generative image modeling, and provide an intuitive and powerful user interface to drive the image generation process. In this paper, we propose ZestGuide, a “zero-shot” segmentation guidance approach that can be integrated into pre-trained text-image diffusion models, and requires no additional training. It exploits the implicit segmentation maps that can be extracted from cross-attention layers, and uses them to align generation with input masks.



![zest_overview]({{ site.baseurl }}/images/posts/2023_iccv/zest-guide.png){:height="100%" width="100%"}
<div class="caption">ZestGuide generates images conditioned on segmentation maps with corresponding free-form textual descriptions.
</div>


<hr>


## DiffHPE: Robust, Coherent 3D Human Pose Lifting with Diffusion
<p class="page-description"><a href="https://web.northeastern.edu/smilelab/amfg2023/">ICCV Workshop on Analysis and Modeling of Faces and Gestures</a></p>

#### Authors: Cédric Rommel, Eduardo Valle, Mickaël Chen, Souhaiel Khalfaoui, Renaud Marlet, Matthieu Cord, Patrick Pérez


<h4 align="center"> [<a href="https://arxiv.org/abs/2309.01575">Paper</a>] &nbsp;&nbsp; [<a href="https://github.com/valeoai/diffhpe">Code</a>] &nbsp;&nbsp; [<a href="https://valeoai.github.io/blog/publications/diffhpe.html">Project page</a>]</h4>

With the rapid advances in generative adversarial networks (GANs), the visual quality of synthesized scenes keeps improving, including for complex urban scenes with applications to automated driving. We address in this work a continual scene generation setup in which GANs are trained on a stream of distinct domains; ideally, the learned models should eventually be able to generate new scenes in all seen domains. This setup reflects the real-life scenario where data are continuously acquired in different places at different times. In such a continual setup, we aim for learning with zero forgetting, i.e., with no degradation in synthesis quality over earlier domains due to catastrophic forgetting. To this end, we introduce a novel framework, named CSG0, that not only (i) enables seamless knowledge transfer in continual training but also (ii) guarantees zero forgetting with a small overhead cost.

![]({{ site.baseurl }}/images/posts/2023_iccv/diffhpe.gif){:height="100%" width="100%"}
<div class="caption">Poses across the learned reverse diffusion process converge to an accurate 3D reconstruction of the corresponding 2D pose in pixel space.</div>


More precisely, we propose DiffHPE, a novel strategy to use diffusion models in 3D-HPE, and show that combining diffusion with pre-trained supervised models allows to outperform both pure diffusion and pure supervised models trained separately. Our analysis demonstrates not only that the diffusion framework can be used to enhance accuracy, as previously understood, but also that it can improve robustness and coherence. Namely, our experiments showcase how poses estimated with diffusion models' display better bilateral and temporal coherence, and are more robust to occlusions, even when not perfectly trained for the latter.
