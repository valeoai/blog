---
toc: false
layout: post
description: "Corentin Sautier, Alexandre Boulch, Patrick Pérez, Tuan-Hung Vu, Matthieu Cord, Andrei Bursuc"
categories: [domain adaptation, 3d perception, reliability, multi-sensor, limited supervision]
title: "valeo.ai at CVPR 2022"
hide: true
image: images/posts/2022_cvpr/cvpr_logo.png
---


The [IEEE / CVF Computer Vision and Pattern Recognition Conference (CVPR)](https://cvpr2022.thecvf.com/) is a major event for researchers and engineers working on computer vision and machine learning. At the 2022 edition the [valeo.ai](https://ptrckprz.github.io/valeoai/) team will present four [papers](https://ptrckprz.github.io/vaipub/) in the main conference and three [papers](https://ptrckprz.github.io/vaipub/) in workshops. The team will be in CVPR to present these works and will be happy to discuss more about these projects and ideas and share our exciting ongoing research. 


## Image-to-Lidar Self-Supervised Distillation for Autonomous Driving Data 
#### Authors: Corentin Sautier, <a href="https://sites.google.com/site/puygilles/home">Gilles Puy</a>,  <a href="https://scholar.google.fr/citations?user=7atfg7EAAAAJ&hl=en">Spyros Gidaris</a>,  <a href="https://www.boulch.eu/">Alexandre Boulch</a>, <a href="https://abursuc.github.io/">Andrei Bursuc</a>, <a href="http://imagine.enpc.fr/~marletr/">Renaud Marlet</a>


<h4 align="center"> [<a href="https://arxiv.org/abs/2203.16258">Paper</a>] &nbsp;&nbsp; [<a href="https://github.com/valeoai/SLidR">Code</a>] &nbsp;&nbsp; [<a href="https://valeoai.github.io/blog/publications/slidr/">Project page</a>]</h4>

Self-driving vehicles require object detection or segmentation to safely maneuver in their environment. Yet such safety-critical tasks are usually performed by neural networks demanding huge Lidar datasets with high quality annotations, and no domain shift between training and testing conditions. Yet annotating 3D Lidar data for these tasks is tedious and costly. In [Image-to-Lidar Self-Supervised Distillation for Autonomous Driving Data]( https://arxiv.org/abs/2203.16258), we propose a self-supervised pre-training method for 3D perception models that is tailored to autonomous driving data. Specifically, we leverage the availability of synchronized and calibrated image and Lidar sensors in autonomous driving setups for distilling self-supervised pre-trained image representations into 3D models, using neither point cloud nor image annotations.


![slidr_overview]({{ site.baseurl }}/images/posts/2022_cvpr/SLidR_overview_2.png){:height="100%" width="100%"}
<div class="caption">Synchronized Lidar and Camera frames are encoded through two modality-specific features extractors. The camera backbone has pre-trained weights obtained with no annotations (e.g. with MoCo v2 {% cite chen2020improved %}). Features are pooled at a pseudo-object level using image superpixels, and contrasted between both modalities</div>


A key ingredient of our method is the use of superpixels which are used to pool 3D point features and 2D pixel features in visually similar regions. We then train a 3D network on the self-supervised task of matching these pooled point features with the corresponding pooled image pixel features. 
Extensive experiments on autonomous driving datasets demonstrate the ability of our image-to-Lidar distillation strategy to produce 3D representations that transfer well on semantic segmentation and object detection tasks.

![slidr_results]({{ site.baseurl }}/images/posts/2022_cvpr/SLidR_results.jpg){:height="100%" width="100%"}
<div class="caption">The similarity between a query point's features (in red) and all other Lidar points is shown, to assert the quality of the learned representation. Colorscale goes from purple to yellow. 
</div>

With our pre-training, a Lidar network can learn features that are mostly consistent within an object class. This first step can greatly improve data annotation efficiency, both in semantic segmentation and object detection, and is even applicable in a cross-datasets setup.

<hr>

## Raw High-Definition Radar for Multi-Task Learning
#### Authors:  <a href="https://scholar.google.com/citations?user=BJcQNcoAAAAJ">Julien Rebut</a>, <a href="https://arthurouaknine.github.io/">Arthur Ouaknine</a>, Waqas Walik, <a href="https://ptrckprz.github.io/">Patrick Pérez</a>

<h4 align="center"> [<a href="https://arxiv.org/abs/2112.10646 ">Paper</a>] &nbsp;&nbsp; [<a href="https://github.com/valeoai/RADIal">Code</a>] &nbsp;&nbsp; [<a href="https://valeoai.github.io/blog/publications/radial/">Project page</a>]</h4>

With their robustness to adverse weather conditions and ability to measure speeds, radar sensors have been part of the automotive landscape for more than two decades. Recent progress toward High Definition (HD) Imaging radar has driven the angular resolution below the degree, thus approaching laser scanning performance. However, the amount of data a HD radar delivers and the computational cost to estimate the angular positions remain a challenge. In this paper, we propose a novel HD radar sensing model, FFT-RadNet, that eliminates the overhead of computing the range-azimuth-Doppler 3D tensor, learning instead to recover angles from a range-Doppler spectrum. This architecture can be leveraged for various perception tasks with raw HD radar signals. In particular we show how to train FFT-RadNet both to detect vehicles and to segment free driving space. On both tasks, it competes with the most recent radar-based models while requiring less compute and memory. 


![]({{ site.baseurl }}/images/posts/2022_cvpr/radial_overview.png){:height="100%" width="100%"}
<div class="caption">Overview of FFT-RadNet for vehicle detection and drivable space segmentation in raw HD radar signal.</div>

Also, and importantly, we collected and annotated 2-hour worth of raw data from synchronized automotive-grade sensors (camera, laser, HD radar) in various environments (city street, highway, countryside road). This unique dataset, nick-named RADIal for "Radar, Lidar et al.", is [publicly available](https://valeoai.github.io/blog/publications/radial/).

![]({{ site.baseurl }}/images/posts/2022_cvpr/radial_teaser.jpg){:height="100%" width="100%"}
<div class="caption"><b>Scene sample form RADIal dataset</b> with (a) camera image, (b) radar power spectrum, (c) free-space in bird-eye view, (d) Range-azimuth map in Cartesian coordinates and (e) GPS trace (red) and odometry trajectory (green); laser (resp. radar) points are in red (resp. indigo), annotated vehicle bounding boxes in orange and annotated drivable space in green.</div>


<hr>

## POCO: Point convolution for surface reconstruction
#### Authors: <a href="https://boulch.eu/">Alexandre Boulch</a>, <a href="http://imagine.enpc.fr/~marletr/">Renaud Marlet</a>

<h4 align="center"> [<a href="https://arxiv.org/abs/2201.01831">Paper</a>] &nbsp;&nbsp; [<a href="https://github.com/valeoai/POCO">Code</a>] &nbsp;&nbsp; [<a href="https://valeoai.github.io/blog/publications/poco/">Project page</a>]</h4>

Implicit neural networks have been successfully used for surface reconstruction from point clouds. However, many of them face scalability issues as they encode the isosurface function of a whole object or scene into a single latent vector. To overcome this limitation, a few approaches infer latent vectors on a coarse regular 3D grid or on 3D patches, and interpolate them to answer occupancy queries. In doing so, they lose the direct connection with the input points sampled on the surface of objects, and they attach information uniformly in space rather than where it matters the most, i.e., near the surface. Besides, relying on fixed patch sizes may require discretization tuning.


In POCO, we propose to use point cloud convolution and compute a latent vector at each input point. We then perform a learning-based interpolation on nearest neighbors using inferred weights. On the one hand, using a convolutional backbone allows to aggregate global information about the shape needed to correctly orientate the surface (decide which side of the surface is inside or outside). On the other hand, surface location is inferred via a local attention-based approach which enables precise surface positioning.


![]({{ site.baseurl }}/images/posts/2022_cvpr/poco_teaser.png){:height="100%" width="100%"}
<div class="caption"><b>POCO overview.</b> Top row: the decoding mechanism takes as input local latent vectors and local coordinates which are lifted with a point-wise MLP. The resulting representations are weighted with an attention mechanism in order to take the occupancy decision.
Bottom row: reconstruction examples with POCO, scene reconstruction with a model trained on objects (left), object reconstruction with noisy point cloud (middle) and out of domain object reconstruction (right).
</div>

We show that our approach, while being very simple to set up, reaches the state of the art on several reconstruction-from-point-cloud benchmarks. This underlines the importance of reasoning about the surface location at a local scale, close to the input points.
POCO also shows good generalization properties including the possibility of learning on object datasets and reconstructing complete scenes.

<hr>

## DyTox: Transformers for Continual Learning with DYnamic TOken eXpansion
#### Authors: <a href="https://arthurdouillard.com/">Arthur Douillard</a>,  <a href="https://alexrame.github.io/">Alexandre Ramé</a>,  Guillaume Couairon, <a href="http://webia.lip6.fr/~cord/">Matthieu Cord</a>


<h4 align="center"> [<a href="https://arxiv.org/abs/2111.11326">Paper</a>] &nbsp;&nbsp; [<a href="https://github.com/arthurdouillard/dytox">Code</a>] </h4>

Deep network architectures struggle to continually learn new tasks without forgetting the previous tasks. In this paper, we propose a transformer architecture based on a dedicated encoder/decoder framework. Critically, the encoder and decoder are shared among all tasks. Through a dynamic expansion of special tokens, we specialize each forward of our decoder network on a task distribution. Our strategy scales to a large number of tasks while having negligible memory and time overheads due to strict control of the parameters expansion. Moreover, this efficient strategy doesn't need any hyperparameter tuning to control the network's expansion. Our model reaches excellent results on CIFAR100 and state-of-the-art performances on the large-scale ImageNet100 and ImageNet1000 while having less parameters than concurrent dynamic frameworks.


![]({{ site.baseurl }}/images/posts/2022_cvpr/dytox.png){:height="85%" width="85%"}


<hr>


## Raising context awareness in motion forecasting
<p class="page-description"><a href="https://cvpr2022.wad.vision/">CVPR 2022 Workshop on Autonomous Driving</a></p>

#### Authors: <a href="https://scholar.google.com/citations?hl=fr&user=IFLcfvUAAAAJ">Hédi Ben-Younes</a>, <a href="https://scholar.google.com/citations?user=dOkbUmEAAAAJ&hl=fr">Éloi Zablocki</a>, <a href="https://scholar.google.com/citations?user=QnRpMJAAAAAJ&hl=fr&oi=sra">Mickaël Chen</a>, <a href="https://ptrckprz.github.io/">Patrick Pérez</a>, <a href="http://webia.lip6.fr/~cord/">Matthieu Cord</a>


<h4 align="center"> [<a href="https://arxiv.org/abs/2109.08048">Paper</a>]</h4>


![cab_overview]({{ site.baseurl }}/images/posts/2022_cvpr/cab.png){:height="50%" width="50%"}
<div class="caption"><b>Overview of CAB.</b> CAB employs a CVAE backbone which produces distributions over the latent variable and the future trajectory. During training, a blind input is forwarded into the CVAE and the resulting distribution over the latent variable is used to encourage the prediction of the model to be different from the context-agnostic distribution, thanks to the CAB-KL loss.</div>

Learning-based trajectory prediction models have encountered great success, with the promise of leveraging contextual information in addition to motion history. Yet, we find that state-of-the-art forecasting methods tend to overly rely on the agent's current dynamics, failing to exploit the semantic contextual cues provided at its input. To alleviate this issue, we introduce CAB, a motion forecasting model equipped with a training procedure designed to promote the use of semantic contextual information. We also introduce two novel metrics, dispersion and convergence-to-range, to measure the temporal consistency of successive forecasts, which we found missing in standard metrics. Our method is evaluated on the widely adopted nuScenes Prediction benchmark as well as on a subset of the most difficult examples from this benchmark.


<hr>


## CSG0: Continual Urban Scene Generation with Zero Forgetting
<p class="page-description"><a href="https://sites.google.com/view/clvision2022">CVPR 2022 Workshop on Continual Learning (CLVision)</a></p>

#### Authors:  <a href="https://himalayajain.github.io/">Himalaya Jain</a>, <a href="https://tuanhungvu.github.io/">Tuan-Hung Vu</a>, <a href="https://ptrckprz.github.io/">Patrick Pérez</a>, <a href="http://webia.lip6.fr/~cord/">Matthieu Cord</a>


<h4 align="center"> [<a href="https://arxiv.org/abs/2112.03252">Paper</a>] &nbsp;&nbsp; [<a href=" https://valeoai.github.io/blog/publications/csg0/ 
">Project page</a>]</h4>

With the rapid advances in generative adversarial networks (GANs), the visual quality of synthesized scenes keeps improving, including for complex urban scenes with applications to automated driving. We address in this work a continual scene generation setup in which GANs are trained on a stream of distinct domains; ideally, the learned models should eventually be able to generate new scenes in all seen domains. This setup reflects the real-life scenario where data are continuously acquired in different places at different times. In such a continual setup, we aim for learning with zero forgetting, i.e., with no degradation in synthesis quality over earlier domains due to catastrophic forgetting. To this end, we introduce a novel framework, named CSG0, that not only (i) enables seamless knowledge transfer in continual training but also (ii) guarantees zero forgetting with a small overhead cost.

![]({{ site.baseurl }}/images/posts/2022_cvpr/csg0_teaser.png){:height="100%" width="100%"}
<div class="caption"><b>Overview of CSG0.</b> Our continual setup for urban-scene generation involves a stream of datasets, with GANs trained from one dataset to another. Our framework makes use of the knowledge learned from previous domains and adapts to new ones with a small overhead.</div>


To showcase the merit of our framework, we conduct intensive experiments on various continual urban scene setups, covering both synthetic-to-real and real-to-real scenarios. Quantitative evaluations and qualitative visualizations demonstrate the interest of our CSG0 framework, which operates with minimal overhead cost (in terms of architecture size and training). Benefiting from continual learning, CSG0 outperforms the state-of-the-art OASIS model trained on single domains. We also provide experiments with three datasets to emphasize how well our strategy generalizes despite its cost constraints. Under extreme low-data regimes, our approach outperforms the baseline by a large margin.




<hr>


## Multi-Head Distillation for Continual Unsupervised Domain Adaptation in Semantic Segmentation
<p class="page-description"><a href="https://sites.google.com/view/clvision2022">CVPR 2022 Workshop on Continual Learning (CLVision)</a></p>

#### Authors:  <a href="https://scholar.google.com/citations?user=jSwfIU4AAAAJ">Antoine Saporta</a>, <a href="https://arthurdouillard.com/">Arthur Douillard</a>, <a href="https://tuanhungvu.github.io/">Tuan-Hung Vu</a>, <a href="https://ptrckprz.github.io/">Patrick Pérez</a>&nbsp;&nbsp; <a href="http://webia.lip6.fr/~cord/">Matthieu Cord</a>


<h4 align="center"> [<a href="https://arxiv.org/abs/2204.11667">Paper</a>] &nbsp;&nbsp; [<a href="https://github.com/valeoai/MuHDi">Code</a>] &nbsp;&nbsp; [<a href="https://valeoai.github.io/blog/publications/muhdi/">Project page</a>]</h4>


This work focuses on a novel framework for learning UDA, continuous UDA, in which models operate on multiple target domains discovered sequentially, without access to previous target domains. We propose MuHDi, for Multi-Head Distillation, a method that solves the catastrophic forgetting problem, inherent in continual learning tasks. MuHDi performs distillation at multiple levels from the previous model as well as an auxiliary target-specialist segmentation head. We report both extensive ablation and experiments on challenging multi-target UDA semantic segmentation benchmarks to validate the proposed learning scheme and architecture. 

![]({{ site.baseurl }}/images/posts/2022_cvpr/muhdi_teaser.png){:height="90%" width="90%"}
<div class="caption"><b>Overview of CSG0.</b> Predictions of continual baseline and MuHDi in a Cityscapes scene.</b> The baseline model suffers from catastrophic forgetting when adapting from one domain to another. The proposed MuHDi is more resilient to continual adaptation and preserve predictive accuracy.</div>



## References

{% bibliography --cited %}


