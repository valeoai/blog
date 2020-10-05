---
layout: project
title: Projects
permalink: /projects/
---

# Projects

{% for projects in site.projects %}


{% if projects.category == "project" %}

<div class="pubitem">
  <div class="pubteaser">
    <a href="{{site.url  | append: site.baseurl | append: projects.permalink}}">
      <img src="../{{ projects.image }}" alt="{{projects.image}} project teaser"/>
    </a>
  </div>
   <h3><a href="{{site.url  | append: site.baseurl | append: projects.permalink}}">{{ projects.title }}</a></h3>
  <p>{{ projects.description }}</p>
</div>
<br>

<!-- for some reason the first line is weirdly formated -->
{% if forloop.first == true %}
<!-- <br> -->
{% endif %}

{% if forloop.last == false %}
<hr>
{% endif %}

{% endif %}

{% endfor %} 
