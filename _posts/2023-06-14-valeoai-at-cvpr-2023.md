---
toc: false
layout: post
description: "Alexandre Boulch, Oriane Siméoni, Gilles Puy, Éloi Zablocki, Spyros Gidaris, Andrei Bursuc"
categories: [3d perception, multi-sensor, limited supervision, reliability]
title: "valeo.ai at CVPR 2023"
hide: false
image: images/posts/2023_cvpr/cvpr_banner.svg
---


The [IEEE / CVF Computer Vision and Pattern Recognition Conference (CVPR)](https://cvpr2023.thecvf.com/) is a key event for researchers and engineers working on computer vision and machine learning. At the 2023 edition the [valeo.ai](https://ptrckprz.github.io/valeoai/) team will present six [papers](https://ptrckprz.github.io/vaipub/) in the main conference, one workshop [keynote](https://vision4allseason.net/) and organize a [tutorial](https://osimeoni.github.io/object-localization-for-free/). The team will be at CVPR to present these works and will be happy to discuss more about these projects and ideas, and share our exciting ongoing research.
We outline four of our team papers below. 



## OCTET: Object-aware Counterfactual Explanations
#### Authors: Mehdi Zemni, <a href="https://scholar.google.com/citations?user=QnRpMJAAAAAJ&hl=fr&oi=sra">Mickaël Chen</a>, <a href="https://scholar.google.com/citations?user=dOkbUmEAAAAJ&hl=fr">Éloi Zablocki</a>, <a href="https://scholar.google.com/citations?hl=fr&user=IFLcfvUAAAAJ">Hédi Ben-Younes</a>, <a href="https://ptrckprz.github.io/">Patrick Pérez</a>, <a href="https://cord.isir.upmc.fr/">Matthieu Cord</a>




<h4 align="center"> [<a href="https://arxiv.org/abs/2211.12380 ">Paper</a>] &nbsp;&nbsp; [<a href="https://github.com/valeoai/octet">Code</a>] &nbsp;&nbsp; [<a href="https://www.youtube.com/watch?v=Xfq0uRcw9jQ">Video</a>]  &nbsp;&nbsp; [<a href="https://valeoai.github.io/blog/publications/octet/">Project page</a>]</h4>



Nowadays, deep vision models are being widely deployed in safety-critical applications, e.g., autonomous driving, and explainability of such models is becoming a pressing concern. Among explanation methods, counterfactual explanations aim to find minimal and interpretable changes to the input image that would also change the output of the model to be explained. Such explanations point end-users at the main factors that impact the decision of the model. However, previous methods struggle to explain decision models trained on images with many objects, e.g., urban scenes, which are more difficult to work with but also arguably more critical to explain. In this work, we propose to tackle this issue with an object-centric framework for counterfactual explanation generation. Our method, inspired by recent generative modeling works, encodes the query image into a latent space that is structured in a way to ease object-level manipulations. Doing so, it provides the end-user with control over which search directions (e.g., spatial displacement of objects, style modification, etc.) are to be explored during the counterfactual generation. We conduct a set of experiments on counterfactual explanation benchmarks for driving scenes, and we show that our method can be adapted beyond classification, e.g., to explain semantic segmentation models. To complete our analysis, we design and run a user study that measures the usefulness of counterfactual explanations in understanding a decision model.

![octet_overview]({{ site.baseurl }}/images/posts/2023_cvpr/octet.png){:height="80%" width="80%"}
<div class="caption"><b>Counterfactual explanations generated by OCTET.</b>  Given a classifier that predicts whether or not it is possible to go left, and a query image (top left), OCTET produces a counterfactual explanation where the most influential features that led to the decision are changed (top right). On the bottom row, we show that OCTET can also operate under different settings that result in different focused explanations. We report the prediction made by the decision model at the top left of each image. 
</div>

<hr>



## ALSO: Automotive Lidar Self-supervision by Occupancy estimation 
#### Authors: <a href="https://www.boulch.eu/">Alexandre Boulch</a>, <a href="https://scholar.google.com/citations?user=xYDkHEsAAAAJ">Corentin Sautier</a>, <a href="https://scholar.google.com/citations?user=xQcKnXkAAAAJ&hl=en">Björn Michele</a>, <a href="https://sites.google.com/site/puygilles/home">Gilles Puy</a>, <a href="http://imagine.enpc.fr/~marletr/">Renaud Marlet</a>


<h4 align="center"> [<a href="https://arxiv.org/abs/2212.05867">Paper</a>] &nbsp;&nbsp; [<a href="https://github.com/valeoai/ALSO">Code</a>] &nbsp;&nbsp; [<a href="https://www.youtube.com/watch?v=GGIBKlMvphw">Video</a>]  &nbsp;&nbsp; [<a href="https://valeoai.github.io/blog/publications/also/">Project page</a>]</h4>



We propose a new self-supervised method for pre-training the backbone of deep perception models operating on point clouds. The core idea is to train the model on a pretext task which is the reconstruction of the surface on which the 3D points are sampled, and to use the underlying latent vectors as input to the perception head. The intuition is that if the network is able to reconstruct the scene surface, given only sparse input points, then it probably also captures some fragments of semantic information that can be used to boost an actual perception task. This principle has a very simple formulation, which makes it both easy to implement and widely applicable to a large range of 3D sensors and deep networks performing semantic segmentation or object detection. In fact, it supports a single-stream pipeline, as opposed to most contrastive learning approaches, allowing training on limited resources. We conducted extensive experiments on various autonomous driving datasets, involving very different kinds of lidars, for both semantic segmentation and object detection. The results show the effectiveness of our method to learn useful representations without any annotation, compared to existing approaches.

![also_overview]({{ site.baseurl }}/images/posts/2023_cvpr/also.png){:height="100%" width="100%"}
<div class="caption"><b>ALSO overview.</b> The backbone to pre-train produces latent vectors for each input point. At pre-training time, the latent vector are fed into an volumetric occupancy head that classifies query points as full or empty. At semantic training or test time, the same latent vectors are fed into a semantic head, e.g., for semantic segmentation or object detection. 
</div>

<hr>

## Unsupervised Object Localization: Observing the Background to Discover Objects
#### Authors: <a href="https://osimeoni.github.io/">Oriane Siméoni</a>, <a href="https://github.com/chloeskt">Chloé Sekkat</a>, <a href="https://sites.google.com/site/puygilles/home">Gilles Puy</a>, <a href="https://vobecant.github.io/">Antonin Vobecky</a>, <a href="https://scholar.google.com/citations?user=dOkbUmEAAAAJ&hl=fr">Éloi Zablocki</a>, <a href="https://ptrckprz.github.io/">Patrick Pérez</a>

<h4 align="center"> [<a href="https://arxiv.org/abs/2212.07834">Paper</a>] &nbsp;&nbsp; [<a href="https://github.com/valeoai/FOUND">Code</a>] &nbsp;&nbsp; [<a href="https://youtu.be/jfYQfFcrJBE">Video</a>]  &nbsp;&nbsp; [<a href="https://valeoai.github.io/blog/publications/found">Project page</a>]</h4>


Recent advances in self-supervised visual representation learning have paved the way for unsupervised methods tackling tasks such as object discovery and instance segmentation. However, discovering objects in an image with no supervision is a very hard task; what are the desired objects, when to separate them into parts, how many are there, and of what classes? The answers to these questions depend on the tasks and datasets of evaluation. In this work, we take a different approach and propose to look for the background instead. This way, the salient objects emerge as a by-product without any strong assumption on what an object should be. We propose FOUND, a simple model made of a single conv1 × 1 initialized with coarse background masks extracted from self-supervised patch-based representations. After fast training and refining these seed masks, the model reaches state-of-the-art results on unsupervised saliency detection and object discovery benchmarks. Moreover, we show that our approach yields good results in the unsupervised semantic segmentation retrieval task. 

![found_overview]({{ site.baseurl }}/images/posts/2023_cvpr/found.png){:height="65%" width="65%"}
<div class="caption"><b>Overview of FOUND. </b>In the first stage (green upperpart), a background mask is discovered by mining a seed patch through a reweighting of the self-attention maps of a frozen DINO self-supervised features. This seed is then used to find similar patches likely belonging to the background. In the second stage (blue lower part), we train a lightweight 1 × 1 convolutional layer that produces refined masks from the self-supervised features. It is trained in a self-supervised fashion to predict both smoothed inverse coarse masks of the first step, and smoothed binarized version of its own output. Blue arrows denote where the gradients flow (in the reverse direction).</div>



<hr>


## RangeViT: Towards Vision Transformers for 3D Semantic Segmentation in Autonomous Driving 
#### Authors: Angelika Ando, <a href="https://scholar.google.fr/citations?user=7atfg7EAAAAJ&hl=en">Spyros Gidaris</a>, <a href="https://abursuc.github.io/">Andrei Bursuc</a>, <a href="https://sites.google.com/site/puygilles/home">Gilles Puy</a>, <a href="https://www.boulch.eu/">Alexandre Boulch</a>, <a href="http://imagine.enpc.fr/~marletr/">Renaud Marlet</a>


<h4 align="center"> [<a href="https://arxiv.org/abs/2301.10222">Paper</a>] &nbsp;&nbsp; [<a href="https://github.com/valeoai/rangevit ">Code</a>] &nbsp;&nbsp; [<a href="https://www.youtube.com/watch?v=urd2ZIJ70WY">Video</a>]  &nbsp;&nbsp; [<a href="https://valeoai.github.io/blog/publications/rangevit/">Project page</a>]</h4>

Semantic segmentation of LiDAR point clouds permits vehicles to perceive their surrounding 3D environment independently of the lighting condition, providing useful information to build safe and reliable vehicles. A common approach to segment large scale LiDAR point clouds is to project the points on a 2D surface and then to use regular CNNs, originally designed for images, to process the projected point clouds. These projection-based methods usually benefit from fast computations and, when combined with techniques which use other point cloud representations, achieve state-of-the-art results. 

Today, projection-based methods leverage 2D CNNs but recent advances in computer vision show that vision transformers (ViTs) have achieved state-of-the-art results in many image-based benchmarks. Despite the absence of almost any domain-specific inductive bias apart from the image tokenization process, ViTs have a strong representation learning capacity and achieve excellent results on various image perception tasks, such as image classification, object detection or semantic segmentation. Inspired by this success of ViTs for image understanding, in this work, we show that projection-based methods for 3D semantic segmentation can benefit from these latest improvements on ViTs when combined with three key ingredients, all described in our <a href="https://arxiv.org/abs/2301.10222">paper</a>.



![rangevit_teaser]({{ site.baseurl }}/images/posts/2023_cvpr/rangevit-teaser.png){:height="75%" width="75%"}
<div class="caption"><b>Exploiting vision transformer (ViT) architectures and weights for LiDAR point cloud semantic segmentation.</b> We leverage the flexibility of transformer-based architectures to re-purpose them with minimal changes for processing sparse point clouds in autonomous driving tasks. The common ViT backbone across modalities allows to effectively transfer weights pre-trained on large image repositories towards improving point cloud segmentation performance with fine-tuning.
</div>

We answer positively but only after combining them with three key ingredients: (a) ViTs are notoriously hard to train and require a lot of training data to learn powerful representations. By preserving the same backbone architecture as for RGB images, we can exploit the knowledge from long training on large image collections that are much cheaper to acquire and annotate than point clouds. We reach our best results with pre-trained ViTs on large image datasets. (b) We compensate for ViTs' lack of inductive bias by substituting a tailored non-linear convolutional stem for the classical linear embedding layer. (c) We refine pixel-wise predictions with a convolutional decoder and a skip connection from the convolutional stem to combine low-level but fine-grained features of the convolutional stem with the high-level but coarse predictions of the ViT encoder. With these ingredients, we show that our method, called RangeViT, outperforms prior projection-based methods on nuScenes and SemanticKITTI.

![rangevit_overview]({{ site.baseurl }}/images/posts/2023_cvpr/rangevit-overview.png){:height="100%" width="100%"}
<div class="caption"><b> Overview of RangeViT architecture.</b> First, the point cloud is projected in a 2D space with range projection. Then, the produced range image is processed by the convolutional stem, the ViT encoder and the decoder to obtain a 2D feature map. It is then processed by a 3D refiner layer for 3D point-wise predictions. Note that there is a single skip connection between the convolutional stem and the decoder.
</div>


In summary, our work offers the following contributions:
- Exploiting the powerful representation learning capacity of vision transformers for LiDAR semantic segmentation.
- Unifying the network architectures for processing LiDAR point clouds and images, enabling advancements in one domain to benefit both.
- Demonstrating the utilization of pre-trained ViTs on large-scale natural image datasets for LiDAR point cloud segmentation.


We believe that this finding is highly intriguing. The RangeViT approach can leverage off-the-shelf pre-trained ViT models, enabling direct benefits from ongoing and future advances in training ViT models with natural RGB images - a rapidly growing research field.


