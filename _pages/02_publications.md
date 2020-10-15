---
layout: project
title: Publications
permalink: /publications/
---



<hr>
<hr>
<hr>
<!-- {% assign grouped_publications = site.publications | group_by: 'year' | sort: 'month' | reverse %}
{% for group in items_grouped %}
  {% comment %} Create the items within the groups, now sorting by the criteria you want them sorted {% endcomment %}
  {% assign items = item.items | sort: 'date' | reverse %}
  {% comment %} Loop through the items {% endcomment %}
  {% for item in items  %}
    {{ item.title }}
  {% endfor %}
{% endfor %}

 -->

{% assign publication_years = "2020,2019" | split: ',' %}
<!-- {% assign publications = site.publications | sort: "year" | reverse %} -->
{% assign publications = site.publications | where: 'hide', false %}


<h2>__2020__</h2>

{% assign curr_publications = site.publications | where: 'year', '2020' %}

<h2>{{curr_publications.size}} publications in {{curr_year}}</h2>

{% assign curr_publications = curr_publications | sort: "month" | reverse %}

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

<hr>
<hr>
<hr>

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



<h2>__2020__</h2>

{% for pub in publications %}

<p>{{pub.year}}-{{pub.month}}-{{pub.title}} </p>

{% endfor %} 

<hr>

{% assign curr_publications = publications | where: "year", 2020 %}

<h2>{{curr_publications.size}} publications in {{curr_year}}</h2>

{% for pub in curr_publications %}

<p>{{pub.year}}-{{pub.month}}-{{pub.title}} </p>

{% endfor %} 

{% assign curr_publications = curr_publications | sort: "month" | reverse %}

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

<hr>
<hr>
<hr>

{% for curr_year in publication_years %}

<h2>{{curr_year}}</h2>

{% assign curr_publications = publications | where: "year", curr_year %}

<h2>{{curr_publications.size}} publications in {{curr_year}}</h2>

{% assign curr_publications = curr_publications | sort: "month" | reverse %}

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