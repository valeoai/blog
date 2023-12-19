---
layout: project
title: Publications
permalink: /publications/
nav: true
nav_order: 3 
---

# All publications

For the comprehensive collection of our research papers, please refer to <a href="https://scholar.google.com/citations?user=eM4nZ1sAAAAJ&hl=en" target="_blank">our team's Google Scholar page</a>.  
By following our account, you will be updated with notifications about new papers published by our team.

# Selected publications

{% assign publications = site.publications | where: 'hide', false %}
<!-- {% assign publications_by_year = publications | group_by: 'year' | sort: 'year' |  reverse %} -->
{% assign publications_by_year = publications |  sort: 'year' |  reverse %}
{% assign publications_by_year = publications_by_year | group_by: 'year'%}

{% for year_publications in publications_by_year %}

<h2>{{year_publications.items[0].year}}</h2>

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

{% endfor %}
