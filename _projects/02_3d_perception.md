---
layout: project
title: 3D dynamic perception
permalink: /projects/3d-perception
description: Each sensor delivers information about the 3D world around the vehicle and its temporal evolution. Detecting, segmenting and tracking important objects (road users, obstacles, street furnitures, etc.) in 3D, as well as forecasting their possible futures, is required for the driving system to plan and act in the safest and most confortable way. This encompasses a wide range of challenging tasks that our research tackles.
image: "images/projects/3d_perception.jpg"
category: project
url: /projects/3d-perception/
---


<h1>{{page.title}}</h1> 
<p>{{page.description}}</p>


<h2>Publications</h2>

{% assign publications = site.publications | sort: "year" | reverse %}
{% assign publications = publications | where:"hide",false %}
{% assign publications = publications | where:"category","3d-perception" %}


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
