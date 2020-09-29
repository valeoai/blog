---
layout: project
title: Uncertainty estimation and performance prediction
permalink: /projects/uncertainty
description: When the unexpected happens, when the weather badly degrades, when a sensor gets blocked, the embarked perception system should diagnose the situation and react accordingly, <em>e.g.,</em> by calling an alternative system or the human driver. With this in mind, we investigate automatic ways to assess the uncertainty of a system and to predict its performance.
image: "images/publications/confidnet/visu_camvid.png"
category: project
url: /projects/uncertainty/
---


<h1>{{page.title}}</h1> 
<p>{{page.description}}</p>


<h2>Publications</h2>

{% assign publications = site.publications | sort: "year" | reverse %}
{% assign publications = publications | where:"hide",false %}
{% assign publications = publications | where:"category","uncertainty" %}


{% for pub in publications %}

<div class="pubitem">
  <div class="pubteaser">
    <a href="{{site.url  | append: site.baseurl | append: pub.permalink}}">
      <img src="../../{{ pub.image }}" alt="{{pub.image}} publication teaser"/>
    </a>
  </div>
   <h3><a href="{{site.url  | append: site.baseurl | append: pub.permalink}}">{{ pub.title }}</a></h3>
 <!--  <p class="b">{{ pub.authors }}</p>
  <p class="c">{{ pub.venue_long }}, {{ pub.year }}</p> -->
  <p class="b">{{ pub.authors }}
    <br>
    <em>{{ pub.venue_long }}, {{ pub.year }}</em>
   </p>
</div>

<br>

{% if forloop.last == false %}
<hr>
{% endif %}

{% endfor %} 