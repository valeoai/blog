---
toc: true
layout: post
description: "Unsupervised domain adaptation for semantic segmentation."
categories: [domain adaptation, semantic segmentation, object detection ]
title: "ADVENT - Adversarial Entropy Minimization for Domain Adaptation in Semantic Segmentation"
hide: false
image: images/advent/qualitative_results.png
---

*This post describes our [recent work](https://openaccess.thecvf.com/content_CVPR_2019/html/Vu_ADVENT_Adversarial_Entropy_Minimization_for_Domain_Adaptation_in_Semantic_Segmentation_CVPR_2019_paper.html) on unsupervised domain adaptation for semantic segmentation presented at CVPR 2019. ADVENT is a flexible technique for bridging the gap between two different domains through entropy minimization. Our work builds upon a simple observation: models trained only on source domain tend to produce over-confident, i.e., low-entropy, predictions on source-like images and under-confident, i.e., high-entropy, predictions on target-like ones. Consequently by minimizing the entropy on the target domain, we make the feature distributions from the two domains more similar. We show that our approach achieves competitive performances on standard semantic segmentation benchmarks and that it can be successfully extended to other tasks such as object detection.*

Visual perception is a remarkable ability that human drivers leverage for understanding their surroundings and for supporting the multiple micro-decisions needed in traffic. Since many years, researchers have been working on mimicking this human capability by means of computer algorithms. This research field is known as computer vision and it has seen impressive progress and wide adoption. Most of the modern *computer vision* systems rely on Deep Neural Networks (DNNs) which are powerful and widely employed tools able to learn from large amounts of data and make accurate predictions. In autonomous driving, DNN-based visual perception is also at the heart of the complex architectures under intelligent cars, and supports downstream decisions of the vehicle, *e.g.,* steering, braking, signaling, etc.

The diversity and complexity of the situations encountered in real-world driving is tremendous. Unlike humans who can extrapolate effortlessly from previous experience in order to adapt to new environments and conditions, the scope of DNNs beyond the types of conditions and scenes seen during training is limited. For instance a model trained on data from a sunny country, would have a hard time delivering the same performance on streets with mixed weather conditions in a different country (with different urban architecture, furniture, vegetation, types of cars and pedestrian appearance and clothing). Similarly a model trained on a particular type of camera, is expected to see a drop in performance with images coming from a camera with different specifications. This difference between environments that leads to performance drops is referred to as *domain gap*.

## Bridging domains

We can resort to two options for narrowing the domain gap: (i) annotate more data; (ii) leverage the experience acquired on an initial environment and transfer it to the new environment. More annotated data has been shown to always improve performance of DNNs (Sun et al.). However the labeling process brings a significant financial and temporal burden. The time required for a high-quality annotation, such as the ones from the popular Cityscapes dataset is ∼90 minutes per image (Cordts et al. \cite{cordts2016cityscapes} {% cite cordts2016cityscapes %} ). The amount of images required to train high performance DNNs typically counts in hundreds of thousands. The acquisition of diverse data across seasons and weather conditions adds up even more time. It makes then sense to look for a solution elsewhere and the second option seems now more appealing, though achieving it remains technically challenging. This is actually the area of research of domain adaptation (DA) which addresses the domain-gap problem by transferring knowledge from a source domain (with full annotations) to a target domain (with fewer annotations if any), aiming to reach good performances on target samples. DA has consistently attracted interest from different communities across years (Csurka et al.)


### References

{% bibliography --cited %}


