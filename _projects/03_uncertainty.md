---
layout: project
title: Uncertainty estimation and performance prediction
permalink: /projects/uncertainty
description: When the unexpected happens, when the weather badly degrades, when a sensor gets blocked, the embarked perception system should diagnose the situation and react accordingly, <em>e.g.,</em> by calling an alternative system or the human driver. With this in mind, we investigate automatic ways to assess the uncertainty of a system and to predict its performance.
image: "images/projects/uncertainty.jpg"
category: project
url: ""
---



<h1>{{page.title}}</h1> 
<p>{{page.description}}</p>


<h2>Publications</h2>

{% assign publications = site.publications | sort: "year" | reverse %}
{% assign publications = publications | where:"hide",false %}
{% assign publications = publications | where:"category","uncertainty" %}


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
