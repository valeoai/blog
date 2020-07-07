---
toc: true
layout: post
description: "A minimal example of using markdown with fastpages."
categories: [domain adaptation, semantic segmentation, object detection ]
title: "ADVENT - Adversarial Entropy Minimization for Domain Adaptation in Semantic Segmentation"
hide: false
image: images/advent/qualitative_results.png
---


Visual perception is a remarkable ability that human drivers leverage for understanding their surroundings and for supporting the multiple micro-decisions needed in traffic. Since many years, researchers have been working on mimicking this human capability by means of computer algorithms. This research field is known as computer vision and it has seen impressive progress and wide adoption. Most of the modern *computer vision* systems rely on Deep Neural Networks (DNNs) which are powerful and widely employed tools able to learn from large amounts of data and make accurate predictions. In autonomous driving, DNN-based visual perception is also at the heart of the complex architectures under intelligent cars, and supports downstream decisions of the vehicle, *e.g.,* steering, braking, signaling, etc.

The diversity and complexity of the situations encountered in real-world driving is tremendous. Unlike humans who can extrapolate effortlessly from previous experience in order to adapt to new environments and conditions, the scope of DNNs beyond the types of conditions and scenes seen during training is limited. For instance a model trained on data from a sunny country, would have a hard time delivering the same performance on streets with mixed weather conditions in a different country (with different urban architecture, furniture, vegetation, types of cars and pedestrian appearance and clothing). Similarly a model trained on a particular type of camera, is expected to see a drop in performance with images coming from a camera with different specifications. This difference between environments that leads to performance drops is referred to as *domain gap*.

## Bridging domains

We can resort to two options for narrowing the domain gap: (i) annotate more data; (ii) leverage the experience acquired on an initial environment and transfer it to the new environment. More annotated data has been shown to always improve performance of DNNs (Sun et al.). However the labeling process brings a significant financial and temporal burden. The time required for a high-quality annotation, such as the ones from the popular Cityscapes dataset is ∼90 minutes per image (Cordts et al.). The amount of images required to train high performance DNNs typically counts in hundreds of thousands. The acquisition of diverse data across seasons and weather conditions adds up even more time. It makes then sense to look for a solution elsewhere and the second option seems now more appealing, though achieving it remains technically challenging. This is actually the area of research of domain adaptation (DA) which addresses the domain-gap problem by transferring knowledge from a source domain (with full annotations) to a target domain (with fewer annotations if any), aiming to reach good performances on target samples. DA has consistently attracted interest from different communities across years (Csurka et al.)

## Basic setup

Jekyll requires blog post files to be named according to the following format:

`YEAR-MONTH-DAY-filename.md`

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `filename` is whatever file name you choose, to remind yourself what this post is about. `.md` is the file extension for markdown files.

The first line of the file should start with a single hash character, then a space, then your title. This is how you create a "*level 1 heading*" in markdown. Then you can create level 2, 3, etc headings as you wish but repeating the hash character, such as you see in the line `## File names` above.

## Basic formatting

You can use *italics*, **bold**, `code font text`, and create [links](https://www.markdownguide.org/cheat-sheet/). Here's a footnote [^1]. Here's a horizontal rule:

---

## Lists

Here's a list:

- item 1
- item 2

And a numbered list:

1. item 1
1. item 2

## Boxes and stuff

> This is a quotation

{% include alert.html text="You can include alert boxes" %}

...and...

{% include info.html text="You can include info boxes" %}

## Images

![]({{ site.baseurl }}/images/logo.png "fast.ai's logo")

## Code

You can format text and code per usual 

General preformatted text:

    # Do a thing
    do_thing()

Python code and output:

```python
# Prints '2'
print(1+1)
```

    2

Formatting text as shell commands:

```shell
echo "hello world"
./some_script.sh --option "value"
wget https://example.com/cat_photo1.png
```

Formatting text as YAML:

```yaml
key: value
- another_key: "another value"
```


## Tables

| Column 1 | Column 2 |
|-|-|
| A thing | Another thing |


## Tweetcards

{% twitter https://twitter.com/jakevdp/status/1204765621767901185?s=20 %}


## Footnotes



[^1]: This is the footnote.

