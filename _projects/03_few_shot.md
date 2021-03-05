---
layout: project
title: Frugal learning
permalink: /projects/limited-supervision
description: Collecting diverse enough data, and annotating it precisely, is complex, costly and time-consuming. To reduce dramatically these needs, we explore various alternatives to fully-supervised learning, e.g, training that is unsupervised (as <a href="https://valeoai.github.io/blog/publications/rosd/">rOSD</a> at ECCCV’20), self-supervised (as <a href="https://valeoai.github.io/blog/publications/bownet/">BoWNet</a> at CVPR’20), semi-supervised, active, zero-shot (as <a href="https://valeoai.github.io/blog/publications/zs3/">ZS3</a> at NeurIPS’19) or few-shot. We also investigate training with fully-synthetic data (in combination with unsupervised domain adaptation) and with GAN-augmented data (as <a href="https://valeoai.github.io/blog/publications/semanticpalette/">Semantic Palette</a> at CVPR’21).
image: "images/projects/limited_supervision.jpg"
category: project
url: ""
---



<h1>{{page.title}}</h1> 
<p>{{page.description}}</p>


<h2>Publications</h2>

{% assign publications = site.publications | where: 'hide', false %}
{% assign publications = publications | where:"category", "limited-supervision" %}
{% assign publications_by_year = publications | group_by: 'year' | sort: 'year' |  reverse %}

{% for year_publications in publications_by_year %}

<!-- <h2>{{year_publications.items[0].year}}</h2> -->

{% assign curr_publications = year_publications.items | sort: 'month' | reverse %}

{% for pub in curr_publications %}

<div class="row">
    <div class="col-md-4">
         <div class="pubteaserbs">
            <a href="{{site.url  | append: site.baseurl | append: pub.permalink}}">
            <img class="media-object" src="../{{ pub.image }}" alt="{{pub.image}} publication teaser"/>
             </a>
        </div>
    </div>
    <!-- <div class="col-md-1"></div> -->
    <div class="col-md-8">
        <div class="pubitembs">
  <h3><a href="{{site.url  | append: site.baseurl | append: pub.permalink}}">{{ pub.title }}</a></h3>
  <p class="b">{{ pub.authors }}
    <br>
    <em>{{ pub.venue_long }}, {{ pub.year }}</em>
   </p>
</div>
</div>
</div>

{% if forloop.last == false %}
<hr>
{% endif %}

{% endfor %} 

{% if forloop.last == false %}
<hr>

{% endif %}

{% endfor %} 
