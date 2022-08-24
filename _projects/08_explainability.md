---
layout: project
title: Interpretability and Explainability of Deep Models
permalink: /projects/explainability
description: The concept of explainability has several facets and the need for explainability is strong in safety-critical applications such as autonomous driving where deep learning models are now widely used. As the underlying mechanisms of these models remain opaque, explainability and trustworthiness have become major concerns. Among other things, we investigate methods providing explanations to a black-box visual-based systems in a post-hoc fashion, as well as approaches that aim at building more interpretable self-driving systems by design.
image: "images/projects/logo_explainable.png"
category: project
url: ""
---



<h1>{{page.title}}</h1>
<p>{{page.description}}</p>


<h2>Publications</h2>

{% assign publications = site.publications | where: 'hide', false %}
{% assign publications = publications | where:"category", "explainability" %}

<!-- {% assign publications_by_year = publications | group_by: 'year' | sort: 'year' |  reverse %} -->
{% assign publications_by_year = publications |  sort: 'year' |  reverse %}
{% assign publications_by_year = publications_by_year | group_by: 'year'%}

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
