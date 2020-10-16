---
layout: project
title: Publications
permalink: /publications/
---




# Publications


{% assign publication_years = "2020,2019" | split: ',' %}
{% assign publications = site.publications | sort: "year" | reverse %}
{% assign publications = publications | where: "hide", false %}

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

{% endfor %} 



<hr>
<hr>
<hr>

<h2> __Attempt 1__ </h2>


{% assign publication_years = "2020,2019" | split: ',' %}
{% assign publications = site.publications | sort: "month" | reverse %}
{% assign publications = publications | where:"hide", false %}



<h2>{{publications.size}} publications across years </h2> 

{% for curr_year in publication_years %}


<h2>{{curr_year}}</h2>

{% assign curr_publications = publications | where: "year", {{curr_year}} %}

<h2>{{curr_publications.size}} publications in {{curr_year}}</h2>

<!-- {% assign curr_publications = curr_publications | sort: "month" | reverse %} -->

{% for pub in curr_publications %}

<p>month {{pub.month}}</p>

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


<hr>
<hr>
<hr>

<h2> --Attempt 2-- </h2>


{% assign publication_years = "2020,2019" | split: ',' %}
{% assign publications = site.publications | sort: "month" | reverse %}
{% assign publications = publications | where:"hide", false %}



<h2>{{publications.size}} publications across years </h2> 

{% for curr_year in publication_years %}



<h2>{{curr_year}}</h2>

{% for pub in publications %}

{% if pub.year contains curr_year %}

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

{% endif %}

{% if forloop.last == false %}
<hr>
{% endif %}

{% endfor %} 

{% endfor %} 



<hr>
<hr>
<hr>

<h2> --Attempt 3-- </h2>


{% assign publication_years = "2020,2019" | split: ',' %}
{% assign publications = site.publications | where: 'hide', false %}
{% assign publications_by_year = publications | group_by: 'year' | sort: 'year' |  reverse %}


{% for year_publications in publications_by_year %}

<h2>{{year_publications.items[0].year}}</h2>

{% assign curr_publications = year_publications.items | sort: 'month' | reverse %}

{% for pub in curr_publications %}


<p>month {{pub.month}}</p>

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