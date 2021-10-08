---
layout: project
title: Reliability
permalink: /projects/reliability
description: When the unexpected happens, when the weather badly degrades, when a sensor gets blocked, the embarked perception system should diagnose the situation and react accordingly, <em>e.g.,</em> by calling an alternative system or the human driver. With this in mind, we investigate ways to improve the robustness of neural nets to input variations, including to adversarial attacks, and to predict automatically the performance and the confidence of their predictions as in <a href="https://valeoai.github.io/blog/publications/confidnet">ConfidNet</a> at NeurIPS’19.
image: "images/projects/uncertainty.jpg"
category: project
url: ""
---


<h1>{{page.title}}</h1> 
<p>{{page.description}}</p>


<h2>Publications</h2>

{% assign publications = site.publications | where: 'hide', false %}
{% assign publications = publications | where:"category", "reliability" %}
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
