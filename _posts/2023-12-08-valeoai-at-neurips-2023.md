---
toc: true
layout: post
description: "Victor Letzelter, Andrei Bursuc"
categories: [multi-sensor, limited supervision, reliability, deep-learning]
title: "valeo.ai at NeurIPS 2023"
hide: true
image: images/posts/2023_neurips/logo_neurips.svg
---


The [Neural Information Porcessing Systems Conference (NeurIPS)](https://neurips.cc/) is a major inter-disciplinary event that brings together researchers and practicioners in machine learning, computer vision, natural language processing, optimization, statistics, but also neuroscience, natural sciensie, social sciences, etc. This year, at the thirty-seventh edition of NeurIPS, the [valeo.ai](https://ptrckprz.github.io/valeoai/) team will present 4 papers in the main conference. We will be happy to discuss more about these projects and ideas, and share our exciting ongoing research. Take a quick view of our papers in the conference and come meet us at the posters, at our booth or in the hallway. Take a quick view of our papers and come meet us at the posters or catch us for a coffer in the hallways.



## Resilient Multiple Choice Learning: A learned scoring scheme with application to audio scene analysis
#### Authors: Victor Letzelter, Mathieu Fontaine, Mickaël Chen, Patrick Pérez, Slim Essid, Gaël Richard


<h4 align="center"> [<a href="https://arxiv.org/abs/2311.01052">Paper</a>] &nbsp;&nbsp; [<a href="https://github.com/Victorletzelter/code-rMCL">Code</a>] &nbsp;&nbsp; [<a href="https://valeoai.github.io/blog/publications/rmcl/">Project page</a>]</h4>


In this work, we tackle ambiguous machine learning tasks, where single predictions don’t suffice due to the task's nature or inherent uncertainties.

We introduce a robust multi-hypotheses framework that is capable of deterministically offering a range of plausible predictions at inference time. 
Our experiments on both synthetic data and real-world audio data affirm the potential and versatility of our method. Check out the paper and the code for more details.



![rmcl_overview]({{ site.baseurl }}/images/posts/2023_neurips/training_dynamics.gif){:height="100%" width="100%"}


This problem involves estimating a conditional distribution that is dependent on the input. The accompanying animation illustrates the early stages in the evolution of our model's learning process, highlighting how it progressively refines its predictions (represented by shaded blue points) to the actual data distribution (indicated by green points), which varies with the input 't'.


This is a joint work with: Mathieu Fontaine, Mickaël Chen, Patrick Pérez, Slim Essid and Gaël Richard at valeo.ai and Telecom Paris.

<hr>



## POP-3D: Open-Vocabulary 3D Occupancy Prediction from Images

#### Authors: Antonin Vobecky, Oriane Siméoni, David Hurych, Spyros Gidaris, Andrei Bursuc, Patrick Pérez, Josef Sivic



<h4 align="center"> [<a href="https://openreview.net/forum?id=eBXM62SqKY ">Paper</a>] &nbsp;&nbsp; [<a href="https://github.com/vobecant/POP3D">Code</a>] &nbsp;&nbsp; [<a href="https://vobecant.github.io/POP3D">Project page</a>]</h4>



POP-3D is an approach to predict open-vocabulary 3D semantic voxel occupancy map from input 2D images to enable 3D grounding, segmentation, and retrieval of free-form language queries. 



![pop3d_overview]({{ site.baseurl }}/images/posts/2023_neurips/pop3d-overview.png){:height="100%" width="100%"}
<div class="caption">Given surround-view images on the input, our POP-3D outputs voxel occupancy with 3D-language features, which one can query using text, e.g., to obtain zero-shot semantic segmentation.
</div>

We design a new model architecture for open-vocabulary 3D semantic occupancy prediction. The architecture consists of a 2D-3D encoder together with occupancy prediction and 3D-language heads. The output is a dense voxel map of 3D grounded language embeddings enabling a range of open-vocabulary tasks. Next, we develop a tri-modal self-supervised learning algorithm that leverages three modalities: (i) images, (ii) language, and (iii) LiDAR point clouds and enables training the proposed architecture using a strong pre-trained vision-language model without the need for any 3D manual language annotations.

![pop3d_model]({{ site.baseurl }}/images/posts/2023_neurips/pop3d-model.png){:height="100%" width="100%"}
<div class="caption">Overview of POP-3D architecture and training approach.</div>

Finally, we demonstrate the strengths of the proposed model quantitatively on several open-vocabulary tasks: Zero-shot 3D semantic segmentation using existing datasets; 3D grounding, and retrieval of free-form language queries, using a small dataset that we propose as an extension of nuScenes.


![pop3d_example]({{ site.baseurl }}/images/posts/2023_neurips/pop3d-qualitative.png){:height="100%" width="100%"}


<hr>

## Rewarded soups: towards Pareto-optimal alignment by interpolating weights fine-tuned on diverse rewards
#### Authors: Alexandre Ramé, Guillaume Couairon, Mustafa Shukor, Corentin Dancette, Jean-Baptiste Gaya, Laure Soulier, Matthieu Cord

<h4 align="center"> [<a href="https://arxiv.org/abs/2306.04488">Paper</a>] &nbsp;&nbsp; [<a href="https://github.com/alexrame/rewardedsoups">Code</a>] &nbsp;&nbsp; [<a href="https://huggingface.co/spaces/alexrame/rewardedsoups">Project page</a>]</h4>



Foundation models are first pre-trained on vast unsupervised datasets and then fine-tuned on labeled data. Reinforcement learning, notably from human feedback (RLHF), can further align the network with the intended usage. Yet the imperfections in the proxy reward may hinder the training and lead to suboptimal results; the diversity of objectives in real-world tasks and human opinions exacerbate the issue. This paper proposes embracing the heterogeneity of diverse rewards by following a multi-policy strategy. Rather than focusing on a single a priori reward, we aim for Pareto-optimal generalization across the entire space of preferences. To this end, we propose rewarded soup, first specializing multiple networks independently (one for each proxy reward) and then interpolating their weights linearly. This succeeds empirically because we show that the weights remain linearly connected when fine-tuned on diverse rewards from a shared pre-trained initialization. We demonstrate the effectiveness of our approach for text-to-text (summarization, Q&A, helpful assistant, review), text-image (image captioning, text-to-image generation, visual grounding, VQA), and control (locomotion) tasks. We hope to enhance the alignment of deep models, and how they interact with the world in all its diversity.


![rs_overview]({{ site.baseurl }}/images/posts/2023_neurips/rewarded-soups.png){:height="100%" width="100%"}
<div class="caption"><b>Illustration of the different steps of our proposed rewarded soup (RS).</b>  After unsupervised pre-training and supervised fine-tuning, we launch $N$ independent RL fine-tunings on the proxy rewards $\{R_i\}^{N}_{i=1}$. Then we combine the trained networks by interpolation in the weight space. The final weights are adapted at test time by selecting the coefficient $\lambda$.</div>



<hr>


## Unifying GANs and Score-Based Diffusion as Generative Particle Models 
#### Authors: Jean-Yves Franceschi, Mike Gartrell, Ludovic Dos Santos, Thibaut Issenhuth, Emmanuel de Bézenac, Mickaël Chen, Alain Rakotomamonjy


<h4 align="center"> [<a href="https://arxiv.org/abs/2305.16150">Paper</a>] &nbsp;&nbsp; [Code (soon)]</h4>

By describing the trajectories of GAN outputs during training with particle evolution equations, we propose an unifying framework for GAN and Diffusion Models. We provide a new insights on the role of the generator network, and as proof of concept validating our theories, we propose methods to train a generator with score-based gradient instead of a discriminator, or to use a discriminator's gradient flow to generate instead of training a generator.



![unigan_overview]({{ site.baseurl }}/images/posts/2023_neurips/unify-gan.png){:height="70%" width="70%"}



