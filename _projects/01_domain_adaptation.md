---
layout: project
title: Domain adaptation
permalink: /projects/domain-adaptation/
description: Deep learning and reinforcement learning are key technologies for autonomous driving. One of the challenges they face is to adapt to conditions which differ from those met during training. To improve systems’ performance in such situations, we explore so-called <em>“domain adaptation”</em> techniques.
image: "images/projects/advent_teaser_small.png"
category: project
url: /projects/domain-adaptation/
---



<h1>{{page.title}}</h1> 
<!-- <h3>Project overview</h3> -->
<p>{{page.description}}</p>

<!-- <hr> -->

<h2>Publications</h2>

{% assign publications = site.publications | sort: "year" | reverse %}
{% assign publications = publications | where:"hide",false %}
{% assign publications = publications | where:"category","domain adaptation" %}


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
