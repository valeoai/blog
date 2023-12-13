---
layout: project
title: Projects
permalink: /projects/
nav: true
nav_order: 2 
---



# Projects

{% for projects in site.projects %}


{% if projects.category == "project" %}

<div class="row">
    <div class="col-md-4">
        <div class="pubteaserbs">
            <a href="{{site.url  | append: site.baseurl | append: projects.permalink}}">
                <img class="media-object" src="../{{ projects.image }}" alt="{{projects.image}} project teaser"/>
           </a>
        </div>
    </div>
    <div class="col-md-8">
        <div class="pubitembs">
          <h3><a href="{{site.url  | append: site.baseurl | append: projects.permalink}}">{{ projects.title }}</a></h3>
          <p>{{ projects.description }}</p>
        </div>
</div>
</div>


{% if forloop.last == false %}
<hr>
{% endif %}

{% endif %}

{% endfor %} 
