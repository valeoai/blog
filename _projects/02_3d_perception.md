---
layout: project
title: 3D perception
permalink: /projects/3d-perception
description: Each sensor delivers information about the 3D world around the vehicle. Making sense of this information in terms of drivable space and important objects (road users, curb, obstacles, street furnitures) in 3D is required for the driving system to plan and act in the safest and most confortable way. This encompasses several challenging tasks, in particular detection and segmentation of objects in point clouds as in <a href="https://valeoai.github.io/blog/publications/fkaconv/">FKAConv</a> at ACCV’20.
image: "images/projects/3d_perception.jpg"
category: project
url: /projects/3d-perception/
---


<h1>{{page.title}}</h1> 
<p>{{page.description}}</p>


<h2>Publications</h2>

{% assign publications = site.publications | where: 'hide', false %}
{% assign publications = publications | where:"category", "3d-perception" %}

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

