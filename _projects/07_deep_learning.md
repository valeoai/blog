---
layout: project
title: Core Deep Learning
permalink: /projects/deep-learning
description: Deep learning being now a key component of AD systems, it is important to get a better understanding of its inner workings, in particular the link between the specifics of the learning optimization and the key properities (performance, regularity, robustness, generalization) of the trained models. Among other things, we investigate the impact of popular batch normalization on standard learning procedures and the ability to learn through unsupervised distillation.
image: "images/projects/deep_learning.jpg"
category: project
url: ""
---



<h1>{{page.title}}</h1> 
<p>{{page.description}}</p>


<h2>Publications</h2>

{% assign publications = site.publications | sort: "year" | reverse %}
{% assign publications = publications | where:"hide",false %}
{% assign publications = publications | where:"category","deep-learning" %}


{% for pub in publications %}


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
