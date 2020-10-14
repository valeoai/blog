---
layout: project
title: "Multi-sensor perception"
permalink: /projects/multi-sensor
description: Automated driving relies first on a diverse range of sensors, like Valeo’s <a href="https://www.valeo.com/en/360-vue/">fish-eye cameras</a>, <a href="https://www.valeo.com/en/valeo-scala/">LiDARs</a>, radars and ultrasonics. Exploiting at best the outputs of each of these sensors at any instant is fundamental to understand the complex environment of the vehicle. To this end, we explore various deep learning approaches where sensors are considered both in isolation and collectively.
image: "images/projects/valeo_sensors.jpg"
category: project
url: ""
---



<h1>{{page.title}}</h1> 
<p>{{page.description}}</p>


<h2>Publications</h2>

{% assign publications = site.publications | sort: "year" | reverse %}
{% assign publications = publications | where:"hide",false %}
{% assign publications = publications | where:"category","multi-sensor" %}


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
