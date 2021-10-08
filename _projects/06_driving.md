---
layout: project
title: Driving in action
permalink: /projects/driving
description: Getting from sensory inputs to car control goes either through a modular stack (perception > localization > forecast > planning > actuation) or, more radically, through a single end-to-end model. We work on both strategies, more specificaly on action forecasting, automatic interpretation of decisions taken by a driving system, and reinforcement / imitation learning for end-to-end systems (as in <a href="https://valeoai.github.io/blog/publications/e2e-rl-driving/">RL work</a> at CVPR’20).
image: "images/projects/driving.jpg"
category: project
url: ""
---



<h1>{{page.title}}</h1>
<p>{{page.description}}</p>


<h2>Publications</h2>

{% assign publications = site.publications | where: 'hide', false %}
{% assign publications = publications | where:"category", "driving" %}
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
