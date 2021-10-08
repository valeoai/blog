---
layout: project
title: Domain adaptation
permalink: /projects/domain-adaptation
description: Deep learning and reinforcement learning are key technologies for autonomous driving. One of the challenges they face is to adapt to conditions which differ from those met during training. To improve systems’ performance in such situations, we explore so-called “domain adaptation” techniques, as in <a href="https://valeoai.github.io/blog/publications/advent/">AdvEnt</a> at CVPR’19 and <a href="https://valeoai.github.io/blog/publications/dada/">DADA</a> its extension at ICCV’19.
image: "images/projects/domain_adaptation.jpg"
category: project
url: ""
---



<h1>{{page.title}}</h1>
<p>{{page.description}}</p>


<h2>Publications</h2>

{% assign publications = site.publications | where: 'hide', false %}
{% assign publications = publications | where:"category", "domain-adaptation" %}
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
